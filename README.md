# An introduction to __Conda__

An introduction to Conda by _Anastasiia Hyhorzhevska_. This repository serves as a guide for understanding and utilizing Conda for package management and environment control. Your feedback and contributions are highly encouraged!

- [What is conda?](#What-is-conda)
- [What conda do I have on the cluster?](#What-conda-do-I-have-on-the-cluster)
- [Anaconda3 installation/activation on the cluster](#Anaconda3-installation/activation-on-the-cluster)
- [Miniconda installation](#Miniconda-installation)
- [Environments](#Environments)
    - [Base environment](#Base-environment)
    - [Creating environment](#Creating-environment)
    - [Enter environment](#Enter-environment)
    - [Exiting environment](#Exiting-environment)
    - [Sharing environment](#Sharing-environment)
    - [Removing environment](#Removing-environment)
- [Running conda in interactive mode](#Running-conda-in-interactive-mode)
- [Running conda in batch mode](#Running-conda-in-batch-mode)
- [Useful resources](#Useful-resources)
- [Authors](#Authors)

# What is __conda__?

__Conda__ is an open source package and environment management system for any programming language.

__Conda__ allows you easily create and manage separate environments to avoid different types of version conflicts, and automatically checks for you when you try to install something new.

__Conda__ comes in two forms: __Anaconda__ and __Miniconda__:

- __Anaconda__ is a conda distribution that comes with a lot of packages.

- __Miniconda__ doesn’t come with any installed packages by default, hence it is more lightweight and you can install what you want.

# What __conda__ do I have on the cluster?

__On the slurmgate__, you have __anaconda2__ ditribution by default (__2__ means the version of __python__ it uses). To check this, you can run:

```conda info```

And you should see:

```js
     active environment : None
            shell level : 0
       user config file : /home/USER/.condarc
 populated config files :
          conda version : 4.5.11
    conda-build version : not installed
         python version : 2.7.15.final.0
       base environment : /opt/anaconda2  (read only)
           channel URLs : https://repo.anaconda.com/pkgs/main/linux-64
                          https://repo.anaconda.com/pkgs/main/noarch
                          https://repo.anaconda.com/pkgs/free/linux-64
                          https://repo.anaconda.com/pkgs/free/noarch
                          https://repo.anaconda.com/pkgs/r/linux-64
                          https://repo.anaconda.com/pkgs/r/noarch
                          https://repo.anaconda.com/pkgs/pro/linux-64
                          https://repo.anaconda.com/pkgs/pro/noarch
          package cache : /opt/anaconda2/pkgs
                          /home/USER.conda/pkgs
       envs directories : /home/USER/.conda/envs
                          /opt/anaconda2/envs
               platform : linux-64
             user-agent : conda/4.5.11 requests/2.12.4 CPython/2.7.15 Linux/3.10.0-1160.15.2.el7.x86_64 scientific/7.9 glibc/2.17
                UID:GID : 18948:403
             netrc file : None
           offline mode : False
```

__On the compute node PE__, __anaconda3__ is available and it is located: 
```/net/PE1/raid1/apps/anaconda/anaconda3```

# __Anaconda3__ installation/activation on the cluster

If you want to use anaconda3, you have two options:

__Use PE anaconda:__

1. Initialize your shell by running:

```/net/PE1/raid1/apps/anaconda/anaconda3/condabin/conda init bash```

This modifies your ```~/.bashrc``` file. 

2. Activate the base environment

```source ~/.bashrc``` 

which will be reflected in your shell prompt: 

```(base) [USER@slurmgate ~]$```

By default, the base environment will now be activated every time you log in to the cluster. 

3. To disable this, enter:

```conda config --set auto_activate_base false```

This will create a ```~/.condarc``` file.

__Install anaconda3 in your local directory__

1. Download the bash installer by running:

```wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh ```

2. Install it by running it as a bash command:

```bash Anaconda3-2020.11-Linux-x86_64.sh```

3. Activate the base environment:

```source ~/.bashrc```

# __Miniconda__ installation

To install miniconda

1. Download the bash installer by running:

```wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh```

2. Install it by running it as a bash command:

```bash Miniconda3-latest-Linux-x86_64.sh```

3. Activate the base environment:

```source ~/.bashrc```


# Environments

An __environment__ is a set of packages that can be used in one or multiple projects. Using conda, you can create an isolated environment for your project.

## Base environment

The __base__ conda environment is kind of your home base inside conda. This environment is somewhere you might want to install smaller programs that you tend to frequently use.

## Creating environment

The simplest way to create a new conda environment:

```sh
conda create -n my_env
```
where

__-n__: an argument for specifying the name of our new environment. It will check some things out and tell you where it is going to put it. And, when you hit __y__ and enter, it will be created:

```js
[user@slurmgate ~]$ conda create -n my_env
Solving environment: done

## Package Plan ##

  environment location: /home/user/.conda/envs/my_env


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate my_env
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

There are two ways of creating a conda environment:

1. An environment file in YAML format, e.g. __my_env.yml__.
2. Manual specifications of packages.

### __Creating environment with an environment file__

This is an example of an environment file, __my_env.yml__, that will install python 3.8 with numpy and pandas libraries:

```yaml
name: my_env
channels:
- conda-forge
dependencies:
- python=3.8
- numpy
- pandas
```

To install the environment with environment file above, run:

```sh
conda env create --file my_env.yml
```

The output you will see:

```js
Collecting package metadata (repodata.json): done
Solving environment: done

Downloading and Extracting Packages
libgfortran-5.0.0    | 19 KB     | ##################################################### | 100%
tk-8.6.10            | 3.3 MB    | ##################################################### | 100%
six-1.16.0           | 14 KB     | ##################################################### | 100%
libgfortran5-9.3.0   | 1.7 MB    | ##################################################### | 100%
libopenblas-0.3.15   | 8.7 MB    | ##################################################### | 100%
numpy-1.20.2         | 5.5 MB    | ##################################################### | 100%
pip-21.1.1           | 1.1 MB    | ##################################################### | 100%
liblapack-3.9.0      | 11 KB     | ##################################################### | 100%
libcblas-3.9.0       | 11 KB     | ##################################################### | 100%
pandas-1.2.4         | 10.6 MB   | ##################################################### | 100%
sqlite-3.35.5        | 1.7 MB    | ##################################################### | 100%
llvm-openmp-11.1.0   | 268 KB    | ##################################################### | 100%
setuptools-49.6.0    | 931 KB    | ##################################################### | 100%
readline-8.1         | 266 KB    | ##################################################### | 100%
libblas-3.9.0        | 11 KB     | ##################################################### | 100%
python-3.8.8         | 12.4 MB   | ##################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate my_env
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

### __Creating environment by manually specifying packages__

Alternatively, you can create conda environment by specifying the name, channel, and list of packages within the terminal window, e.g.:

```sh
conda create -c conda-forge -n my_env python=3.8 numpy pandas
```

where 

__-c:__ is a channel argument

__conda-forge:__ is a channel which provides conda packages for a wide range of software

You can specify several channeles. Th epriority will be given for the first listed, e.g. __conda-forge__ have highest priority:

```sh
conda install -c conda-forge -c bioconda -c defaults my_env python=3.8 numpy pandas
```

## Enter environment

To enter the environment, you need to execute:

```sh
conda activate my_env
```
You we can see you prompt has changed to have __my_env__ at the front, telling that you are in that environment:

```js
(my_env) [user@slurmgate ~]$  %
```

To see all of your environments, run:

```sh
conda env list
```

It will print out all of the available conda environments with an asterisk next to the one you are currently in.

## Exiting environment

To exit whatever conda environment you are currently, run:

```sh
conda deactivate 
```

## Sharing environment

To share an environment, you can export your conda environment to an environment file by running:

```sh
conda env export -f new_env.yml -n my_env
```

This will export a very detailed environment file:

```js
name: my_env
channels:
  - conda-forge
  - defaults
dependencies:
  - ca-certificates=2020.12.5=h033912b_0
  - certifi=2020.12.5=py38h50d1736_1
  - libblas=3.9.0=9_openblas
  - libcblas=3.9.0=9_openblas
  - libcxx=11.1.0=habf9029_0
  - libffi=3.3=h046ec9c_2
  - libgfortran=5.0.0=9_3_0_h6c81a4c_22
  - libgfortran5=9.3.0=h6c81a4c_22
  - liblapack=3.9.0=9_openblas
  - libopenblas=0.3.15=openmp_h5e1b9

  ...
```

## Removing environment

To remove an environment, you should first exit it, and then run:

```sh
conda env remove -n my_env
```

# Running __conda__ in interactive mode


1. Log into a compute node by running:

```srun -p pe -c 1 --mem=2G --pty bash```

Notice that the shell prompt changes from ```user@slurmgate``` to ```user@<pe{id}>``` to indicate that you are now on a compute node. 

2. Activate your environment, e.g. my_env

```(base) [USER@pe8 ~]$ conda activate my_env```

The shell prompt changes to: ```(my_env) [USER@pe8 ~]$``` 

3. Enter the relevant command, e.g. R.

# Running __conda__ in batch mode

In order to submit jobs to the Slurm job scheduler, you will need to use the main application you are using with your Anaconda environment in batch mode. There are a few steps to follow:

1. Create an application script
2. Create a Slurm job script that runs the application script
3. Submit the job script to the job scheduler with sbatch

For a job using Anaconda, a Slurm job script should look something like the following:

```sh
#!/bin/bash
#SBATCH --job-name="testconda"
#SBATCH --part=pe
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=16GB
#SBATCH --output=test_conda.out
#SBATCH --error=test_conda.err

source /etc/profile.d/modules.sh

module purge
module load anaconda/anaconda3

eval "$(conda shell.bash hook)"

conda activate my_env

sleep 30
echo "It works!" > test_conda.txt
```

where

```module purge```: clear environment modules

```module load anaconda/anaconda3```: load the anaconda3 environment module

```eval "$(conda shell.bash hook)"```: initialize the shell to use Conda

__Submit__ your script to the job scheduler by runnning:

```user@slurmgate:~$ sbatch test_conda.sh```

To __check__ the status of your job, enter ```squeue -u <username>```:

```js
[USER@slurmgate]$ squeue -u <username>
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           2659988        pe testcond     USER  R       0:22      1 pe8
```

# Useful resources

- [Conda Documentation](https://docs.conda.io/en/latest/)
- [Conda Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html)

## Authors

[Anastasiia Hryhorzhevska](https://www.linkedin.com/in/ahryhorzhevska)
