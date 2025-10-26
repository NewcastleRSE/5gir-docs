# 5GIR Dara Warehouse Export Guide

This guide ([https://newcastlerse.github.io/5gir-docs]([https://newcastlerse.github.io/5gir-docs)) is in our GitHub
repository ([https://github.com/NewcastleRSE/5gir-docs](https://github.com/NewcastleRSE/5gir-docs)).


## Install Required Software

To install:
- Anaconda, follow the instructions in [here](install_anaconda.md).
- PostgreSQL, follow the instructions in [here](install_postgres.md).


## Create Conda Environment

To run the python package Data Wherehouse Client, you need to create a conda environment. To create it, follow the
instructions in [here](create_conda_env.md).

## Log in to the 5GIR Database

You need to log in to the 5GIR database with either Bash, CMD or Python code to export data from the 5GIR data
warehouse. For instructions on how to log in, click [here](login.md).

## Get Data

You can get and export the data from the data warehouse via PostgreSQL queries or python code.

### Via PostgreSQL queries

Once you logged in to the data warehouse database, you can get and export the data from the data warehouse via
PostgreSQL queries from the command line. You run the same SQL queries, regardless of your terminal (Bash or CMD) and
Operating System (OS; Linux, Mac or Windows).


#### Run Local Commands
When you are connected to the database, you can run commands of your local (Bash or CMD) terminal by using the below
format and replacing `<command>` with the command that you want to run. 
```postgresql
\! <command>
```
##### Bash Commands
For example, if you are connected to the database by a bash terminal, you can get the current working directory with the
bash command `pwd` with this syntax:
```postgresql
\! pwd
```
You can list the files and subdirectories of your current working directory with command `ls` by using the below format:
```postgresql
\! ls
```
You can change your working directory with command `cd` by using the below format and replacing `</path/to/directory>`
with any other directory path in your local PC.
```postgresql
\! cd </path/to/directory>
```
##### CMD Commands
If you connected to the database via Windows Command Prompt (CMD), you can run the below to get your current working
directory 
```postgresql
\! echo %cd%
```
You can list the files and the subdirectories in your current directory with the CMD command `dir` as it follows:
```postgresql
\! dir
```
You can also change your current directory with command `cd` in the following way by replacing `<C:\path\to\directory>`
with the destination directory path in your local PC.
```postgresql
\! cd /d <C:\path\to\directory>
```


#### Run some PostgreSQL queries
View all table names in the DW with: 
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
SELECT column_name,data_type 
FROM information_schema.columns 
WHERE table_catalog = 'fgir_three' 
AND table_schema = 'public'
AND table_name = 'measurement';
```


```postgresql
select * from measurement where study = 0 and measurementgroup = 0
```


```postgresql
select * from measurement where study = 0 and measurementgroup = 0 and time >= '2025-09-08 00:00:00.000' and time < '2025-09-15 00:00:00.000' order by time;
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


### Get DATA via Python

TODO

### Get DATA via R

TODO
