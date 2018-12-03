Entwicklungsserver
------------------

Django besitzt einen integrierten Entwicklungsserver. Dieser wird wie folgt gestartet:

.. code:: bash

    python manage.py runserver

Danach ist RDMO unter http://localhost:8000 in Ihrem (lokalen) Browser verfügbar. Der Entwicklungsserver ist **nicht** geeignet, um die Anwendung im Internet anzubieten.

Falls Sie den Entwicklungsserver für andere Rechner in ihrem lokalen Netzwerk zugänglich machen wollen, müssen sie folgendes verwenden:

.. code:: bash

    python manage.py runserver 0.0.0.0:8000

wobei ``8000`` der HTTP-Port ist und angepasst werden kann. Bitte benutzten Sie dieses Setup ausschließlich für Tests und Entwicklung, da der Server nicht sicher ist. Der Entwicklungsserver liefert statische Dateien nur im Debug-Modus aus. Bitte vergesse Sie daher nicht die Zeile ``DEBUG = False`` in ihrer ``config/settings/local.py`` auf ``DEBUG = True`` zu ändern.

Weitere Informationen über den Entwicklungsserver können unter `Django Dokumentation <https://docs.djangoproject.com/en/1.10/intro/tutorial01/#the-development-server>`_ nachgelesen werden.
