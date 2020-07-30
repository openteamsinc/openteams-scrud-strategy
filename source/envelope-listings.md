# Envelope Listings

Endpoints for collections of resources, query services, and search services **SHOULD**
return paged listings of {ref}`envelopes <Envelope-Properties>`. These envelope listings
will need to be described in the JSON Schema and JSON-LD for those services.

## Example

```json
{
  "count": 1
  , "page_count": 1
  , "first": "/partner-profiles?page=1"
  , "previous": null
  , "next": null
  , "last": "/partner-profiles?page=1"
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

### JSON Schema 

```json
{
  "$id": "https://api.openteams.com/json-schema/PartnerProfile-Listing"
  , "$schema": "http://json-schema.org/draft-04/schema"
  , "description": "A listing of Partner Profile resources."
  , "properties": {
    "count": {
      "type": "integer"
      , "description": "The total number of items in the collection."
    }
    , "page_count": {
      "type": "integer"
      , "description": "The total number of pages in the collection."
    }
    , "first": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the first page."
    }
    , "previous": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the previous page, if any."
    }
    , "next": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the next page, if any."
    }
    , "last": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the last page."
    }
    , "content": {
      "properties": {
        "type": "array"
        , "description": "Listing items, Partner Profile resources, in Envelopes."
        , "items": {
          "$ref": "https://api.openteams.com/json-schema/Envelope"
        }
      }
    }
  }
}
```

### JSON-LD Context

```json
{
  "openteams": "https://ap.openteams.com/json-ld/"
  , "count": {
    "@id": "openteams:count"
  }
  , "page_count": {
    "@id": "openteams:page_count"
  }
  , "first": {
    "@id": "opententeams:first"
  }
  , "previous": {
    "@id": "opententeams:previous"
  }
  , "next": {
    "@id": "opententeams:next"
  }
  , "last": {
    "@id": "opententeams:last"
  }
  , "content": {
    "@id": "openteams:Envelope"
    , "@container": "@list"
    , "openteams:envelopeContents": "openteams:PartnerProfile"
  }
}
```

### JSON Schema Template

This Python string format template defines the minimal form of any paginated Listing
resource.

```json
{
  "$id": "{resource_type_uri}"
  , "$schema": "http://json-schema.org/draft-04/schema"
  , "description": "A listing of {resource_type_name} resources."
  , "properties": {
    "count": {
      "type": "integer"
      , "description": "The total number of items in the collection."
    }
    , "page_count": {
      "type": "integer"
      , "description": "The total number of pages in the collection."
    }
    , "first": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the first page."
    }
    , "previous": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the previous page, if any."
    }
    , "next": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the next page, if any."
    }
    , "last": {
      "type": "string"
      , "format": "uri"
      , "description": "URL of the last page."
    }
    , "content": {
      "properties": {
        "type": "array"
        , "description": "Listing items, {resource_type_name} resources, in Envelopes."
        , "items": {
          "$ref": "https://api.openteams.com/json-schema/Envelope"
        }
      }
    }
  }
}
```

### JSON-LD Context Template

This Python string format template defines the minimal form of any paginated Listing
resource.

```json
{
  "openteams": "https://ap.openteams.com/json-ld/"
  , "count": {
    "@id": "openteams:count"
  }
  , "page_count": {
    "@id": "openteams:page_count"
  }
  , "first": {
    "@id": "opententeams:first"
  }
  , "previous": {
    "@id": "opententeams:previous"
  }
  , "next": {
    "@id": "opententeams:next"
  }
  , "last": {
    "@id": "opententeams:last"
  }
  , "content": {
    "@id": "openteams:Envelope"
    , "@container": "@list"
    , "openteams:envelopeContents": "{resource_rdf_type_uri}"
  }
}
```

