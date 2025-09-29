
# Create Conda Environment

To run the python package Data Wherehouse Client, you need to create a conda environment.

## On Ubuntu

Run the below to create a conda environment `fgir` on an Ubuntu computer.
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
