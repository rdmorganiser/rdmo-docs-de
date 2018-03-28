Management
==========

RDMO benutzt einen strukturierten Fragebogen. Die Antworten werden gespeichert und in verschiedenen Formen ausgegeben. Es stehen hierzu verschiedene Templates (wie z.B. DMP-Vorlagen) zur Verfügung.
Die Hauptidee von RDMO ist die Anpassbarkeit einer jeden Frage und eines jeden Outputs. RDMO benutzt dabei ein Datenmodell, welches entlang der Django-Apps und den Django-Modellen organisiert ist. Eine graphische Übersicht ist folgend zu sehen:

.. figure:: ../_static/img/datamodel_de.svg
   :target: ../_static/img/datamodel_de.svg

   Übersicht über das RDMO-Datenmodel.

Eine vollständige Darstellung ist :doc:`auf einer anderen Seite </development/figures>` zu finden. Hier erklären wir die unterschiedlichen Teile des Datenmodels. Jeder Abschnitt ist mit einer detailierten Beschreibung verlinkt wie die wichtigen Elemente erstellt und verändert werden.

Für die meisten Benutzer wird der strukturierte Fragebogen von RDMO das wesentliche Element sein. Dieser ist aus **Kataloge**, **Abschnitte**, **Unterabschnitte**, **Fragensets** und **Fragen** aufgebaut. Eine einzelne Installation von RDMO kann mehrere Kataloge haben. Wenn ein neues Projekt erstellt wird, kann der Benutzer einen dieser Kataloge mit seinem Projekt verknüpfen. Ein Katalog hat diverse Abschnitte, die wiederum in weitere Unterabschnitte gegliedert sind. Fragen können in den einzelnen Unterabschnitten eingefügt werden. Sie erscheinen dann als einzelne Frage auf einer einzelnen Seite der Interview-Ansicht. Alternativ können auch Fragensets in den Unterabschnitten eingefügt werden. Eine Frage besitzt einen Text, der fettgedruckt ist, und einen optionalen Hilfetext. Man kann auch zwischen verschiedenen Widget-Typen auswählen, die dann entscheiden, welche Antwortmöglichkeiten auszuwählen sind (z.B. Textfeld, Auswahlfeld, Radio Buttons). Der Fragenkatalog wird unter ``/Fragen`` im Mangementmenü konfiguriert. Weitere Dokumentation zum Management des Fragenkatalogs ist unter :doc:`/management/questions` zu finden.

Das **Domänenmodell** ist der zentrale Teil des Datenmodells und verbindet die Fragen des Fragebogens mit den Antwortmöglichkeiten, die der Benutzer zur Auswahl hat. Es liegt eine baumartige Struktur vor. Jede Information in einem Projekt ist über ein bestimmtes **Attribut** repräsentiert. In diesem Sinne können Attribute verglichen werden mit einer Variablen im Sourcecode. Attribute sind die Blätter im Modellbaum und können verschiedenen **Entitäten** zugeordnet werden, so wie Ordner einem Pfad auf dem Computer zugeordnet werden. Jede Frage muss mit einem Attribut, jedes Fragenset muss mit einer Entität verknüpft sein. Ein Beispiel: für den Start eines Projekts ist der Pfad ``projekt/planung/projektstart``. Das Attribut ist dabei ``projektstart`` und befindet sich innerhalb der Entität ``planung``, die wiederum in der Entität ``projekt`` angehängt ist.

Attribute können als Sammlung markiert werden. Dies erlaubt dem Benutzer mehrere Antworten  auf die zugehörige Frage zu geben. Eine Frage, die mit diesem Attribut verknüpft ist, wird eine Schaltfläche zum Hinzufügen einer neuen Zeile zeigen. Ein Beispiel wäre: mehre Stichwörter für ein Projekt. Fragen mit Checkbox-Widgets brauchen ebenfalls das Sammlungsattribut. Entitäten können auch als Sammlungen markiert werden. In diesem Fall kann der Benutzer ein Fragenset für alle Attribute unterhalb der Entität im Baum erstellen. Ein Fragenset, das mit dieser Entität verknüpft ist, wird Interface-Elemente zeigen, um neue Fragesets erstellen zu können. Dies kann verwendet werden, um das gleiche Fragenset für verschiedene Datensätze oder Partnerinstitute abzufragen. Alle Entitäten im Baum unterhalb der Entitätensammlung besitzen dies Verhalten, so dass Fragen vom gleichen Set über mehrere Fragensets auf verschiedene Seiten des Interview-Ansicht verteilt sein können.

