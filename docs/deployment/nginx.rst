nginx und gunicorn
------------------

Wie bereits mehrfach erwähnt sollte eine dezidierter Benutzer für RDMO verwendet werden. Alle Schritte in der Anleitung, welche keine Root-Rechte benötigen, sollten mit diesem dezidierten Benutzer ausgeführt werden. Hier gehen wir davon aus, dass der Benutzer ``rdmo`´ genannt wurde und sein Home-Verzeichnis ``/srv/rdmo`` ist und demnach ihre ``rdmo-app`` unter ``/srv/rdmo/rdmo-app`` zu finden ist.

Als erstes installieren Sie gunicorn in ihrer virtuellen Umgebung:

.. code:: bash

    pip install -r requirements/gunicorn.txt

Dann testen Sie ``gunicorn``:

.. code:: bash

    gunicorn --bind 0.0.0.0:8000 config.wsgi:application

Dies sollte die Anwendung genauso wie ``runserver`` laufen lassen, aber ohne statische Inhalte wie CSS-Dateien oder Bilder. Nach dem Test beenden Sie den ``gunicorn``-Prozess wieder.

Jetzt erstellen Sie eine systemd service Datei für RDMO. Systemd wird den gunicorn-Prozess bei der Intriebnahme launchen und es am Laufen halten. Erstellen Sie eine neue Datei unter `/etc/systemd/system/rdmo.service`  und geben Sie ein (Sie benötigen Root/sudo-Rechte dafür): 
::

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

Dieser Service muss gestartet und aktiviert werden wie jeder andere Service auch:

.. code:: bash

    sudo systemctl start rdmo
    sudo systemctl enable rdmo

Danach installieren Sie nginx:

.. code:: bash

    sudo apt install nginx  # on Debian/Ubuntu
    sudo yum install nginx  # on RHEL/CentOS

Veränderen Sie die nginx-Konfiguration wie folgt (mit root/sudo-Rechten):

.. code:: bash

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

Starten Sie nginx neu. RDMO sollte nun unter ``YOURDOMAIN`` verfügbar sein. Beachten Sie, dass der Unix-Socket ``/srv/rdmo/rdmo.sock`` für nginx zugänglich sein muss.

Wie Sie der virtuellen Host-Konfirguration entnehmen können, werden statische Inhalte wie CSS und JavaScript-Dateien unabhängig von dem entgegengesetzten Proxy zu dem gunicorn-Prozess bedient. Um dies zu erreichen müssen diese in dem ``static_root``-Ordner erfasst werden. Dies kann durch folgendes:

.. code:: bash

    python manage.py collectstatic

in ihrer virtuellen Umgebung erreicht werden.

Um Veränderungen im RDMO-Code (z.B. nach einem :doc:`Upgrade </upgrade/index>`) umzusetzen, muss der gunicorn-Prozess neu gestartet werden: 

.. code:: bash

    sudo systemctl restart rdmo
