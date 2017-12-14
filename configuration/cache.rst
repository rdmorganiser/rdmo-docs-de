Cache
-----

RDMO benutzt einen Cache für einige seiner Seiten. Im Entwicklungsmodus ist dies mit einem local-memory Caching gmeacht. Im Betrieb empfehlen wir `memcached <https://memcached.org>`_ zu nutzen. Memcached kann auf Debian/Ubuntu installiert werden:

.. code:: bash

    sudo apt install memcached

Auf  RHEL/CentOS sind weitere Schritte notwendig. Installiere zunächst die Pakete:

.. code:: bash

    sudo yum install memcached

Danach verändere die Einstellungen, um externe Verbindungen zu verhindern:

.. code:: bash

    # in /etc/sysconfig/memcached
    PORT="11211"
    USER="memcached"
    MAXCONN="1024"
    CACHESIZE="64"
    OPTIONS="-l 127.0.0.1"

Dann starte den Service:

.. code:: bash

    systemctl start memcached
    systemctl enable memcached

Zurück in deiner virtuellen Umgebung musst du Python-memcached installieren:

.. code:: bash

    pip install -r requirements/memcached.txt

und füge zu ``config/settings/local.py`` folgende Zeiten hinzu:

.. code:: python

    CACHES = {
        {
            'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
            'LOCATION': '127.0.0.1:11211',
            'KEY_PREFIX': 'rdmo_default'
        },
        'api': {
            'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
            'LOCATION': '127.0.0.1:11211',
            'KEY_PREFIX': 'rdmo_api'
        }
    }
