# Federated Datasources
Note that you will also need to hand in a documentation for this assignment.  
[Assignment](<https://olat.bbw.ch/auth/RepositoryEntry/635961710/CourseNode/107315659184604/path%3D~~75%2DZusatzAufgaben~~Auftrag%5FFederation/0>)

## Part 1
- connect to dbbw004 and run the scripts from Olat as user db2inst1
- add this command to the `CONFIG_DATABASE.sql` file
```
update db cfg for dbbw004 using LOGSECOND 200;
```

 you may need to add more, depending on the next step.

- run the script `HRACCESS_Create.sql`. It will likely not work due to certain permissions. Add the required permissions to the file `CONFIG_DATABASE.sql`.
- run the script `HRACCESS_LOAD_DATA.sql`. This will take a while.
- run the script `HRACCESS_COUNT_ROWS.sql` This verifies if the Data was loaded
- create a linux user called `m141fed`. Run the following command as root:
```
useradd -p $(openssl passwd -1 m141fed) -s /bin/bash m141fed -d /home/m141fed
```  
Then proceed to grant all the priviliges the user needs and save them in the script `HRACCESS_GRANT_m141fed.sql`

### HRACCESS_GRANT_m141fed.sql
```
GRANT CONNECT ON DATABASE TO USER m141fed;
GRANT USAGE ON WORKLOAD SYSDEFAULTUSERWORKLOAD TO USER m141fed;
GRANT EXECUTE ON PACKAGE NULLID.SQLC2P31 TO USER m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPARTMENTS TO USER m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPT_EMP TO USER m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPT_MANAGER TO USER m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.EMPLOYEES TO USER m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.SALARIES TO USER m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.TITLES TO USER m141fed;
```

## Part 2
- configure federated datasources as documented in the [db2 Knowledge Center](https://www.ibm.com/docs/en/db2/11.5?topic=wrapper-configuring-access-db2-data-sources)  
All the commands should be saved into the script `HRREMOTE_Create.sql`. You should also create a script `HRREMOTE_Drop.sql` where you remove all the data.

For this part you must be connected to DBBW003!

### HRREMOTE_Create.sql
```
CATALOG TCPIP NODE db2_node REMOTE system42 SERVER db2tcp42;
-- this part is not required, but would be if the server was remote: CATALOG DATABASE DBBW004 AT NODE db2_node AUTHENTICATION SERVER; 

-- Wrapper registrieren
CREATE WRAPPER DRDA;

-- Server Definitionen registrieren
CREATE SERVER BBW TYPE DB2/LUW VERSION 11 WRAPPER DRDA AUTHORIZATION "db2inst1" PASSWORD "db2inst1" OPTIONS (DBNAME 'DBBW004') ;

-- User mappings werden nicht benötigt, da sich alle auf dem gleichen Server befinden
-- Verbindung zur Datenbank testen
SET PASSTHRU BBW
SELECT count(*) FROM syscat.systables
SET PASSTHRU RESET;

-- Nicknames aus DBBW004 hinzufügen
CREATE NICKNAME HRREMOTE.DEPARTMENTS FOR BBW.HRACCESS.DEPARTMENTS;
CREATE NICKNAME HRREMOTE.DEPT_MANAGER FOR BBW.HRACCESS.DEPT_MANAGER;
CREATE NICKNAME HRREMOTE.EMPLOYEES FOR BBW.HRACCESS.EMPLOYEES;
CREATE NICKNAME HRREMOTE.DEPT_EMP FOR BBW.HRACCESS.DEPT_EMP;
CREATE NICKNAME HRREMOTE.TITLES FOR BBW.HRACCESS.TITLES;
CREATE NICKNAME HRREMOTE.SALARIES FOR BBW.HRACCESS.SALARIES;
```

### HRREMOTE_Drop.sql
```
-- Nicknames löschen
DROP NICKNAME HRREMOTE.DEPARTMENTS;
DROP NICKNAME HRREMOTE.DEPT_MANAGER;
DROP NICKNAME HRREMOTE.EMPLOYEES;
DROP NICKNAME HRREMOTE.DEPT_EMP;
DROP NICKNAME HRREMOTE.TITLES;
DROP NICKNAME HRREMOTE.SALARIES;

-- Server-Definition löschen
DROP SERVER BBW;

-- Wrapper löschen
DROP WRAPPER DRDA;

-- Datenbankkatalog entfernen
UNCATALOG DATABASE DBBW004;

-- Node entfernen
UNCATALOG NODE db2_node;
```

After running the script `HRREMOTE_Create.sql`, run `HRREMOTE_CHECK_ACCESS.sql`.

### HRACCESS_GRANT_bbwuser.sql
- Create a script named `HRACCESS_GRANT_bbwuser.sql`
- Add the following content to the script and run the script.
```
GRANT CONNECT ON DATABASE TO USER bbwuser;
GRANT USAGE ON WORKLOAD SYSDEFAULTUSERWORKLOAD TO USER bbwuser;
GRANT EXECUTE ON PACKAGE NULLID.SQLC2P31 TO USER bbwuser;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPARTMENTS TO bbwuser;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPT_EMP TO bbwuser;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPT_MANAGER TO bbwuser;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.EMPLOYEES TO bbwuser;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.SALARIES TO bbwuser;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.TITLES TO bbwuser;
```
