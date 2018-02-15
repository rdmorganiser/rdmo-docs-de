Social Accounts
---------------

Falls Sie django-allauth für die Authentifizierung verwenden und RDMO konfiguriert haben, um ein oder mehrere OAuth-Anbieter zu verwenden (wie im  :doc:`Konfiguration Kapitel </configuration/authentication/allauth>`) beschrieben, müssen Sie ihre RDMO-Website bei diesen Services registrieren. Die Vorgehensweise ist jeweils verschieden. Meistens müssen Sie einige Informationen zu ihrer Website angeben. Es wird immer eine Umleitungs- oder Rückruf-URI verlangt. Im folgenden werden wir als Beispiel http://127.0.0.1:8000 verwenden (welche auf dem Entwicklungsserver funktioniert). Diese muss durch die richtige URI ihrer RDMO-Anwendung dann im Betrieb ersetzt werden.

ORCID
    Loggen Sie sich bei https://orcid.org ein und gehen Sie auf die Seite mit den Entwicklungstools: https://orcid.org/developer-tools. Erstellen Sie eine App mit der Umleitungs-URI.

    ::

        http://127.0.0.1:8000/account/orcid/login/callback/

GitHub
    Loggen Sie sich bei GitHub ein und gehen Sie auf https://github.com/settings/applications/new, um eine neue App zu erstellen. Verwenden Sie: 

    ::

        http://127.0.0.1:8000/account/github/login/callback/

Facebook
    Loggen Sie sich bei Facebook ein und gehen Sie auf https://developers.facebook.com/. Klicken Sie oben rechts im Menü auf *Meine Apps* und wählen Sie *Neue App hinzufügen*. Erstellen Sie eine neue App. In dem darauffolgenden Fenster wählen Sie Facebook Login -> Starten und wählen *Web* als Plattform. Fügen Sie eine URI ein unter der ihre Anwendung zugänglich ist (Beachten Sie: 127.0.0.1 wird nicht funktionieren.). Zurück zum Dashboard, gehen Sie zu Einstellungen -> Grundeinstellungen und kopieren `App ID` und das `App Secret`.

Twitter
    Log Sie sich bei Twitter ein und gehen Sie auf https://apps.twitter.com/app/ne, um eine neue App zu erstellen. 

    ::

        http://127.0.0.1:8000/account/facebook/login/callback/

    als die autorisierte Umleitungs-URI. Kopieren Sie die Client-ID und den Client-Schlüssel.

Google
    Loggen Sie sich bei Google ein und gehen Sie auf https://console.developers.google.com. Erstellen Sie ein neues Projekt. Gehen Sie danach zu den Zugangsdaten auf der linken Seite und richten Sie das OAuth Athentifizierungsfenster (zweiter Tab) ein. Dann erstellen sie die Zugangsdaten (erster Tab), genauer gesagt die OAuth-ID. Verwenden Sie: 

    ::

        http://127.0.0.1:8000/account/google/login/callback/

    als die authentifizierte Umleitungs-URI. Kopieren Sie die Client-ID und den Client-Schlüssel.

Sobald die Zugangsdaten gültig sind, können Sie diese in dem Admin-Interface eingeben. Dafür gehen Sie auf **Soziale Anwendungen* unter **Soziale Accounts** und klicken auf **Sozialen Account hinzufügen**. Dann:

1. Wählen Sie den entsprechenden **Anbieter**.

2. Geben Sie einen **Namen** ihrer Wahl ein.

3. Geben Sie die **Client-ID** (oder App-ID) und den **Geheimschlüssel** (oder Client secret, Client-Schlüssel, App Secret) ein.

4. Fügen Sie ihre Seite zu den ausgewählten Seiten hinzu.

5. Klicken Sie auf speichern.

