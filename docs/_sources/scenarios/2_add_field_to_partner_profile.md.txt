# Add a field to the Partner Profile resource type

This scenario will demonstrate the value of the SCRUD architecture by defining a new
field for the Partner Profile resource. The result will be automatic default support for
the new field in both the `scrud-django` and `scrud-vue` tools.

```{todo}
Figure out how versioning should work. In this scenario, we run up against it - there
will be existing resources that are missing the new property. We could require
registrations to include revisions and imply that any update to a resource **MUST**
upgrade it to the most recent revision. We could also require a migration, at some
point... but that's a bit onerous to start...
```

## Updating the JSON Schema

```{todo}
Link to previous, highlight the added field
```

## Updating the JSON-LD Context

```{todo}
Link to previous, highlight the added field
```

## Observe the changes in the REST API

### Get the OPTIONS for a Partner Profile resource

```{todo}
Add http traces
```

### GET the JSON Schema for a Partner Profile resource

```{todo}
Add http traces
```

### GET the JSON-LD for a Partner Profile resource

```{todo}
Add http traces
```

## Observe the changes in the UI

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
