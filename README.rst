RDMO - Dokumentation (Deutsch)
==============================

.. image:: http://unmaintained.tech/badge.svg
   :alt: No Maintenance Intended
   :target: http://unmaintained.tech/

**Die deutsche Dokumentation wird seit Januar 2020 nicht mehr weiter gepflegt und sollte auch nicht mehr über https://rdmo.readthedocs.io verfügbar sein.**


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
