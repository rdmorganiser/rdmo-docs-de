Management
==========

RDMO benutzt Fragebögen, die beantwortet werden können, und DMP Vorlagen, die mit den gegebenen Antworten gefüllt werden.
Die Hauptidee von RDMO ist die Personalisierung einer jeden Frage und eines jeden Outputs. RDMO benutzt dabei ein Datenmodell, welches entlang der Django-Apps und den Django-Modellen organisiert ist. Eine graphische Übersicht ist folgend zu sehen:

.. figure:: ../_static/img/datamodel.svg
   :target: ../_static/img/datamodel.svg

   Übersicht über das RDMO-Datenmodel.

Eine vollständige Darstellung ist :doc:`auf einer anderen Seite </development/figures>` zu finden. Hier erklären wir die unterschiedlichen Teile des Datenmodels. Jeder Abschnitt ist mit einer detailierten Beschreibung verlinkt wie die wichtigen Elemente erstellt und verändert werden.

Für die meisten Benutzer wird größtenteils nur der strukturierte Fragebogen von RDMO zu sehen sein. Es ist aus **Kataloge**, **Abschnitte**, **Unterabschnitte**, **Fragensets** und **Fragen** aufgebaut. Eine einzelne Installation von RDMO kann mehrere Kataloge haben. Wenn ein neues Projekt erstellt wird, kann der Benutzer einen dieser Kataloge mit seinem Projekt verknüpfen. Ein Katalog hat diverse Abschnitte, die wiederum in weitere Unterabschnitte gegliedert sind. Fragen können in den einzelnen Unterabschnitten eingefügt werden. Sie erscheinen dann als einzelne Frage auf einer einzelnen Seite des Interviews. Alternativ können auch Fragensets in den Unterabschnitten eingefügt werden. Eine Frage besitzt einen Text, der fettgedruckt ist, und einen optionalen Hilfetext. Man kann auch zwischen verschiedenen Widget-Typen auswählen, die dann entscheiden, wie die Antwortmöglichkeiten auszuwählen sind (z.B. Textfeld, Auswahlfeld, Radio Buttons). Der Fragenkatalog wird unter ``/Fragen`` im Mangementmenü konfiguriert. Weitere Dokumentation zum Management der Fragen kann unter :doc:`/management/questions` gefunden werden.

Das **Domänenmodell** ist der zentrale Teil des Datenmodells und verbindet die Fragen des Fragebogens mit den Antwortmöglichkeiten, die der Benutzer zur Auswahl hat. Es liegt eine baumartige Struktur vor. Jede Information in einem Projekt ist über ein bestimmtes **Attribut** repräsentiert. In diesem Sinne können Attribute verglichen werden mit einer Variablen im Sourcecode. Attribute sind die Blätter im Modelbaum und können verschiedenen **Entitäten** zugeordnet werden, so wie Ordner einem Pfad auf dem Computer zugeordnet werden. Jede Frage muss mit einem Attribut und jedes Fragenset muss mit einer Entität verknüpft sein. Ein Beispiel für den Start eines Projekts ist der Pfad ``projekt/planung/projektstart``. Das Attribut ist dabei ``projektstart`` und befindet sich innerhalb der Entität ``planung``, die sich wiederum in der Entität ``projekt`` befindet.

Attribute können als Sammlung markiert werden. Dies erlaubt dem Benutzer mehrere Antworten für die zugehörige Frage zu geben. Eine Frage, die mit diesem Attribut verknüpft ist, wird eine Schaltfläche zum Hinzufügen einer neuen Zeile zeigen. Eine Beispiel wären mehre Stichwörter für ein Projekt. Fragen mit Checkbox Widgets brauchen ebenfalls Sammlungsattribute. Entitäten können auch als Sammlungen markiert werden. In diesem Fall kann der Benutzer ein Fragenset für alle Attribute unterhalb der Entität im Baum erstellen. Eine Fragenset, das mit dieser Entität verknüpft ist, wird Interface-Elemente zeigen, um neue Fragesets erstellen zu können. Dies kann verwendet werden, um das gleiche Fragenset für verschiedene Datensätze oder Partnerinstitute zu fragen. Alle Entitäten im Baum unterhalb der Entitätensammlung adoptieren ihr Verhalten, so dass Fragen vom gleichen Set über mehrere Fragensets auf verschienden Seiten des Interviews verteilt sein können.

