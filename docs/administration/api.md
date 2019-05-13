# API

RDMO verfügt über eine API, mit der Daten in maschinenlesbarer Form ausgelesen werden können. Zugegriffen werden kann mit jedem Tool, das http beherrscht und in der Lage ist, das nötige Authentifizierungstoken im Request-Header bereitzustellen. In den folgenden Beispielen wird `curl` verwendet.

## Authentifizierung

Um Daten in RDMO mit Hilfe einer programmierbaren API eingeben zu können, muss ein Benutzer mit einem Token assoziiert sein. Dies kann unter **AUTH TOKEN / Tokens** eingerichtet werden. Um einen Token zu erstellen, klicken Sie auf **token hinzufügen**, (der Button rechts) und:

1. Wählen Sie den **Benutzer** für den Token.
1. Speichern Sie den Token.

Dieser Token kann anstatt des Benutzernamens und des Passwortes für autmatisierte HTTP-Anfragen genutzt werden. Dafür muss ein HTTP-Header in der folgenden Form zur Verfügung gestellt werden.

```
Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b
```

Nur `Superuser` können auf die API zugreifen. Ob ein bestimmter User die nötigen Zugriffsrechte hat, kann in den User Details überprüft werden. Anfragen von Usern ohne Superuser-Rechte scheitern unter Angabge des Status Codes 403.


## API-Layout / Swagger

Eine klarere Vorstellung vom Layout vermittelt `Swagger`, das in der Lage ist eine detaillierte Beschreibung aller Endpunkte zu geben.

### Was ist Swagger?
Swagger ist ein Werkzeug zur Dokumentation von REST-APIs, das die OpenAPI-Spezifikationen berücksichtigt. Es ist in RDMO implementiert. RDMOs Swagger-Seite wird von einer Bibliothek namens [Django REST Swagger](https://github.com/marcgibbons/django-rest-swagger) bereit gestellt.

Die interaktive Swagger-Seite bietet die Möglichkeit API-Anfragen zu designen und diese mitsamt ihrer Anfrage-Parameter auszuprobieren.

### Swagger nutzen

Swagger ist von Hause aus aktiviert. Der entsprechende Eintrag befindet sich in der 'urls.py' der RDMO-App.

```python
path('api/v1/', include('rdmo.core.urls.swagger')),
```

Er kann bei Bedarf gelöscht, auskommentiert oder modifiziert werden, ohne dass etwas anderes dadurch beeinträchtigt wird. Die Standard-URL der Swagger-Seite lautet: `http://$YOUR_RDMO/api/v1/`.

Wenn man die Anfrage zu `http://$YOUR_RDMO/api/v1/?format=openapi` modifiziert, bekommt man eine maschinenlesbare Beschreibung der RDMO-API im Json-Format.

### API-Struktur
Die RDMO-Api hat folgende Endpunkte:

```
/api/v1/conditions/conditions
/api/v1/conditions/conditions/{id}

/api/v1/core

/api/v1/domain/attributes
/api/v1/domain/attributes/{id}
/api/v1/domain/entities
/api/v1/domain/entities/{id}

/api/v1/options/options
/api/v1/options/optionsets
/api/v1/options/optionsets/{id}
/api/v1/options/options/{id}

/api/v1/projects/projects
/api/v1/projects/projects/{id}
/api/v1/projects/snapshots
/api/v1/projects/snapshots/{id}
/api/v1/projects/values
/api/v1/projects/values/{id}

/api/v1/questions/catalogs
/api/v1/questions/catalogs/{id}
/api/v1/questions/questions
/api/v1/questions/questionsets
/api/v1/questions/questionsets/{id}
/api/v1/questions/questions/{id}
/api/v1/questions/sections
/api/v1/questions/sections/{id}

/api/v1/tasks/tasks
/api/v1/tasks/tasks/{id}

/api/v1/views/views
/api/v1/views/views/{id}
```

Die API-Struktur ist grob bestimmt durch die Art von Daten, die verarbeitet werden können. Der '{id}'-Platzhalter gibt an, dass eine ID eingefügt werden kann, so dass Daten eines bestimmten Elementes gezogen werden. Im Wesentlichen gibt es zwei Arten von API-Endpunkten. Entweder werden Listen von Datensätzen ausgegeben oder einzelne Datensätze. Viele Endpunkte bieten Filter-Funktionen, die durch Anfrage-Parameter genutzt werden können.

Aus praktischen Gründen werden im Folgenden nicht alle Filter-Optionen genann. Ein Blick auf die mit Swagger generierte [JSON-Spezifikation](../_static/others/api_description.json) der API gibt einen detaillierten Einblick. Diese JSON-Datei kann in den [Swagger Editor](https://editor.swagger.io) geladen werden, um ein leichter lesbares Dokument zu erhalten. Doch nun zu ein paar Anfrage-Beispielen.

## Curl Anfragen

Die unten genannten Anfragen nutzen den `-L`-Parameter, der dafür sorgt, dass Curl Umleitungen folgt. Er ist nötig, da die Authentifizierung sonst nicht funktionieren würde, weil diese einen Redirect macht. Ohne Umleitungen zu verarbeiten produziert eine Anfrage eine leere Antwort und den Status Code 301.

Einige Beispiele...

1. Das Projekt mit der ID 1

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "https://$YOUR_RDMO/api/v1/project/projects/1"
```

2. Eine Liste aller Projekte

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "https://$YOUR_RDMO/api/v1/project/projects"
```

3. Eine Liste von Usern eines bestimmten Projekts

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "http://$YOUR_RDMO/api/v1/accounts/users/?project=1"
```

4. Eine Liste von Optionen, die zu Optionenset 1 gehören

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "http://$YOUR_RDMO/api/v1/options/options/?optionset=1"
```

5. Eine Liste von Optionen mit der uri `https://rdmorganiser.github.io/terms/options/research_fields/216`
Achtung: Strings sollten URL-encodiert seint.

```bash
    curl -LH "Authorization: Token $YOUR_TOKEN" \
        "http://localhost/api/v1/options/options/?uri=https%3A%2F%2Frdmorganiser.github.io%2Fterms%2Foptions%2Fresearch_fields%2F216"
```

## RDMO Client
Es gibt einen RDMO Client, der die Nutzung der API vereinfachen soll. Außerdem kann er gut für den Einstieg in das Thema verwendet werden. Er ist in Python geschrieben und kann auf [GitHub](https://github.com/rdmorganiser/rdmo-client) gefunden werden.
