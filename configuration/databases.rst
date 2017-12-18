Datenbanken
-----------

RDMO kann mit allen Datenbanken, die vom Django-Framework unterstützt werden, verwendet werden. Die jeweilige Datenbankverbindung wird mit der Einstllung ``DATABASE`` definiert. Eine Übersicht über die Django Datenbaneinstlelungen findest du `hier <https://docs.djangoproject.com/en/1.10/ref/settings/#databases>`_. Im folgenden zeigen wir die Einstellungen für PostgreSQL, MySQL und SQLite.

PostgreSQL
``````````

PostgreSQL kann wie folgt installiert werden:

.. code:: bash

    # Debian/Ubuntu
    sudo apt install postgresql

    # CentOS
    sudo yum install postgresql-server postgresql-contrib
    sudo postgresql-setup initdb
    sudo systemctl start postgresql
    sudo systemctl enable postgresql

Um PostgreSQL als ihre Datenbank-Backend nutzen zu können, installieren Sie ``psycopg2`` in ihrer virtuellen Umgebung:

.. code:: bash

    pip install -r requirements/postgres.txt

Dann fügen Sie folgende Zeilen zu ``config/settings/local.py`` hinzu:

.. code:: python

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'rdmo',
            'USER': 'rdmo',
            'PASSWORD': '',
            'HOST': '',
            'PORT': '',
        }
    }

wobei ``Name`` der Name der Datenbank ist, ``USER`` der PostgreSQL Benutzer, ``PASSWORD`` dessen Passwort, ``HOST`` der Datenbankhost und ``PORT`` der Port von PostgreSQL. Beachten Sie, dass abhängig von ihrem Setup nicht alle Einstellungen benötigt werden. Falls Sie Peer-Authenfizierungsmethoden verwendeen, brauchen Sie nur die ``NAME`` und ``ENGINE``-Einstellungen. Der Benutzer und die Datenbank werden wie folgt gesetzt:

.. code-block:: bash

    sudo su - postgres
    createuser rdmo
    createdb rdmo -O rdmo

Dies setzt Peer-Authentifizierung für den RDMO-Benutzer voraus.

Das Kommando

.. code:: bash

    python manage.py migrate

sollte nun die RDMO Datenbank-Tabellen in PostegreSQL erstellen.


MySQL
`````

MySQL (oder den Community-entwickleten Abzweig MariaDB) kann wie folgt installiert werden: 

.. code:: bash

    # Debian/Ubuntu
    sudo apt install mysql-client mysql-server libmysqlclient-dev        # for MySQL
    sudo apt install mariadb-client mariadb-server libmariadbclient-dev  # for MariaDB

    # CentOS
    sudo yum install -y mysql mysql-server mysql-devel                            # for MySQL
    sudo yum install -y mariadb mariadb-server mariadb-devel                      # for MariaDB
    sudo systemctl enable mariadb
    sudo systemctl start mariadb
    sudo mysql_secure_installation

Um MYSQL als ihren Datenbank-Backend zu nutzen, installieren Sie ``mysqlclient´´ in ihrer virtuellen Umgebung:

.. code:: bash

    pip install -r requirements/mysql.txt

Danach, fügen Sie folgendes ihrer ``config/settings/local.py`` hinzu:

.. code:: python

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'rdmo',
            'USER': 'rdmo',
            'PASSWORD': 'not a good password',
            'HOST': '',
            'PORT': '',
            'OPTIONS': {
                'unix_socket': '',
            }
        }
    }

Hier ist ``Name`` der Name der Datenbank, ``USER`` der MySQL-Benutzer, ``PASSWORD`` das selbstgwählte Passwort, ``HOST`` der Datenbank-Host und ``PORT`` der zugehörige Port. Falls Sie``/tmp/mysql.sock`` nicht benutzen, können Sie ``unix-socket`` verwenden, um den Pfad zu setzen. Der Benutzer und die Datenbank werden wie folgt erstellt:

.. code-block:: mysql

    CREATE USER 'rdmo'@'localhost' identified by 'not a good password';
    GRANT ALL ON `rdmo`.* to 'rdmo'@'localhost';
    CREATE DATABASE `rdmo`;

auf der MySQL-shell.

Das Kommando

.. code:: bash

    python manage.py migrate

sollte jetzt die RDMO Datenbank-Tabellen in MySQL angelegen.


SQLite
``````

SQLite ist die Standardoption in RDMO und unter ``config/settings/base.py`` konfiguriert. Wir empfehlen dies nur für das Entwicklungs-/Test-Setup zu verwenden. Es kann unter ``config/settings/local.py`` konfiguriert werden, indem folgendes hinzugefügt wird:

.. code:: python

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': '',
        }
    }

wobei ``Name`` der Name der Datenbankdatei ist.

Das Kommando

.. code:: bash

    python manage.py migrate

sollte nun die RDMO Datenbank-Tabellen in der angegeben Datenbankdatei erstellen.
