========
Backends
========

PKI role has few generic functions defined:

- generating certificate authorities
- generating service certificates
- installing certificate authorities
- installing service certificates

That's the common part applicable for all the backends, but each backend
has its own way of handling these functions.

.. toctree::
   :maxdepth: 1

   standalone.rst
   hashi_vault.rst
