Installation
============

Für Demonstrations-, Entwicklungs- oder Testzwecke kann RDMO auf Linux, WIndows und maxOS installiert werden. Falls du jedoch eine Produktionsumgebung aufsetzen möchtest, RDMO über ein Netzwerk oder das Internet anbieten möchtest, dann empfehlen wir sehr eine aktuelle Linux-Version, namentlich CentOS7, Debian 8 oder 9, oder Ubuntu 16.04.3 LTS (Xenial Xerus) zu verwenden.

Der Code ist hauptsächlich in Python geschrieben und sollte mit Python höher als 3.4 laufen. RDMO funktioniert auch mit Python 2.7. Beachte, dass für CentOS7/Apache-Setup nut Python 2.7 verwendet werden kann.

Eine RDMO-Installation enthält drei Teile:

1) Ein Ordner, der alle Einstellungen und Anspassungen enthält, die deine RDMO-Installation individualisiert. Wir werden diesen Ordner ``rdmo-app`` nennen, aber du kannst jeden beliebigen Namen verwenden.
2) Das eigentliche ``rdmo`` Paket, welches zentral vom RDMO-Team unterhalten wird und als Abhängigkeit in einer virutellen Umgebung installiert ist.
3) Eine Datenbank, um den vom Benutzer erstellten Inhalt deiner RDMO-Installation zu speichern. Aktuell untersützen wir Postgres, MySQL und SQLite.

Dieses Kapitel zeigt wie diese Komponenten aufgebaut werden. Optionale Komponenten können im Anschluss installiert werden und sind unter  :doc:`Konfiguration </configuration/index>` dokumentiert.

Für Test- und Entwicklungszwecke kann RDMO mit deinem regulären Benutzer-Account betrieben werden. Im Produktionsbetrieb sollte ein dedizierter Benutzer verwendet werden. Wir empfehlen einen Benutzer names ``rdmo`` mit der Gruppe ``rdmo`` und dem Homeverzeichnis ``/srv/rdmo`` zu erstellen. Wir werden diesen Benutzer in der gesamten Dokumentation verwenden.

Verwende nicht den ``root`` Benutzer, um RDMO auszuführen! Es ist generell eine schlechte Idee  und viele Installationsschritte würden nicht funktionieren. ``sudo`` wird während der Installation verwendet, wenn Root-Rechte nötig sind, um Pakete zu installiren.

.. toctree::
   :caption: Index
   :maxdepth: 2

   prerequisites
   clone
   packages
   setup
