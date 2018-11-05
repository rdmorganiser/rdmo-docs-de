Fragen
------

Das Fragenmanagement ist unter *Fragen* im Managementmenü in der Navigationsleiste verfügbar. Direkt nach einer RDMO-Instalaltion ist dieser Bereich zunächst leer. Daher wird empfohlen erst unsere Domain und ggf. auch unseren generischen Fragenkatalog zu importieren. Die entsprechenden XML-Dateien finden Sie unter https://github.com/rdmorganiser/rdmo-catalog .

Falls bereits mindestens ein Fragenkatalog vorhanden ist, so wird dieser automatisch angezeigt. Weitere Kataloge können in der Seitenleiste darunter ausgewählt werden.

.. figure:: ../_static/img/screens/fragen.png
   :target: ../_static/img/screens/fragen.png

   Screenshot des Fragenmangements-Interfaces.

Auf der linken Seite werden die Abschnitte, Teilabschnitte und Fragen des aktuellen Katalogs angezeigt. Für Abschnitte und Teilabschnitte wird der Titel und Schlüssel angezeigt. Für Fragen und Fragensets wird der Schlüssel und der Schlüssel des verknüpften Attributes angezeigt. Die Reihenfolge der verschiedenen Elemente ist die Gleiche wie im strukturierten Interview, welches dem Benutzer angezeigt wird. Auf der rechten Seite eines jeden Elementfeldes zeigen Symbole die Interaktionsmöglichkeiten an. Folgende Optionen sind verfügbar:

* **Hinzufügen** (|add|) eines neuen Abschnittes, einer neuen Frage oder eines Fragensets zu einem Teilabschnitt oder eine neue Frage zu einem Fragenset.
* **Bearbeiten** (|update|) eines Elements, um seine Eigenschaften zu ändern.
* **Kopieren** (|copy|) einer Frage oder eines Fragekatalogs. Dies wird das gleiche Fenster öffnen wie das Bearbeiten. Es können einige der Eigenschaften verändert werden und das Element wird als ein neues Element gespeichert. Dies kann Zeit sparen wenn mehrere ähnliche Fragen erstellt werden.
* **Löschen** (|delete|) eines Elements und all seiner Abkömmlinge (z.B. Unterabschnitte und all dessen Fragen und Fragensets). **Diese Aktion kann nicht rückgängig gemacht werden!**

.. |add| image:: ../_static/img/icons/add.png
.. |update| image:: ../_static/img/icons/update.png
.. |copy| image:: ../_static/img/icons/copy.png
.. |delete| image:: ../_static/img/icons/delete.png

Der Sidebar rechts enthält weitere Bedienelemente:

* **Katalog** wechselt zu der Ansicht eines anderen Katalogs.
* **Filter** filtert die Ansicht anhand eines vom Benutzer eingegebenen Strings. Nur Elemente, die diese Zeichenkette in ihrem Pfad enthalten, werden gezeigt.
* **Optionen** enthält weitere Operationen:

  * Katalogeigenschaften bearbeiten
  * Katalog entfernen
  * Neuen Katalog erstellen
  * Neuen Abschnitt erstellen
  * Neuen Unterabschnitt erstellen
  * Neuen Frageset erstellen
  * Neue Frage erstellen

* **Export** exportiert den aktuellen Katalog in eines der angebotenen Formate. Während Textformate hauptächlich für Präsentationszwecke sind, können XML-Exporte für den Transfer des Kataloges zu einer anderen RDMO-Installation verwendet werden.

Die verschiedenen Elemente des Fragebogens haben verschiedenen Eigenschaften, um ihr Verhalten zu beschreiben. Wie in :doc:`der Einleitung <index>` erwähnt, haben alle Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, die nur dem Manager der RDMO-Installation zugänglich sind. Außerdem können folgende Parameter geändert werden:

Katalog
"""""""

Reihenfolge
  Bestimmt die Reihenfolge des Katalogs in der Liste oder der Interview-Ansicht.

Titel (en)
  Der englische Titel für den Katalog, der dem Benutzer angezeigt wird.

Titel (de)
  Der deutsche Titel für den Katalog, der dem Nutzer angezeigt wird.