Attribute haben einen Wertetyp, der beschreibt, ob eine Information ein Teil eines Textes, eine Zahl, oder ein Datum ist. Außerdem kann ein Attribut eine Einheit haben. Eine **Wertebereich** wird über einen Slider Widget eingestellt. Beides, Attribute und Entitäten, können einen **Anzeigenamen** haben. Im Falle einer Sammlung wird dieser Anzeigename dem Benutzer in Interface-Elementen angezeigt anstatt "Hinzufügen" oder "Set hinzufügen". Attribute und Entitäten sind unter ``/Domäne`` im Managementmenü konfiguriert. Weitere Dokumentation über Optionen-Management kann unter :doc:`/management/options` gefunden werden.

Ferner können Attribute mit **Optionensets** bestehend aus **Optionen** verknüpft sein. Dies erlaubt es ein kontrolliertes Vokabular für die Benutzerantworten zu verwenden. Falls ein Attribut ein oder mehrere Optionensets hat (und den Wertetyp "Optionen") kann der Benutzer seine Antwort aus verschiedenen Optionen von diesem Optionenset auswählen. Auswahl, Radio-Widget oder Check box widgets werden im Interview für solche Features verwendet. Optionensets und Optionen sind unter ``/Optionen`` im Datenmenü konfiguriert. Weitere Dokumentation über Optionendaten-Management kann unter :doc:`/management/options` gefunden werden.

**Bedingungen** können mit Attributen und Entitäten verknüpft sein. Bedingungen überprüfen, ob die Attribute im aktuellen Kontext gültig sind. Falls ein Attribut nicht gültig ist, wird die verknüpfte Frage dem Benutzer nicht angezeigt werden. Genauso verhält es sich, wenn eine Entität nicht gültig ist. Bedingungen sind auch nötig, um Optionensets und Aufgaben zu aktivieren/deaktivieren und können in Ansichten verwendet werden. Bedingungen sind mit Hilfe eines auszuwertenen Source-Attributes konfiguriert, einer Beziehung wie "gleich" oder "größer als" und einem Ziel konfiguriert. Das Ziel ist ein Text-String oder eine Option. Beispielsweise, wenn die Quelle das Attribut ``project/legal_aspects/ipr/yesno`` ist und der Zieltext ist "1". Die Bedingung wird für ein Projekt wahr sein, in dem die Antwort verknüpft mit dem Attribut  ``project/legal_aspects/ipr/yesno`` gleich "1" (oder "ja" für ein Ja/Nein Widget) ist. Bedingungen sind unter ``/Bedingungen`` im Managementmenü konfiguriert. Weitere Dokumentation über Bedinungsmanagment kann unter :doc:`/management/conditions` gefunden werden.

**Ansichten** erlauben es ein DMP-Vorlage (Template) in RDMO zu erstellen. Dafür besitzt jede Ansicht eine Vorlage, welche mit Hilfe von Django template syntax basierend auf HTML editiert wwerden kann. Ansichten haben auch einen Titel und einen Hilfetext, der in der Projektübersicht angezeigt wird. Ansichten sind unter ``/views`` im Managementmenü konfiguriert. Weitere Dokumentation über das Editieren von Ansichten kann unter :doc:`/management/views` gefunden werden.

Nach dem Ausfüllen des Interviews, werden dem Benutzer anstehende **Aufgaben** aufgrund seiner Antworten präsentiert. Eine Aufgabe hat einen Titel und einen Text. **Zeitfenster** können den Aufgaben hinzugefügt sein, welche Attribute vom Wertetyp "datetime" auswerten, um aus Antworten wie Beginn oder Ende des Projekts bedeutsame Aufgaben zu ermitteln. Meistens werden Aufgaben mit einer Bedingung verknüpft sein, um zu ermitteln, ob diese für ein bestimmtes Projekt notwendig sind oder nicht. Aufgaben werden unter ``/tasks`` im Managementmenü konfiguriert. Weitere Dokumentation über das Erstellen von Aufgaeb kann unter :doc:`/management/tasks` gefunden werden.

Die verschiedenen Elemente des RDMO Datenmodells haben diverse Parameter, die unter den unterschiedlichen Managementseiten konfiguriert werden können. Alle Elemente besitzen folgende gleiche Parameter:

-	Ein URI-Präfix, um die Entität zu identifizieren, die das Element kreiert hat.
-	Einen Schlüssel, also eine interne Bezeichnung für das Element.
-	Einen internen Kommentar um Informationen mit den Benutzern zu teilen, die Zugang zum Managementbereich besitzen.

Der Schlüssel ist eine Pflichtangabe und dient als interne Bezeichnung. Zusammen mit der URI Präfix bestimmt der Schlüssel die eigentliche URI des Elements. Diese URI wird als globale Funktionsbezeichnung für den Export und Import verwendet.

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
