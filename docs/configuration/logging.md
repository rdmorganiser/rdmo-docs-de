# Protokollieren

Das Protokollieren (Schreiben von Logs) kann in Django sehr komplex werden und ist ausführlich in der [Django Dokumentation](https://docs.djangoproject.com/en/stable/topics/logging/) erklärt. Für ein zu RDMO passendes Protokollieren ergänzen Sie folgende Zeilen in ihrer `config/settings/local.py` :

```python
import os

LOG_LEVEL = 'INFO'          # or 'DEBUG' for the full logging
LOG_DIR = '/var/log/rdmo/'  # this directory needs to be writable by the rdmo user
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'filters': {
        'require_debug_false': {
            '()': 'django.utils.log.RequireDebugFalse'
        },
        'require_debug_true': {
            '()': 'django.utils.log.RequireDebugTrue'
        }
    },
    'formatters': {
        'default': {
            'format': '[%(asctime)s] %(levelname)s: %(message)s'
        },
        'name': {
            'format': '[%(asctime)s] %(levelname)s %(name)s: %(message)s'
        }
    },
    'handlers': {
        'mail_admins': {
            'level': 'ERROR',
            'filters': ['require_debug_false'],
            'class': 'django.utils.log.AdminEmailHandler'
        },
        'error_log': {
            'level': 'ERROR',
            'class':'logging.FileHandler',
            'filename': os.path.join(LOG_DIR, 'error.log'),
            'formatter': 'default'
        },
        'ldap_log': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',
            'filename': os.path.join(LOG_DIR, 'ldap.log'),
            'formatter': 'name'
        },
        'rules_log': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',
            'filename': os.path.join(LOG_DIR, 'rules.log'),
            'formatter': 'name'
        },
        'rdmo_log': {
            'level': 'DEBUG',
            'class':'logging.FileHandler',
            'filename': os.path.join(LOG_DIR, 'rdmo.log'),
            'formatter': 'name'
        }
    },
    'loggers': {
        'django.request': {
            'handlers': ['mail_admins', 'error_log'],
            'level': 'ERROR',
            'propagate': True
        },
        'django_auth_ldap': {
            'handlers': ['ldap_log'],
            'level': LOG_LEVEL,
            'propagate': True
        },
        'rules': {
            'handlers': ['rules_log'],
            'level': LOG_LEVEL,
            'propagate': True,
        },
        'rdmo': {
            'handlers': ['rdmo_log'],
            'level': LOG_LEVEL,
            'propagate': True
        }
    }
}
```

Dies produziert eine Reihe von Log-Dateien:

* `/var/log/rdmo/error.log` wird Ausnahme-Nachrichten von Anwendungsfehlern enthalten (Statuscode: 500). Diese Nachrichten entsprechen denen, die `DEBUG = True` erzeugt. Im normalen Betrieb sollen solche Meldungen nicht vorkommen. Hinzukommt eine E-Mail an alle Admins, die in der `ADMINS`-Einstellung konfiguriert sind.
* `/var/log/rdmo/rdmo.log` sind weitere Log-Informationen vom RDMO-Code enthalten.
* `/var/log/rdmo/ldap.log` und `/var/log/rdmo/rules.log` können zum Debuggen einer LDAP Autentifizierung bzw. des internen Rechtesystems genutzt werden.
