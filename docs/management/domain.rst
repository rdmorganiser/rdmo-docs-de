Domäne
------

Das Domänenmodel kann unter *Domäne* im Managementmenü in der Navigationsleiste verändert werden.

.. figure:: ../_static/img/screens/domaene.png
   :target: ../_static/img/screens/domaene.png

   Screenshot vom Domain-Management Interface.

Nach der Installation von RDMO ist die Domäne zunächst leer. Wir bitten Sie unsere Domäne zu importieren. Die entsprechende XML-Datei ist unter https://github.com/rdmorganiser/rdmo-catalog verfügbar. Sie können die Domäne gerne nach Ihren Wünschen erweitern. Bedenken Sie aber, dass sie immer der Startpunkt für das Erstellen von Fragenkatalogen und daher nicht weniger als die Grundlage der Interoperabilität und Kooperativität verschiedener RDMO-Instanzen ist.

Es werden alle Attribute der RDMO-Installation gezeigt. Außerdem wird ist der Pfad erkennbar und ob Attribute eine ``Sammlung`` (collection) sind. Auf der rechten Seite eines jeden Elementfeldes gibt es Icons mit folgender Bedeutung:

* **Hinzufügen** (|add|) eines neuen Attributes zur gewählten Entität.
* **Bearbeiten** (|update|) eines Attributes, um seine Eigenschaften zu ändern.
* **Entfernen** (|delete|) eines Attributes oder einer Entität und all ihrer abhängigen Elemente (z.B. eine Entität und all ihre abhängigen Entitäten und Attribute im Domänen-Modelbaum). **Diese Aktion kann nicht rückgängig gemacht werden!**

.. |add| image:: ../_static/img/icons/add.png
.. |update| image:: ../_static/img/icons/update.png
.. |verbosename| image:: ../_static/img/icons/verbosename.png
.. |range| image:: ../_static/img/icons/range.png
.. |conditions| image:: ../_static/img/icons/conditions.png
.. |optionsets| image:: ../_static/img/icons/optionsets.png
.. |delete| image:: ../_static/img/icons/delete.png

Die Sidebar auf der rechten Seite zeigt weitere Bedienelemente:

* **Filter** filtert die Ansicht anhand eines vom Benutzer eingegebenen Strings. Nur Elemente, die diese Zeichenkette in ihrem Pfad enthalten, werden gezeigt.
* **Optionen** bietet weitere Operationen:

  * Neues (leeres) Attribute erstellen

* **Export** exportiert den aktuellen Katalog zu einem der angezeigten Formate. Während Textformate vor allem für die Darstellung gedacht sind, kann der XML Export genutzt werden, um das Domainmodel zu einer anderen RDMO-Installtion zu transferieren.

Die verschiedenen Elemente eines Domänenmodels haben unterschiedliche Eigenschaften, die ihr spezifisches Verhalten bestimmen. Wie in :doc:`der Einleitung <index>` beschrieben, haben alle Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, welche nur von dem Manager der RDMO-Installation gesehen werden kann. Außerdem können folgende Parameter verändert werden:

Attribute
"""""""""

Übergeordnetes Attribut
  Gibt an welches Attribut im Domänenmodell über dem vorliegenden steht. Wird das Eltern-Attribut verändert, verschiebt es sich mitsamt seiner Abkömmlinge an einen anderen Zweig des Domänen-Baummodells.
