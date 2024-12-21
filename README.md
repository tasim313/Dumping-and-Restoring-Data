# Dumping-and-Restoring-Data
Dumping and restoring data in PostgreSQL using pg_dump and viewing the restored data in pgAdmin

## 1. Dump PostgreSQL Data

- **Using Command Line**
- 1. Open a terminal or command prompt.
  2. Use the pg_dump command to create a dump file:
     ````bash
         pg_dump -U <username> -h <host> -p <port> -d <database_name> -F c -b -v -f <output_file>.dump
     ````
     **Replace <username> with your PostgreSQL username.**
     -- Replace <host> and <port> with the host (e.g., localhost) and port (e.g., 5432).
     -- Replace <database_name> with the name of the database you want to dump.
     -- -F c specifies the custom format for the dump.
     -- Replace <output_file>.dump with the desired file name for the dump file.
