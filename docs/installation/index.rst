Installation
============

Für Demonstrations-, Entwicklungs- oder Testzwecke kann RDMO auf Linux, Windows und macOS installiert werden. Falls Sie jedoch eine Produktionsumgebung aufsetzen möchten, RDMO über ein Netzwerk oder das Internet anbieten möchten, empfehlen wir die Verwendung einer aktuellen Linux-Distribution, insbesondere CentOS7, Debian 8 oder 9, oder Ubuntu 16.04.3 LTS (Xenial Xerus).

Der Code ist hauptsächlich in Python geschrieben und sollte mit Python höher als Version 3.4 laufen. RDMO funktioniert auch mit Python 2.7. Beachten Sie, dass für ein CentOS7/Apache-Setup nur Python 2.7 verwendet werden kann.

Eine RDMO-Installation hat drei Komponenten:

1) Ein Ordner, der alle Einstellungen und Anspassungen enthält, die ihre RDMO-Installation individualisiert. Wir werden diesen Ordner ``rdmo-app`` nennen.
2) Das eigentliche ``rdmo`` Paket, welches zentral vom RDMO-Team gepflegt wird. Dies Paket wird in einer virtuellen Umgebung installiert.
3) Eine Datenbank, um den vom Benutzer erstellten Inhalt ihrer RDMO-Installation zu speichern. Aktuell untersützen wir PostgreSQL, MySQL und SQLite.

Dieses Kapitel zeigt wie diese Komponenten installiert werden. Optionale Komponenten können danach installiert werden, sie sind unter :doc:`Konfiguration </configuration/index>` dokumentiert.

Für Test- und Entwicklungszwecke kann RDMO mit ihrem regulären Benutzer-Account betrieben werden. Im Produktionsbetrieb sollte ein dedizierter Benutzer verwendet werden. Wir empfehlen einen Benutzer namens ``rdmo`` mit der Gruppe ``rdmo`` und dem Homeverzeichnis ``/srv/rdmo`` zu erstellen: ``sudo adduser rdmo --home /srv/rdmo`` . Wir werden diesen Benutzer mit dem genannten Profil in der gesamten Dokumentation verwenden.

Verwenden Sie nicht den ``root`` Benutzer, um RDMO auszuführen! Es ist generell eine schlechte Idee und viele Installationsschritte  funktionieren nicht. ``sudo`` wird während der Installation verwendet, wenn root-Rechte nötig sind, um Pakete zu installieren.

.. toctree::
   :caption: Index
   :maxdepth: 2

   prerequisites
   clone
   packages
   setup
