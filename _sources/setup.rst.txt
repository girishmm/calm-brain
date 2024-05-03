Setting up the Infrastructure
==================================

A similar setup to the one used to store the CALM-Brain data might be
of use to a data acquisition project of similar scale. This document
briefly summarises the packages, tools, and platforms that act in
cohesion to make this dataset possible.

Data Storage Platform
---------------------

A local instance of `GIN`_ in a docker container is the platform of
choice for data storage. Its support for `git-annex`_ and `datalad`_
were the main factors behind this decision. Detailed steps to setup
can be found in the `documentation`_.

The web interface of this local instance can be accessed from outside
the campus network and user registration is controlled. Seperate
repositories enact different zones of access. `almirah`_ can be used
to download data from these repositories provided the user has access.

.. _GIN: https://gin.g-node.org/
.. _datalad: https://www.datalad.org/
.. _almirah: https://girishmm.github.io/almirah/
.. _git-annex: https://git-annex.branchable.com/
.. _documentation: https://gin.g-node.org/G-Node/Info/wiki/In+House

Library Dependencies
--------------------

`almirah`_ provides out-of-the-box routines that are implemented as
wrappers around other standard libraries in different languages. These
libraries might have dependencies that are not resolved during
`almirah`_ installation. The pipelines and their respective externally
installed dependencies are:

  * MRI format conversion : `dcm2niix`_
  * MRI defacing          : `FMRIB Software Library`_
  * MRI preprocessing     : `FreeSurfer`_, `Statistical Parametric Mapping`_

.. _dcm2niix: https://github.com/rordenlab/dcm2niix
.. _FreeSurfer: https://surfer.nmr.mgh.harvard.edu/
.. _FMRIB Software Library: https://fsl.fmrib.ox.ac.uk/fsl/fslwiki
.. _Statistical Parametric Mapping: https://www.fil.ion.ucl.ac.uk/spm/

.. important::
   
   Though not mentioned explicitly, it is implied that it is necessary
   to have the language the library is implemented in installed. For
   example, `SPM`_ requires `MATLAB`_.

.. _SPM: https://www.fil.ion.ucl.ac.uk/spm/
.. _MATLAB: https://in.mathworks.com/products/matlab.html



