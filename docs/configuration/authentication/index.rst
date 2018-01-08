Authentifikation
----------------

RDMO hat drei Hauptmethoden für die Authentifikation:

* Reguläre Benutzeraccounts mit Registrierung unter Verwendung der:doc:`django-allauth <allauth>` Bibliothek.
* Verwendung deiner (read-only) Verbindung zu einem :doc:`LDAP Server <ldap>`
* Installieren eines :doc:`Shibboleth <shibboleth>` Service-Anbieters neben RDMO, um sich mit einem Identitätenanbieter oder sogar einer ganzen Shibboleth-Förderation zu verbinden. 

**Wichtig:** Diese Methoden sind nur separat gestestet worden und sollten daher als **sich gegenseitig ausschließend** betrachtet werden (bis gegenteiliges bewiesen ist).

Falls keine der Methoden aktiviert ist, ist nur ein einfacher Login verfügbar und Benutzer müssen über das Djange Admin-Interface erstellt werden.


.. toctree::
   :hidden:

   allauth
   ldap
   shibboleth
