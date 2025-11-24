
# Create Conda Environment

To run the python package Data Wherehouse Client, you need to create a conda environment.

Before create the conda environment, confirm that you have `git` installed in your system, by following the steps in
[here](install_git.md)

## On Ubuntu

Create a conda environment `fgir` on an Ubuntu computer, by running the below:
```bash
name_conda_env=fgir

conda create -n "$name_conda_env" python=3.12 -y
conda activate "$name_conda_env"
python -m pip install --upgrade pip

python -m pip install git+https://github.com/NewcastleRSE/data-warehouse-client.git

conda deactivate
```

From now on, you can activate this conda environment with just:
```bash
name_conda_env=fgir
conda activate "$name_conda_env"
```

## On Windows

Run the below to create a conda environment `fgir` on a Windows computer.
```CMD
set "name_conda_env=fgir"

conda create -n %name_conda_env% python=3.12 -y
conda activate %name_conda_env%
python -m pip install --upgrade pip

python -m pip install git+https://github.com/NewcastleRSE/data-warehouse-client.git

conda deactivate

```

From now on, you can activate this conda environment with just:
```CMD
set "name_conda_env=fgir"
conda activate %name_conda_env%

```

## On Mac
TODO
