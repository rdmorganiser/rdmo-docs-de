# Cache

RDMO benutzt einen Cache für einige seiner Seiten. Im Entwicklungsmodus ist dies mit einem local-memory Caching gemacht. Im Betrieb empfehlen wir [Memcached](https://memcached.org) zu nutzen. Memcached kann auf Debian/Ubuntu wie folgt installiert werden:

```bash
sudo apt install memcached
```

Auf  RHEL/CentOS sind weitere Schritte notwendig. Installieren Sie zunächst die Pakete:

```bash
sudo yum install memcached
```

Danach veränderen Sie die Einstellungen, um externe Verbindungen zu verhindern:

```
# in /etc/sysconfig/memcached
PORT="11211"
USER="memcached"
MAXCONN="1024"
CACHESIZE="64"
OPTIONS="-l 127.0.0.1"
```

Dann starten Sie den Service:

```bash
systemctl start memcached
systemctl enable memcached
```

Zurück in ihrer virtuellen Umgebung müssen Sie Python-memcached installieren:

```bash
pip install -r requirements/memcached.txt
```

und fügen Sie zu `config/settings/local.py` folgende Zeiten hinzu:

```python
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
```
