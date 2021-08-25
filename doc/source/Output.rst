Output
------

Outputing is handled in ``chemcomp/chemcomp/planets/_planet_class.py`` with the class ``DataObject``.

Every run creates a ``.h5`` file with the following structure:

.. code-block :: bash

   .
   ├── disk              # all the disk quantities
       ├── [quantities]
   ├── planet            # all the planet quantities
       ├── [quantities]
       ├── units
   ├── acc               # accretion related quantities
       ├── [quantities]



Get familiar with the output
""""""""""""""""""""""""""""

``.h5`` files are self documented files!

Browse through the content using:

.. code-block :: python

   import h5py
   file = "yourfilename.h5"
   with h5py.File(file, "r") as f:
     print(dict(f["planet"].keys()))
     print(dict(f["acc"].keys()))
     print(dict(f["disk"].keys()))


Units for planets can be retrieved by

.. code-block :: python

   with h5py.File(file, "r") as f:
     units = dict(f["planet"]["units"].attrs)


Examples
""""""""

* See `import_data()` in `chemcomp/chemcomp/helper/analysis_helper` for an example of how to load planet data
* See `chemcomp/analysis/paper_1/disk.py` for an example of how to load disk data

.. note :: Mention the GrowthPlot Class!