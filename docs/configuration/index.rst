Konfiguration
=============

Die RDMO-Anwendung benutzt das `Django Einstellungsmodul <https://docs.djangoproject.com/en/1.10/topics/settings>`_ für seine Konfiguration. Um die Basiskonfiguration und ihre lokalen Anpassungen und geheime Informationen (z.B.: Datenbankverbindungen) von einander zu trennen, sind die RDMO-Einstelluungen in zwei Dateien aufgeteilt:

* ``config/settings/base.py``, als Teil des Git-Repositoriums, die vom RDMO-Entwicklungsteam verwaltet wird.
* ``config/settings/local.py``, die von Git ignoriert wird und von Ihnen verändert werden muss.

Als Teil der Installation sollte ``config/settings/local.py`` anhand der Vorlage ``config/settings/sample.local.py`` erstellt werden.

Da die Einträge in der lokalen Einstellungsdatei ``config/settings/local.py`` Einträge in den Einstellungen in ``config/settings/sample.local.py`` überschreiben, sollte dieser Mechanismus verwendet werden, um die Einstellungen, die bereits in ``config/settings/sample.local.py`` vorhanden sind, anzupassen. 

Dies beinhaltet :doc:`allgemeine Einstellungen <general>`, :doc:`Datenbankverbindungen <databases>`, wie :doc:`E-mails <email>` versendet werden, die verschiedenen :doc:`Authentifizierungsmethoen <authentication/index>`, die Verwendung von  :doc:`Themen <themes>`, und :doc:`Caches <cache>`.

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
