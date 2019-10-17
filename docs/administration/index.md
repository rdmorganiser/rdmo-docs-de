# Administration

Das Django-Framework bietet ein reichhaltiges Administrationsinterface (kurz Admin-Interface), das Ihnen erlaubt die meisten Einträge in der Datenbank direkt zu verändern. Natürlich können nur Benutzer mit den entsprechenden Berechtigungen dieses Interface benutzen. Der Benutzer, der während der Installation mit Hilfe von `./manage.py createsuperuser` erstellt wurde, hat diesen *Superuser*-Status.

Das Admin-Interface ist unter dem Link *Admin* in der Navigationsleiste verfügbar. Es wird nur in seltenen Fällen benutzt, da die meisten Konfigurationen des Fragebogens und andere Funktionen von RDMO über das benutzerfreundliche Management-Interface geändert werden können wie
[in dem folgenden Kapitel der Dokumentation](../management/index.html) beschrieben.

Das Admin-Interface wird nach der Installation benötigt, um den Titel und die URI auf der [Website](site.html) zu ändern, um die [Benutzer und Gruppe](users.html) zu konfigurieren, um die Verbindung zu [OAuth Anbietern](allauth.html) zu konfigurieren und die mit der API genutzten [Tokens](api.html) zu ändern.


```eval_rst
----

.. toctree::
   :maxdepth: 2

   site
   users
   allauth
   api
```
