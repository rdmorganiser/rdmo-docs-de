Shibboleth
~~~~~~~~~~

Um Shibboleth mit RMDO zu verwenden, ist es notwendig in einer Betriebsumgebung mit Apache2 zu sein. Das Setup ist :doc:`hier </deployment/apache>` dokumentiert.

Als nächstes installiere das Shibboleth Apache Modul für die Service-Anbieter von deinem Distributionsrepository, z.B. für Debian/Ubuntu:

.. code:: bash

    sudo apt-get install libapache2-mod-shib2

Zusätzlich muss der `Django-shibboleth-remoteuser <https://github.com/Brown-University-Library/django-shibboleth-remoteuser>`_ in der virtuellen RDMO-Umgebung installiert werden: 

.. code:: bash

    pip install -r requirements/shibboleth.txt

Konfiguriere deinen Shibboleth Service-Anbieter mit den Dateien in ``/etc/shibboleth/``. Dies kann zwischen den Identitäts-Anbietern variieren. Für RDMO muss der ``REMOTE_SERVER`` gesetzt sein und vier weitere Attribute von ihrem Identitäts-Anbieter:

* ein Username(meistens ``eppn``)
* eine E-Mail-Addresse (meistens ``mail`` oder ``email``)
* ein Vorname (meistens ``givenName``)
* ein Familienname (meistens ``sn``)

In unserer Testumgebung, kann dies durch das Verändern von ``/etc/shibboleth/shibboleth2.xml`` erreicht werden:

.. code:: xml

    <ApplicationDefaults entityID="https://sp.vbox/shibboleth"
                         REMOTE_USER="uid eppn persistent-id targeted-id">


und '/etc/shibboleth/attribute-map.xml':

.. code:: xml

    <Attribute name="urn:oid:0.9.2342.19200300.100.1.1" id="uid"/>
    <Attribute name="urn:oid:2.5.4.4" id="sn"/>
    <Attribute name="urn:oid:2.5.4.42" id="givenName"/>
    <Attribute name="urn:oid:0.9.2342.19200300.100.1.3" id="mail"/>

Starten Sie den Shibboleth Service-Anbieter Demon neu:

.. code:: bash

    service shibd restart

In ihrer Apache2 virtuellen Host-Konfiguration fügen Sie folgendes hinzu:

::

    <Location /Shibboleth.sso>
        SetHandler shib
    </Location>
    <LocationMatch /(account|domain|options|projects|questions|tasks|conditions|views)>
        AuthType shibboleth
        require shibboleth
        ShibRequireSession On
        ShibUseHeaders On
    </LocationMatch>

In ihrer ``config/settings/local.py`` fügen Sie folgendes hinzu oder entfernen die Kommentarsymbole:

.. code:: python

    from rdmo.core.settings import INSTALLED_APPS, AUTHENTICATION_BACKENDS, MIDDLEWARE_CLASSES

    SHIBBOLETH = True
    PROFILE_UPDATE = False

    INSTALLED_APPS += ['shibboleth']

    AUTHENTICATION_BACKENDS.append('shibboleth.backends.ShibbolethRemoteUserBackend')
    MIDDLEWARE_CLASSES.insert(
        MIDDLEWARE_CLASSES.index('django.contrib.auth.middleware.AuthenticationMiddleware') + 1,
        'shibboleth.middleware.ShibbolethRemoteUserMiddleware'
    )

    SHIBBOLETH_ATTRIBUTE_MAP = {
        'uid': (True, 'username'),
        'givenName': (True, 'first_name'),
        'sn': (True, 'last_name'),
        'mail': (True, 'email'),
    }

    LOGIN_URL = '/Shibboleth.sso/Login?target=/projects'
    LOGOUT_URL = '/Shibboleth.sso/Logout'

wobei die Schlüssel von ``SHIBBOLETH_ATTRIBUTE_MAP``, ``LOGIN_URL``, und ``LOGOUT_URL`` entsprechend ihrem Setup geändert werden müssen. Die Einstellung ``SHIBBOLETH = True`` deaktiviert das reguläre Login-Formular von RDMO und sagt RDMO das Udpateformular für das Benutzerprofil zu deaktivieren, so dass der Benutzer seine Zugangsdaten nicht mehr ändern kann.  Die ``INSTALLED_APPS``, ``AUTHENTICATION_BACKENDS``, und ``MIDDLEWARE_CLASSES`` Einstellungen erlauben es den django-shibboleth-remoteuser mit RDMO zu verwenden. 

Starte den Webserver neu.

.. code:: bash

    service apache2 restart
