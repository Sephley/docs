# This assignment is about federated datasources
Note that you will also need to hand in a documentation for this assignment.  
[Assignment](<https://olat.bbw.ch/auth/RepositoryEntry/635961710/CourseNode/107315659184604/path%3D~~75%2DZusatzAufgaben~~Auftrag%5FFederation/0>)

## Part 1
- connect to dbbw004 and run the scripts Olat as user db2inst1
- add this command to the `CONFIG_DATABASE.sql` file
```
update db cfg for dbbw004 using LOGSECOND 200;
```

you may need to add more, depending on the next step.

- run the script `HRACCESS_Create.sql`. It will likely not work due to certain permissions. Add the required permissions to the file `CONFIG_DATABASE.sql`.
- run the script `HRACCESS_COUNT_ROWS.sql` and verfiy if all the data was loaded by running the script `HRACCESS_COUNT_ROWS.sql`.
- create a linux user called `m141fed`. Use the follwing command:
```
useradd -p $(openssl passwd -1 m141fed) -s /bin/bash m141fed -d /home/m141fed
```  
Then proceed to grant all the priviliges the user needs and save them in the script `HRACCESS_GRANT_m141fed.sql`

### HRACCESS_GRANT_m141fed.sql
```
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPARTMENTS TO m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPT_EMP TO m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.DEPT_MANAGER TO m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.EMPLOYEES TO m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.SALARIES TO m141fed;
GRANT SELECT, INSERT, UPDATE, DELETE ON HRACCESS.TITLES TO m141fed;
```

## Part 2
- configure federated datasources as documented in the [db2 Knowledge Center](https://www.ibm.com/docs/en/db2/11.5?topic=wrapper-configuring-access-db2-data-sources)  
All the commands should be saved into the script `HRREMOTE_Create.sql`. You should also create a script `HHREMOTE_Drop.sql` where you remove all the data.

### HRREMOTE_Create.sql
```
CATALOG TCPIP NODE db2_node REMOTE system42 SERVER db2tcp42;
CATALOG DATABASE DBBW004 AT NODE db2_node AUTHENTICATION SERVER;

// Wrapper registrieren
CREATE WRAPPER DRDA;

// Server Definitionen registrieren
CREATE SERVER server_definition_name 
 TYPE server_type 
 VERSION version_number WRAPPER DRDA
 AUTHORIZATION "db2inst1" PASSWORD "db2inst1" OPTIONS (DBNAME DBBW004);
```

### HRREMOTE_Drop.sql
