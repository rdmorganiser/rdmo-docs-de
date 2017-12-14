Allgemeine Einstellungen
------------------------

Einige genrelle Einstellungen sollten in deiner ``config/settings/local.py`` enthalten sein. Die erste und wahrscheinlich wichtigste, wenn du RDMO im `Debug-Modus<https://docs.djangoproject.com/en/1.10/ref/settings/#std:setting-DEBUG>`_ ausführst:

.. code:: python

    DEBUG = True

Im Debug-Modus werden ausführliche Fehlerseiten angezeigt, falls etwas schief läuft und statische Inhalte wie CSS und JavaScript-Dateien werden vom Entwicklungsserver automatisch gefunden. Der Debug-Modus *darf nicht* aktiviert sein, wenn RDMO im normalen Betrieb mit dem Internet verbunden ist.

Django braucht einen `Geheimschlüssel <https://docs.djangoproject.com/en/1.10/ref/settings/#std:setting-SECRET_KEY>`_, der auf einen `` einzigartigen, unvorsagbaren Wert gesetzt wird ``:

.. code:: python

    SECRET_KEY = 'this is not a very secret key'

Dieser Schlüssel muss geheim gelaten werden, da ansosnten viele von Djangos Sicherheitsmaßnahmen versagen.

Im Betrieb, erlaubt Django nur `Anfragen zu bestimmten URLs <https://docs.djangoproject.com/en/1.10/ref/settings/#allowed-hosts>`_, welche festgelegt werden müssen:

.. code:: python

    ALLOWED_HOSTS = ['localhost', 'rdmo.example.com']

Wenn du RDMO unter einem Alias wie http://example.com/rdmo laufen lassen möchtest, musst du die Basis-URL festlegen: 
.. code:: python

    BASE_URL = '/rdmo'

Ferner, möchtest du vielleicht eine Hauptsprache für dein RDMO und die Zeitzone festlegen:

.. code:: python

    LANGUAGE_CODE = 'en-us'
    TIME_ZONE = 'Europe/Berlin'
