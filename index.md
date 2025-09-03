# 5GIR Dara Warehouse Export Guide

This guide (https://newcastlerse.github.io/5gir-docs) is in our GitHub repository
(https://github.com/NewcastleRSE/5gir-docs).

## Install Required Software

### On Ubuntu


#### PostgreSQL
Install `postgresql-14` in your local machine with:
```bash
sudo apt-get install postgresql-14 -y
```
Visit [here](https://www.postgresql.org/download/linux/ubuntu/) for more.


#### Anaconda

```bash
filename_installer=Anaconda3-2025.06-1-Linux-x86_64.sh

dirname_installer_local="$HOME"/Downloads
dirname_installer_remote=https://repo.anaconda.com/archive

dirname_installation="$HOME"/anaconda3

filename_installer_local="$dirname_installer_local"/"$filename_installer"

filename_installer_remote="$dirname_installer_remote"/"$filename_installer"

#cd "$dirname_installer_local"
#curl -O "$filename_installer_remote"
#cd -

wget -P "$dirname_installer_local" "$filename_installer_remote"

bash "$filename_installer_local" -b -p "$dirname_installation"

source "$dirname_installation"/bin/activate
conda init --all
conda config --set auto_activate_base false
conda deactivate

source "$HOME"/.bashrc
```




### On Windows


#### Git Bash

Git Bash comes with Git For Windows, download the Git installer in [here](https://git-scm.com/downloads/win) and install
it. For now on, any bash code in the documentation to be run on your Windows machine must be run on a Git Bash terminal.


#### PostgreSQL
Install PostgreSQL on Windows with the following steps:

1. Download the PostgreSQL 14 installer for Windows from
[here](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
2. Run the installer as administrator and follow the steps;
3. Add the directory of the PostgreSQL executable file "psql.exe" to the Path as you did for terraform above. In my
case, the directory to add is "C:\Program Files\PostgreSQL\14\bin", but it could be different in your machine. Bear in
mind that the directory should contain a file with name "psql.exe".
4. Verify the PostgreSQL installation by opening a new Git Bash terminal and running `psql --version` from the new
terminal. The command should print the PostgreSQL version installed into your machine.

More info in [here](https://medium.com/@itayperry91/get-started-with-postgresql-on-windows-a-juniors-life-4adfa6dd10e) 


#### Anaconda

Download and Install Anaconda with the following CMD code:
```CMD
set "filename_installer=Anaconda3-2025.06-1-Windows-x86_64.exe"

set "dirname_installer_local=%UserProfile%\Downloads"

set "dirname_installer_remote=https://repo.anaconda.com/archive"

set "dirname_installation=%UserProfile%\Anaconda3"

set "filename_installer_local=%dirname_installer_local%\%filename_installer%"

set "filename_installer_remote=%dirname_installer_remote%/%filename_installer%"

set "cwd=%cd%"

cd %dirname_installer_local%

curl -O %filename_installer_remote%

cd %cwd%

start /wait "" %filename_installer_local% /InstallationType=JustMe /AddToPath=0 /RegisterPython=0 /S /D=%dirname_installation%

%dirname_installation%\condabin\conda.bat activate
conda init --all
conda config --set auto_activate false
conda deactivate

```

### On Mac
TODO




## Conda Environment

To run the python package Data Wherehouse Client, you to create a conda environment.

### Only On Windows Git Bash
If you are not Windows Git Bash, please skip this subsection and continue from "Create Conda Environment".

Only if you are on Windows Git Bash, you need to start conda at least once on the terminal before running any conda
commands. First, define the anaconda directory:
```bash
dirname_anaconda=/c/ProgramData/Anaconda2024
```
Mind that the Anaconda directory can be different in your PC. Then, start conda with:
```bash
. "$dirname_anaconda"/etc/profile.d/conda.sh
```
Please, include the `.` and the space characters at the beginning of the line above 

### Create Conda Environment

Run the below to create a conda environment `fgir`.
```bash
name_conda_env=fgir

conda create -n "$name_conda_env" python=3.12 -y
conda activate "$name_conda_env"
python -m pip install --upgrade pip

python -m pip install git+https://github.com/NewcastleRSE/data-warehouse-client.git

conda deactivate

```
From now on you can activate this conda environment with just:
```bash
conda activate "$name_conda_env"
```

## Get DATA via PostgreSQL queries

You can export the data from the data warehouse via PostgreSQL queries from the command line of your PC.

### Log in to the 5GIR Database

You can log in to the 5GIR database with either CMD or bash code

#### Log in with Bash

1. Open the bash terminal on Linux and MACs, or Git bash on Windows, and run the following bash code.

2. Define the database name, host name, server port and username with the code below by replacing database_name,
   host_domain, host_port and user_name with the database name, host name, server port and username, respectively.
   ```bash
   dbname=database_name
   host=host_domain
   port=host_port
   username=user_name
   ```

3. If you are on Git Bash on Windows, you have admin permissions, and you have added the Postgres directory containing
   the file "psql.exe" to the environment variable `PATH`, then you can skip this step and move to step 4. Otherwise,
   you need to locate the directory and add it to `PATH` every time you open a new Git bash window before running the
   command `psql`. An example of a Postgres directory is "C:\Program Files\PostgreSQL\14\bin" which must contain the
   file "psql.exe". If this is the case for you, you can add it to `PATH` with:
   ```bash
   PATH="$PATH":/c/Program\ Files/PostgreSQL/14/bin
   ```
   Note that you need to replace "C:" with "/c", replace all "\" with "/", and add a "\" before each space character if
   the directory full path has any spaces, like in the example above. If the directory is different in your case, adjust
   the directory accordingly.

4. Run the following code in the same bash shell where you ran the previous code above.
   ```bash
   psql --dbname="$dbname" --host="$host" --port="$port" --username="$username" --password
   ```

5. Lastly, type the password of your user and press enter.

#### Log in with Windows CMD

1. Open the Command Prompt on Windows, and run the following CMD code.

2. Define the database name, host name, server port and username with the code below by replacing database_name,
   host_domain, host_port and user_name with the database name, host name, server port and username, respectively.

   ```CMD
   set "dbname=database_name"
   set "host=host_domain"
   set "port=host_port"
   set "username=user_name"
   ```
3. If you have admin permissions, and you have added the Postgres directory containing the file "psql.exe" to the
   environment variable `PATH`, then you can skip this step and move to step 4. Otherwise, you need to locate the
   directory and add it to `PATH` every time you open a new Git bash window before running the command `psql`. An
   example of a Postgres directory is "C:\Program Files\PostgreSQL\14\bin" which must
   contain the file "psql.exe". If this is the case for you, you can add it to `PATH` with:
   ```CMD
   set "PATH=%PATH%;C:\Program Files\PostgreSQL\14\bin;"
   ```
   If the directory is different in your case, adjust the directory accordingly.

4. Run the following code in the same command prompt window where you ran the previous code above.
   ```CMD
   psql --dbname=%dbname% --host=%host% --port=%port% --username=%username% --password
   ```

5. Lastly, type the password of your user and press enter.

### Run SQL Query

Once you logged in to the data warehouse database, you run the same SQL queries, regardless of your terminal (Bash or
CMD) and Operating System (OS; Linux, Mac or Windows). 




```postgresql
\dt
```


```postgresql
select * from study;
```

```postgresql
select * from measurementtype;
```

```postgresql
select * from measurement;
```


```postgresql
\COPY study TO 'study.csv' DELIMITER ',' CSV HEADER
```


```postgresql
\COPY (select * from measurement where study = 0 and measurementgroup = 0) TO 'wet150.csv' DELIMITER ',' CSV HEADER
```


```postgresql
\COPY (select * from measurement where study = 0 and measurementgroup = 1) TO 'apogee.csv' DELIMITER ',' CSV HEADER
```


