Protokollieren
--------------

Das Protokollieren (Schreiben von Logs) kann in Django sehr komplex werden und ist ausführlich in der `Django Dokumentation <https://docs.djangoproject.com/en/1.11/topics/logging/>`_ erklärt. Für ein zu RDMO passendes Protokollieren können Sie folgende Zeilen in ihrer ``config/settings/local.py`` ergänzen:

.. code:: python

    import os
    from . import BASE_DIR

    LOGGING_DIR = '/var/log/rdmo/'
    LOGGING = {
        'version': 1,
        'disable_existing_loggers': True,
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
            },
            'console': {
                'format': '[%(asctime)s] %(message)s'
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
                'filename': os.path.join(LOGGING_DIR, 'error.log'),
                'formatter': 'default'
            },
            'rdmo_log': {
                'level': 'DEBUG',
                'class':'logging.FileHandler',
                'filename': os.path.join(LOGGING_DIR, 'rdmo.log'),
                'formatter': 'name'
            },
            'console': {
                'level': 'DEBUG',
                'filters': ['require_debug_true'],
                'class': 'logging.StreamHandler',
                'formatter': 'console'
            }
        },
        'loggers': {
            'django': {
                'handlers': ['console'],
                'level': 'INFO',
            },
            'django.request': {
                'handlers': ['mail_admins', 'error_log'],
                'level': 'ERROR',
                'propagate': True
            },
            'rdmo': {
                'handlers': ['rdmo_log'],
                'level': 'DEBUG',
                'propagate': False
            }
        }
    }

Dies produziert zwei Log-Dateien:

* ``/var/log/rdmo/error.log`` wird Ausnahme-Nachrichten von Anwendungsfehlern enthalten (Statuscode: 500). Diese Nachrichten entsprechen denen, die ``DEBUG = True`` erzeugt. Im normalen Betrieb sollen solche Meldungen nicht vorkommen. Hinzukommt eine E-Mail an alle Admins, die in der ``ADMINS``-Einstellung konfiguriert sind.
* ``/var/log/rdmo/rdmo.log`` wird weitere Log-Informationen vom RDMO-Code enthalten.
