
# Install PostgreSQL

## On Ubuntu

Install PostgreSQL on Ubuntu with:
```bash
sudo apt -y install postgresql-14
```
Visit [here](https://www.postgresql.org/download/linux/ubuntu) for more.

## On Windows

Install PostgreSQL on Windows with the following steps:

1. Download the PostgreSQL 14 installer. Click on
   [here](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads) to open the website. There is a table of
   all possible installers. The different PostgreSQL versions are in different rows and the different operating
   systems are in different columns. Click on the download icon in the column "Windows x86-64" where the "PostgreSQL
   Version" is "14.N" (N can be any number);
2. Run the installer as administrator. In the first installer page "Setup - PostgreSQL", click on "Next". In page
   "Installation Directory", leave the default value `C:\Program Files\PostgreSQL\14` for field "Installation Directory"
   and click on "Next". In page "Select Components", uncheck "PostgreSQL Server", "pgAdmin 4", "Stack Builder", check
   "Command Line Tools", and click on "Next". In both next pages "Pre Installation Summary" and "Ready to Install"",
   click on "Next". Wait for the installation to be completed. Finally, click on "Finish";
3. Once the installation is completed, add the directory containing the PostgreSQL executable file `psql.exe` to the
   Path environment variable. In my case, the directory to add to the Path is `C:\Program Files\PostgreSQL\14\bin`, but
   it could be different in your machine. Bear in mind that the directory should contain the file with name `psql.exe`.
   To add the directory to the Path, click on "Start" > "Settings" > "System" > "About" > "Advanced system settings" >
   "Advanced tab" > "Environment Variables". Then, select the "Path" under "System variable" and click on "Edit". In the
   new window, click on "New", paste the directory of the PostgreSQL executable file and press "Enter". Finally, click
   "OK" in the last three opened windows "Edit environment variable", "Environment Variables" and "System Properties";
4. Verify the PostgreSQL installation by opening a new CMD terminal and running `psql --version` from the new terminal.
   If the installation were properly installed, the command should print the PostgreSQL version installed into your
   machine.

## On Mac
TODO
