.. _arch_services:

.. index:
  Services; Overview

Services
--------

Digital Rebar is made up of services.  These services are run in containers.  Most containers provide 
a single service that is exposed through consul.  The other services use consul connect and interact with
each other.  Some services are exposed to the user or nodes.

.. toctree::
  :maxdepth: 2
  :glob:

  containers
  *

