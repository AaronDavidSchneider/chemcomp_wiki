Outputing is handled in `chemcomp/chemcomp/planets/_planet_class.py` with the class `DataObject`.

Every run creates a `.h5` file with the following structure:
```bash
.
├── disk              # all the disk quantities
    ├── [quantities]
├── planet            # all the planet quantities
    ├── [quantities]
    ├── units           
├── acc               # accretion related quantities
    ├── [quantities]
```

#### Get started:
`.h5` files are self documented files!  

Browse through the content using:
```python
import h5py
file = "yourfilename.h5"
with h5py.File(file, "r") as f:
  print(dict(f["planet"].keys())
  print(dict(f["acc"].keys())
  print(dict(f["disk"].keys())
```

Units for planets can be retrieved by
```python
with h5py.File(file, "r") as f:
  units = dict(f["planet"]["units"].attrs)
```

#### Examples
- See `import_data()` in `chemcomp/chemcomp/helper/analysis_helper` for an example of how to load planet data
- See `chemcomp/analysis/paper_1/disk.py` for an example of how to load disk data