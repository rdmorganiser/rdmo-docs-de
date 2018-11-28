E-Mail
------

RDMO muss E-Mails an seine Benutzer schicken können. Die Vebindung zu dem SMPT-Server wird über folgende Einstellungen in ihrer ``config/settings/local.py`` konfiguriert:

.. code:: python

    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'localhost'
    EMAIL_PORT = '25'
    EMAIL_HOST_USER = ''
    EMAIL_HOST_PASSWORD = ''
    EMAIL_USE_TLS = False
    EMAIL_USE_SSL = False

    DEFAULT_FROM_EMAIL = ''

Hier ist ``EMAIL_HOST`` die URL oder IP des SMTP-Servers, ``EMAIL_PORT`` ist der zugehörige Port (meistens 25, 465, oder 587), ``EMAIL_HOST_USER`` und ``EMAIL_HOST_PASSWORD`` sind die Zugangsdaten, falls der SMTP-Server eine Authenfizierung verlangt.

Für eine ``STARTTLS``-Verbindung (meistens auf Port 587) muss ``EMAIL_USE_TLS`` auf ``True`` gesetzt werden, während ``EMAIL_USE_SSL`` auf ``True`` gesetzt sein muss, um  eine implizite TLS/SSL Verbindung (meistens auf dem Port 465) zu ermöglichen.

``DEFAULT_FROM_EMAIL`` setzt das Absender-Feld für die E-Mails, die dem Benutzer geschickt werden.

Für ein Entwicklungs-/Test-Setup kann ein einfaches E-Mail-Backend verwendet werden, dass nur die E-Mail auf dem Terminal anzeigt:

.. code:: python

    EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
    EMAIL_FROM = 'info@example.com'

Dies ist auch das Standard-Backend, falls keine E-Mail-Einstellungen in ``config/settings/local.py`` hinzugefügt wurden.
