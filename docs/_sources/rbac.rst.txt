Attribute and Role-Based Access Control
=======================================

For access control OpenTeams will use the `django-scoped-rbac project
<https://github.com/openteamsinc/django-scoped-rbac>`_ and `js-scoped-rbac project
<https://github.com/openteamsinc/js-scoped-rbac>`_. This project provides a flexible
framework for defining access control policies using the same REST architecture proposed
for OpenTeams.

For nuxt, the scoped-rbac package in NPM will be used to inform UI disclosure based on
authorization.
