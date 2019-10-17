# Authentifizierung

RDMO hat drei Hauptmethoden für die Authentifizierung:

* Reguläre Benutzeraccounts mit Registrierung unter Verwendung der [django-allauth](./allauth.html) Bibliothek
* Verwendung deiner (read-only) Verbindung zu einem [LDAP Server](./ldap.html)
* Installieren eines [Shibboleth](./shibboleth.html) Service-Anbieters neben RDMO, um sich mit einem Identity-Provider oder einer ganzen Shibboleth-Förderation zu verbinden

**Wichtig:** Diese Methoden sind nur separat getestet worden und sollten daher als **sich gegenseitig ausschließend** betrachtet werden (bis gegenteiliges bewiesen ist).

Falls keine der Methoden aktiviert ist, ist nur ein einfacher Login verfügbar und Benutzer müssen über das Django Admin-Interface erstellt werden.


```eval_rst
----

.. toctree::
   :hidden:

   allauth
   ldap
   shibboleth
```
