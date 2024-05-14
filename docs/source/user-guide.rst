From access to analysis
=======================

.. currentmodule:: almirah

The CALM-Brain resource is a rich collection of data obtained from
over 2500 subjects. To know more about the contents of the dataset,
please head over to :doc:`reference`. The resource is made of two
parts: *data files* that organized according to or close to `BIDS`_
and *tabular records* that are stored in SQL tables.

.. _BIDS: https://bids.neuroimaging.io/

Requesting for access
---------------------

If you are interested and would like access, we are happy to help
you. Due to the sensitive nature of the dataset, it is currently not
possible to make it openly available. Please raise an access request
from the `portal`_ and you will receive your credentials for access
shortly. You might want to check out :ref:`looking-without-touching`
before raising the request if you would like to confirm if the
resource fits your needs.

It is possible to request for compute resources too and run analysis
locally on the server too!!

Once you have hold of your credentials, you can access the data files
of the resource!!  To quickly skim through the contents, head over to
the `GIN instance`_. You can think of this as GitHub for
datasets. Once you login, you will notice that you are a part of the
CBM organization and can access parts of the resource you have been
approved to. You can now download the data files to your local
system and use it :)

.. note::

   GIN is `DataLad`_ compatible. This means, when the dataset is
   cloned, not all file contents will be available right after. Only
   small files will be available right away. So, you can `look without
   touching`_ datalad style.

.. _DataLad: https://www.datalad.org/
.. _GIN instance: http://tekeli.ncbs.res.in:3000/
.. _look without touching: https://handbook.datalad.org/en/latest/basics/101-116-sharelocal.html

.. _looking-without-touching:

Looking without touching
------------------------

The `portal`_ has a search bar which allows querying the resource with
arguments compatible with `almirah`_ based on the ``Specification``
used. Since CALM-Brain is organized according to BIDS, all
BIDS-entities are accepted as arguments. The ``returns`` argument
allows you to mention the preferred return type. It defaults to the
string representation of `~layout.File` by default.

Here are some queries you can try find data files:

#. Files that are belong to the EEG modality.

   .. code-block:: python

		datatype="eeg"

#. EEG files that belong to the subject '*D0019*'.

   .. code-block:: python

		datatype="eeg", subject="D0019"

#. EEG files that belong to the first session of the subject '*D0019*'.

   .. code-block:: python

		datatype="eeg", subject="D0019", session="101"

#. EEG files recorded during the auditory paired-click paradigm task
   that belong to the first session of the subject '*D0019*'.

   .. code-block:: python				

		datatype="eeg", subject="D0019", session="101", task="auditoryPCP"

#. EEG files recorded during the auditory paired-click paradigm task
   of either subject '*D0019*' or '*D0274*'.

   .. code-block:: python				

		datatype="eeg", subject=["D0019", "D0274"], task="auditoryPCP"

To have a peek at the tabular records, you can provide the *table
name* of interest using the ``table`` argument. To find the *table
name* for a questionnaire or cognitive test, check out the
:doc:`reference`.

Here are some more queries to get tabular records:

#. Get the list of subjects.

   .. code-block:: python

		table="subjects"

#. Get only the '*subject ID*' from the list of subjects.

   .. code-block:: python

		table="subjects", returns="subjectID"

Results from the search query can be downloaded as a csv file.

.. tip::

   If you would like assistance building more sophisticated queries,
   use the query builder below the search bar. Some pre-built queries
   are available further below. Try them out!

Obtaining a subset of data files
--------------------------------

Let us *look without touching* using `almirah`_. This is often helpful
when you want to run an analysis on a storage constrained system and
you are interested in only a subset of the data files. For example,
you would like to download data relating to only the OCD cohort or
specific to resting state EEG. This is the same as the search bar, but
here you can find files that fit your need and download them. Then,
you can pass these maybe to a python function you have written. Search
bar is helpful for checking out the resource, but it cannot interface
with toolkits and allow analysis.

Each dataset release comes with an index. The index is an `SQLite`
file that can be downloaded from the portal. This index is the same
thing that is looked up by the search bar in the backend to provide
the results you see. The index allows you to filter through the
resource by associating each file in the resource to a set of tags and
storing it.

