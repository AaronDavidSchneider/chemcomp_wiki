## Overview of directories

```bash
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
```

Including the files `main.py` and `pipeline.py` and `submit.sh`

#### main.py
Wrapper for running a single configuration. Execute with:
```bash
python main.py [-h/--help][-c/--Config-File]
```
`-c` specifies the path to the config file.  
`-h` shows the help dialog.

Parameters that are set in the config file can be found [here](Config-File).  

#### pipeline.py
Wrapper for running a multiple configurations. Execute with:
```bash
python pipeline.py [-h/--help][-c/--config_file][-d/--delete][-j/--job_file]
```
`-c` specifies the path to the config file.  
`-h` shows the help dialog.  
`-d` specifies wether to delete (use `-d 1`) or not delete (use `-d 0`) the files in `output` after zipping.    
`-j` specifies the path to the job file.  

Explanations about the config file can be found [here](Config-File).       
Explanations of the job file can be found [here](Job-File).  

#### submit.sh
Shell wrapper for `pipeline.py` for running on a `slurm` cluster (like `bachelor` from the MPIA). Execute with same arguments like `pipeline.py`. Execute on cluster with:
```bash
sbatch submit.sh [-c][-j]
```

##### submit_MA.sh, submit_paper1.sh, submit_paper2.sh
Sometimes its good to collect all run-configurations into a single file. Execute on cluster with:
```bash
./submit_paper1.sh
```



## the chemcomp directory
The `chemcomp/chemcomp` directory is the directory where the main code resides.


## other directories

The paths for `output`,`zip_output`,`config` and `jobs` can be adjusted in `chemcomp/chemcomp/helpers/__init__.py`

| Path | Variable | Use of path |  
|:--- |:--- |:--- |  
| `output` | `OUTPUT_PATH` | storage path for the output files |  
| `zip_output` | `ZIP_OUTPUT_PATH` | storage path for the zipped output files |  
| `jobs` | `JOB_PATH` | path in which job configurations are stored |  
| `config` | `CONFIG_PATH` | path in which configuration/parameter files are stored |  

The complete set of parameters in the config file is explained [here](Config-File).       
Explanations of the job file can be found [here](Job-File). 



