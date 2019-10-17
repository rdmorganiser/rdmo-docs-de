# Nginx und Gunicorn

Für RDMO sollte ein dezidierter Benutzer verwendet werden. Alle Schritte in der Anleitung, welche keine Root-Rechte benötigen, sollten mit diesem dezidierten Benutzer ausgeführt werden. Hier gehen wir davon aus, dass der Benutzer `rdmo`´ genannt wurde, sein Home-Verzeichnis `/srv/rdmo` ist und demnach ihre `rdmo-app` unter `/srv/rdmo/rdmo-app` zu finden ist.

Als erstes installieren Sie  `gunicorn` in ihrer virtuellen Umgebung:

```bash
pip install -r requirements/gunicorn.txt
```

Dann testen Sie `Gunicorn`:

```bash
gunicorn --bind 0.0.0.0:8000 config.wsgi:application
```

Dies sollte die Anwendung genauso wie `runserver` laufen lassen, aber ohne statische Inhalte wie CSS-Dateien oder Bilder. Nach dem Test beenden Sie den `gunicorn`-Prozess wieder.

Dann erstellen Sie für den systemd service eine Datei für RDMO. Systemd wird den gunicorn-Prozess bei der Intriebnahme starten und überwachen. Erstellen Sie eine neue Datei unter `/etc/systemd/system/rdmo.service`  und geben Sie ein (Sie benötigen root/sudo-Rechte dafür):

```
[Unit]
Description=RDMO gunicorn daemon
After=network.target

[Service]
User=rdmo
Group=rdmo
WorkingDirectory=/srv/rdmo/rdmo-app
ExecStart=/srv/rdmo/rdmo-app/env/bin/gunicorn --bind unix:/srv/rdmo/rdmo.sock config.wsgi:application

[Install]
WantedBy=multi-user.target
```

Dieser Service muss gestartet und aktiviert werden wie jeder andere Service auch:

```bash
sudo systemctl start rdmo
sudo systemctl enable rdmo
```

Danach installieren Sie nginx:

```bash
sudo apt install nginx  # on Debian/Ubuntu
sudo yum install nginx  # on RHEL/CentOS
```

Veränderen Sie die nginx-Konfiguration wie folgt (mit root/sudo-Rechten):

```nginx
    # in /etc/nginx/sites-available/default  on Debian/Ubuntu
    # in /etc/nginx/conf.d/vhost.conf        on RHEL/CentOS
    server {
        listen 80;
        server_name YOURDOMAIN;

        location / {
            proxy_pass http://unix:/srv/rdmo/rdmo.sock;
        }
        location /static/ {
            alias /srv/rdmo/rdmo-app/static_root/;
        }
    }
```

Starten Sie nginx neu. RDMO sollte nun unter `YOURDOMAIN` verfügbar sein. Beachten Sie, dass der Unix-Socket `/srv/rdmo/rdmo.sock` für nginx zugänglich sein muss.

Wie Sie der virtuellen Host-Konfiguration entnehmen können, werden statische Inhalte wie CSS und JavaScript-Dateien unabhängig über den Reverse-Proxy dem gunicorn-Prozess zur Verfügung gestellt. Um dies zu erreichen, werden diese in dem `static_root`-Ordner erfasst. Hierzu wird das Kommando

```bash
python manage.py collectstatic
```

in ihrer virtuellen Umgebung ausgeführt.

Bei Veränderungen im RDMO-Code (z.B. nach einem [Upgrade](../upgrade/index.html)) muss der gunicorn-Prozess neu gestartet werden:

```bash
sudo systemctl restart rdmo
```
