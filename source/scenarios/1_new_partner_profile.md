# Define a new Partner Profile resource type

In this scenario, we'll create a new kind of resource, an OpenTeams Partner resource.
We'll define this resource by creating a JSON Schema as well as a JSON-LD context to
describe the meaning of the fields specified in the JSON Schema. We'll show how to
configure this new resource type in Django using the `scrud-django` application and
demosntrate how to use the REST API this creates. Next, we'll show how the profile will
be rendered by default and customize the rendering of one of the fields.

## Defining and implementing the REST API

Defining a REST API in SCRUD requires the creation of a JSON Schema to define the
JSON supported for the new REST API. The definition of a REST API in SCRUD also requires
the creation of a JSON-LD context describing the properties specified in the JSON Schema
for the resource. Given a JSON Schema and a JSON-LD context, libraries like
`scrud-django` can create a default REST API implementation supporting the resource
defined by the combination of the JSON Schema and JSON-LD schema that satisfies the
`semanantic-http-spec` standard.

### Defining the JSON Schema

```{todo}
Define the schema, add some text
```

### Defining the JSON-LD Context

```{todo}
Define the context, add soem text
```

### Configuring the Partner Profile resource in Django

```{todo}
Show how to configure in Django
```

## Using the Partner Profile REST API

```{todo}
Show HTTP traces
```

### Get a listing of the existing Partner Profile resources

```{todo}
Add http traces
```

### Get the OPTIONS for the Partner Profile listing

```{todo}
Add http traces
```

### POST a new Partner Profile resource

```{todo}
Add http traces
```

### GET the resulting Partner Profile resource

```{todo}
Add http traces
```

### GET the listing of Partner Profile resources and see the new resource

```{todo}
Add http traces
```

### Get the OPTIONS for the Partner Profile resource

```{todo}
Add http traces
```

### PUT an update to the Partner Profile resource

```{todo}
Add http traces
```

### DELETE the Partner Profile resource

```{todo}
Add http traces
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
