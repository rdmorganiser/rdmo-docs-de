Erstellung des App-Verzeichnis
----------------------------------

Im nächsten Schritt ist ein ``rdmo-app``-Verzeichnis durch Klonen des entsprechenden Repositories zu erstellen:

.. code:: bash

    git clone https://github.com/rdmorganiser/rdmo-app
 
Beachten Sie, dass dies nicht das Haupt-``rdmo``-Repository ist, sondern nur die Konfigurationsdateien enthält. In diesem Ordner finden Sie folgendes:

* einen ``config``-Ordner, der die Haupteinstellungen ihrer RDMO-Installation enthält,
* einen ``requirements``-Order, der Schnellverfahren zur Installierung von verschiedenen obligatoritschen und optionalen Abhängigkeiten enthält, und
* ein ``manage.py``-Skript, dass die Hauptmethode darstellt, um mit ihrer RDMO-Installation über die Kommandozeile zu interagieren. Für fast alle folgenden Schritte wird dieses Skript verwendet.

Der ``rdmo-app``-Ordner entspricht einem `project <https://docs.djangoproject.com/en/1.11/intro/tutorial01>`_ in Django.
