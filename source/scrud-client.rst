SCRUD Client
============

The SCRUD Client will be a Nuxt application comprised of several parts.

Caching Client
--------------

An :ref:`envelopes <Envelope Properties>` aware wrapper for the browser's `Cache` API.
All HTTP requests made by SCRUD Vue/Nuxt components will be made through the Caching
Client. The Caching Client will notify components that are listening to a particular URL
when the resource for that URL is known to have changed. The Caching Client will cache
all :ref:`envelopes <Envelope Properties>` contained in a resource.

JSON-LD Context Lookup
----------------------

This will provide a mechanism to lookup the RDF type for a given JSON property.

SCRUD Vue Component
-------------------

This Vue component will accept a configuration mapping relating RDF Type URIs to Vue
components responsible for rendering those RDF Types. The SCRUD Vue component will be
nestable, as well, to support nested components that are themselves constructed from
mappings from RDF types to other Vue components.

This component may be an extension of the Vue JSON Schema Forms component.

SCRUD Vue Layout Component
--------------------------

This component will define complex layouts comprised of regular Vue components and
nested SCRUD Vue components.

SCRUD Vue Pages
---------------

A SCRUD Vue page will be a Vue/Nuxt page addressable by URL that is comprised of a SCRUD
Vue Layout and its associated SCRUD Vue components.
