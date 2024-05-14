Setting up the Infrastructure
=============================

A similar setup to the one used to store the CALM-Brain data might be
of use to a data acquisition project of similar scale. This document
briefly summarises the packages, tools, and platforms that act in
cohesion to make this resource possible.

Data Storage Platform
---------------------

A local instance of `GIN`_ in a docker container is the platform of
choice for data storage of files. Its support for `git-annex`_ and
`datalad`_ were the main factors behind this decision. Detailed steps
to setup can be found in the `documentation`_.

The web interface of this local instance can be accessed from outside
the campus network and user registration is controlled. Seperate
repositories enact different zones of access. `almirah`_ can be used
to download data from these repositories provided the user has access.

.. _GIN: https://gin.g-node.org/
.. _datalad: https://www.datalad.org/
.. _almirah: https://girishmm.github.io/almirah/
.. _git-annex: https://git-annex.branchable.com/
.. _documentation: https://gin.g-node.org/G-Node/Info/wiki/In+House

Tabular Record Storage
----------------------

Tabular records are stored in a database on a `MariaDB`_ instance.

.. _MariaDB: https://mariadb.com/

Online Portal
-------------

Access requests and minimal searches are facilitated by a web app
developed using `django`_.

.. _django: https://www.djangoproject.com/

Authentication
--------------

To facilitate authentication using the same credentials into all of
these, a central `LDAP`_ is used. Each user is part of different groups
and the groups decide their access. For example, all members of `gin`
can access the data storage platform.

.. _LDAP: https://ldap.com/
