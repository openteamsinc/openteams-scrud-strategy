(SCRUD)=
# SCRUD 

```{rubric} Semantic Create, Retrieve, Update, and Delete
```

SCRUD is specified by the
[semantic-http-spec](https://github.com/Quansight-Labs/semantic-http-spec), which
defines a set of standards for HTTP REST APIs. This architecture specifies the
requirements for an HTTP {ref}`REST` API that satisfies SCRUD principles and is the
basis for the technical strategy outlined in this document.

SCRUD makes resources and services very discoverable by requiring specific support for
the HTTP OPTIONS method as well as standard headers required for compliant APIs.

The result of the SCRUD standards is a base REST architecture intended to provide a rich
foundation for access control and automated UI binding. This is achieved by providing a
schema for the structure of a resource as well as a linked data context to provide the
meaning of the data contained in the resource. The combination of discoverable structure
and meaning for the resource, along with rich support for HTTP OPTIONS, enable the
automated binding of data contained in the resource to UI components.
