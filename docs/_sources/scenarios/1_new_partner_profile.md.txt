# Define a new Partner Profile resource type

In this scenario, we'll create a new kind of resource, an OpenTeams Partner resource.
We'll define this resource by creating a JSON Schema as well as a JSON-LD context to
describe the meaning of the fields specified in the JSON Schema. We'll show how to
configure this new resource type in Django using the `scrud-django` application and
demosntrate how to use the REST API this creates. Next, we'll show how the profile will
be rendered by default and customize the rendering of one of the fields.

## Example JSON for a Partner Profile resource

```json
{
  "name": "Semantics and CRUD, LLC"
  , "display_name": "Semantics and CRUD"
  , "slug": "semantics-crud"
  , "logo": "http://backend.openteams.com/partners/semantics-crud/media/logo.png"
  , "id": "some-uuid"
}
```

## Defining and implementing the REST API

Defining a REST API in SCRUD requires the creation of a JSON Schema to define the
JSON supported for the new REST API. The definition of a REST API in SCRUD also requires
the creation of a JSON-LD context describing the properties specified in the JSON Schema
for the resource. Given a JSON Schema and a JSON-LD context, libraries like
`scrud-django` can create a default REST API implementation supporting the resource
defined by the combination of the JSON Schema and JSON-LD schema that satisfies the
`semanantic-http-spec` standard.

### Defining the JSON Schema

```json
{
  "$id": "https://api.openteams.com/json-schema/PartnerProfile"
  , "$schema": "http://json-schema.org/draft-04/schema"
  , "title": "Partner Profile"
  , "description": "A resource detailing an OpenTeams Partner."
  , "properties": {
    "name": {
      "type": "string"
      , "description": "The legal name of the Partner business entity."
    }
    , "display_name": {
      "type": "string"
      , "description": "The name to display when referencing the Partner."
    }
    , "slug": {
      "type": "string"
      , "description": "Suggested short name to use in URLs."
    }
    , "logo": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of a logo to display for the Partner."
    }
    , "id": {
      "type": "string"
      , "description": "The system identifier for the Partner Profile resource."
    }
  }
}
```

### Defining the JSON-LD Context

```json
{
  "schema": "http://schema.org/"
  , "openteams": "http://api.openteams.com/json-ld/"
  , "@type": "schema:Organization"
  , "name": {
    "@id": "schema:legalName"
  }
  , "display_name": {
    "@id": "schema:name"
  }
  , "slug": {
    "@id": "schema:identifier"
  }
  , "logo": {
    "@id": "schema:logo"
  }
  , "id": {
    "@id": "rdfs:id"
  }
}
```

### Configuring the Partner Profile resource in Django

```{todo}
Show how to configure in Django
```

Define a new application. Configure the new model in `models.py` in the new application.

```python
from importlib import resources
from scrud import register_resource_type

register_resource_type(
  json_schema=resources.path("my.django.app", "partner_profile_schema.json"),
  json_ld_context=resources.path("my.django.app", "partner_profile_context.json"),
  rdf_type_uri="https://api.openteams.com/json-ld/PartnerProfile",
  )
```

## Using the Partner Profile REST API

### Get a listing of the existing Partner Profile resources

#### Request

```http
GET /partner-profiles HTTP/1.1
Host: backend.openteams.com
Accept: application/json
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 12:12:12 GMT
Last-Modified: Tue, 21 Jul 2020 12:12:12 GMT
ETag: "11111"
Link: <https://api.openteams.com/json-schema/PartnerProfile-Listing>; rel="describedBy"
Link: <https://api.openteams.com/json-ld/PartnerProfile-Listing>;
      rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"

{
  "count": 1
  , "page_count": 1
  , "previous": null
  , "next": null
  , "content": [
    {
      "url": "/partner-profiles/semantics-crud"
      , "last_modified": "Tue, 21 Jul 2020 12:12:12 GMT"
      , "etag": "00000"
      , "content": {
        "name": "Semantics and CRUD, LLC"
        , "display_name": "Semantics and CRUD"
        , "slug": "semantics-crud"
        , "logo": "http://backend.openteams.com/partners/semantics-crud/media/logo.png"
        , "id": "some-uuid"
      }
    }
  ]
}
```

### Get the OPTIONS for the Partner Profile listing resource

#### Request

