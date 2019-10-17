# Upgrade

Das `rdmo` Paket kann ganz bequem mit dem `pip`-Kommando akualisiert werden. Bevor Sie irgendwelche Änderungen an ihrer Installation vornehmen, sollten Sie allerdings ein Backup der wichtigsten Bestandteile an einem sicheren Ort erstellen.

Eine PostgreSQL oder MySQL-Datenbank kann in eine Datei geschrieben werden:

```bash
pg_dump [DBNAME] > rdmo.sql  # PostgreSQL
mysqldump -uroot -p [DBNAME] > rdmo.sql # MySQL, MariaDB
```

Ihr `rdmo-app`-Ordner (einschließlich jeglicher sqlite3-Datenbank) kann mit üblichen Befehlen kopiert werden. Beachten Sie, dass ihre virtuelle Umgebung nicht funktionieren wird, nachdem sie an einen anderen Ort (Pfad) kopiert wurde.

Um ihre RDMO-Installation zu aktualisieren, gehen Sie in ihren `rdmo-app`-Ordner, aktivieren Sie ihre virtuelle Umgebung und aktualisieren Sie `rdmo` mit Hilfe von `pip`:

```bash
pip install --upgrade rdmo
```

Um eine bestimmte Version von RDMO (z.B. 0.9.0) zu installieren, verwenden Sie:

```bash
pip install --upgrade rdmo==0.9.0
```

Nach der Aktualisierung, kann eine Datenbank-Migration notwendig sein:

```bash
python manage.py migrate
```

In jedem Fall ist es notwendig folgendes Kommando auszuführen, damit das Upgrade auch umgesetzt wird:

```bash
python manage.py deploy
```

Bitte beachten Sie die Release-Hinweise, ob dieser oder weitere Schritte notwendig sind.


Upgrade zu Version 0.9.0
------------------------

Mit der Version 0.9.0 haben wir die Teilung in `rdmo-app` und dem zentral verwalteten `rdmo`-Paket vorgenommen. Daher sind einige zusätzliche Schritte für die Aktualisierung zur Version 0.9.0 und höher notwendig:

1. Erstellen Sie immer ein Backup ihres `rdmo`-Ordners und ihrer Datenbank wie oben beschrieben.

1. Führen Sie die Schritte wie unter [klonen](../installation/clone.html) und [Pakete installieren](../installation/packages.html) beschrieben durch, wie sie eine neue RDMO-Instanz installieren würden.

1. Kopieren Sie ihre alte Einstellungen von `/path/to/old/rdmo/rdmo/settings/local.py` zu `/path/to/new/rdmo-app/config/settings/local.py`. Der neue `config`-Ordner ersetzt den alten `rdmo`-Ordner.

1. Falls sie einen `theme`-Ordner besitzen, kopieren Sie diesen bitte in den neuen `rdmo-app`-Ordner.

1. Führen Sie eine Datenbank-Migration durch (Falls Sie einige Versionen übersprungen haben, kann auch die Meldung: `Keine Migration notwendig.`) erscheinen:

    ```bash
    python manage.py migrate
    ```

1. Downloaden Sie die Front-End-Dateien vom CDN. Wir verwenden [Bower](https://bower.io) und [npm](https://www.npmjs.com) nicht mehr.

    ```bash
    python manage.py download_vendor_files
    ```

1. Aktualisieren Sie den Pfad zum `wsgi.py` Skript in ihren Apache- oder nginx-Einstellungen. Es befindet sich nun unter `/path/to/new/rdmo-app/config/wsgi.py`.

1. Setzen Sie RDMO neu auf wie unter [Apache](../deployment/apache.html) oder [Nginx](../deployment/nginx.html) beschrieben.

Falls irgendwelche Probleme während des Aktualisierungsprozesses auftreten, zögern Sie nicht das RDMO-Team um Hilfe zu bitten.


Upgrade zu Version 0.14
-----------------------

Mit Version 0.14 wird die Python2 unterstützung eingestellt und zu Django 2.2 gewechselt. Dies benötige Änderungen an der `rdmo-app`:

* `MIDDLEWARE_CLASSES` in `config/settings/local.py` muss in `MIDDLEWARE` umbenannt werden.
* `config/urls.py` wird deutlich vereinfacht, die Bezeichner der Funktionen ändert sich jedoch. Eine Vorlage kann [hier](https://github.com/rdmorganiser/rdmo-app/blob/master/config/urls.py) eingesehen werden.
