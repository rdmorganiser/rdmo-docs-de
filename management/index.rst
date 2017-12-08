Management
==========

RDMO benutzt Fragebögen, die beantwortet werden können, und DMP Vorlagen, die mit den gegebenen Antworten gefüllt werden. 
Die Hauptidee von RDMO ist die Personalisierung einer jeden Frage und eines jeden Outputs. RDMO benutzt dabei ein Datenmodell, welches entlang der Django-Apps und den Django-Modellen organisiert ist. Eine graphische Übersicht ist folgend zu sehen:

.. figure:: ../_static/img/datamodel.svg
   :target: ../_static/img/datamodel.svg

   Overview of the RDMO data model.

Eine vollständige Darstellung ist :doc:`auf einer anderen Seite </development/figures>` zu finden. Hier erklären wir die unterschiedlichen Teile des Datenmodels. Jeder Abschnitt ist mit einer detailierten Beschreibung verlinkt wie die wichtigen Elemente erstellt und verändert werden. 

Für die meisten Benutzer wird größtenteils nur der strukturierte Fragebogen von RDMO zu sehen sein. Es ist auf **Kataloge**, **Abschnitte**, **Unterabschnitte**, **Fragensets** und **Fragen** aufgebaut. Eine einzelne Installation von RDMO kann mehrere Kataloge haben. Wenn ein neues Projekt kreiert wird, kann der Benutzer einen dieser Kataloge mit seinem Projekt verknüpfen. Ein Katalog hat diverse Abschnitte, die wiederum in weitere Unterabschnitte gegliedert sind. Fragen können in den einzelnen Unterabschnitten eingefügt werden. Sie erscheinen dann als einzelne Frage auf einer einzelnen Seite des Interviews. Alternativ können auch Fragensets in den Unterabschnitten eingefügt werden. Eine Frage bestizt einen Text, der fettgedruckt ist, und einen optionalen Hilfetext. Man kann auch zwischen verschiedenen Widget-Typen auswählen, die dann entscheiden, wie die Antwortmöglichkeiten auszuwählen sind (z.B. Textfeld, Auswahlfeld, Radio Buttons). Der Fragenkatalog wird unter ``/questions` im Mangementmenü konfiguriert. Weitere Dokumentation zum Management der Fragen kann unter gefunden :doc:`here </management/questions>` werden.

Das **Domänenmodell** ist der zentrale Teil des Datenmodells und verbindet die Fragen des Fragebogens mit den Antwortmöglichkeiten, die der Benutzer zur Auswahl hat. Es liegt eine baumartige Struktur vor. Jede Information in einem Projekt ist über ein bestimmtes **Attribut** repräsentiert. In diesem Sinne können Attribute verglichen werden mit einer Variable im Sourcecode. Attribute sind die Blätter im Modelbaum und können verschiedenen **Entitäten** zugeordnet werden, so wie Ordner einem Pfad auf dem Computer zugeordnet werden. Jede Frage muss mit einem Attribut und jedes Fragenset mit einer Entität verknüpft sein. Ein Beispiel für den Start eines Projekts ist der Pfad ``projekt/planung/projektstart``. Das Attribut ist dabei ``projektstart`` und befindet sich innerhalb der Entität ``planun``, die sich wiederum in der Entität ``projek`` befindet.

Attribute können als Sammlung markiert werden. Dies erlaubt dem Benutzer mehrere Antworten für die zugehörige Frage zu geben. Eine Frage, die mit diesem Attribut verknüpft ist, wird eine Schaltfläche zum Hinzugügren einer neuen Zeile zeigen. Eine Beispiel wären mehre Stichwörter für ein Projekt. Fragen mit Checkbox Wudgets brauchen ebenfalls Kollegtionsattribute. Entitäten können auch als Kollektionen markiert werden. In diesem Fall kann der Benutzer ein Fragenset für alle Attribute unterhalb der Entität im Baum erstellen. Eine Fragenset, das mit dieser Entität verknüpft ist, wird Interface-Elemente zeigen, um neue Fragesets erstellen zu können. Dies kann verwendet werden, um das gleiche Fragenset für verschiedene Datensätze oder Partnerinstitute zu fragen. Alle Entitäten im Baum unterhalb der Entitätenkollektion adoptieren ihr Verhalten, so dass Fragen vom gleichen Set können über mehrere Fragensets auf verschienden Seiten des Interviews verteilt sein.

Attribute haben einen Werttyp, der beschreibt, ob eine Information ein Teil eines Textes, eine Zahl, oder ein Datum ist. Außerdem kann ein Attribut eine Einheit haben. Eine **Spannbreite** an Werte wird über einen Slider Widget eingestellt. Beides, Attribute und Entitäten, können einen **verbose name** haben. Im Falle einer Kollktion wird dieser verbose name dem Benutzer in Interface-Elementen angezeigt anstatt "Add item" oder "Add set". Attribute und Entitäten sind unter ``/domain`` im Managementmenü konfoguriert. Weitere Dokumentation über Optionen-Management kann unter :doc:`here </management/options>` gefunden werden.

Attributes can further be connected to **option sets** consisting of **options**. This allows to use a controlled vocabulary for the user's answers. If an attribute has one or more option sets (and the value type "Options"), the user can choose his/her answer from the different options of these option sets. Select, radio or check box widgets are used in the interview for this feature. Option sets and Options are configured under ``/options`` available in the management menu. More documentation about the options management can be found :doc:`here </management/options>`.

**Conditions** can be connected to attributes and entities. Conditions control if the attributes and entities are valid in the current context. If an attribute is not valid, a question connected to this attribute will not be shown to the user. Similarly, if an entity is not valid, the connected question set is not shown. Conditions are also needed to disable/enable option sets, tasks and can be used in views. Conditions are configured with a source attribute, which will be evaluated, a relation like "equal" or "greater than", and a target. The target is a text string or an option. As an example, if the source is the attribute ``project/legal_aspects/ipr/yesno``, the relations is "equal to", and the target text is "1". The condition will be true for a project where the answer to the question connected to the attribute ``project/legal_aspects/ipr/yesno`` is "1" (or "yes" for a yesno widget). Conditions configured under ``/conditions`` are available in the management menu. More documentation about the conditions management can be found :doc:`here </management/conditions>`.

**Views** allow to custom DMP templates in RDMO. To this purpose every view has a template, which can be edited using the Django template sytax based on HTML. Views have also a title and a help text to be shown in the project overview. Views are configured under ``/views`` and are  available in the management menu. More documentation about editing views can be found :doc:`here </management/views>`.

After filling out the interview, the user will be presented with follow up **tasks** based on his/her answers. A task has a title and a text. **Time frames** can be added to tasks, which themselves are evaluating attributes of the value type "datetime", to use answers such as the beginning or the end of a project to compute meaningful tasks. Most of the time tasks will have a condition connected to them, to determine if this task is needed for a particular project or not. Tasks configured under ``/tasks`` are available in the management menu. More documentation about editing views can be found :doc:`here </management/tasks>`.

The different elements of the RDMO datamodel have various parameters, which control their behavior in RDMO and can be configured using the different management pages, which are decribed on the following pages. In addition, all elements contain a set of common parameters:

* An URI Prefix to identify the entity who created this element.
* A key which is the internal identifier for this element.
* An internal comment to share information to be seen by users with access to the management backend.

The key is used as an internal identifier and determines, together with the URI Prefix, the URI of the element. This URI is used as a global identifier for the export/import functionality.

.. toctree::
   :caption: Index
   :maxdepth: 2

   questions
   domain
   options
   conditions
   views
   tasks
   export
