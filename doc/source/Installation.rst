Installation
-------------

Install `anaconda <https://www.anaconda.com/products/individual>`_. Familiarise with python.


Clone the project


.. code-block:: bash

   git clone git@github.com:AaronDavidSchneider/chemcomp.git

move into directory:

.. code-block:: bash

   cd chemcomp


Install `conda <https://www.anaconda.com/products/individual>`_. virtual environment:

.. code-block:: bash

   conda create -n chemcomp astropy numpy scipy numba matplotlib pyyaml PyTables h5py
   conda activate chemcomp


Install `chemcomp`:

.. code-block:: bash

   pip install -e .


Adjust paths in `chemcomp/helper/main_helper` if you need different directories for output and config
