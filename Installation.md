## Preperation:
Install [anaconda](https://www.anaconda.com/products/individual "anaconda"). 
Familiarise with python.

## Install instructions:
Clone the project
```
git clone git@github.com:AaronDavidSchneider/chemcomp.git
```
move into directory:
```
cd chemcomp`
```
Install [conda](https://www.anaconda.com/products/individual "anaconda") environment:
```
conda create -n chemcomp astropy numpy scipy numba matplotlib pyyaml PyTables h5py  
conda activate chemcomp
```
Install `chemcomp`:
```
pip install -e .
````
Adjust paths in `chemcomp/helper/main_helper` if you need different directories for output and config