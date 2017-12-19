Social Accounts
---------------

Falls Sie Allauth für die Authetifizierung verwenden und RDMO konfiguriert haben, um ein oder mehrere OAuth-Anbieter zu verwenden (wie im  :doc:`Konfiguration Kapitel </configuration/authentication/allauth>`) beschrieben, mussen Sie ihre RDMO-Seite mit diesen Services registrieren. Die Vorgehensweise ist jeweils verschieden. Meistens mussen Sie einige Informationen zu ihrer Seite angeben. Es wird immer eine Umleitungs- oder Rückruf-URI verlangt. Im folgenden werden wir als Beispiel http://127.0.0.1:8000 verwenden (welche auf dem Entwicklungsserver funktioniert) und die Sie mit der richtigen URL ihrer RDMO-Anwendung dann im Betrieb ersetzen müssen.

ORCID
    Loggen Sie sich bei https://orcid.org ein und gehen Sie auf die Seite mit den Entwicklungstools: https://orcid.org/developer-tools. Erstellen Sie eine App mit der Umleitungs-URL.

    ::

        http://127.0.0.1:8000/account/orcid/login/callback/

GitHub
    Loggen Sie sich bei GitHub ein und gehen Sie auf https://github.com/settings/applications/new, um eine neue App zu erstellen. Verwenden Sie: 

    ::

        http://127.0.0.1:8000/account/github/login/callback/

Facebook
    Loggen Sie sich bei Facebook ein und gehen Sie auf https://developers.facebook.com/. Klicken Sie oben rechts im Menü auf *Meine Apps* und wählen Sie *Neue App hinzufügen*. Erstellen Sie eine neue App. In dem darauffolgenden Fenster wählen Sie Facebook login -> Starten und wählen *Web* als Plattform. Fügen Sie eine URI ein unter der ihre Anwendung zugänglich ist (Beachten Sie: 127.0.0.1 wird nicht funktionieren.). Zurück auf dem Dashboard, gehen Sie zu Einstellungen -> Grundeinstellungen und kopieren `App ID` und das `App Secret`.

Twitter
    Log Sie sich bei Twitter ein und gehen Sie auf https://apps.twitter.com/app/ne, um eine neue App zu erstellen. 

    ::

        http://127.0.0.1:8000/account/facebook/login/callback/

    als die atuorisierte Umleitungs-URI. Kopieren Sie die Client-ID und den Client-Schlüssel.

Google
    Loggen Sie sich bei Google ein und gehen Sie auf https://console.developers.google.com. Erstellen Sie ein neues Projekt. Gehen Sie danach zu den Zugangsdaten auf der linken Seite und richtigen Sie das OAuth Athentifizierungsfesnter (zweiter Tab) ein. Dann erstellen sie die Zugangsdaten (erster Tab), genauer gesagt die OAuth-ID. Verwende: 

    ::

        http://127.0.0.1:8000/account/google/login/callback/

    als die authentifizierte Umleitungs-URI. Kopieren Sie die Client-ID und den Client-Schlüssel.

Sobald die Zugangsdaten gelten, können Sie sie in dem Admin-Interface eingeben, Dafür gehen Sie auf **Sozialle Anwendungen* unter **Soziale Accounts** und klicken auf **Sozialen Account hinzufügen**. Dann:

1. Wählen Sie den entsprechenden **Anbieter**

2. Geben Sie einen **Namen** ihrer Wahl ein

3. Geben Sie die **Client-ID* (oder App-ID) und den **Geheimschlüssel** (oder Client secret, Client-Schlüssel, App Secret)

3. Fügen Sie  ihre Seite zu den ausgewählten Seiten hinzu.

4. Klicken Sie auf speichern.

