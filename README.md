# Helpful scripts for working at Datarmor

This repository contain scripts to run a Jupyter notebook instance within datarmor. 
It follows the repository https://github.com/coecms/nci_scripts created by:
**Scott Wales**

#### Great power, comes with great responsibility. Thus if you use this repository, make sure you use the resources wisely.
Make sure you kill the processes by using `Ctrl+C` whenever you want to stop the PBS job (killing the job locally will kill the job remotely). 

## Instructions of installation:

Clone the repository:

```
git clone git@github.com:josuemtzmo/datarmor_scripts.git
```

Navigate to the new folder:

```
cd datarmor_scripts
```

create an alias in your `~/.bashrc` by simply copy and paste the output of the command at the end of your `~/.bashrc`:

```
echo 'alias datarmor_jupyter='$(pwd)'/datarmor_scripts/datarmor_jupyter'
```

or run the following command (**Disclaimer, only modify .bashrc with a command if you know what you are doing**):

```
echo 'alias datarmor_jupyter='$(pwd)'/datarmor_scripts/datarmor_jupyter' >> ~/.bashrc
```

Make sure you already set up your ssh-keys to connect to `datarmor`, if not, do that now. Afterwards, you can create a default jupyter-lab instance using:

```
datarmor_jupyter
```

if you want to modify the default parameters, you can use the following command, which will create a jupyter-lab instance with 4 cores, 24 Gb of RAM, and 8 hours of wall-time. 

```
datarmor_jupyter -n 4 -t 08:00:00 -m 24
```

where `n` is the number of cores to use, `t` the wall-time in hours, and `m` the total memory of the job in Gb.


## datarmor_jupyter

Run a Jupyter notebook on `datarmor`, displaying it in a local web browser (run from your own computer, works on mac/linux/windows (using e.g. git bash)).

By default the script will spawn a job with a two CPUs, 4GB of memory and a walltime of 1 hour.

Command line options can be used to alter the resources requested, the conda environment used to spawn the job and NCI username

Usage:

```
datarmor_jupyter -h
```

Run a Jupyter notebook on Datarmor's compute nodes, presenting the interface in a browser on the local machine. This allows the user to specify a longer wall-time rather than the default 2 hours in the Datarmor Jupyter-Hub instance. 

You can set a default username in your local ~/.ssh/config, e.g.

    Host datarmor
    User abc123

General Options:
    -h:         Print help
    -l USER:    NCI username
    -L HOST:    NCI login node (default 'datarmor')
    -e ENVIRON: Conda environment
    -d:         Debug mode

Queue Options:
    -q QUEUE:   Queue name
    -n NCPU:    Use NCPU cpus (default: 2)
    -m MEM:     Memory allocation (default: 2*NCPU GB)
    -t TIME:    Walltime limit (default: 1 hour)

You will need to have ssh keys setup for logging into datarmor.
