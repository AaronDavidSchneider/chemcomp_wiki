## Example of a Job File
```yaml
par_1:
  vals: [NoAccretion]
  name: model
  section: config_planet

par_2:
  vals: [3.5]
  section: config_planet
  name: t_0

four_disks: True
save_disk: True
output_name: only_disk
```

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
