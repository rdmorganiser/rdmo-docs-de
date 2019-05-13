# Einrichten der Anwendung

Um die Anwendung einzurichten, erstellen Sie eine neue Datei `config/settings/local.py` in ihrem geklonten`rdmo-app`-Ordner. Für unseren Beispielbenutzer mit dem Homeverzeichnis `/srv/rdmo` wäre dies `/srv/rdmo/rdmo-app/config/settings/local.py`.

Sie können `config/settings/sample.local.py` als Vorlage verwenden, d.h.:

```bash
cp config/settings/sample.local.py config/settings/local.py    # on Linux or macOS
copy config\settings\sample.local.py config\settings\local.py  # on Windows
```

Die meisten Einstellungen ihrer RDMO-Instanz sind in dieser Datei festgelegt. Die unterschiedlichen Einträge sind im Detail in  [später in der Dokumentation](../../configuration/index.html) erklärt. Für eine Minimal-Konfiguration müssen Sie `DEBUG = True` setzen, um ausführliche Fehlermeldungen zu erhalten und statische Dateien zu nutzen. Setzen Sie außerdem `SECRET_KEY` zu einem langen, zufälligen String, den Sie geheim halten. Ihre Datenbank-Verbindung wird mit Hilfe der  `DATABASES` Variablen gesetzt. Die Konfiguration der Datenbank wird  [später in der Dokumentation](../../configuration/databases.html) erklärt. Wenn keine `DATABASE` gesetzt ist, wird `sqlite2` verwendet.

Dann starten Sie die Datenbank der Anwendung:

```bash
python manage.py migrate                # initializes the database
python manage.py setup_groups           # creates groups with different permissions
python manage.py createsuperuser        # creates the admin user
```

## Vendor Files von Drittanbietern

Standardmäßig werden Drittanbieterdateien (wie jQuery oder Bootstrap-Javascripts) aus den Content-Delivery-Netzwerken abgerufen, in denen sie bereitgestellt werden. Wenn Sie Anfragen von Dritten vermeiden möchten, können Sie diese selbst hosten. Dies kann mit zwei einfachen Schritten einfach erreicht werden.



1. Laden Sie die Herstellerdateien von den CDs herunter, indem Sie das mitgelieferte Skript ausführen.

    ```python
    python manage.py download_vendor_files
    ```

2. Stellen Sie sicher, dass Ihre `local.py` die folgende Zeile enthält

    ```
    VENDOR_CDN = False
    ```

## RDMO development server

Nach diesen Schritten kann RDMO mit dem integriertem Entwicklungsserver von Django betrieben werden:

```bash
python manage.py runserver
```

Anschließend ist RDMO unter http://127.0.0.1:8000 in ihrem (lokalen) Browser verfügbar. Die unterschiedlichen Wege, wie RDMO betrieben werden kann, werden im nächsten Kapitel behandelt. Die neu installierte RDMO-Instanz ist noch leer, d.h. es sind keine Fragebögen oder Ansichten verfügbar. Sie müssen[importiert](../../../management/export.html) und/oder wie unter[Management](../../../management/index.html) beschrieben erstellt werden.
