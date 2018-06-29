Domäne
------

Das Domänenmodel kann unter *Domäne* im Managementmenü in der Navigationsleiste verändert werden.

.. figure:: ../_static/img/screens/Domain.PNG
   :target: ../_static/img/screens/Domain.PNG

   Screenshot vom Domain-Management Interface.

Nach der Instalaltion von RDMO ist die Domäne zunächst leer. Wir bitten Sie unsere Domäne zu importieren. Die entsprechende XML-Datei ist unter  https://github.com/rdmorganiser/rdmo-catalog verfügbar. Sie können die Domäne gerne nach Ihren Wünschen erweitern, aber sie ist die Gundlage für die Interoperabilität und Kooperativität verschiedener RDMO-Instanzen und daher immer der Startpunkt für das Erstellen von Fragenkatalogen.

Es werden alle Entitäten und Attribute der RDMO-Installation gezeigt, wozu der Pfad gehört und es eine Sammlung (collection) ist. Auf der rechten Seite eines jeden Elementfeldes gibt es Icons mit folgender Bedeutung:

* **Hinzufügen** (|add|) eines neuen Attributes oder einer Entität zu der gewählten Entität.
* **Entität bearbeiten** (|update|) eines Attributes oder einer Entität, um ihre Eigenschaften zu ändern.
* **Bereich bearbeiten** (|range|) eines Attributes. Der Wertebereich wird nur benötigt, wenn das Attribut mit einer Frage verknüpft ist die ein Auswahl-, Radio Buttons- oder Checkbox-Widget verwendet. 
* **Optionenset bearbeiten** (|optionsets|) eines Attributes. Optionensets bestimmen die Auswahl, wenn das Attribut mit einer Frage verknüpft ist, die Auswahl-, Radio Buttons- oder Checkbox-Widget verwendet. Die Optionensets selbst werden unter :doc:` Optionenmangament <options>` konfiguriert.
* **Anzeigename bearbeiten** (|verbosename|) eines Attributes oder einer Entität. Für eine Entität wird der Anzeigename für den Benutzer sichtbar, wenn Sets einer Frage hinzugefügt werden (anstatt "Set hinzufügen", z.B. "Datensatz hinzufügen"), während für Attribute der Anzeigename für den Benutzer sichtbar wird, wenn ein Item der Frage mit mehreren Antworten hinzugefügt wird (anstatt "Item hinzufügen", z.B. "Stichwort hinzufügen").
* **Bedingung hinzufügen** (|conditions|) eines Attributes oder einer Entität. Eine Frage, die ein Attribut mit einer oder mehreren Bedingungen hat, wird automatisch im Fragenkatalog übersprungen, wenn die Bedingung als falsch ausgewertet wird. Das Gleiche gilt für Fragesets, deren Entitäten mit einer Bedingung verknüpft sind. Die Bedingungen selbst werden unter :doc:`Bedingungsmangement <conditions>` konfiguriert.
* **Entfernen** (|delete|) eines Attributes oder einer Entität und all ihrer abhängigen Elemente (z.B. eine Entität und all ihre abhängigen Entitäten und Attribute im Domänen-Modelbaum). **Diese Handlung kann nicht rückgängig gemacht werden!**

.. |add| image:: ../_static/img/icons/add.png
.. |update| image:: ../_static/img/icons/update.png
.. |verbosename| image:: ../_static/img/icons/verbosename.png
.. |range| image:: ../_static/img/icons/range.png
.. |conditions| image:: ../_static/img/icons/conditions.png
.. |optionsets| image:: ../_static/img/icons/optionsets.png
.. |delete| image:: ../_static/img/icons/delete.png

Die Sidebar auf der rechten Seite zeigt weitere Interface-Objekte:

* **Filter** filtert die Ansicht anhand des Strings vorgegeben vom Benutzer. Nur Elemente, die diesen String in ihrem Pfad enhtalten, werden gezeigt.
* **Optionen** bietet weitere Operationen:

  * Neue (leere) Entität erstellen
  * Neues (leeres) Attribute erstellen

