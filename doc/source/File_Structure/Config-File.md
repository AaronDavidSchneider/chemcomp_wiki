## Explanation of `config.yaml`
**IMPORTANT: The code is build to use cgs units!**<br/>
*Either use cgs values or set unit conversion with `scale` in `chemcomp/helpers/import_config.py`*  

#### Example of unit conversion:  
In `config.yaml`:
```yaml
config_disk:
  M_STAR:   1.0
  ALPHA:    5.0e-4
```
| Variable | Unit | `import_config.py` | `__init__()` of module `Disk` |
|:---:|:---:|:---:|:---:|
| `ALPHA` | unit less value | untouched | untouched |    
| `M_STAR` | solar masses | becomes a quantity (with unit solar masses) by use of `scale` | `M_STAR.cgs.value` |

The same applies for all modules

#### The journey of parameters
There are generally two ways to bring a value from the configuration file into a module:
1. Use `kwargs` (example: `a_0` in `__init__()` of `Disk`)
2. Use function arguments in `__init__()` (example: `M_STAR` in `__init__()` of `Disk`)

#### The sections
A config file contains the following sections:

| Section | Used by `__init__()` of |
|:---:|:---:|
| `config_disk` | `Disk` module (specify with parameter `model`) |
| `config_planet` | `Planet` (specify with parameter `model`) |
| `config_pebble_accretion` |`PebbleAccretion` |
| `config_planetesimal_accretion` | `PlanetesimalAccretion` |
| `config_gas_accretion` | `GasAccretion` |
| `chemistry` |`Chemistry` |
| `defaults` | `Disk` |
| `output` | `Planet` |

## Example Of A Config File 

```yaml
# default config file

# Take care of units here! Otherwise adapt in import_config.scale_units!
# Physical parameters
config_disk:
  model:                        DiskLabDisk
  #SIGMA0:                       2000
  M_STAR:                       1.0        # mass of central star in sun massses
  ALPHA:                        5.0e-4     # Alpha viscosity
  ALPHAHEIGHT:                  1.0e-4
  #ALPHAFRAG:                    1.0e-4
  #ALPHAHMIG:                    1.0e-4
  M0:                           0.128       # needed for DiskLabDisk
  R0:                           137       # needed for DiskLabDisk
  DTG_total:                    0.02                              # Dust to gas ratios
  #DTG_pla:                        0.000
  #DTG_peb:                        0.666
  static:                       False
  evaporation:                  True
  static_stokes:                False
  #FUV_MDOT:                     1.0e-8
  #f_photoevap_int:              0.1
  tau_disk:                     1.0e4
  begin_photoevap:              3.0  # Myr

chemistry:
  FeH: 0.0
  use_FeH: False    # use FeH proxy fit according to Bitsch, Battestini 2020
  C_frac: 0.0     # Fraction of C/H in C (will be reduced from CH4)

config_planet:
  model:                        BertPlanet
  matter_removal:               True
  use_heat_torque:              True #True
  use_dynamical_torque:         True
  M0_fact:                      1
  #M_c:                          0.0045
  #M_a:                          0.0005
  a_p:                          20.0
  t_0:                          0.1      # time before planets start growing, total time: time_disk_0+t_0
  rho_c:                        5.5      # density of the core (g/cm**3)
  CFL:                          10      # timestep criterion

config_pebble_accretion:
  #STOKES:                       0.01     # Stokes Number
  rho_peb:                      2.0         # density of a single pebble (g/cm**3) gets ignored if STOKES is defined
  u_frag:                       5.0       # m/s
  epsilon_p: 0.5
  #H_p_over_H:                   0.1
  #twoD:                         True
  #REGIME:                       Hill

config_gas_accretion:
  kappa_env:                    0.01
  f:                            0.2
  f_machida:                    1
  f_disk_max:                   1.0

config_planetesimal_accretion:
  R_pla:                        50      # Planetesimal radius in km
  rho_pla:                      1       # density of a single planetesimal (g/cm^3) = 1000 kg/m^3
  stirring:                     1.0e-4
  efficiency:                   0.01

# modelling parameters
defaults:
  DEF_R_IN:                     0.1      # inner r boundary (in AU)
  DEF_R_OUT:                    5000     # outer r boundary (in AU)
  DEF_GRIDSIZE:                 300      # radial gridsize
  DEF_LIN_SPACING:              False    # Spacing of radial grid

output:
  name:                        Bert
  save_disk:                   True
  save_interval:               5000  # time in years
  save_disk_interval:          20
  plot_sigma_live:             False
  # acc_files:
  #   - "pebble"
  #   - "planetesimal"
  #   - "gas"
```
