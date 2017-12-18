Ansichten
-----
Ansichten können unter *Ansichten* im Mangementmenü in der Navigationsleiste konfiguriert werden.

.. figure:: ../_static/img/screens/Ansichten.PNG
   :target: ../_static/img/screens/Ansichten.PNG

   Screenshot des Ansichtenmangement-Interfaces.
   
   Auf der linken Seite werden alle Ansichten der RDMO-Installation angezeigt. Ansichten zeigen ihren Schlüssel, ihren Titel und eine Beschreibung. Auf der rechten Seite von jedem Ansichtenfeld zeigen Symbole die Interaktionsmöglichkeiten an. Folgende Otptionen stehen zur Verfügung:

* **Bearbeiten** (|update|) einer Ansciht, um dessen Eigenschaften zu ändern.
* **Template bearbeiten** (|template|) eines Ansicht.
* **Entfernen** (|delete|) einer Ansicht. **Diese Handlung kann nicht rückgängig gemacht werden!**

.. |update| image:: ../_static/img/icons/update.png
.. |template| image:: ../_static/img/icons/template.png
.. |delete| image:: ../_static/img/icons/delete.png

Die Sidebar auf der rechten Seite enthält weitere Interface-Objekte:

* **Filter** filtert die Ansicht anhand eines vom Benutzer gegeben Strings. Nur Ansichten, die diesen String in ihrem Pfad haben, werden angezeigt.
* **Optioen** ermöglichen weitere Operationen: 

  * Neue Ansicht erstellen

* **Export** exportiert die Ansichten zu eine der angegeben Formate. Während TextFormate hauptsächlich für die Präsentation sind, können XML-Ausgaben für den Transfer der Ansichten zu einer anderen RDMO-Installation verwendet werden.

Ansichten haben unterschiedliche Eigenschaften, um ihr Verhalten zu bestimmen. Wie in :doc:`der Einleitung <index>` beschrieben haben alles Elemente einen URI-Präfix, einen Schlüssel und einen internen Kommentar, die nur von den Managern der RDMO-Installation gesehen werden können. Ferner können folgende Parameter geändert werden:

Ansicht
"""""""

Title (en)
  Der englische Titel der Ansicht. Der Titel wird in der Projektübersicht angezeigt.

Title (de)
  Der deutsche Titel der Ansicht. Der Titel wird in der Projektübersicht angezeigt.

Hilfe (en)
  Der englische Hilfetext der Ansicht. Der Hilfetext wird in der Projektübersicht angezeigt.

Help (de)
  Der deutsche Hilfetext der Ansicht. Der Hilfetext wird in der Projektübersicht angezeigt.


Vorlage
"""""""

.. figure:: ../_static/img/screens/Template.PNG
   :target: ../_static/img/screens/template.PNG

   Screenshot des Vorlagen-Fensters.
   
Jede Ansicht hat eine Vorlage, die bestimmt wie die vom Benutzer gegeben Antworten auf ein Textdokument gemappt wird. Die Vorlage benutzt aus `Django template <https://docs.djangoproject.com/en/1.11/ref/templates/language/>`_ syntax, welche in Kombination mit regulärem HTML, Variabeln, dessen Werte  bei der Vorlageauswertung ersetzt werden (``{{ a_variable }}``), und Tags, welche die Logik der Vorlage kontrolliert (``{% a_tag %}``).

Zwei Variabeln können in RDMO Vorlagen verwendet werden:

* ``values``, welche ein verschachteltes Wörterbuch von den Antworten des Benutzers auf deren Attribute mappt. 
* ``conditions``, welche ein Wörterbuch auf die Schlüssel von den Bedingungen mappt, um die Bedingungen anhand des aktuellen Projekts auszuwerten (z.B. ``wahr`` or ``falsch``).

Ein Attribut wie  ``project/research_question/title`` (spezifischer eine Attribut ``titel`` in der Entität ``fragestellung`` in der Entität ``project``) und eine Benutzer, der die Frage zu dem Attribut mit "Wo noch kein Mensch gewesen ist" beantwortet. Das Attribut wäre dann in der Vorlage als ``values.project.fragestellung.title`` (beachte den ``.`` anstatt des ``/``). In der Vorlage wird die Syntax für eine Variable verwendet: 

.. code-block:: django

    Die Fragestellung des Projekts ist: {{ values.project.research_question.title }}

würde dann, wenn ausgewertet im Kontext beim Benutzer seines Projekts, ausgeben:

.. code-block:: django

    Die Fragestellung des Projekts ist: Wo noch kein Mensch gewesen ist.
    
Kollektionen können mit dem ``for`` tag von Django template syntax realisiert werden.

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

Für Kollektionsentitäten:

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

Bitte lesen sie die Dokumentation von Django template syntax für alle verfügbaren Tags und Filter: https://docs.djangoproject.com/en/1.11/ref/templates/language.
