# Django-allauth

RDMO verwendet das großartige [django-allauth](http://www.intenct.nl/projects/django-allauth) als  Haupt-Authentifizierungs-Modul. Es ermöglicht Workflows für Benutzerregistration und Passwortabfrage, genauso wie Authentifizierung durch Drittanbieter-Webseiten mit Hilfe von OAUTH2.

## Accounts

Um reguläre Accounts in RDMO anzulegen, fügen Sie folgendes zu ihrer `config/settings/local.py` hinzu:

```python
from rdmo.core.settings import INSTALLED_APPS, AUTHENTICATION_BACKENDS

ACCOUNT = True
ACCOUNT_SIGNUP = True

INSTALLED_APPS += [
    'allauth',
    'allauth.account',
]

AUTHENTICATION_BACKENDS.append('allauth.account.auth_backends.AuthenticationBackend')
```

Die Einstellung `ACCOUNT = True` aktiviert die allgemeinen Django-allauth Eigenschaften in RDMO, `ACCOUNT_SIGNUP = True` erlaubt es neue Benutzer in Ihrer RDMO-Instanz zu registrieren.
Das Verhalten von `Django-allauth` kann durch weitere Einstellungen konfiguriert werden, die unter [django-allauth documentation](http://django-allauth.readthedocs.io/en/latest/configuration.html) dokumentiert sind. RDMO setzt einige Standardwerte, die in `config/settings/base.py` gefunden werden können.


## Soziale Accounts

Um Accounts von Webseiten dritter Anbieter (Facebook, Github, etc.) mit RDMO zu verwenden, fügen Sie folgendes zu ihrer `config/settings/local.py` hinzu:

```python
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
```

Die Einstellung `SOCIALACCOUNT = True` wird von RDMO verwendet, um bestimmte Teile der Benutzeroberfläche mit den Accounts dritter Anbieter anzuzeigen, während wie zuvor die Zeilen nach `INSTALLED_APPS` es dem Feature erlaubt von RDMO verwendet zu werden. Jeder Anbieter hat eine separate App, die Sie zu `INSTALLED_APPS` hinzufügen können. Eine Liste aller von Django-allauth unterstützen Anbieter finden Sie [hier](http://django-allauth.readthedocs.io/en/latest/providers.html).

Sobald die Installation abgeschlossen ist, müssen die Zugangsdaten ihres OAuth-Anbieters im Admin-Interface eingegeben werden. Dies wird im [Administration-Kapitel](../../../../administration/allauth.html) dieser Dokumentation erklärt.
