Allgemeine Einstellungen
------------------------

Einige allgemeine Einstellungen sollten in ihrer ``config/settings/local.py`` enthalten sein. Die erste und wahrscheinlich wichtigste Einstellung ist, wenn Sie RDMO im `Debug-Modus <https://docs.djangoproject.com/en/1.10/ref/settings/#std:setting-DEBUG>`_ ausführen:

.. code:: python

    DEBUG = True

Im Debug-Modus werden ausführliche Fehlerseiten angezeigt, falls etwas schief läuft, werden statische Inhalte wie CSS und JavaScript-Dateien vom Entwicklungsserver automatisch gefunden. Der Debug-Modus *darf nicht* aktiviert sein, wenn RDMO im normalen Betrieb mit dem Internet verbunden ist.

Django braucht einen `Geheimschlüssel <https://docs.djangoproject.com/en/1.10/ref/settings/#std:setting-SECRET_KEY>`_, der auf einen einzigartigen, unvorhersehbaren Wert gesetzt wird:

.. code:: python

    SECRET_KEY = 'this is not a very secret key'

Dieser Schlüssel muss geheim bleiben, da ansonsten viele der eingebauten Sicherheitsmaßnahmen von Django versagen.

Im Betrieb erlaubt Django nur `Anfragen an bestimmte URLs <https://docs.djangoproject.com/en/1.10/ref/settings/#allowed-hosts>`_, welche festgelegt werden müssen:

.. code:: python

    ALLOWED_HOSTS = ['localhost', 'rdmo.example.com']

Wenn Sie RDMO unter einem Alias wie http://example.com/rdmo laufen lassen möchten, mussen Sie die Basis-URL festlegen:

.. code:: python

    BASE_URL = '/rdmo'

Ferner, möchten Sie vielleicht eine Hauptsprache für ihr RDMO und die Zeitzone festlegen:

.. code:: python

    LANGUAGE_CODE = 'en-us'
    TIME_ZONE = 'Europe/Berlin'
