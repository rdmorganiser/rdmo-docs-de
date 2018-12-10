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


## API-Layout

Die RDMO-Api hat folgende Endpunkte:

```
/api/v1/accounts/users
/api/v1/accounts/users/{id}

/api/v1/conditions/conditions
/api/v1/conditions/conditions/{id}

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

As you can see roughly the structure is determined by the element types of which data can be fetched. The `{id}` placeholder at the end of the URLs is indicating that an element ID can be provided to fetch data of a distinct single element. So basically we have to types of requests. The first returning lists of elements and the second returning single elements. Many of the endpoints provide multiple filter functions that are accessible using request parameters. If you for example would like to retrieve information about the admin user you could use `?username=admin` as filter parameter at the end of the url.

For practical reasons all the different filters will not be named here. But you can have a look into the [JSON description](/_static/others/api_description.json) of the API generated using Swagger. It covers every piece of information regarding all the endpoints and their available filters. As JSON can be a hard read sometimes you could also copy and paste the content of file into the [Swagger Editor](https://editor.swagger.io) to get a more consumable version of the description. If you would like to use Swagger to interact with your RDMO's API in a web  browser you could set it up for your RDMO installation. Information about how to do that are provided below in the [Swagger paragraph](#swagger-openapi). But let's have a look at some request examples first.


## Curl Request Examples

Note that the examples below use the `-L` parameter. It tells curl to follow redirects and is necessary because the token authentication process involves a redirect. If you do not follow it you will get an empty-bodied response having status code 301.

You could for example request...

1. The project having the id 1

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "https://$YOUR_RDMO/api/v1/project/projects/1"
```

2. A list of all projects

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "https://$YOUR_RDMO/api/v1/project/projects"
```

3. A list of users in a certain project

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "http://$YOUR_RDMO/api/v1/accounts/users/?project=1"
```

4. A list of options belonging to optionset 1

```bash
curl -LH "Authorization: Token $YOUR_TOKEN" \
    "http://$YOUR_RDMO/api/v1/options/options/?optionset=1"
```

5. A list of options having uri `https://rdmorganiser.github.io/terms/options/research_fields/216`
Note that strings of course need to be url encoded.

```bash
    curl -LH "Authorization: Token $YOUR_TOKEN" \
        "http://localhost/api/v1/options/options/?uri=https%3A%2F%2Frdmorganiser.github.io%2Fterms%2Foptions%2Fresearch_fields%2F216"
```


## Swagger / OpenAPI

### What is Swagger?

Swagger is a set of tools built around the OpenAPI Specification. These tools help to design, build and document REST APIs. OpenAPI is already implemented in RDMO but usually disabled. The Swagger page in RDMO is provided by a python library called [Django REST Swagger](https://github.com/marcgibbons/django-rest-swagger).

The Swagger page can help you to design API queries because it gives a well-arranged interactive overview of all the available endpoints and query parameters. If you need help to get an idea about the possibilities of the RDMO API you should have a look.


### Enable Swagger Tools

If you want to have a look at a detailed description of all the API interfaces that RDMO provides you need to add the necessary import and setup a url scheme to access the view.

All this can be achieved by adding two lines to the `config/urls.py` in your RDMO-App. Please note that `urlpatterns` is an array. Do not simply copy the snippet from below but add the array entry into your already existing one.

```bash
from rdmo.core.swagger import swagger_schema_view

urlpatterns = [
    url(r'^swagger$', swagger_schema_view.as_view()),
]
```

The Swagger page can now be accessed at the defined URL scheme. In the case of the example above at `swagger/`. Of course you are free to change this to fit your needs.

Apppend request parameter `?format=openapi` to the url to get a detailed API description in JSON format. It is the exact same description that we mentioned at the end of the [API Layout](#api-layout) paragraph above.
