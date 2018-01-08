Administration
==============

Das Django-Framework bietet ein reichhaliges Administrationsinterface (kurz Admin), was Ihnen erlaubt die meisten der Einträge in der Datenbank direkt zu verändern. Offensichtlich können nur Benutzer mit den richtigen Rechten dieses Interface benutzen. Der Benutzer, der während der Installation mit Hilfe von ``./manage.py createsuperuser`` erstellt wurde, hat diesen *Superuser*-Status.

Das Admin-Interface ist unter dem Link *Admin* in der Navigationsleiste verfügbar. Es wird nur in seltenen Fällen bentuzt, da die meisten Konfigurationen des Fragebogens und andere Funktionen von RDMO über das benutzerfreundliche Management-Interface geändert werden können wie 
:doc:`in dem folgenden Kapitel der Dokumentation </management/index>` beschrieben.

Demnach wird das Admin-Interface nach der Installation benötigt, um den Titel und die UR auf der :doc:`Seite <site>` zu ändern, um die :doc:`Benutzer und Gruppe <users>` zu konfigurieren, um die Verbindung zu :doc:`OAuth Anbietern <allauth>` zu konfigurieren und um die mit der API genutzen :doc:`Tokens <tokens>` zu ändern.

.. toctree::
   :caption: Index
   :maxdepth: 2

   site
   users
   allauth
   tokens