```http
OPTIONS /partner-profiles HTTP/1.1
Host: backend.openteams.com
Accept: application/json
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 12:12:12 GMT
Last-Modified: Tue, 21 Jul 2020 12:12:12 GMT
ETag: "22222"
Link: <http://scrud.io/schemas/semantic_http.json>; rel=”describedby”
Link: <http://scrud.io/contexts/semantic_http.json>;
      rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"

{
   "get": {
      "responses": {
         "200": {
             "description": "OK"
             , "content": {
                 "application/json": {
                     "context":
                     "https://api.openteams.com/json-ld/PartnerProfile-Listing"
                     , "schema":
                     "https://api.openteams.com/json-schema/PartnerProfile-Listing"
                 }
             }
         }
      }
   }
   , "post": {
      "requestBody": {
         "description": "Create a new resource in this collection."
         , "required": true
         , "content": {
             "application/json": {
                 "context": "https://api.openteams.com/json-ld/PartnerProfile"
                 , "schema": "https://api.openteams.com/json-schema/PartnerProfile"
             }
         }
      }
      , "responses": {
         "201": {
            "description": "OK"
         }
         , "400": {
             "description": "BAD REQUEST: The request was malformed or
                             missing required content."
             , "content": {
                 "application/json": {
                     "context": "https://api.openteams.com/json-ld/ErrorResponse"
                     , "schema": "https://api.openteams.com/json-schema/ErrorResponse"
                 }
             }
         }
         , "401": {
             "description": "UNAUTHORIZED: The request requires
                             authentication."
         }
         , "403": {
             "description": "FORBIDDEN: The requires requires
                             permissions the current authenticated
                             request does not have."
         }
      }
   }
   , "delete": {
      "responses": {
         "200": {
             "description": "OK"
         }
         , "400": {
             "description": "BAD REQUEST: The request was malformed or
                             missing required content."
             , "content": {
                 "application/json": {
                     "context": "https://api.openteams.com/json-ld/ErrorResponse"
                     , "schema": "https://api.openteams.com/json-schema/ErrorResponse"
                 }
             }
         }
         , "401": {
             "description": "UNAUTHORIZED: The request requires
                             authentication."
         }
         , "403": {
             "description": "FORBIDDEN: The requires requires permissions
                             the current authenticated request does not
                             have."
         }

      }
   }
}
```

### POST a new Partner Profile resource

#### Request

```http
POST /partner-profiles HTTP/1.1
Host: backend.openteams.com
Content-Type: application/json

{
  "name": "Safety Dancers, Inc."
  , "display_name": "Safety Dancers"
  , "slug": "safety-dancers"
  , "logo": null
}
```

#### Response

```http
HTTP/1.1 201 Created
Content-Type: application/json
Date: Wed, 22 Jul 2020 12:12:12 GMT
Last-Modified: Wed, 22 Jul 2020 12:12:12 GMT
ETag: "33333"
Location: https://backend.openteams.com/partner-profiles/safety-dancers

{
  "name": "Safety Dancers, Inc."
  , "display_name": "Safety Dancers"
  , "slug": "safety-dancers"
  , "logo": null
  , "id": "some-other-uuid"
}
```

### GET the resulting Partner Profile resource

#### Request

```http
GET /partner-profiles/safety-dancers HTTP/1.1
Host: backend.openteams.com
Accept: application/json
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 13:13:13 GMT
Last-Modified: Wed, 22 Jul 2020 12:12:12 GMT
ETag: "33333"
Link: <https://api.openteams.com/json-schema/PartnerProfile>; rel="describedBy"
Link: <https://api.openteams.com/json-ld/PartnerProfile>;
      rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"

{
  "name": "Safety Dancers, Inc."
  , "display_name": "Safety Dancers"
  , "slug": "safety-dancers"
  , "logo": null
  , "id": "some-other-uuid"
}
```

### GET the listing of Partner Profile resources and see the new resource

#### Request

```http
GET /partner-profiles HTTP/1.1
Host: backend.openteams.com
Accept: application/json
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 12:12:12 GMT
Last-Modified: Tue, 21 Jul 2020 12:12:12 GMT
ETag: "44444"
Link: <https://api.openteams.com/json-schema/PartnerProfile-Listing>; rel="describedBy"
Link: <https://api.openteams.com/json-ld/PartnerProfile-Listing>;
      rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"

{
  "count": 2
  , "page_count": 1
  , "previous": null
  , "next": null
  , "content": [
    {
      "url": "/partner-profiles/semantics-crud"
      , "last_modified": "Tue, 21 Jul 2020 12:12:12 GMT"
      , "etag": "00000"
      , "content": {
        "name": "Semantics and CRUD, LLC"
        , "display_name": "Semantics and CRUD"
        , "slug": "semantics-crud"
        , "logo": "http://backend.openteams.com/partners/semantics-crud/media/logo.png"
        , "id": "some-uuid"
      }
    }
    , {
      "url": "/partner-profiles/safety-dancers"
      , "last_modified": "Wed, 22 Jul 2020 12:12:12 GMT"
      , "etag": "33333"
      , "content": {
        "name": "Safety Dancers, Inc."
        , "display_name": "Safety Dancers"
        , "slug": "safety-dancers"
        , "logo": null
        , "id": "some-other-uuid"
      }
    }
  ]
}
```


