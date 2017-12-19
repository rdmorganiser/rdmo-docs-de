Einrichten der Anwendung
------------------------

Um die Anwendung einzurichten erstellen Sie eine neue Datei ``config/settings/local.py`` in ihrem geklonten``rdmo-app``-Ordner. Für unseren Beispielbenutzer mit dem Homeverzeichnis ``/srv/rdmo`` wäre dies ``/srv/rdmo/rdmo-app/config/settings/local.py``.

Sie können ``config/settings/sample.local.py`` als Vorlage verwenden, d.h.:

.. code:: bash

    cp config/settings/sample.local.py config/settings/local.py    # on Linux or macOS
    copy config\settings\sample.local.py config\settings\local.py  # on Windows

Die meisten Einstellungen ihrer RDMO-Instanz sind in dieser Datei festgelegt. Die unterschiedlichen Einstellungen sind im Detail :doc:`später in der Dokumentation </configuration/index>` erklärt. Für eine Minimal-Kofniguration müssen Sie ``DEBUG = True`` setzen, um ausführliche Fehlermeldungen zu erhalten und statische Dateien zu nutzen. Setzen Sie außerdem ``SECRET_KEY`` zu einem langen, zufälligen String, den Sie geheim halten. Ihre Datenbank-Verbindung wird mit Hilfe der  ``DATABASES`` Variablen gesetzt. Die Konfiguration der Datenbank wird  :doc:`später in der Dokumentation </configuration/databases>` erklärt. Wenn keine ``DATABASE`` gesetzt ist, wird ``sqlite2`` verwendet.

Dann starten Sie die Datenbank der Anwendung:

.. code:: bash

    python manage.py migrate                # initializes the database
    python manage.py create_groups          # creates groups with different permissions
    python manage.py createsuperuser        # creates the admin user
    python manage.py download_vendor_files  # dowloads front-end files from the CDN

Nach diesen Schritten kann RDMO mit Djangos integriertem Entwicklungsserver betrieben werden:

.. code:: bash

    python manage.py runserver

Anschließend ist RDMO unter http://127.0.0.1:8000 in ihrem (lokalen) Browser verfügbar. Die unterschiedlichen Wege wie RDMO eingesetzt werden kann, werden im nächsten Kapitel behandelt. 
