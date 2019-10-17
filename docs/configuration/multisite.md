Multisite
=========

```eval_rst
.. warning::
    Das folgende Feature is noch nicht Teil der veröffentlichten Version von RDMO. Es wird Teil eines späteren Releases.
```

RDMO kann in einem Multi-Site-Setup betrieben werden, das mehrere verschiedene `rdmo-apps` mit unterschiedlichen URLs und Themes auf einem Server mit einer gemeinsamen Datenbank verbindet. Die verschiedenen Seiten teilen ihre Kataloge, Ansichten usw., aber die Verfügbarkeit dieses Inhalts kann zwischen den Seiten eingeschränkt werden. Nutzer können sich über alle Sites einloggen (sofern es dir Authentifizierungsschnittstellen zulassen) und Projekte können zwischen den Sites geteilt werden. Jede dieser RDMO Sites hat ein eigenes `rdmo-app` Verzeichnis und eine eigene Konfigurationsdatei (`config/settings/local.py`).

Setup
-----

Um eine solche Multi-Site-Installation einzurichten, müssen Sie mit einer ersten regulären RDMO-Instanz beginnen, wie unter [installation](../installation) beschrieben. Im Prinzip kann auch eine existierende RDMO Instanz auf ein Multi-Site Setup erweitert werden, in dieser Dokumentation gehen wir aber von einer Neuinstallation aus.

* Erstellen Sie eine neue virtuelle Umgebung außerhalb der `rdmo-app`, z.B. in `/srv/rdmo/env`. Im Multi-Site Setup verwenden *alle* RDMO Sites die gleiche virtuelle Umgebung. RDMO und die anderen Python Abhängigkeiten müssen dann auch immer nur einmal, in dieser Umgebung, aktualisiert werden.

* Ansonsten befolgen Sie die Anweisungen wie gewohnt, fügen Sie aber `MULTISITE = True` zu `config/settings/local.py` hinzu. Dadurch werden die Multi-Site-spezifischen Funktionen in der Benutzeroberfläche aktiviert.

* Melden Sie sich nach der Installation an der Admin-Oberfläche an und fügen Sie Ihre zusätzlichen Websites im Abschnitt Sites hinzu (wie [hier](../administration/site) beschrieben). Notieren Sie sich die numerische ID der verschiedenen Sites, wie sie in der URL beim Bearbeiten der Site angezeigt wird (z.B. `http://localhost:8000/admin/sites/site/2/change/`).

* Klonen Sie dann eine zweite `rdmo-app` neben der ersten, verwenden Sie aber die gleiche virtuelle Umgebung wie zuvor (daher ist keine `pip install` erforderlich). Richten Sie `rdmo-app2/config/settings/local.py` wie gewohnt ein. Fügen Sie `MULTISITE = True` und `SITE_ID = X` in `rdmo-app2/config/settings/local.py` ein, wobei `X` die ID der Seite aus dem vorherigen Schritt ist. Verwenden Sie für `DATABASE` die **gleichen** Einstellungen wie in `rdmo-app`.

Wenn Sie nun `./manage.py runserver 0.0.0.0.0.0:8000` in `rdmo-app` und `./manage.py runserver 0.0.0.0.0:8002` in `rdmo-app2` ausführen, sollten die beiden Seiten bereits funktionieren.


Bereitstellung
--------------

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
<SPConfig xmlns="urn:mace:shibboleth:3.0:native:sp:config"
    xmlns:conf="urn:mace:shibboleth:3.0:native:sp:config"
    clockSkew="180">

    <OutOfProcess tranLogFormat="%u|%s|%IDP|%i|%ac|%t|%attr|%n|%b|%E|%S|%SS|%L|%UA|%a" />

    <ApplicationDefaults entityID="https://sp.test.rdmo.org/shibboleth"
        REMOTE_USER="eppn"
        cipherSuites="DEFAULT:!EXP:!LOW:!aNULL:!eNULL:!DES:!IDEA:!SEED:!RC4:!3DES:!kRSA:!SSLv2:!SSLv3:!TLSv1:!TLSv1.1">

        <Sessions lifetime="28800" timeout="3600" relayState="ss:mem"
                  checkAddress="false" handlerSSL="true" cookieProps="https">
            <SSO entityID="https://idp.test.rdmo.org/idp/shibboleth"
                 discoveryProtocol="SAMLDS" discoveryURL="https://ds.example.org/DS/WAYF">SAML2</SSO>

            ...

        </Sessions>

        ...

        <AttributeFilter type="XML" validate="true" path="attribute-policy.xml"/>
            <CredentialResolver type="File" use="signing" key="sp-key.pem" certificate="sp-cert.pem"/>
            <CredentialResolver type="File" use="encryption" key="sp-key.pem" certificate="sp-cert.pem"/>

        <MetadataProvider type="XML" validate="true" path="idp-metadata.xml"/>

        <ApplicationOverride id="sp2" entityID="https://sp2.test.rdmo.org/shibboleth">
            <Sessions lifetime="28800" timeout="3600" relayState="ss:mem"
                      checkAddress="false" handlerSSL="true" cookieProps="https">
                <SSO entityID="https://idp2.test.rdmo.org/idp/shibboleth"
                     discoveryProtocol="SAMLDS" discoveryURL="https://ds.example.org/DS/WAYF">SAML2</SSO>

                ...

            </Sessions>

            <CredentialResolver type="File" use="signing" key="sp2-key.pem" certificate="sp2-cert.pem"/>
            <CredentialResolver type="File" use="encryption" key="sp2-key.pem" certificate="sp2-cert.pem"/>
            <MetadataProvider type="XML" validate="true" path="idp2-metadata.xml"/>
        </ApplicationOverride>

    </ApplicationDefaults>

    ...

</SPConfig>
```

wobei `https://idp.test.rdmo.org` und `https://idp2.test.rdmo.org/idp/shibboleth` zwei verschiedene IdP für die beiden Sites sind. Wie schon erwähnt kann kann Ihr Shibboleth-Setup von dem hier beschriebenen abweichen.

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
