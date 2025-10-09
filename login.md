
# Log in to the 5GIR data warehouse Database

To export data from the data warehouse (DW), you need to log in to the 5GIR DW database with either Bash code on Linux
(and Mac? not tested), CMD code on Windows, or Python code on any operating system.

## Bash on Linux (and Mac? Not tested!)

1. Open the bash terminal on Linux and MACs.

2. Define the database name, host name, server port and username with the code below by replacing database_name,
   host_domain, host_port and user_name with the database name, host name, server port and username, respectively.
   ```bash
   dbname=database_name
   host=host_domain
   port=host_port
   username=user_name
   ```

3. Run the following code in the same bash shell where you ran the previous code above.
   ```bash
   psql --dbname="$dbname" --host="$host" --port="$port" --username="$username" --password
   ```

4. Lastly, type the password of your user and press enter.

## CMD on Windows

1. Open the Command Prompt on Windows.

2. If the Postgres directory containing the file `psql.exe` has been added to the Path environment variable, then you
   can skip this step and move to step 3. Otherwise, you need to locate the directory and add it to `PATH` every time
   you open a new Git bash window before running the command `psql`. An example of a Postgres directory is
   `C:\Program Files\PostgreSQL\14\bin` which must contain the file "psql.exe". If this is the case for you, you can add
   it to `PATH` with:
   ```CMD
   set "PATH=%PATH%;C:\Program Files\PostgreSQL\14\bin;"
   ```
   If the directory is different in your case, adjust the directory accordingly.

3. Define the database name, host name, server port and username with the code below by replacing database_name,
   host_domain, host_port and user_name with the database name, host name, server port and username, respectively.

   ```CMD
   set "dbname=database_name"
   set "host=host_domain"
   set "port=host_port"
   set "username=user_name"
   ```

4. Run the following code in the same command prompt window where you ran the previous code above.
   ```CMD
   psql --dbname=%dbname% --host=%host% --port=%port% --username=%username% --password
   ```

5. Lastly, type the password of your user and press enter.

## Python

1. If you haven't, create a JSON file with name `credentials.json`. (If you do not know what a JSON file is and how to
   create it, it is a text file. So, create a text file with name `credentials.json`.) Add to the new file with the
   following content, and replace <username>, <password>, <postgresql_server_domain> and <postgresql_server_port> with
   your username, your password, the database server domain and port, respectively.
   ```json
   {
       "user": <username>,
       "pass": <password>,
       "IP": <postgresql_server_domain>,
       "port": <postgresql_server_port>
   }
   ```
2. Create a python script `main.py`. (If you don't know how, just create a text file and name it `main.py`). Next, add
   the following Python code in the new file and replace <database> with the database name (leaving the single
   quotations on).
   ```python
   from data_warehouse_client import data_warehouse
   
   
   dw = data_warehouse.DataWarehouse('credentials.json', '<database>')
   ```
3. Make sure you have the conda environment activated. If it isn't, activate it by running the below on either a Bash
   terminal or CMD window:
   ```
   conda activate fgir
   ```
4. Run the Python script with:
   ```
   python main.py
   ```
   If you have successfully connected to the database, you should see a message saying:  
   ```text
   Init successful! Running queries.
   ```



