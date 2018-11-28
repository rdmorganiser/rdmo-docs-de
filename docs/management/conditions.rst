Bedingungen
-----------

Bedingungen können erstellt und bearbeitet werden. Wählen Sie *Bedingungen* im Managementmenü der Navigationsleiste. Die Bedingungen kömmen dann später mit Fragen sets, Optionensets oder Aufgaben verbunden.


.. figure:: ../_static/img/screens/bedingungen.png
   :target: ../_static/img/screens/bedingungen.png

   Screenshot des Bedingungen-Managments.

Auf der linken Seite sind alle Bedingungen der RDMO-Installation verfügbar. Für jede Bedingung wird ihr Schlüssel und eine textuelle Darstellung angezeigt. Auf der rechten Seite von jedem Bedingungsfeld zeigen Symbole an wie mit dem jeweiligen Element interagiert werden kann. Die folgenden Optionen stehen zur Auswahl:


* **Bearbeiten** (|update|) der Eigenschaften einer Bedingung.
* **Löschen** (|delete|) einer Bedingung. **Diese Aktion kann nicht rückgängig gemacht werden!**

.. |update| image:: ../_static/img/icons/update.png
.. |delete| image:: ../_static/img/icons/delete.png

In der rechten Sidebar gibt es weitere Schaltflächen:

* **Filter** filtert die Ansicht anhand eines vom Benutzer eingegebenen Strings. Nur Elemente, die diese Zeichenkette in ihrem Pfad enthalten, werden gezeigt.

**Optionen** bietet weitere Optionen:

  * **Neue Bedingung erstellen**

  * **Export** exportiert die Bedingungen in eines der angezeigten Formate. Während die Textformate hauptsächlich für die Darstellung sind, können XML Ausgaben für den Transfer von Bedingungen zu anderen RDMO Installationen genutzt werden.

Bedingungen haben unterschiedliche Eigenschaften, um ihr Verhalten zu kontrollieren. Wie in :doc:`in der Einleitung <index>` beschrieben, haben alle Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, die nur von den anderen Managern der RDMO Installation gesehen werden können. Es können folgende Parameter verändert werden:

Bedingung
"""""""""

Bedingungen sind mit einem Quellen-Attribut, das ausgewertet wird, einer Beziehung wie "gleich" oder "größer als" und einem Ziel ausgestattet. Hat beispielsweise eine Quelle das Attribut ``project\legal_aspects/ipr/yesno``, die Beziehung "gleich" und das Ziel "1", dann wird die Bedingung für ein Projekt als wahr ausgewertet, wenn die Antwort zu der Frage verbunden mit dem Attribut ``project/legal_aspects/ipr/yesno`` "1" ist (oder "ja" für ein Ja-Nein Widget).

Quelle
  Das Attribut der Bedingung wird ausgewertet.

Beziehung
  Die Beziehung dieser Begingung

Ziel (Text)
  Falls ein normaler Wert verwendet wird: Der Text gegen den diese Bedingung ausgewertet wird.

Ziel (Option)
  Falls ein Optionen-Wert verwendet wird, die Option gegen die diese Bedingung ausgewertet wird.