Abschnitt
"""""""""

Katalog
  Der Katalog zu dem der Abschnitt gehört. Ändern des Katalogs wird den Abschnitt zu einem anderen Katalog verschieben. Daher wird er dann nicht mehr in der aktuellen Ansicht sichtbar sein.

Reihenfolge
  Bestimmt die Reihenfolge des Abschnittes in der Liste oder der Interview-Ansicht.

Titel (en)
  Der englische Titel des Abschnittes, der dem Benutzer angezeigt wird.

Titel (de)
  Der deutsche Titel des Abschnittes, der dem Benutzer angezeigt wird.


Unterabschnitt
""""""""""""""

Katalog
  Der Katalog zu dem der Unterabschnitt gehört. Ändern des Katalogs wird den Unterabschnitt zu einem anderen Katalog verschieben. Daher wird er dann nicht mehr in der aktuellen Ansicht sichtbar sein.

Reihenfolge
  Bestimmt die Reihenfolge des Unterabschnittes in der Liste oder der Interview-Ansicht.

Titel (en)
  Der englische Titel des Unterabschnittes, der dem Benutzer angezeigt wird.

Titel (de)
  Der deutsche Titel des Unterabschnittes, der dem Benutzer angezeigt wird.

Fragenset
"""""""""

Tab Allgemein
  Teilabschnitt
    Der Teilabschnitt zu dem das Frageset gehört. Ändern des Unterabschnittes verschiebt die Frage zu einem anderen Abschnitt.

  Reihenfolge
    Bestimmt die Position des Fragesets in der Liste oder der Interview-Ansicht.

  Attribut
    Das Attribut mit dem Fragenset verknüpfte Attribut.

  Titel (en)
    Der englische Titel des Unterabschnittes, der dem Benutzer angezeigt wird.

  Titel (de)
    Der deutsche Titel des Unterabschnittes, der dem Benutzer angezeigt wird.

Tab Englisch
  Name
    Der englische Name der für die Frage angezeigt wird

  Help
    Der englische Hilfetext des Fragensets

  Plural name
    Der englische Name dieses Fragensets im Plural

*Der Tab ``Deutsch`` enthält die gleichen Informationen wie der der englischen Sprache. Offenkundig jedoch in Übersetzung.*

Tab Bedingungen
    Bedingungen
        Zeigt die mit dem Fragenset verknüpften Bedingungen an.

Fragen
""""""

Tab Allgemein
  Unterabschnitt
    Der Unterabschnitt zu dem die Frage gehört. Ändern des Teilabschnittes verschiebt die Frage zu einem anderen Abschnitt.

  Übergeordnete Entität
    Das Fragenset zu dem die Frage gehört. Dies sollte "- - - " für eine Frage sein, die direkt zu einem Unterabschnitt hinzugefügt wird und nicht zu einem Fragenset.

  Reihenfolge
    Bestimmt die Position des Teilabschnittes in der Liste oder der Interview-Ansicht.

  Attribut
    Das Attribut von dem Domänenmodel zu dem die Frage zugeordnet ist. Beachten Sie, dass die Art wie die Frage sich dem Benutzer darstellt, teilweise vom Attribute selbst festgelegt wird. Eine Frage, die mit einer Sammlungsentität verknüpft ist, erlaubt mehrere Antworten und zeigt ein "Hinzufügen"-Symbol.

  Widget-Typ
    Die Art des Widgets für die Frage.  Folgende Widgets können gewählt werden:

    * **Text** (Ein Einzeiler-Textfeld)
    * **Textarea** (Ein Mehrzeiler-Textfeld)
    * **Yes/No** (Ein Set aus Radio Buttons für "Ja" und "Nein")
    * **Checkboxes** (Ein Set aus Checkboxen, das verknüpfte Attribut muss eine Kollektion sein)
    * **Radio Buttons** (Ein Set aus Radio buttons, das verknüpfte Attribut muss ein Optionenset sein)
    * **Select drop down** (Ein Dropdown-Menu, das verknüpfte Attribut muss ein Optionenset haben)
    * **Range slider** (Ein horizontaler Schieber, das verknüpfte Attribut muss einen Wertebereich haben)
    * **Date picker** (Ein Dropdown-Element mit einem Kalender, um ein Datum zu wählen. Das verknüpfte Attribut muss vom Datentyp Datetime sein)

  Wert-Typ
    Die Art von Wert, der für diese Frage eingegeben werden kann. Zur Auswahl stehen:
    Text, URL, Ganzzahl, Kommazahl, Boolsche Variable, Datum und Zeit, Option

  Einheit
    Die Maßeinheit dieser Frage

Tab Englisch
  Text
    Der englische Text für die Frage. Der Text wird in fett gedruckt dem Benutzer angezeigt.

  Hilfe
    Der englische Hilfetext für die Frage. Der Hilfetext wird dem Benutzer in grau angezeigt.

*Der Tab ``Deutsch`` enthält die gleichen Informationen wie der der englischen Sprache. Offenkundig jedoch in Übersetzung.*
