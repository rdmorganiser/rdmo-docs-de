Cache
-----

Für einige Seiten verwendet RDMO einen Cache. Im Entwicklungsmodus wird ein einfaches local-memory Caching genutzt. Im Produktiv-Betrieb empfehlen wir die Nutzung von `memcached <https://memcached.org>`_. Memcached kann auf Debian/Ubuntu wie folgt installiert werden:

.. code:: bash

    sudo apt install memcached

Auf  RHEL/CentOS sind weitere Schritte notwendig. Installieren Sie zunächst die Pakete:

.. code:: bash

    sudo yum install memcached

Danach veränderen Sie die Einstellungen, um externe Verbindungen zu verhindern:

.. code:: bash

    # in /etc/sysconfig/memcached
    PORT="11211"
    USER="memcached"
    MAXCONN="1024"
    CACHESIZE="64"
    OPTIONS="-l 127.0.0.1"

Dann starten Sie den Service:

.. code:: bash

    systemctl start memcached
    systemctl enable memcached

Zurück in ihrer virtuellen Umgebung müssen Sie python-memcached installieren:

.. code:: bash

    pip install -r requirements/memcached.txt

und fügen Sie zu ``config/settings/local.py`` folgende Zeiten hinzu:

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
