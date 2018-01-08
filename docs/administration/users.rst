Benutzer und Gruppen
--------------------

Die Benutzer und Gruppen ihrer RDMO-Instanz könen unter **Authentifizierung und Autorisierung** verwaltet werden. Sie können Benutzer erstellen und verändern und deren Passworter direkt setzen, wobei dies meistens von den Benutzern selbst über das Account-Menü getan wird. 

Der in der Installation erstellte Benutzer hat zu allen Features von RDMO Zugang. Um anderen Benutzern den Zugang zum Management oder dem Admin-Interface zu gewähren, muss ihnen die notwendigen Rechte zuegwiesen werden. Dies kann auf zwei Wege erfolgen: durch die Gruppen oder durch das Superuser-Flag.

Gruppen
"""""""

Während der Installtion erstellte das``./manage create-groups`` Kommando drei Gruppen:

Editor
  Benutzer der Editorgruppe haben Zugang zum :doc:`Management Interface </management/index>` und können alle Elemente des Datenmodels editieren bisauf die Benutzerdaten, die über das strukturierte Interview eingegeben wurden. 

Reviewer
  Benutzer der Reviewergruppe haben Zugang zum :doc:`Management Interface </management/index>` genauso wie die Editoren, aber ihnen ist es nicht gestattet dort Veränderungen vorzunehmen (Speichern wird nicht funktionieren). Diese Gruppe kann verwendet werden, um ausgewählten Benutzern das Management-Backend zu zeigen.

API
  Benutzer der API-Gruppe können ein programmierbares API verwenden, um auf alle Elemente des Datenmodels zuzgreifen. Sie benötigen einen  :doc:`Token <tokens>`, um einen API-Klienten nutzen zu können.
  
Bereits existierende Benutzer können diesen Gruppen zugeordnet werden, um Zugang zu diesen Funktionen zu erhalten:

1. Klicken Sie auf **Benutzer** unter **Authentifizierung und Autorisierung** im Admin-Interface.

2. Klicken Sie auf den zu bearbeitenen Benutzer.

3. Klicken Sie auf die Gruppe zu dem der Benutzer hinzugefügt werden soll in dem **Verfügbare Gruppen**-Feld.

4. Klicken Sie auf den kleinen Pfeil, um die Gruppe zu dem **Gewählte Gruppen**-Feld zu bewegen.

5. Speichern Sie den Benutzer.


Superuser
"""""""""

Superusers haben alle verfügbaren Rechte und alle Rechteüberprüfungen werden für sie positiv sein. Dies ermöglicht ihnen nicht nur den Zugang zu den Management- und Admin-Interfaces, sondern auch den **Zugang zu den Daten von allen anderen Benutzern** (einschließlich der Projektseite).
Um einen Benutzer zum Superuser zu erheben, gehen Sie wie folgt vor:

1. Klicken Sie auf **Benutzer** unter **Authentifizierung und Autorisierung** im Admin-Interface.

2. Klicken Sie auf den gewünschten Benutzer.

3. Kreuzen Sie die Box **Superuser-Status** an.

4. Speichern Sie den Benutzer.

