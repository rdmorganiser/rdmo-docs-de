Erstellung des App-Verzeichnis
----------------------------------

Im nächsten Schritt ist ein ``rdmo-app``-Verzeichnis durch Klonen des entsprechenden Repositoriums im Home-Verzeichnis ihres ``rdmo``-Benutzers zu erstellen:

.. code:: bash

    git clone https://github.com/rdmorganiser/rdmo-app

Beachten Sie, dass dies nicht das Haupt-``rdmo``-Repositorium ist, da es nur die Konfigurationsdateien enthält. In diesem Ordner finden Sie folgendes:

* einen ``config``-Ordner, der die Haupteinstellungen ihrer RDMO-Installation enthält
* einen ``requirements``-Order, der Schnellverfahren zur Installation von verschiedenen obligatorischen und optionalen Abhängigkeiten enthält
* ein ``manage.py``-Skript, durch das Sie mit ihrer RDMO-Installation über die Kommandozeile interagieren können. Für fast alle folgenden Schritte wird dieses Skript verwendet.

Der ``rdmo-app``-Ordner entspricht einem `Projekt <https://docs.djangoproject.com/en/1.11/intro/tutorial01>`_ in Django.