* **Export** exportiert den aktuelen Katalog zu einem der angezeigten Formate. Während Textformate vor allem für Darstellung gedacht sind, kann der XML Export genutzt werden, um das Domainmodel zu einer anderen RDMO-Installtion zu transferieren.

Die verschiedenen Elemente eines Domänenmodels haben unterschiedliche Eigenschaften, die ihr spezifisches Verhalten bestimmen. Wie in :doc:`der Einleitung <index>` beschrieben, haben alle Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, welche nur von dem Manager der RDMO-Installation gesehen werden kann. Außerdem können folgende Parameter verändert werden:

Entität
"""""""

Übergeordnete Entität
  Übergeordnete Entität in dem Domänenmodel. Das Ändern der übergeordneten Entität verschiebt die Entität und seine Abkömmlinge zu einem anderen Zweig des Domänen-Baummodels.

Kollektion
  Bestimmt, ob diese Entität mehrere Wertesets haben kann. Eine Frage verknüpft mit dieser Entität wird Interface-Elemente zeigen, um einen neune Fragensatz zu erstellen. Alle Entitäten in dem Baum unterhalb einer Entitätensammlung übernehmen dessen Verhalten, so dass Fragen über das gleiche Set über mehrere Fragen auf separaten Seiten des Interviews verteilt werden können.

  Falls eine Attribut ``ID`` mit einem Wertetyp `Text` der Entität hinzugefügt wird, ermöglicht dies dem Benutzer, einen Titel zu einzelnen Sets (wie "Datensatz A" oder "Finanzgeber X") zu geben, anderenfalls werden die Sets #1, #2, usw. genannt.

Attribute
"""""""""

Wertetyp
  Der Typ des Wertes für dieses Attributes. Die folgende Typen können gewählt werden:

  * **Text**
  * **URL**
  * **Integer**
  * **Float**
  * **Boolean**
  * **Datetime**
  * **Options**

  Bisher zeigen nur Datetime und Options ein anderes Verhalten. Dies kann sich ändern, sobald die Validierung des Interviews in RDMO implementiert ist.

Einheit
  Einheit eines Attributes. Die Einheit wird in den unterschiedlichen Ouput-Features angezeigt werden.

Übergeordnete Entität
  Übergeordnete Entität im Domänenmodell. Das Ändern der Eltern-Entität versetzt die Entität und seine Abkömmlinge zu einem anderen Zweig des Domänen-Baummodells.

Kollektion
  Bestimmt, ob diese Entität mehrere Wertesets haben kann. Eine Frage verknüpft mit diesem Attribut erlaubt dem Benutzer mehrere Antworten für die verknüpfte Frage zu geben. Die Frage wird einen Button zeigen, um ein neues Objekt in einer weiteren Zeile hinzufügen zu können. Ein Anwendungsbeispiel ist die Sammlung mehrerer Stichwörter für ein Projekt. Fragen mit Checkbox-Widgets benötigen ebenfalls Kollektions-Attributte.

Bereich
"""""""

Der (Werte-)Bereich wird verwendet, wenn ein Attribut mit einer Frage verknüpft ist, die ein Slider-Widget verwendet.

Minimum
  Minimlwert für das Attribut.

Maximum
  Maximalwert für das Attribut.

Schritt
   Schrittweite für das Attribut kann erhöht/verringert werden.

Anzeigename
""""""""""""

Der Anzeigename ist im Singular und Plural in Deutsch und Englisch konfiguriert und wird als Buttonbeschriftung gezeigt und ist im automatisch erstellten Hilfetext enthalten.

Name (en)
  Der englische Name für das Attribut/Entität (z.B. project), der angezeigt wird.

Plural name (en)
  Der englische Plural-Name für das Attribut/Entität (z.B. projects), der angezeigt wird.

Name (de)
  Der deutsche Name für das Attribut/Entität (z.B. Projekt), der angezeigt wird.

Plural name (de)
  Der deutsche Plural-Name für das Attribut/Entität (z.B. Projekte), der angezeigt wird.
