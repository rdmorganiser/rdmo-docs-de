Konfiguration
=============

Die RDMO-Anwendung benutzt das `Django Einstellungsmodule <https://docs.djangoproject.com/en/1.10/topics/settings>`_ für seine Konfiguration. Um die Basiskonfiguration und deine lokalen Anpassungen und geheime Informationen (z.B: Datenbankverbindungen) zu von einander zu trennen, sind die RDMO-Einstlelungen in zwei Dateien aufgeteilt:

* ``config/settings/base.py``, als Teil des Git-Repositoriums und vom RDMO Entwicklungsteam verwaltet wird.
* ``config/settings/local.py``, welches von Git ignoriert wird und von dir verändert werden sollte.

Als Teil der Installtion sollte ``config/settings/local.py`` erstellt werden ausgehend von der Vorlage ``config/settings/sample.local.py``.

Während technisch die lokalen Einstellungsdatei ``config/settings/local.py`` genutzt werrden kann, um alle Einstellungen in ``config/settings/sample.local.py`` zu überschreiben, sollte es verwendet werden, um die Einstellungen, die bereits in ``config/settings/sample.local.py`` vorhanden sind anzupassen. 

Dies beinhaltet :doc:`allgemeine Einstellungen <general>`, :doc:`Datenbankverbindungen <databases>`, hwie :doc:`E-mails <email>` versendet werden, die verschiedenen :doc:`Authentifizierungsmethoen <authentication/index>`, die Verwendung von  :doc:`Themen <themes>`, und :doc:`Caches <cache>`.

.. toctree::
   :caption: Index
   :maxdepth: 2

   general
   databases
   email
   authentication/index
   themes
   export-formats
   cache
   logging
