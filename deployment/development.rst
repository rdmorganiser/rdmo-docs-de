Entwicklungsserver
------------------

Django besitzt einen integrierten Entwicklungsserver. Diese kann wie folgt gestart werden:

.. code:: bash

    python manage.py runserver

Danach ist RDMO unter http://localhost:8000 in ihrem (lokalen) Browser verfügbar. Der Entwicklungsserver ist **nicht** geeignet, um die Anwendung im Internet anzubieten.

Falls Sie den Entwicklungsserver für andere Machinen zugänglich machen wollen, müssen sie folgendes verwenden:

.. code:: bash

    python manage.py runserver 0.0.0.0:8000

wobei ``8000`` der Port ist und für ihre Bedürfnisse angepasst werden kann. Bitte benutzten Sie dieses Setup ausschließlich für Tests und Entwicklung, da es nciht sicher ist.

Weitere Informationen über den Entwicklungsserver kann unter `Django Dokumentation <https://docs.djangoproject.com/en/1.10/intro/tutorial01/#the-development-server>`_ gefunden werden.