Attribute haben einen Wertetyp, der beschreibt, ob eine Information ein Teil eines Textes, eine Zahl, oder ein Datum ist. Außerdem kann ein Attribut eine Einheit haben (z.B. Wert=1, Einheit [kg]). Eine **Wertebereich** wird über einen Slider Widget eingestellt. Beides, Attribute und Entitäten, können einen **Anzeigenamen** haben. Im Falle einer Sammlung wird dieser Anzeigename dem Benutzer in Interface-Elementen angezeigt, anstelle von "Hinzufügen" oder "Set hinzufügen". Attribute und Entitäten sind unter ``/Domäne`` im Managementmenü konfigurierbar. Weitere Dokumentation über Optionen-Management kann unter :doc:`/management/options` gefunden werden.

Ferner können Attribute mit **Optionensets**, bestehend aus **Optionen** verknüpft sein. Dies erlaubt die Verwendung eines kontrollierten Vokabulars für die Benutzerantworten. Falls ein Attribut ein oder mehrere Optionensets hat (und den Wertetyp "Optionen") kann der Benutzer seine Antwort aus verschiedenen Optionen dieses Optionensets wählen. Auswahl, Radio-Widget oder Checkbox-Widgets werden im Interview für solche Features verwendet. Optionensets und Optionen sind unter ``/Optionen`` im Datenmenü konfigurierbar. Weitere Dokumentation über Optionen-Management kann unter :doc:`/management/options` gefunden werden.

**Bedingungen** können mit Attributen und Entitäten verknüpft sein. Bedingungen prüfen, ob die Attribute im aktuellen Kontext gültig sind. Falls ein Attribut nicht gültig ist, wird die verknüpfte Frage dem Benutzer nicht angezeigt werden. Genauso verhält es sich, wenn eine Entität nicht gültig ist. Bedingungen sind auch notwendig, um Optionensets und Aufgaben zu aktivieren/deaktivieren und können in Ansichten verwendet werden. Bedingungen sind mit Hilfe eines auszuwertenden Source-Attributes konfiguriert, einer Beziehung wie "gleich" oder "größer als" und einem Ziel konfiguriert. Das Ziel ist ein Text-String oder eine Option. Beispielsweise sei die Quelle das Attribut ``project/legal_aspects/ipr/yesno`` und der Zieltext ist "1". Die Bedingung wird für ein Projekt wahr sein, in dem die Antwort verknüpft mit dem Attribut  ``project/legal_aspects/ipr/yesno`` gleich "1" (oder "ja" für ein Ja/Nein Widget) ist. Bedingungen sind unter ``/Bedingungen`` im Managementmenü konfigurierbar. Weitere Dokumentation über Bedinungsmanagment kann unter :doc:`/management/conditions` gefunden werden.

**Ansichten** erlauben es, ein Ausgabe-Template (z.B. DMP-Vorlage) in RDMO zu erstellen. Jede Ansicht hat eine Vorlage, welche mit Hilfe der Django template syntax editiert werden kann. Ansichten haben auch einen Titel und einen Hilfetext, der in der Projektübersicht angezeigt wird. Ansichten sind unter ``/views`` im Managementmenü konfigurierbar. Weitere Dokumentation über das Editieren von Ansichten kann unter :doc:`/management/views` gefunden werden.

Nach dem Ausfüllen des Interviews, können dem Benutzer anstehende **Aufgaben** aufgrund seiner Antworten präsentiert werden. Eine Aufgabe hat einen Titel und einen Text. **Zeitfenster** können den Aufgaben hinzugefügt sein, welche Attribute vom Wertetyp "datetime" auswerten, um aus Antworten wie Beginn oder Ende des Projekts wichtige Aufgaben zu ermitteln. Meistens werden Aufgaben mit einer Bedingung verknüpft sein, um zu ermitteln, ob diese für ein bestimmtes Projekt notwendig sind oder nicht. Aufgaben werden unter ``/tasks`` im Managementmenü konfiguriert. Weitere Dokumentation über das Erstellen von Aufgaben sind unter :doc:`/management/tasks` zu finden.

Die verschiedenen Elemente des RDMO Datenmodells haben diverse Parameter, die unter den unterschiedlichen Managementseiten konfiguriert werden können. Alle Elemente besitzen die folgenden Parameter:

-	Ein URI-Präfix, um die Entität zu identifizieren, die das Element erzeugt hat.
-	Einen Schlüssel, also eine interne Bezeichnung für das Element.
-	Einen internen Kommentar um Informationen mit den Benutzern zu teilen, die Zugang zum Managementbereich besitzen.

Der Schlüssel ist eine Pflichtangabe und dient als interne Bezeichnung. Zusammen mit dem URI Präfix bestimmt der Schlüssel die eigentliche URI des Elements. Diese URI wird als globale Funktionsbezeichnung für den Export und Import verwendet.

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
