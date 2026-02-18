# 5GIR Dara Warehouse Export Guide

This source to this guide ([https://newcastlerse.github.io/5gir-docs]([https://newcastlerse.github.io/5gir-docs)) is in the RSE Team GitHub
repository ([https://github.com/NewcastleRSE/5gir-docs](https://github.com/NewcastleRSE/5gir-docs)).


## Install Required Software

To install:
- Git, follow the instructions in [here](install_git.md).
- Anaconda, follow the instructions in [here](install_anaconda.md).
- PostgreSQL, follow the instructions in [here](install_postgres.md).


## Create Conda Environment

To run the Python package Data Warehouse Client, you need to create a conda environment. To create it, follow the
instructions in [here](create_conda_env.md).

## Log in to the 5GIR Database

You need to log in to the 5GIR database with either Bash, CMD or Python code to export data from the 5GIR Data
Warehouse. For instructions on how to log in, click [here](login.md).

## Get Data

You can get and export the data from the Data Warehouse via PostgreSQL queries or Python code.

### Via PostgreSQL queries

Once logged in to the Data Warehouse Postgres database server, you can get and export the data from the Data Warehouse via
SQL queries from the command line. You run the same SQL queries, regardless of your terminal (Bash or CMD) and
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

Preview the table study with:
```postgresql
select * from study;
```
You can view any of the tables in the DW, using this query, changing the table name (i.e., `measurement`,
`measurementgroup`, `textvalue`, `sourcetype` ect.)

For example, view measurement types and: 
```postgresql
select * from measurementtype;
```

And the source (sensor) types with:
```postgresql
select * from sourcetype;
```

When previewing the table `measurement`, you should limit the number of rows in the preview as the table
`measurement` has millions of rows. Preview the table `measurement` with a maximum of 20 rows with:
```postgresql
SELECT * FROM measurement limit 20;
```

You can count how many rows are in table measurement with:
```postgresql
select count(*) from measurement;
```

You can show only the column names of table `measurement` with:
```postgresql
SELECT column_name,data_type 
FROM information_schema.columns 
WHERE table_catalog = 'fgir' 
AND table_schema = 'public'
AND table_name = 'measurement';
```

Only display a maximum of 20 rows in `measurement` of the study `0` and measurement group `0` with:
```postgresql
select * from measurement where study = 0 and measurementgroup = 0 limit 20;
```

Only display a maximum of 20 rows in `measurement` of the study `0` and measurement group `1` with:
```postgresql
select * from measurement where study = 0 and measurementgroup = 1 limit 20;
```

You can also sort them by the timestamp of the recordings from older to newer (smaller to larger) with:
```postgresql
select * from measurement where study = 0 and measurementgroup = 0 order by time limit 40;
```
or with:
```postgresql
select * from measurement where study = 0 and measurementgroup = 0 order by time asc limit 40;
```

You can sort them by timestamp from newer to older with:
```postgresql
select * from measurement where study = 0 and measurementgroup = 0 order by time desc limit 40;
```

You can also sort them by multiple columns. The order of the columns in query matters. For example, the query below
sorts the recordings by `time` from newer to older. If two recordings have the same `time`, it sorts them by
`groupinstance` from smaller to larger. If they have the same `time` and `groupinstance`, it sorts them by
`measurementtype` from smaller to bigger.
```postgresql
select *
from measurement
where study = 0 and measurementgroup = 0
order by time desc, groupinstance asc, measurementtype asc
limit 40;
```

You can also choose to display only the recordings in a time period. The below only gets the measurements of study `0`
and measurement group `0` that were recorded between the beginning and the end of the 1st of September 2025. The
measurements are sorted by time, group instance and measurement type.
```postgresql
select *
from measurement
where study = 0 and measurementgroup = 0 and time >= '2025-09-01 00:00:00.000' and time < '2025-09-02 00:00:00.000'
order by time asc, groupinstance asc, measurementtype asc
limit 40;
```

An issue with the above queries of the table `measurement` is that they only get the measurement values that are stored
as integers and floats. There is no value for the measurements stored as stings because the string values are stored in
another table, the table `textvalue`. Therefore, you need to join the tables `measurement` and `textvalue`  to get all
measurement in one single table. You can do it with the following two queries.

This query is more readable, but slower:
```postgresql
select m.id, m.groupinstance, m.measurementtype, m.participant, m.study, m.source, m.valtype, t.textval, m.valinteger, m.valreal, m.time, m.measurementgroup, m.trial
from measurement as m left join textvalue as t on m.id = t.measurement
where m.study = 0 and m.measurementgroup = 0 and m.time >= '2025-09-01 00:00:00.000' and m.time < '2025-09-02 00:00:00.000'
order by time asc, groupinstance asc, measurementtype asc
limit 40;
```

This is less readable, but faster:
```postgresql
select m.id, m.groupinstance, m.measurementtype, m.participant, m.study, m.source, m.valtype, t.textval, m.valinteger, m.valreal, m.time, m.measurementgroup, m.trial
from (select * from measurement as m where m.study = 0 and m.measurementgroup = 1 and m.time >= '2025-09-01 00:00:00.000' and m.time < '2025-09-02 00:00:00.000') as m
left join textvalue as t on m.id = t.measurement
order by time asc, groupinstance asc, measurementtype asc
limit 40;
```

#### Export Data as CSV File


You can export data as csv file. Note that export will fail if your user does not have write permission in the directory
of your local machine where you are trying to write the csv file.

##### Export a Table 
You can export a whole table in the DW as csv file in your local machine with the query format: 
```postgresql
\COPY <TABLE_NAME> TO '<FILENAME>' DELIMITER ',' CSV HEADER
```
For example:
```postgresql
\COPY study TO 'study.csv' DELIMITER ',' CSV HEADER
```
or
```postgresql
\COPY measurement TO 'measurement.csv' DELIMITER ',' CSV HEADER
```
However, the two examples above create files `study.csv` and `measurement.csv` in your current working directory of your
local machine. Thus, if you do not have write permission in your current working directory the above two queries will
fail. If you don't know what is your current directory, and you logged in to the DW from a Windows Command Prompt, then
run the below to print your current working directory:
```postgresql
\! echo %cd%
```
If you looged in from Linux or Mac terminal, then run the below to print your current working directory:
```postgresql
\! pwd
```

If you want to save the file to another directory, you can either change the working directory or define the full path
of the csv file in the export query.

To change working directory, you need to:
1. log out from the DW with:
   ```postgresql
   \! q
   ```
2. Change directory with:
   ```
   cd <path_to_directory>
   ```
   replacing `<path_to_directory>` with the path of the directory where you want to write the csv file.
3. log in to the DW again with your credentials.
4. Run the export queries like:
   ```postgresql
   \COPY study TO 'study.csv' DELIMITER ',' CSV HEADER
   ```

Alternatively, if you are in the wrong working directory, you can just write the full path to the csv file in the query,
without changing working directory. For example, run the below on Windows Command Prompt replacing username with your
username.
```postgresql
\COPY study TO 'C:\Users\<username>\dw\study.csv' DELIMITER ',' CSV HEADER
```
If your username is `james`, then the query becomes:
```postgresql
\COPY study TO 'C:\Users\james\dw\study.csv' DELIMITER ',' CSV HEADER
```
Before running the above, make sure that directory `C:\Users\james\dw` already exists.

Run the below on Linux or Mac Terminal replacing username with your username.
```postgresql
\COPY study TO '/home/<username>/dw/study.csv' DELIMITER ',' CSV HEADER
```
If your username is `james`, then the query becomes:
```postgresql
\COPY study TO '/home/james/dw/study.csv' DELIMITER ',' CSV HEADER
```
Before running the above, make sure that directory `/home/james/dw` already exists.


##### Export a Query

you can export a query as csv file with the query format:
```postgresql
\COPY (<QUERY>) TO '<FILENAME>' DELIMITER ',' CSV HEADER
```
replacing `<QUERY>` and `<FILENAME>` with the query that you want to export and csv file name, respectively. For
example:
```postgresql
\COPY (select * from measurement where study = 0 and measurementgroup = 0) TO 'wet150.csv' DELIMITER ',' CSV HEADER
```
or
```postgresql
\COPY (select * from measurement where study = 0 and measurementgroup = 1) TO 'apogee.csv' DELIMITER ',' CSV HEADER
```



### Get DATA via Python

TODO

### Get DATA via R

TODO


## Manage Users

Administrators can manage other users. They can create new users, delete any other users, change the passwords of any
other users, change any other users' permission to the data. Administrators can also make some users administrators. If
you are an administrator, see the instructions on how to manage users in [here](manage_users.md).
