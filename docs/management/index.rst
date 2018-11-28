Management
==========

RDMO benutzt einen strukturierten Fragebogen. Die Antworten werden gespeichert und in verschiedenen Formen ausgegeben. Es stehen hierzu verschiedene Templates (wie z.B. DMP-Vorlagen) zur Verfügung.
Der Leitgedanke von RDMO ist die Anpassbarkeit einer jeden Frage und eines jeden Outputs. Dafür nutzt RDMO ein Datenmodell, das entlang der Django-Apps und den Django-Models organisiert ist. Eine graphische Übersicht ist folgend zu sehen:

.. figure:: ../_static/img/datenmodell.svg
   :target: ../_static/img/datenmodell.svg

   Übersicht über das RDMO-Datenmodel.

Hier erklären wir die unterschiedlichen Teile des Datenmodels. Jeder Abschnitt ist mit einer detaillierten Beschreibung verlinkt, wie die wichtigen Elemente erstellt und verändert werden.

Für die meisten Benutzer wird der strukturierte Fragebogen von RDMO das wesentliche Element sein. Dieser ist aus **Katalogen**, **Abschnitten**, **Fragensets** und **Fragen** aufgebaut. Eine RDMO-Installation kann mehrere Kataloge haben. Wenn ein neues Projekt erstellt wird, kann der Benutzer einen dieser Kataloge mit seinem Projekt verknüpfen. Ein Katalog hat diverse Abschnitte, die wiederum in Fragensets gegliedert sind. Fragen können zu den einzelnen Fragensets hinzugefügt werden. Eine Frage besitzt einen Text, der fettgedruckt ist, und einen optionalen Hilfetext. Man kann auch zwischen verschiedenen Widget-Typen auswählen, die dann entscheiden, welche Antwortmöglichkeiten auszuwählen sind (z.B. Textfeld, Auswahlfeld, Radio Buttons). Der Fragenkatalog wird unter ``/questions`` im Mangementmenü konfiguriert. Weitere Dokumentation zum Management des Fragenkatalogs ist unter :doc:`/management/questions` zu finden.

Das **Domänenmodell** ist der zentrale Teil des Datenmodells und verbindet die Fragen des Fragebogens mit den Antwortmöglichkeiten, die der Benutzer zur Auswahl hat. Es liegt eine baumartige Struktur vor. Jede Information in einem Projekt ist über ein bestimmtes **Attribut** repräsentiert. Attribute ähneln Variablen, die Platzhalter für unterschiedlichste Ausdrücke sein können. Man sollte sich sich aber eher als die Blätter des Modellbaums vorstellen, die durch einen ihnen eigenen Pfad Verknüpfungen zwischen den Elementen erzeugen, die ihnen zugeordnet sind. Gewissermaßen so wie Ordner eines Dateisystems, die Dateien organisieren. Jede Frage oder jedes Fragenset muss mit einem Attribut verknüpft sein. Ein Beispiel: für den Start eines Projekts ist der Pfad ``project/schedule/project_start``. Dabei ist das Attribut ``project_start`` und befindet sich innerhalb des Attributes ``schedule``, das wiederum dem Attribut ``project`` zugeordnet ist.

**Bedingungen** können mit Fragensets verknüpft sein. Bedingungen prüfen, ob die Fragensets im aktuellen Kontext gültig sind. Falls ein Fragenset nicht gültig ist, wird es dem Benutzer nicht angezeigt. Bedingungen sind auch notwendig, um Optionensets und Aufgaben zu aktivieren/deaktivieren und können in Ansichten verwendet werden. Bedingungen sind mit Hilfe eines auszuwertenden Source-Attributes konfiguriert, einer Beziehung wie "gleich" oder "größer als" und einem Ziel konfiguriert. Das Ziel ist ein Text-String oder eine Option. Beispielsweise sei die Quelle das Attribut ``project/legal_aspects/ipr/yesno`` und der Zieltext ist "1". Die Bedingung wird für ein Projekt wahr sein, in dem die Antwort verknüpft mit dem Attribut  ``project/legal_aspects/ipr/yesno`` gleich "1" (oder "ja" für ein Ja/Nein Widget) ist. Bedingungen sind unter ``/conditions`` im Managementmenü konfigurierbar. Weitere Dokumentation über Bedinungsmanagment kann unter :doc:`/management/conditions` gefunden werden.

**Ansichten** erlauben es, ein Ausgabe-Template (z.B. DMP-Vorlage) in RDMO zu erstellen. Jede Ansicht hat eine Vorlage, welche mit Hilfe der Django-Template-Syntax editiert werden kann. Ansichten haben auch einen Titel und einen Hilfetext, der in der Projektübersicht angezeigt wird. Ansichten sind unter ``/views`` im Managementmenü konfigurierbar. Weitere Dokumentation über das Editieren von Ansichten kann unter :doc:`/management/views` gefunden werden.

Nach dem Ausfüllen des Interviews, können dem Benutzer anstehende **Aufgaben** aufgrund seiner Antworten präsentiert werden. Eine Aufgabe hat einen Titel und einen Text. **Zeitfenster** können den Aufgaben hinzugefügt sein, welche Attribute vom Wertetyp "datetime" auswerten, um aus Antworten wie Beginn oder Ende des Projekts wichtige Aufgaben zu ermitteln. Meistens werden Aufgaben mit einer Bedingung verknüpft sein, um zu ermitteln, ob diese für ein bestimmtes Projekt notwendig sind oder nicht. Aufgaben werden unter ``/tasks`` im Managementmenü konfiguriert. Weitere Dokumentation über das Erstellen von Aufgaben sind unter :doc:`/management/tasks` zu finden.

Die verschiedenen Elemente des RDMO Datenmodells haben diverse Parameter, die unter den unterschiedlichen Managementseiten konfiguriert werden können. Alle Elemente besitzen die folgenden Parameter:

-	Ein URI-Präfix, um die Institution zu identifizieren, die das Element erstellt hat.
-	Einen Schlüssel, der als eine interne Bezeichnung für das Element dient.
-	Einen internen Kommentar um Informationen mit den Benutzern zu teilen, die Zugang zum Managementbereich besitzen.

Der Schlüssel ist eine Pflichtangabe und dient als interne Bezeichnung. Zusammen mit dem URI Präfix bestimmt der Schlüssel die eigentliche URI des Elements. Diese URI wird als globaler Bezeichner für den Export und Import verwendet.

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
   roles
