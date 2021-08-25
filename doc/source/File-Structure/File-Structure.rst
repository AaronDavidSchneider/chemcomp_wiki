Overview of files
-----------------

.. code-block :: bash

   chemcomp
   ├── analysis              # sample python scripts for post-processing
   ├── chemcomp              # main directory of the code
   │   ├── accretion_models  # modules for accretion
   │   ├── disks             # disk modules
   │   │   ├── _0pacity      # opacity files
   │   ├── helpers           # helper (e.g. wrapper for multiprocessing, etc)
   │   │   └── units         # units and other constants
   │   └── planets           # planet modules
   ├── config                # config files
   ├── jobs                  # job files
   ├── output                # output files
   └── zip_output            # ziped output files


Including the files ``main.py`` and ``pipeline.py`` and ``submit.sh``

main.py
^^^^^^^

Wrapper for running a single configuration. Execute with:

.. code-block :: bash

   python main.py [-h/--help][-c/--config_file]


* ``-c`` specifies the path to the config file.
* ``-h`` shows the help dialog.

Parameters that are set in the config file can be found [here](Config-File).

pipeline.py
^^^^^^^^^^^

Wrapper for running a multiple configurations. Execute with:

.. code-block :: bash

   python pipeline.py [-h/--help][-c/--config_file][-d/--delete][-j/--job_file]

* ``-c`` specifies the path to the config file.
* ``-h`` shows the help dialog.
* ``-d`` specifies wether to delete (use ``-d 1``) or not delete (use ``-d 0``) the files in ``output`` after zipping.
* ``-j`` specifies the path to the job file.

Explanations about the config file can be found [here](Config-File).
Explanations of the job file can be found [here](Job-File).

submit.sh
^^^^^^^^^

Shell wrapper for ``pipeline.py`` for running on a ``slurm`` cluster (like ``bachelor`` from the MPIA). Execute with same arguments like ``pipeline.py``. Execute on cluster with:

.. code-block :: bash

   sbatch submit.sh [-c][-j]

submit_MA.sh, submit_paper1.sh, submit_paper2.sh
""""""""""""""""""""""""""""""""""""""""""""""""

Sometimes its good to collect all run-configurations into a single file. Execute on cluster with:

.. code-block :: bash

   ./submit_paper1.sh


The chemcomp directory
^^^^^^^^^^^^^^^^^^^^^^

The ``chemcomp/chemcomp`` directory is the directory where the main code resides.

.. code-block :: bash

   chemcomp/chemcomp
   ├── __init__.py
   ├── accretion_models
   │   ├── __init__.py
   │   ├── _accretion_class.py     # framework for accretion models
   │   ├── gas.py                  # gas accretion model
   │   ├── pebbles.py              # pebble accretion model
   │   └── planetesimals.py        # planetesimal accretion model
   ├── disks
   │   ├── _0pacity
   │   │   ├── __init__.py
   │   │   ├── meanopac1_5050.dat  # opacity lookup table
   │   │   ├── meanopac5.dat       # opacity lookup table
   │   │   └── opacity_models.py   # delivers the opacities
   │   ├── __init__.py
   │   ├── _chemistry.py           # Bitsch2020 composition model
   │   ├── _chemistry_new.py       # SchneiderBitsch2020 composition model
   │   ├── _disk_class.py          # general disk model (parent of individual disks)
   │   ├── aaron.py                # analytical visc heating. Do not use.
   │   ├── bert.py                 # weird disk from bert
   │   ├── ida.py                  # weird Ida2016 disk
   │   ├── kees.py                 # visc heating that works
   │   ├── micha.py                # Michas disk. Do not use.
   │   ├── mmsn.py                 # simple mmsn disk with Hayashi H/R.
   │   └── twopop.py               # disk used in twopop.
   ├── helpers
   │   ├── __init__.py
   │   ├── analysis_helper.py      # framework for post processing
   │   ├── debugger_helper.py      # some useful functions for debugging during runtime
   │   ├── import_config.py        # functions that are used for the import of the parameters in the config file.
   │   ├── main_helpers.py         # functions that are used for main.py and pipeline.py.
   │   ├── solvediffonedee.py      # functions used for visc disk evolution
   │   ├── tridag.py               # functions used for visc disk evolution
   │   └── units
   │       ├── __init__.py
   │       ├── berts_units.py      # Berts weird code units. Not used.
   │       └── chemistry_const.py  # constants used for the _chemistry_new and _chemistry
   └── planets
       ├── __init__.py
       ├── _planet_class.py        # main planet module (parent).
       ├── bertmigration.py        # P11 + K18 migration + feedback torques.
       ├── migration_1.py          # only Lindblad torque.
       ├── no_accretion.py         # no accretion, no migration -> only disk
       └── simple_planet.py        # no migration


The code is structured in four main modules:

+-------------------------------------+-------------------------------------+------------------------------------------------------------------------------+
|              Module                 |   directory of parent class         |                                   Used for                                   |
+=====================================+=====================================+==============================================================================+
| :ref:`Disk <Disk Module>`           |         ``_disk_class``             | Deals with the disk related physics (e.g. dust growth, visc evolution, etc.) |
+-------------------------------------+-------------------------------------+------------------------------------------------------------------------------+
| :ref:`Chemistry <Chemistry Module>` | ``_chemistry_new`` / ``_chemistry`` |                     Chemical compositions used in ``Disk``.                  |
+-------------------------------------+-------------------------------------+------------------------------------------------------------------------------+
| :ref:`Planet <Planet Module>`       |        ``_planet_class``            |                Controls the other modules. Grows and migrates.               |
+-------------------------------------+-------------------------------------+------------------------------------------------------------------------------+
| :ref:`Accretion <Accretion Module>` |       ``_accretion_class``          |               Used in ``Planet``. Calculates the accretion rates.            |
+-------------------------------------+-------------------------------------+------------------------------------------------------------------------------+


Other directories
"""""""""""""""""

The paths for ``output``,``zip_output``,``config`` and ``jobs`` can be adjusted in ``chemcomp/chemcomp/helpers/__init__.py``

+----------------+---------------------+--------------------------------------------------------+
| Path           | Variable            | Use of path                                            |
+================+=====================+========================================================+
| ``output``     | ``OUTPUT_PATH``     | storage path for the output files                      |
+----------------+---------------------+--------------------------------------------------------+
| ``zip_output`` | ``ZIP_OUTPUT_PATH`` | storage path for the zipped output files               |
+----------------+---------------------+--------------------------------------------------------+
| ``jobs``       | ``JOB_PATH``        | path in which job configurations are stored            |
+----------------+---------------------+--------------------------------------------------------+
| ``config``     | ``CONFIG_PATH``     | path in which configuration/parameter files are stored |
+----------------+---------------------+--------------------------------------------------------+

The complete set of parameters in the config file is explained :ref:`here <config.yaml>`.
Explanations of the job file can be found here: :ref:`here <Job.yaml>`.