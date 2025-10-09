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

### Get DATA via PostgreSQL queries

You can get and export the data from the data warehouse via PostgreSQL queries from the command line.



#### Run SQL Query

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
