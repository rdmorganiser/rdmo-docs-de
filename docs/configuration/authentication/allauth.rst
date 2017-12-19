Django-allauth
~~~~~~~~~~~~~~

RDMO verwendet das großartige `django-allauth <http://www.intenct.nl/projects/django-allauth>`_ als seine Hauptauthorizierungsbibliothek. Es ermöglicht Workflows für Benutzerregistration und Passwortabfrage, genauso wie Athentifizierung von Webseiten dritter Anbieter mit Hilfe von OAUTH2.

Accounts
````````

Um reguläre Accounts in RDMO anzulegen, fügen sie folgendes hinzu:

.. code:: python

    from rdmo.core.settings import INSTALLED_APPS, AUTHENTICATION_BACKENDS

    ACCOUNT = True
    ACCOUNT_SIGNUP = True

    INSTALLED_APPS += [
        'allauth',
        'allauth.account',
    ]

    AUTHENTICATION_BACKENDS.append('allauth.account.auth_backends.AuthenticationBackend')

zu ihrer ``config/settings/local.py``. Die Einstellung``ACCOUNT = True`` aktiviert die allgemeinen Django-allauth Eigenschaften in RDMO, ``ACCOUNT_SIGNUP = True`` erlaubt es neue Benutzer in deiner RDMO-Isntanz zu registrieren. 
Das Verhalten von ``Django-allauth`` kann kann durch weitere Eisntlleungen konfiguriert werden, die unter `django-allauth documentation <http://django-allauth.readthedocs.io/en/latest/configuration.html>`_ dokumentiert sind. RDMO etzt einige Standardwerte, die in ``config/settings/base.py`` gefunden werden können.

Soziale Accounts
`````````````````

Um Accounts von Webseiten dritter Anbieter (Facebook, Github, etc.) mit RDMO zu verwenden, fügen Sie hinzu:


.. code:: python

    from rdmo.core.settings import INSTALLED_APPS, AUTHENTICATION_BACKENDS

    ACCOUNT = True
    ACCOUNT_SIGNUP = True
    SOCIALACCOUNT = True

    INSTALLED_APPS += [
        'allauth',
        'allauth.account',
        'allauth.socialaccount'
        'allauth.socialaccount.providers.facebook',
        'allauth.socialaccount.providers.github',
        'allauth.socialaccount.providers.google',
        'allauth.socialaccount.providers.orcid',
        'allauth.socialaccount.providers.twitter',
        ...
    ]

    AUTHENTICATION_BACKENDS.append('allauth.account.auth_backends.AuthenticationBackend')

in ihre ``config/settings/local.py``. Die Einstellung ``SOCIALACCOUNT = True`` wird von RDMO verwendet, um bestimmte Teile der Benutzeroberfläche mit den Accounts dritter Anbieter anzuzeigenm, während wie zuvor die Zeilen nach ``INSTALLED_APPS`` es dem Feauture erlaubt von RDMO verwendet zu werden. Jeder Anbieter hat eine separate App, die du zu ``INSTALLED_APPS`` hinzufügen kannst. Eine Lister aller von Django-allauth unterstützen Anbieter findest du `hier <http://django-allauth.readthedocs.io/en/latest/providers.html>`_.

Sobald die Installation abgeschlossen ist, müssen die Zugangsdaten ihres OAuth-Anbieters in dem Admin-Interface eingegeben werden. Dies wird im :doc:`Administration-Kapitel </administration/allauth>` dieser Dokuemntation erklärt.
