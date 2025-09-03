# 5GIR Dara Warehouse Export Guide

This guide (https://newcastlerse.github.io/5gir-docs) is in our GitHub repository
(https://github.com/NewcastleRSE/5gir-docs).


## Install Required Software

Install the following programs:
- [Anaconda](install_anaconda.md)
- [PostgreSQL](install_postgres.md)


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
3. If you have admin permissions, and you have added the Postgres directory containing the file `psql.exe` to the Path
   environment variable, then you can skip this step and move to step 4. Otherwise, you need to locate the directory and
   add it to `PATH` every time you open a new Git bash window before running the command `psql`. An example of a
   Postgres directory is `C:\Program Files\PostgreSQL\14\bin` which must contain the file "psql.exe". If this is the
   case for you, you can add it to `PATH` with:
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


