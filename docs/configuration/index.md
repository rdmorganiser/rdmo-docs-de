# Konfiguration

Die RDMO-Anwendung benutzt das [Django Einstellungsmodul](https://docs.djangoproject.com/en/1.10/topics/settings) für seine Konfiguration. Um die Basiskonfiguration und ihre lokalen Anpassungen und geheime Informationen (z.B.: Datenbankverbindungen) von einander zu trennen, sind die RDMO-Einstellungen in zwei Dateien aufgeteilt:

* `config/settings/base.py`, als Teil des Git-Repositoriums, die vom RDMO-Entwicklungsteam verwaltet wird.
* `config/settings/local.py`, die von Git ignoriert wird und von Ihnen verändert werden muss.

Als Teil der Installation sollte `config/settings/local.py` anhand der Vorlage `config/settings/sample.local.py` erstellt werden.

Da die Einträge in der lokalen Einstellungsdatei `config/settings/local.py` Einträge in den Einstellungen in `config/settings/sample.local.py` überschreiben, sollte dieser Mechanismus verwendet werden, um die Einstellungen, die bereits in `config/settings/sample.local.py` vorhanden sind, anzupassen.

Dies beinhaltet [allgemeine Einstellungen](../general.html), [Datenbankverbindungen](../databases.html), wie [E-mails](../email.html) versendet werden, die verschiedenen [Authentifizierungsmethoden](../authentication/index.html), die Verwendung von  [Themen](../themes.html), und [Caches](../cache.html).

```eval_rst
.. toctree::
   :maxdepth: 2

   general
   databases
   email
   authentication/index
   themes
   export-formats
   cache
   logging
   multisite
```
