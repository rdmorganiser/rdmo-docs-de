Authentifikation
----------------

RDMO hat drei Hauptmethoden für die Authentifikation:

* Reguläre Benutzeraccounts mit Registrierung unter Verwendung der:doc:`django-allauth <allauth>` Bibliothek.
* Verwendung deiner (read-only) Verbindung zu einem :doc:`LDAP Server <ldap>`
* Instllieren eines :doc:`Shibboleth <shibboleth>` Service-Anbieters neben RDMO und sich mit einem Identitätenanbieter oder sogar einer ganzen Shibboleth-Förderation verbinden. 

**Wichtig:** Diese Methoden sind nur separat gestestet worden und sollten daher als **sich gegenseitig ausschließend** betrachtet werden (bis gegentieliges bewiesen ist).

Falls keine der Methoden aktiviert ist, ist nur ein einfacher Login verfügbar und Benutzer müssen über das Djange Admin-Interface erstellt werden.

**Important:** These modes are only tested individually and may be treated **mutually exclusive** (unless proven otherwise).


.. toctree::
   :hidden:

   allauth
   ldap
   shibboleth
