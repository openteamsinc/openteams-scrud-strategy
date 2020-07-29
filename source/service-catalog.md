# Service Catalog

A *Service Catalog* Resource provides a client a starting point for using the API
provided by a SCRUDful REST API. The catalog maps the primary resource types, by RDF
type URI, to the URL that provides that resource type.

Most resources listed in a *Service Catalog* resource will be listing, or collection,
resources. Other resources provided by the *Service Catalog* could be query services,
search services, or other parameterized services.

## Example

```json
{
  "https://api.openteams.com/json-ld/User-Listing":
      "https://backend.openteams.com/users"
  , "https://api.openteams.com/json-ld/Project-Listing":
      "https://backend.openteams.com/projects"
  , "https://api.openteams.com/json-ld/Organization-Listing":
      "https://backend.openteams.com/organizations"
  , "https://api.openteams.com/json-ld/PartnerProfile-Listing":
      "https://backend.openteams.com/partner-profiles"
  , "https://api.openteams.com/json-ld/ClientProfile-Listing":
      "https://backend.openteams.com/client-profiles"
}
```

## JSON Schema

```json
{
  "$id": "https://api.openteams.com/json-schema/ServiceCatalog"
  , "$schema": "http://json-schema.org/draft-04/schema"
  , "title": "Service Catalog"
  , "description": "A dictionary of SCRUD resources provided by this REST API."
  , "additionalProperties": {
    "type": "string"
    , "format": "uri"
  }
}
```

## JSON-LD Context

```json
{
  "@type": "https://api.openteams.com/json-ld/ServiceCatalog"
  , "@id": "https://api.openteams.com/json-ld/ResourceLink"
  , "@container": "@index"
}
```
