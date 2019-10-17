# Benutzer und Gruppen

Die Benutzer und Gruppen ihrer RDMO-Instanz werden unter **Authentifizierung und Authorisierung** verwaltet. Sie können Benutzer erstellen, verändern und deren Passwörter direkt setzen, wobei dies meist von den Benutzern selbst über das Account-Menü getan wird.

Der mit der Installation erstellte Benutzer hat zu allen Features von RDMO Zugang. Um anderen Benutzern den Zugang zum Management oder dem Admin-Interface zu gewähren, müssen ihnen die notwendigen Rechte zugewiesen werden. Dies kann auf zwei Arten erfolgen: durch die Gruppenzuordnung oder durch das Superuser-Flag.

## Gruppen

Während der Installation erstellt das `./manage setup_groups` Kommando drei Gruppen:

### Editor
Benutzer der Editorgruppe haben Zugang zum [Management Interface](../management/index.html) und können alle Elemente des Datenmodells editieren, mit Ausnahme der Benutzerdaten, die über das strukturierte Interview eingegeben wurden.

### Reviewer
Benutzer der Reviewergruppe haben Zugang zum [Management Interface](../management/index.html) wie die Editoren, jedoch ist es ihnen nicht gestattet, dort Veränderungen vorzunehmen (Speichern von Änderungen nicht erlaubt). Diese Gruppe kann verwendet werden, um ausgewählten Benutzern lesenden Zugriff auf das Management-Backend zu erlauben.

### API
Benutzer der API-Gruppe können eine programmierbare API verwenden, um auf alle Elemente des Datenmodels zuzgreifen. Sie benötigen einen [Token](api.html), um einen API-Klienten nutzen zu können.

Bereits existierende Benutzer können diesen Gruppen zugeordnet werden, um Zugang zu diesen Funktionen zu erhalten:

1. Klicken Sie auf **Benutzer** unter **Authentifizierung und Autorisierung** im Admin-Interface.
1. Klicken Sie auf den zu bearbeitenen Benutzer.
1. Klicken Sie auf die Gruppe zu dem der Benutzer hinzugefügt werden soll in dem **Verfügbare Gruppen**-Feld.
1. Klicken Sie auf den kleinen Pfeil, um die Gruppe zu dem **Gewählte Gruppen**-Feld zu bewegen.
1. Speichern Sie den Benutzer.


## Superuser

Superuser verfügen alle Rechte und alle Rechteüberprüfungs-Routinen geben einen positiven Wert zurück. Dies ermöglicht ihnen nicht nur den Zugang zu den Management- und Admin-Interfaces, sondern auch den **Zugang zu den Daten von allen anderen Benutzern** (einschließlich der Projektseite).
Um einem Benutzer Superuser-Privilegien zuzuweisen, gehen Sie wie folgt vor:

1. Klicken Sie auf **Benutzer** unter **Authentifizierung und Autorisierung** im Admin-Interface.
1. Klicken Sie auf den gewünschten Benutzer.
1. Kreuzen Sie die Box **Superuser-Status** an.
1. Speichern Sie den Benutzer.