The index is also pre-populated with the details of the different
components that make up CALM-Brain. So, you can concentrate on using
the resource instead of adding in the components. `almirah`_ by
default looks for this index at system home. If have requested for
compute resources and are currently using the server to access the
resource locally, then you are good to go! If not, you will have to
download the index from `releases`_ and set it up for use.

Since, we do not know where you plan to store the dataset components,
the root for different layouts is set to various dummy paths like
*/path/to/data*. It is **NECESSARY** that you change this if you are
**not using the resource locally**!! This can be done with `almirah`_
like so:

#. Download the release-specific index to your home directory from the portal.
   
#. Set the path for different components.

   .. code-block:: python
		   
   		from almirah import Dataset
   
		# Retrieve the layout you are interested in.
		# Dummy path have been used while creating the index.
		dataset = Dataset.get(name='calm-brain')

		# View components
		dataset.components

		# Choose a component
		layout = dataset.components[0]

		# Change the layout path.
		layout.move_root('/your/local/path')
		
		# Clone the dataset from host to local path.
		layout.clone()

Now, you have successfully got the look-only version of the data. You
can now query the layout object to get files that only match your
needs.

Say, you only want resting state EEG data, then:

.. code-block:: python

		# Provide tags that fit your search criteria
		files = layout.query(datatype='eeg', task='rest')

		# Download these files
		for file in files:
		    file.download()

Now, you have downloaded the files that fit your search criteria. The
rest are still look-only files without their contents.

.. note::

   The same effect can be achieved using only `DataLad`_ commands to
   some extent. One approach would be to pair commands with patterns
   to choose specific filenames. But obtaining files that match
   certain metadata and study-specific parameters would not be
   possible this way.

.. tip::

   If you don't know what tags to try, use `options()
   <https://girishmm.github.io/almirah/reference/almirah.layout.html#almirah.layout.Tag.options>`_
   to display the possibilities.

Retrieving tabular data
-----------------------

The database information is already built into the index and is in
*request* mode, so all you need is provide the *table name* to
query. Same as in the search bar. Easy right?

   .. code-block:: python

		   from almirah import Dataset

		   # Retrieve the db from components.
		   dataset = Dataset(name='calm-brain')
		   db = dataset.components[1]

		   # Get the records you need from a table.
		   records = db.get_table(name='table_name')

The records are returned as a :doc:`pandas:reference/api/pandas.DataFrame`.

.. tip::

   Use the :doc:`reference` to checkout the info provided by
   each table. This will help you find which table has the info you
   need.

Analysis
--------

Now you know how to access and retrieve contents of the CALM-Brain
resource. How can you use it?

We leave that to you and look forward to how this resource helps with
the question of your interest. Since it is not possible to
exhaustively support all analysis possibilities, we will not be able
be supporting it. But if there is something specific you think we can
help with, do reach out.

It should be possible to interface almirah with any toolkit available in
python. We recommend the below libaries as we have found them to play
well with almirah for neuroimaging and genomics datasets:

.. list-table::
   :header-rows: 1

   * - Datatype
     - Recommended libraries
   * - Magnetic resonance imaging
     - `nibabel <https://nipy.org/nibabel/>`_
   * - Electroencephalography
     - `mne <https://mne.tools/stable/index.html>`_
   * - Eye tracking
     - `mne <https://mne.tools/stable/index.html>`_
   * - Functional near-infrared spectroscopy
     - `mne-nirs <https://mne.tools/mne-nirs/stable/index.html>`_
   * - Genomics
     - `pysam <https://pysam.readthedocs.io/en/latest/index.html>`_,
       `scikit-allel <https://scikit-allel.readthedocs.io/en/latest/>`_

If you would like to get acquainted with CALM-Brain and `almirah`_, do
follow through the :doc:`examples/index`. They will lead you through
simple analysis flows.

Citing and Contributing
-----------------------

If you use the resource in your work, please consider citing the
resource and the version you used. If you would like your analysis
outputs to be available for others, do reach out to `us`_. We would be
happy to add them as derivatives.

.. _us: bhalla@ncbs.res.in
.. _portal: https://www.calm-brain.ncbs.res.in/
.. _almirah: https://girishmm.github.io/almirah/
.. _releases: https://github.com/girishmm/calm-brain/releases


