Authentifizierungs-Token
------------------------

Um Daten in RDMO mit Hilfe einer programmierbaren API eingeben zu können, muss ein Benutzer mit einem Token assoziiert sein. Dies kann unter **AUTH TOKEN / Tokens** eingerichtet werden. Um einen Token zu erstellen, klicken Sie auf **token hinzufügen**, auf den Button rechts und:

1. Wählen Sie den **Benutzer** für den Token.

2. Speichern Sie den Token.

Dieser Token kann nun anstatt des Benutzernamens und des Passwortes genutzt werden, wenn HTTP-Anfragen von einem Script oder der Commandline kommen. Dafür muss ein HTTP-Header in der Form:


.. code-block:: none

    Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b

zur Verfügung gestellt werden.
