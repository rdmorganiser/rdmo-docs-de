LDAP
~~~~

Um ein LDAP-Backend mit RDMO nutzen zu können, muss zunächst die nötige Software installiert werden. Bei Debian/Ubuntu kann dies wie folgt geschehen:

.. code:: bash

    sudo apt-get install libsasl2-dev python-dev libldap2-dev libssl-dev

Auf Python basierend verwenden wir `django-auth-ldap <http://pythonhosted.org/django-auth-ldap>`_ , um uns mit dem LDAP-Server zu verbinden. Wie schon zuvor sollte dies in einer für RDMO erstellten virtuellen Umgebung installiert werden:

.. code:: bash

    pip install -r requirements/ldap.txt

LDAP-Installationen können sehr verschiedenartig sein und wir beschreiben nur einen bestimmten Fall. Wir nehmen an, dass der LDAP-Service auf  ``ldap.example.com`` läuft. RDMO benötigt einen *System Account*. Starten Sie:

.. code:: bash

    ldapmodify -x -D 'cn=Directory Manager' -W

auf der Machine mit dem LDAP-Service und geben Sie ein:

::

    dn: uid=system,cn=sysaccounts,cn=etc,dc=example,dc=com
    changetype: add
    objectclass: account
    objectclass: simplesecurityobject
    uid: rdmo
    userPassword: YOURPASSWORD
    passwordExpirationTime: 20380119031407Z
    nsIdleTimeout: 0

und enden Sie die Datei mit einer Leerzeile gefolgt von  ``ctrl-d``.

Danach fügen Sie folgende Zeilen hinzu oder entfernen die Kommentarzeichen in ``config/settings/local.py``:

.. code:: python

    import ldap
    from django_auth_ldap.config import LDAPSearch
    from rdmo.core.settings import AUTHENTICATION_BACKENDS

    PROFILE_UPDATE = False

    AUTH_LDAP_SERVER_URI = "ldap://ldap.example.com"
    AUTH_LDAP_BIND_DN = "cn=rdmo,dc=ldap,dc=example,dc=com"
    AUTH_LDAP_BIND_PASSWORD = "YOURPASSWORD"
    AUTH_LDAP_USER_SEARCH = LDAPSearch("dc=ldap,dc=example,dc=com", ldap.SCOPE_SUBTREE, "(uid=%(user)s)")

    AUTH_LDAP_USER_ATTR_MAP = {
        "first_name": "givenName",
        "last_name": "sn",
        'email': 'mail'
    }

    AUTHENTICATION_BACKENDS.insert(
        AUTHENTICATION_BACKENDS.index('django.contrib.auth.backends.ModelBackend'),
        'django_auth_ldap.backend.LDAPBackend'
    )

Die Einstellung ``PROFILE_UPDATE = False`` deaktiviert das Updateformular des Benutzerprofils in RDMO, so dass der Benutzer seine Zugangsdaten nicht mehr verändern kann. Die anderen Einstellungen werden von ``Django-auth-ldap`` benötigt und sind in der `django-auth-ldap Dokumentation <http://pythonhosted.org/django-auth-ldap>`_ beschrieben.
