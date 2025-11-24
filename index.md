# 5GIR Dara Warehouse Export Guide

This guide ([https://newcastlerse.github.io/5gir-docs]([https://newcastlerse.github.io/5gir-docs)) is in our GitHub
repository ([https://github.com/NewcastleRSE/5gir-docs](https://github.com/NewcastleRSE/5gir-docs)).


## Install Required Software

To install:
- Git, follow the instructions in [here](install_git.md).
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
select count(*) from measurement;
```

```postgresql
SELECT column_name,data_type 
FROM information_schema.columns 
WHERE table_catalog = 'fgir_three' 
AND table_schema = 'public'
AND table_name = 'measurement';
```


```postgresql
select * from measurement where study = 0 and measurementgroup = 0;
```



```postgresql
select * from measurement where study = 0 and measurementgroup = 0 and time >= '2025-10-26 00:00:00.000' and time < '2025-10-26 00:05:00.000' order by groupinstance, id;
```


```postgresql
select m.id, m.groupinstance, m.measurementtype, m.participant, m.study, m.source, m.valtype, t.textval, m.valinteger, m.valreal, m.time, m.measurementgroup, m.trial
from measurement as m full join textvalue as t on m.id = t.measurement
where m.study = 0 and m.measurementgroup = 1 and m.time >= '2025-10-26 00:00:00.000' and m.time < '2025-10-26 00:10:00.000'
order by m.groupinstance, m.id;
```

```postgresql
select m.id, m.groupinstance, m.measurementtype, m.participant, m.study, m.source, m.valtype, t.textval, m.valinteger, m.valreal, m.time, m.measurementgroup, m.trial
from (select * from measurement as m where m.study = 0 and m.measurementgroup = 1 and m.time >= '2025-10-26 00:00:00.000' and m.time < '2025-10-26 00:10:00.000') as m
left join textvalue as t on m.id = t.measurement
order by m.groupinstance, m.id;
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


## Manage Users

Display all users and their attributes with:
```postgresql
\du
```

select * from current_user;


### Create New Users (Roles)

To create a user `james_smith` that is valid until the end of September 2026, run the below. Note that the username
should not be in quotations while the password should be in single quotations. Also, note to that you need to replace
`jw8s0F4` with an appropriate password for `james_smith`:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4' VALID UNTIL '2026-10-01';
```
To create a user `james_smith` with no expiration date, run this:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4';
```

To create a user `james_smith` that can manage other users (create and remove users) and is valid until the end of
September 2026, run the following:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4' VALID UNTIL '2026-10-01' CREATEROLE;
```

To create a user `james_smith` that can manage other users and does not expire, run this:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4' CREATEROLE;
```

### Change User Passwords

Change the password of the existing user `james_smith` with:

```postgresql
ALTER USER james_smith WITH PASSWORD 'hr9k7zg';
```


### Change the Expiration Date of Users

Change the date when the existing user `james_smith` expires, run this:

```postgresql
ALTER USER james_smith WITH VALID UNTIL '2030-10-01';
```


### Give Users Permission to Manage Other Users

To give the existing user `james_smith` the permission to manage other users (create and remove other users), run this:
```postgresql
ALTER USER james_smith WITH CREATEROLE;
```

To remove the permission to manage other users of the existing user `james_smith`, run this:
```postgresql
ALTER USER james_smith WITH NOCREATEROLE;
```

### Give Read and Write Permission to Users 

If you want to give `james_smith` read-only permission to the DW, then add `james_smith` to the user group
`data_warehouse_read_only` by running:
```postgresql
GRANT data_warehouse_read_only TO james_smith;
```

If you want to give the user `james_smith` read and write permission to the DW, then add `james_smith` to the user group
`data_warehouse_read_write` by running the below:
```postgresql
GRANT data_warehouse_read_write TO james_smith;
```

### Remove Users

To remove the existing user `james_smith`, run this:
```postgresql
DROP ROLE james_smith;
```



### Get DATA via Python

TODO

### Get DATA via R

TODO
