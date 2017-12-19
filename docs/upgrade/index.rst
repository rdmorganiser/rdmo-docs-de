Upgrade
=======

Das ``rdmo`` Paket kann ganz bequem mit dem `pip`-Kommando akualisiert werden. Allerdings, bevor Sie irgendwelche Änderungen an ihrer Installation vornehmen, erstellen Sie bitte ein Backup der wichtigsten Bestandteile an einem sicheren Ort.

Eine PostgreSQL oder MySQL-Datenbank kann in eine Datei geschrieben werden:

.. code:: bash

    pg_dump [DBNAME] > rdmo.sql  # PostgreSQL
    mysqldump -uroot -p [DBNAME] > rdmo.sql

Ihr ``rdmo-app``-Ordner (einschließlich jeglicher sqlite3-Datenbank) kann mit folgendem Kommando kopiert werden. Beachten Sie, dass ihre virtuelle Umgebung nicht funktionieren wird, nachdem sie an einen anderen Ort (Pfad) kopiert wurde.

Um ihre RDMO-Instalaltion zu aktualisieren, gehen Sie in ihren ``rdmo-app``-Ordner, aktivieren Sie ihre virtuelle Umgebung und aktualisieren Sie das ``rdmo`` mit Hilfe von ``pip``:

.. code:: bash

    pip install --upgrade rdmo

Um eine bestimmte Version von RDMO (z.B. 0.9.0) zu installieren, verwenden Sie:

.. code:: bash

    pip install --upgrade rdmo==0.9.0

Nach der Aktualisierung, kann eine Datenbank-Migration notwendig sein:

.. code:: bash

    python manage.py migrate

Bitte beachten Sie die Release-Hinweise, ob dieser oder weitere Schritte notwendig sind.


Upgrade to version 0.9.0
------------------------

Mit der Version 0.9.0 haben wir eine Separation von der -´-´rdmo-app`` und dem zentral verwalteten ``rdmo``-Paket vorgenommen. Daher sind einige zusätzliche Schritte für die Aktualisierung zur Version 0.9.0 und höher notwendig:

1) Erstellen Sie immer ein Backup ihres ``rdmo``-Ordners und ihrer Datenbank wie oben beschrieben.

2) Führen Sie die Schritte wie unter :doc:`/installation/clone` und :doc:`/installation/packages` beschrieben durch, so wiesie eine neue RDMO-Instanz installieren würden.

3) Kopieren Sie ihre alte Einstellungen von ``/path/to/old/rdmo/rdmo/settings/local.py`` zu ``/path/to/new/rdmo-app/config/settings/local.py``. Der neue ``config``-Ordner ersetzt den alten ``rdmo``-Ordner. 

4) Falls sie einen ``theme``-Ordner besitzen, kopieren Sie diesen bitte in den neuen ``rdmo-app``-Ordner.

5) Führen Sie eine Datenbank-Migration durch (Es sei denn Sie haben einige Versionen übersprungen, dann kann der Output ``Keine Migration notwendig.`` sein.):

    .. code:: bash

        python manage.py migrate

6) Downloaden Sie die Front-En-Dateien vom CDN. Wir verwenden Bower und npm nicht mehr.

    .. code:: bash

        python manage.py download_vendor_files

7) Aktualisieren Sie den Pfad im ``wsgi.py`` Skript in ihren Apache oder nginx Einstellungen. Dies befindet sich nun unter ``/path/to/new/rdmo-app/config/wsgi.py``.

8) Setzen Sie RDMO neu auf wie unter :doc:`/deployment/apache` oder :doc:`/deployment/nginx` beschrieben.

Falls irgendwelche Probleme während des Aktualisierungsprozesses auftreten, zögern Sie nicht das RDMO-Team um Hilfe zu fragen.
