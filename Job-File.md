Job files can be used for grid simulations where all parameters that are searched on are combined with each other.

## Example of a Job File
```yaml
par_1:
  name: ALPHA
  vals: [5.0e-5,1.0e-4,5.0e-4,1.0e-3]
  section: config_disk
par_2:
  name: DTG_total
  vals: [0.01,0.015,0.02,0.025]
  section: config_disk
par_3:
  name: begin_photoevap
  vals: [1.0,2.0,3.0]
  section: config_disk
par_4:
  name: a_p
  arange: [3, 51, 10]
  section: config_planet
par_5:
  name: t_0
  arange: [0.1, 1.0, 0.2] 
  section: config_planet
output_name: thorngren
four_disks: True

```
This example runs 1200 simulations (4x4x3x5x5) for every of the four cases of SB20 (plain, pla, evap, evap & pla).

## Explanation

#### Usage of `par_X` (enumerate starting by X=1):

| Parameter | Usage | 
|:---:|:---:|
| `vals` | List of values |
| `arange`| range with [start,stop,step] (e.g.[ 3, 51, 10 ] is eq. with `vals`=[3,13,23,33,43]) |
| `name` | Parameter for which values are given |
| `section` | Section in which parameter is used |

Use either `vals` if you want to give the values explicitly or `arange` for use with `np.arange`. 

#### Usage of other values:
| Parameter | Usage | 
|:---:|:---:|
|`four_disks`| `True` if you want to simulate the four cases of SB20 (plain, evap, pla, evap & pla) or `False` if you don't (e.g. only your config is used). |
|`save_disk` | `True` if you want to additionally save disk quantities else `False` |
|`output_name` | Name of the output files (important!!!)  |
