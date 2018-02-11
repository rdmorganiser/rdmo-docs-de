RDMO - Research Data Management Organiser
=========================================

RDMO unterestuetzt die systematische Planung, Organisation und Durchfuehrung des Datenmanagements waehrend des ganzen Forschungsprozesses. Das Projekt wird gefoerdert von der Deutschen Forschungsgemeinschaft (DFG).

Dokumentation (Deutsch)
------------------

Setup
~~~~~

Zunaechst sind die Python Module `sphinx`, `sphinx-autobuild` und `sphinx_rtd_theme` zu installieren:

.. code:: bash

    pip install -r requirements.txt

Dann koennen die HTML-Seiten erzeugt werden mit:

.. code:: bash

    make html

Ein Live-Server, der automatisch geaenderte Dateien anzeigt, sobald die HTML-Seite gesichert wurde, wird gestartet mit:

.. code:: bash

    make live

Die Documentation ist dann unter der URL http://localhost:8000 abzurufen.
