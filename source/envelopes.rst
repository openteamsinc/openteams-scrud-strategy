Envelope Properties
===================

An :ref:`Envelope Property <Envelope Properties>` is an encapsulation of an  HTTP
resource. The primary use-case for envelopes is listing, search, and query response
resources. The envelop is a JSON object whose properties include the URL of the
resource, the caching headers that were current for the resource when the resource was
retrieved, the required SCRUD headers, and the content of the resource.

Envelopes provide a simple mechanism to provide compound resources comprised of multiple
included resources while enabling an envelope aware client the capability to maintain a
coherent cache for all resources.