### Get the OPTIONS for the Partner Profile resource

#### Request

```http
OPTIONS /partner-profiles/safety-dancers HTTP/1.1
Host: backend.openteams.com
Accept: application/json
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 13:13:13 GMT
Last-Modified: Tue, 21 Jul 2020 12:12:12 GMT
ETag: "55555"
Link: <http://scrud.io/schemas/semantic_http.json>; rel=”describedby”
Link: <http://scrud.io/contexts/semantic_http.json>;
      rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"

{
   "get": {
      "responses": {
         "200": {
             "description": "OK"
             , "content": {
                 "application/json": {
                     "context": "https://api.openteams.com/json-ld/PartnerProfile"
                     , "schema": "https://api.openteams.com/json-schema/PartnerProfile"
                 }
             }
         }
      }
   }
   , "put": {
      "requestBody": {
         "description": "The updated content for the resource."
         , "required": true
         , "content": {
             "application/json": {
                 "context": "https://api.openteams.com/json-ld/PartnerProfile"
                 , "schema": "https://api.openteams.com/json-schema/PartnerProfile"
             }
         }
      }
      , "responses": {
         "200": {
            "description": "OK"
         }
         , "400": {
             "description": "BAD REQUEST: The request was malformed or
                             missing required content."
             , "content": {
                 "application/json": {
                     "context": "https://api.openteams.com/json-ld/ErrorResponse"
                     , "schema": "https://api.openteams.com/json-schema/ErrorResponse"
                 }
             }
         }
         , "401": {
             "description": "UNAUTHORIZED: The request requires
                             authentication."
         }
         , "403": {
             "description": "FORBIDDEN: The requires requires
                             permissions the current authenticated
                             request does not have."
         }
      }
   }
   , "delete": {
      "responses": {
         "200": {
             "description": "OK"
         }
         , "400": {
             "description": "BAD REQUEST: The request was malformed or
                             missing required content."
             , "content": {
                 "application/json": {
                     "context": "https://api.openteams.com/json-ld/ErrorResponse"
                     , "schema": "https://api.openteams.com/json-schema/ErrorResponse"
                 }
             }
         }
         , "401": {
             "description": "UNAUTHORIZED: The request requires
                             authentication."
         }
         , "403": {
             "description": "FORBIDDEN: The requires requires permissions
                             the current authenticated request does not
                             have."
         }

      }
   }
}
```

### PUT an update to the Partner Profile resource

#### Request

```http
PUT /partner-profiles HTTP/1.1
Host: backend.openteams.com
Content-Type: application/json
If-Match: "33333"
If-Unmodified-Since: Wed, 22 Jul 2020 12:12:12 GMT

{
  "name": "Safety Dancers, Inc."
  , "display_name": "Safety Dancers"
  , "slug": "safety-dancers"
  , "logo": "http://backend.openteams.com/partners/safety-dancers/media/logo.png"
  , "id": "some-other-uuid"
}
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 13:13:13 GMT
Last-Modified: Wed, 22 Jul 2020 13:13:13 GMT
ETag: "66666"
```

### DELETE the Partner Profile resource

#### Request

```http
DELETE /partner-profiles HTTP/1.1
Host: backend.openteams.com
If-Match: "66666"
If-Unmodified-Since: Wed, 22 Jul 2020 13:13:13 GMT
```

#### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 22 Jul 2020 13:13:13 GMT
```

## The default Partner Profile UI in `scrud-vue`

```{todo}
Mock up some screens, for now
```

### Get a listing of Partner Profile resources

```{todo}
Mock up some screens, for now
```

### View an individual Partner Profile resource

```{todo}
Mock up some screens, for now
```

### Edit an individual Partner Profile resource

```{todo}
Mock up some screens, for now
```

### Create a new Partner Profile resource

```{todo}
Mock up some screens, for now
```

## Customizing the rendering of the _tbd_ property

```{todo}
Pick a property, register a new vue component for its RDF type.
```

### Defining the new Vue component

```{todo}
Show the definition of a new Vue component.
```

### Registering the new Vue component

```{todo}
Show registering the component in the configuration map.
```

### The new UI after customization

```{todo}
Mock up some screenshots, for now.
```

#### View an individual Partner Profile resource

```{todo}
Mock up some screens, for now
```

#### Edit an individual Partner Profile resource

```{todo}
Mock up some screens, for now
```

#### Create a new Partner Profile resource

```{todo}
Mock up some screens, for now
```
