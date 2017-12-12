Überblick über das App-Verzeichnis
----------------------------------

Der nächste Schritt ist ein ``rdmo-app``-Verzeichnis durch Klonen des entsprechenden Repositories zu erstellen:

.. code:: bash

    git clone https://github.com/rdmorganiser/rdmo-app
 
Beachte, dass dies nicht das Haupt-``rdmo``-Repository ist, sondern nur die Konfigurationsdateien enthält. In diesem Ordner findest du folgendes:

* ein ``config``-Ordner, der die Haupteinstellungen deiner RDMO-Installation enthält,
* ein ``requirements``-Order, der Schnellverfahren zur Installierung von verschiedenen obligatoritschen und optionalen Abhängigkeiten enthält, und
* ein ``manage.py``Skript, dass den Hauptweg darstellt, um mit deiner RDMO-Instalaltion über die Kommandozeile zu interagieren. Die meisten dieser Schritte werden in diesem Skript verwendet.

Der ``rdmo-app``-Ordner entspricht einem `project <https://docs.djangoproject.com/en/1.11/intro/tutorial01>`_ in Django Bestimmungen.
