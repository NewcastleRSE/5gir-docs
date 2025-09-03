
# Install PostgreSQL

## On Ubuntu

Install PostgreSQL on Ubuntu with:
```bash
sudo apt-get install postgresql-14 -y
```
Visit [here](https://www.postgresql.org/download/linux/ubuntu/) for more.

## On Windows

Install PostgreSQL on Windows with the following steps:

1. Download the PostgreSQL 14 installer for Windows from
   [here](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
2. Run the installer as administrator and follow the steps;
3. Add the directory containing the PostgreSQL executable file "psql.exe" to the Path environment variable. In my case,
   the directory to add to the Path is `C:\Program Files\PostgreSQL\14\bin`, but it could be different in your machine.
   Bear in mind that the directory should contain a file with name "psql.exe". To add the directory to the Path, click
   on Start > Settings > System > About > Advanced system settings > Advanced tab > Environment Variables. Then, select 
   the "Path" under "System variable" and click on Edit. In the new window, click on New, paste the directory of the
   PostgreSQL executable file and press "Enter". Finally, click OK in the last three opened windows "Edit environment
   variable", "Environment Variables" and "System Properties";
4. Verify the PostgreSQL installation by opening a new CMD terminal and running `psql --version` from the new terminal.
   The command should print the PostgreSQL version installed into your machine.

More info in [here](https://medium.com/@itayperry91/get-started-with-postgresql-on-windows-a-juniors-life-4adfa6dd10e) 

### On Mac
TODO
