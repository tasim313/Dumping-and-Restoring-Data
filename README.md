# Dumping-and-Restoring-Data
Dumping and restoring data in PostgreSQL using pg_dump and viewing the restored data in pgAdmin

## 1. Dump PostgreSQL Data

- **Using Command Line**
- 1. Open a terminal or command prompt.
  2. Use the pg_dump command to create a dump file:
     ````bash
         pg_dump -U <username> -h <host> -p <port> -d <database_name> -F c -b -v -f <output_file>.dump
     ````
     - **Replace <username> with your PostgreSQL username.**
     - **Replace <host> and <port> with the host (e.g., localhost) and port (e.g., 5432).**
     - **Replace <database_name> with the name of the database you want to dump.**
     - **-F c specifies the custom format for the dump.**
     - **Replace <output_file>.dump with the desired file name for the dump file.**

## Example:
````bash
  pg_dump -U postgres -h localhost -p 5432 -d mydatabase -F c -b -v -f mydatabase.dump
````

## 2. Restore PostgreSQL Data

Using Command Line
- **Open the terminal or command prompt.**
- **Use the pg_restore command to restore the dump file**

````bash
  pg_restore -U <username> -h <host> -p <port> -d <new_database_name> -v <dump_file>.dump
````

- **Replace <new_database_name> with the name of the database you want to restore into. Make sure the database exists beforehand.**

### Creating a New Database

If the target database does not exist, create it first:
````bash
   psql -U <username> -h <host> -p <port> -c "CREATE DATABASE <new_database_name>;"
````
## Example:
````bash
   pg_restore -U postgres -h localhost -p 5432 -d restored_database -v mydatabase.dump
````

## 3. View Data in pgAdmin
- 1. Open pgAdmin and connect to your PostgreSQL server.
- 2. Navigate to the "Databases" section in the browser pane on the left.
- 3. Locate the restored database (e.g., restored_database) and expand its tree.
- 4. Browse the tables to verify the restored data:
     - **Right-click a table.**
     - **Select View/Edit Data > All Rows to see the data.**

Important Notes
  - Dump Options:
   - Use -F c for custom format (recommended for pg_restore).
   - Use -F t for tar format or -F p for plain SQL script if needed.
  - Role and Ownership:
     - Ensure the user restoring the data has sufficient privileges.
     - If ownership issues occur, adjust permissions:
   ````bash
       ALTER DATABASE <database_name> OWNER TO <new_owner>;
   ````
  - Troubleshooting:
    - **If you encounter errors, add the --clean option to pg_restore to drop existing objects before restoring:**
    ````bash
        pg_restore --clean -U postgres -h localhost -p 5432 -d restored_database -v mydatabase.dump
    ````

With these steps, can successfully dump and restore PostgreSQL data and verify it in pgAdmin.
