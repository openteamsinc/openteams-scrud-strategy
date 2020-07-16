# Overview

A general purpose {ref}`REST` architecture is proposed for OpenTeams that enriches the
base principles of {ref}`REST` to to require all resources provide descriptor resources
detailing the allowable structure and semantic meaning of the resources. This
architecture defines base requirements for headers to be provided on all HTTP responses,
as well as required headers to be provided on HTTP requests. This base {ref}`REST`
architecture will provide additional information to support an advanced and largely
automated UI framwork by providing both the {ref}`JSON-Schema` of the resources to
detail their allowable structure and the {ref}`JSON-LD` of those resources to detail
their semantic meaning.

On top of the base HTTP requirements in suport of the {ref}`REST` architecture of the
application, a role and attribute based access control architecture is specified that is
itself compliant with the overall {ref}`REST` architecture.

On top of the base {ref}`REST` architecture, a coherent caching client is specified that
will provide a single coherent cache for all resources accessed by browser clients. This
coherent caching client will provide notifications to listeners when resources are
changed.

Finally, a VueJS based UI client is defined that uses the combination of the
{ref}`JSON-Schema` and the {ref}`JSON-LD` context to render the resources for
presenting, previewing, summarizing, and editing. This UI client will use the coherent
caching client to maintain consistent renderings of individual resources through the
application and will use the attribute and role-based access control architecture to
determine what views are appropriate to display to the user based on authorization. 

## SCRUD

The Semantically enriched Create, Retrieve, Update, and Delete (SCRUD) architecture is
specified in the [semantic-http-spec]
(https://github.com/Quansight-Labs/semantic-http-spec) project. This architecture
specifies the requirements for an HTTP {ref}`REST` API that satisfies SCRUD principles
and is the basis for the technical strategy outlined in this document.
