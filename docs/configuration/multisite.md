Multisite
=========

```eval_rst
.. warning::
    Das folgende Feature is noch nicht Teil der veröffentlichten Version von RDMO. Es wird Teil eines späteren Releases.
```

RDMO kann in einem Multi-Site-Setup betrieben werden, das mehrere verschiedene `rdmo-apps` mit unterschiedlichen URLs und Themes auf einem Server mit einer gemeinsamen Datenbank verbindet. Die verschiedenen Seiten teilen ihre Kataloge, Ansichten usw., aber die Verfügbarkeit dieses Inhalts kann zwischen den Seiten eingeschränkt werden. Nutzer können sich über alle Sites einloggen (sofern es dir Authentifizierungsschnittstellen zulassen) und Projekte können zwischen den Sites geteilt werden.

Setup
-----

Um eine solche Multi-Site-Installation einzurichten, müssen Sie mit einer regulären RDMO-Instanz beginnen, wie unter [installation](../installation) beschrieben.

* Erstellen Sie die virtuelle Umgebung außerhalb der `rdmo-app`, z.B. in `/srv/rdmo/env`. Ansonsten befolgen Sie die Anweisungen wie gewohnt, fügen Sie aber `MULTISITE = True` zu `config/settings/local.py` hinzu. Dadurch werden die Multi-Site-spezifischen Funktionen in der Benutzeroberfläche aktiviert.

* Melden Sie sich nach der Installation an der Admin-Oberfläche an und fügen Sie Ihre zusätzlichen Websites im Abschnitt Sites hinzu (wie [hier](../administration/site) beschrieben). Notieren Sie sich die numerische ID der verschiedenen Sites, wie sie in der URL beim Bearbeiten der Site angezeigt wird (z.B. `http://localhost:8000/admin/sites/site/2/change/`).

* Klonen Sie dann eine zweite `rdmo-app` neben der ersten, verwenden Sie aber die gleiche virtuelle Umgebung wie zuvor (daher ist keine `pip install` erforderlich). Richten Sie `rdmo-app2/config/settings/local.py` wie gewohnt ein. Fügen Sie `MULTISITE = True` und `SITE_ID = X` in `rdmo-app2/config/settings/local.py` ein, wobei `X` die ID der Seite aus dem vorherigen Schritt ist. Verwenden Sie für `Datenbank` die **gleichen** Einstellungen wie in `rdmo-app`.

Wenn Sie nun `./manage.py runserver 0.0.0.0.0.0:8000` in `rdmo-app` und `./manage.py runserver 0.0.0.0.0:8002` in `rdmo-app2` ausführen, sollten die beiden Seiten bereits funktionieren.

Bereitstellung
----------

Die beiden Sites werden separat bereitgestellt, unabhängig davon, ob Sie Apache oder nginx verwenden. Erstellen Sie separate virtuelle Host-Konfigurationen, die die jeweilige Site-URL auf die entsprechende `rdmo-app` abbilden. Z.B. für Apache:

```
<VirtualHost *:443>>
    ServerName example.com

    ...

    Alias /static /srv/rdmo/rdmo/rdmo-app/static_root/
    <Verzeichnis /srv/rdmo/rdmo/rdmo-app/static_root/>
        Erfordern Sie alle gewährten
    </Verzeichnis>

    WSGIDaemonProcess rdmo_app user=rdmo group=rdmo \
        home=/srv/rdmo/rdmo/rdmo-app python-home=/srv/rdmo/env
    WSGIProcessGroup rdmo_app
    WSGIScriptAlias / /srv/rdmo/rdmo/rdmo-app/config/wsgi.py Prozessgruppe=rdmo_app
    WSGIPassAutorisierung Ein

    <Verzeichnis /srv/rdmo/rdmo/rdmo-app/config/>
        <Dateien wsgi.py>
            Erfordern Sie alle gewährten
        </Files>
    </Verzeichnis>
</VirtualHost>
```

und

```
<VirtualHost *:443>>
    ServerName example.org

    ...

    Alias /statisch /srv/rdmo/rdmo/rdmo-app2/static_root/
    <Verzeichnis /srv/rdmo/rdmo/rdmo-app2/static_root/>
        Erfordern Sie alle gewährten
    </Verzeichnis>

    WSGIDaemonProcess rdmo_app2 user=rdmo group=rdmo \
        home=/srv/rdmo/rdmo/rdmo-app2 python-home=/srv/rdmo/env
    WSGIProcessGroup rdmo_app2
    WSGIScriptAlias / /srv/rdmo/rdmo/rdmo-app2/config/wsgi.py Prozessgruppe=rdmo_app2
    WSGIPassAutorisierung Ein

    <Verzeichnis /srv/rdmo/rdmo/rdmo-app2/config/>
        <Dateien wsgi.py>
            Erfordern Sie alle gewährten
        </Files>
    </Verzeichnis>
</VirtualHost>
```

Shibboleth
----------

Um mehrere separate Sites auf einem Rechner betreiben zu können, muss der Service Provider entsprechend konfiguriert werden. Für jede Seite außer der ersten muss eine `ApplicationOverride` in `/etc/shibboleth/shibboleth/shibboleth2.xml` konfiguriert werden, z.B.

````xml
<ApplicationOverride id="example.org" entityID="https://example.org/shibboleth">
    <CredentialResolver type="File" use="signing" key="example-org-key.pem" certificate="example-org-cert.pem"/>
    <CredentialResolver type="File" use="encryption" key="example-org-key.pem" certificate="example-org-cert.pem"/>
</AnwendungOverride>>
```

wobei `example-org-key.pem` und `example-org-cert.pem` der private Schlüssel und das öffentliche Zertifikat für diese URL sind. Wie schon erwähnt kann kann Ihr Shibboleth-Setup von dem hier beschriebenen abweichen.

In der Konfiguration des virtuellen Hosts für jeden einzelnen außer dem ersten Standort muss `ShibRequestSetting applicationId <id>` sowohl zu `<Location /Shibboleth.sso>` als auch `<LocationMatch /(....)>` hinzugefügt werden. `<id>` ist das `id` Attribut des `ApplicationOverride` Nodes, z.B:

```
<Standort /Shibboleth.sso>>
    SetHandler shib
    ShibRequestSetting applicationId example.org
</Standort>
<LocationMatch /(Konto|Domäne|Optionen|Projekte|Fragen|Tasks|Bedingungen|Ansichten)>
    AuthType Schibboleth
    verlangen Shibboleth
    ShibRequireSession Ein
    ShibUseHeaders Ein
    ShibRequestSetting applicationId example.org
</LocationMatch>
```
