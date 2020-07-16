(Envelope-Properties)=
# Envelope Properties

RDF Type
  `https://api.openteams.com/json-ld/Envelope`

An *Envelope Property* is an encapsulation of an  HTTP
resource. The primary use-case for envelopes is listing, search, and query response
resources. The envelop is a JSON object whose properties include the URL of the
resource, the caching headers that were current for the resource when the resource was
retrieved, the required SCRUD headers, and the content of the resource.

Envelopes provide a simple mechanism to provide compound resources comprised of multiple
included resources while enabling an envelope aware client the capability to maintain a
coherent cache for all resources.

(Envelope-Properties-Example)=
## Example

The example below is a JSON envelope object of a resource. The `url` property is the URL
of the resource whose content is contained in the `content` property. The
`last-modified` and `etag` properties are the standard HTTP caching headers.

```json
   {
     "url": "https://openteams.com/profile/230"
     , "last_modified": "Mon, 13 July 2020 12:12:12 GMT"
     , "etag": "XXXXX"
     , "content": {
       "id": "230"
       , "name": "Some Name"
     }
   }
```

(Envelope-Properties-Schema)=
## JSON Schema

```json
   {
     "$id": "https://api.openteams.com/json-schema/Envelope"
     , "$schema": "http://json-schema.org/draft-04/schema"
     , "title": "Resource Envelope"
     , "description": "A resource wrapper providing the url and http caching headers for a contained resource"
     , "properties": {
       "url": {
         "type": "string"
         , "format": "uri"
       }
       , "last_modified": {
         "type": "string"
       }
       , "etag": {
         "type": "string"
       }
       , "content": {
         "type": ["object", "array", "string", "number", "boolean"]
       }
     }
   }
```

(Envelope Properties Context)=
## JSON-LD Context

```json
   {
     "url": {
       "@id": "https://api.openteams.com/json-ld/Envelope/url"
       , "https://www.w3.org/TR/rdf-schema/#ch_subclassof":
           "https://www.w3.org/TR/HTTP-in-RDF10/#absoluteURIProperty"
     }
     , "last_modified": {
       "@id": "https://api.openteams.com/json-ld/Envelope/last_modified"
     }
     , "etag": {
       "@id": "https://api.openteams.com/json-ld/Envelope/etag"
     }
     , "content": {
       "@id": "https://api.openteams.com/json-ld/Envelope/content"
     }
   }
```
