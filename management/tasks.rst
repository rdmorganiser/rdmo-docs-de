Aufgaben
-----

Aufgaben sind unter *Aufgaben* im Managementmenü in der Navigatorleiste konfiguriert.


.. figure:: ../_static/img/screens/Aufgaben.PNG
   :target: ../_static/img/screens/Aufgaben.PNG
   
   
   Screenshot des Aufgabenmangement-Interfaces.

 Auf der linekn Seite werden alle aufgaben der RDMO-Installation angezeigt. Aufgaben ezeigen ihren Schlüssel, Titel und Aufgabenbeschreibung an. Auf der rechten Seite des Aufgabenfeldes zeigen Symbole Interaktionsmöglichkeiten an. Folgende Optionen sind verfügbar:


* **Bearbeiten** (|update|) einer Aufgabe, um dessen Eigenschaften zu ändern. 
* **Bedingung bearbeiten** (|conditions|) einer Aufgabe. eine Aufgabe wird dem Benutzer nur angezeigt, wenn al ihre Bedingungen als ``wahr`´ ausgewertet werden. Die BEdingungen selbst sind unter  :doc:`dem Konditionsmangement <conditions>` konfiguriert.
* **Zeitrahmen bearbeiten** (|timeframe|) einer Aufgabe. Der Zeitrahmen wird erstellt aus einem oder zwei Daten von den Antworten des Benutzers. Dies erlaubt Aufgaben mit einer bestimmten Deadline oder einer bestimmten Dauer festzulegen. 
* **Entfernen** (|delete|) einer Aufgabe. **Diese Handlung kann nicht rückgängig gemacht werden!** 

.. |update| image:: ../_static/img/icons/update.png
.. |conditions| image:: ../_static/img/icons/conditions.png
.. |timeframe| image:: ../_static/img/icons/timeframe.png
.. |delete| image:: ../_static/img/icons/delete.png

Die Sidebar auf der rechten Seite enthält weitere Interface-Objekte:

* **Filter**  filtert eine Ansicht anhand eines vom Benutzer eingegeben Strings. Nur Aufgaben, die diesen String in ihrem Pfad enthalten, werden angezeigt. 
* **Optionen** bietet weitere Optionen: 
 
   * Neue Aufgabe erstellen


* **Export** exportiert in eine der angebenen Formate. Während Textformate hauptsächlich für die Präsentation sind, können XML-Formate für den Transfer der Aufgaeb zu einer anderen RDMO-Installation verwendet werden.

Aufgaben haben unterschiedliche Eigenschafte, um ihr Verhalten zu konfigurieren. Wie in :doc:`der Einleitung <index>` beschrieben besitzen alle Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, die nur bei den Managern der RDMO-Instalaltion gesehen werden können. Ferner können folgende Parameter verändert werden: 

Aufgabe
""""

Title (en)
  Der englische Titel für die Ansicht. Der Titel wird in der Projektübersicht angezeigt.

Title (de)
  Der deutsche Titel für die Ansicht. Der Titel wird in der Projektübersicht angezeigt.

Text (en)
  Der englische Text für die Ansicht. Der Text wird in der Projektübersicht angezeigt.

Text (de)
  Der deutsche Text für die Ansicht. Der Text wird in der Projektübersicht angezeigt.

Zeitrahmen
""""""""""
Startdatum-Attribut
  Das Startdatum-Attribut legt das Startdatum für die Aufgabe fest. Das Attribut benötigt einen Wertetyp *datetime*.

Enddatum-Attribut
  Das Enddatum-Attribut legt das Enddatum der Aufgabe fest (optional, falls kein Enddatum gegeben ist, setzt das startdatum-Attribut auch das Enddatum-Attribut). Das Attribut braucht den Wertetyp *datetime*.

Tage vorher
  Vorrangehende Tage bis zum Starttemrin.

Tage danach
  Anschließende Tage nach dem Enddatum.
