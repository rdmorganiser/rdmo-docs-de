Social Accounts
---------------

Falls du Allauth für die Authetifizierung verwendest und RDMO konfiguriert hast, um ein oder mehrere OAUTH-Anbieter zu verwenden (wie im  :doc:`Konfiguration Kapitel </configuration/authentication/allauth>`) beschrieben, musst du deine RDMO-Seite mit diesen Services registrieren. Die Vorgehensweise ist jeweils verschieden. Meistens musst du einige Informationen zu deiner Seite angeben. Es wird immer eine Umleitungs- oder Rückruf-URL verlangt. Im folgenden werden wir als Beispiel http://127.0.0.1:8000 verwenden (welche auf dem Entwicklungsserver funktioniert) und die du mit der richtigen URL deiner RDMO-Anwendung dann im Betrieb ersetzen musst.

ORCID
    Log dich bei https://orcid.org ein und gehe auf die Seit emit den Entwicklungstools: https://orcid.org/developer-tools. Erstelle eine App mit der Umleitungs-URL.

    ::

        http://127.0.0.1:8000/account/orcid/login/callback/

github
    Log dich bei github ein und gehe auf https://github.com/settings/applications/new, um eine neue App zu erstellen. Verwende: 

    ::

        http://127.0.0.1:8000/account/github/login/callback/

facebook
    Log dich bei Facebook ein und gehe auf https://developers.facebook.com/. Klicke oben rechts im Menü auf *Meine Apps* und wähle *Neue App hinzufügen*. Erstelle eine neue App. In dem darauffolgenden Fenster wähle Facebook login -> Starten und wähle *Web* als Plattform. Füge eine URL ein unter der deine Anwendung zugänglich ist (Beachte:  127.0.0.1 wird nicht funktionieren.). Zurück auf dem Dashboard, gehe zu Einstellungen -> Grundeinstellungen und kopiere Àpp ID`und das App Geheimnis`.


twitter
    Login into twitter and go to https://apps.twitter.com/app/new and create a new app. Use

    ::

        http://127.0.0.1:8000/account/facebook/login/callback/

    as the Authorized redirect URI. Copy the Client-ID and the Client key.

Google
    Login into google and go to https://console.developers.google.com. Create a new project. After the project is created go to Credentials on the left side and configure the OAuth Authorization screen (second tab). Then create the credentials (first tab), more precisely a OAuth Client-ID. Use

    ::

        http://127.0.0.1:8000/account/google/login/callback/

    as the Authorized redirect URI. Copy the Client-ID and the Client key.

Once the credentials are obtained you need to enter them in the admin interface. To this purpose, go to **Social applications** under **SOCIAL ACCOUNTS** and click on **Add social application**. Then:

1. Select the corresponding **provider**

2. Enter a **Name** of your choice

3. Enter the **Client id** (or App ID) and the **Secret key** (or Client secret, Client key, App Secret)

4. Add your site to the chosen sites.

5. Click save.
