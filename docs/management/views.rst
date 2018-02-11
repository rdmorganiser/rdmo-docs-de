Ansichten
---------

Ansichten können unter *Ansichten* im Mangementmenü in der Navigationsleiste konfiguriert werden.

.. figure:: ../_static/img/screens/Ansichten.PNG
   :target: ../_static/img/screens/Ansichten.PNG

   Screenshot des Ansichtenmangement-Interfaces.

Auf der linken Seite werden alle Ansichten der RDMO-Installation angezeigt. Ansichten zeigen ihren Schlüssel, ihren Titel und eine Beschreibung. Auf der rechten Seite von jedem Ansichtenfeld zeigen Symbole die Interaktionsmöglichkeiten an. Folgende Otptionen stehen zur Verfügung:

* **Bearbeiten** (|update|) einer Ansicht, um dessen Eigenschaften zu ändern.
* **Template bearbeiten** (|template|) einer Ansicht.
* **Entfernen** (|delete|) einer Ansicht. **Diese Handlung kann nicht rückgängig gemacht werden!**

.. |update| image:: ../_static/img/icons/update.png
.. |template| image:: ../_static/img/icons/template.png
.. |delete| image:: ../_static/img/icons/delete.png

Die Sidebar auf der rechten Seite enthält weitere Interface-Objekte:

* **Filter** filtert die Ansicht anhand eines vom Benutzer gegeben Strings. Nur Ansichten, die diesen String in ihrem Pfad haben, werden angezeigt.
* **Optionen** ermöglichen weitere Operationen:

  * Neue Ansicht erstellen

* **Export** exportiert die Ansichten zu eine der angegebenen Formate. Während Textformate hauptsächlich für die Präsentation sind, können XML-Ausgaben für den Transfer der Ansichten zu einer anderen RDMO-Installation verwendet werden.

Ansichten haben unterschiedliche Eigenschaften, die ihr Verhalten zu bestimmen. Wie in :doc:`der Einleitung <index>` beschrieben haben alle Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, die nur von den Managern der RDMO-Installation gesehen werden können. Ferner können folgende Parameter geändert werden:

Ansicht
"""""""

Title (en)
  Der englische Titel der Ansicht. Der Titel wird in der Projektübersicht angezeigt.

Title (de)
  Der deutsche Titel der Ansicht. Der Titel wird in der Projektübersicht angezeigt.

Hilfe (en)
  Der englische Hilfetext der Ansicht. Der Hilfetext wird in der Projektübersicht angezeigt.

Hilfe (de)
  Der deutsche Hilfetext der Ansicht. Der Hilfetext wird in der Projektübersicht angezeigt.


Vorlage
"""""""

.. figure:: ../_static/img/screens/Template.PNG
   :target: ../_static/img/screens/template.PNG

   Screenshot des Vorlagen-Fensters.

Jede Ansicht hat eine Vorlage (Template), die bestimmt, wie vom Benutzer gegeben Antworten in einem Textdokument dargestellt wird. Die Vorlage benutzt die `Django template <https://docs.djangoproject.com/en/1.11/ref/templates/language/>`_ syntax, welche in Kombination mit regulärem HTML, Variablen, deren Werte bei der Vorlageauswertung eingefüllt werden (``{{ a_variable }}``), und Tags, welche die Logik der Vorlage kontrollieren (``{% a_tag %}``).

Zwei Variablen können in RDMO Vorlagen verwendet werden:

* ``values``, welche mittels einer verschachtelten Python-Datenstruktur (dictionary) die Antworten des Benutzers unter Verwendung der Attribute abbildet. 
* ``conditions``, welche mittels einer Python-Datenstruktur (dictionary) die Schlüssel der Bedingungen nutzt, um die Werte der eingegebenen Antworten zur Verfuegung zu stellen (z.B. ``wahr`` oder ``falsch``).

Ein Beispiel: das Attribut sei  ``project/research_question/title`` (spezifischer: das Attribut ``titel`` in der Entität ``fragestellung`` in der Entität ``project``). Ein Benutzer beantwortet die zum Attribut gehörige Frage mit: "Kühn dorthin gehen, wohin noch kein Mensch sich gewagt hat". Der Attributwert ist dann in der Vorlage als ``values.project.fragestellung.title`` (beachte den ``.`` anstatt des ``/``) abzurufen. In der Vorlage wird die Syntax für eine Variable verwendet: 

.. code-block:: django

    Die Fragestellung des Projekts ist: {{ values.project.research_question.title }}

würde dann, wenn ausgewertet im Kontext beim Benutzer seines Projekts, ausgeben:

.. code-block:: django

    Die Fragestellung des Projekts ist: "Kühn dorthin gehen, wohin noch kein Mensch sich gewagt hat".

Kollektionen können mit dem ``for``-Tag von Django template syntax realisiert werden.

.. code-block:: django

    <ul>
    {% for keyword in project.research_question.keywords %}
        <li>{{ keyword }}</li>
    {% endfor %}
    </ul>

Die üblichen Filter für die Django-Syntax können auch verwendet werden, z.B.:

.. code-block:: django

    <p>
        {{ values.project.research_question.keywords | join:', ' }}
    </p>

Für Sammlungsentitäten:

.. code-block:: django

    {% for dataset in values.project.dataset %}
    <p>
        <i>Dataset {{ dataset.id }}:</i> {{ dataset.usage_description }}
    </p>
    {% endfor %}

Bedingungen können mit Hilfe des ``if`` tag verwendet werden.

.. code-block:: django

    {% if conditions.personal_data %}
    Dies wird nur ausgeführt, wenn personal_data als wahr ausgewertet wird.
    {% endif %}

Bitte lesen Sie die Dokumentation von Django template syntax für alle verfügbaren Tags und Filter: https://docs.djangoproject.com/en/1.11/ref/templates/language.
