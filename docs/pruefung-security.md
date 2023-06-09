# Prüfung 19.06.2023

## Ueb1

### Linuxusererstellen.sh
Linux user add script for preparation.  

```
cat  /etc/group

# Erstellen der Gruppen
groupadd dbusrgrp 
groupadd dbadmgrp
groupadd dbuser10
groupadd dbuser11
groupadd dbuser12


# Anzeige welche User existieren:
cat /etc/passwd

# Erstellen der User (UserID und PW sind identisch)
useradd -p $(openssl passwd -1 dbuser10) -g dbuser10  -G dbuser10           -s /bin/bash -c "Test user dbuser10"  -d /home/dbuser10   dbuser10
useradd -p $(openssl passwd -1 dbuser11) -g dbuser11  -G dbuser11,dbusrgrp  -s /bin/bash -c "Test user dbuser11"  -d /home/dbuser11   dbuser11
useradd -p $(openssl passwd -1 dbuser12) -g dbuser12  -G dbuser12,dbadmgrp  -s /bin/bash -c "Test user dbuser12"  -d /home/dbuser12   dbuser12
```

### Ueb1_GRANT_User.sql
```
GRANT DATAACCESS ON DBBW001 TO GROUP dbusrgrp;
GRANT DATAACCESS ON DBBW002 TO GROUP dbusrgrp;

GRANT DBADM ON DATABASE DBBW001 TO GROUP dbadmgrp WITHOUT DATAACCESS;
GRANT DBADM ON DATABASE DBBW002 TO GROUP dbadmgrp WITHOUT DATAACCESS;
```
## Ueb2
The objective of this assignment was to make the pre-written scripts function.  
You may have to run `db2 CONNECT TO <database-name>` after you have run the pre-written scripts, as they have a connection reset command in them.
### Ueb2_GRANT_User.sql
```
--
-- Autorisierungen für User dbuser10
--

GRANT CONNECT ON DATABASE TO USER dbuser10;
GRANT USAGE ON WORKLOAD SYSDEFAULTUSERWORKLOAD TO USER dbuser10;
GRANT EXECUTE ON PACKAGE NULLID.SQLC2P31 TO USER dbuser10;
GRANT SELECT ON TABLE BIBLIO.TARTIKEL TO USER dbuser10;

--
-- Autorisierungen für User dbuser11
--

GRANT CONNECT ON DATABASE TO USER dbuser11;
GRANT USAGE ON WORKLOAD SYSDEFAULTUSERWORKLOAD TO USER dbuser11;
GRANT SELECT ON TABLE BIBLIO.TARTIKEL TO USER dbuser11;

--
-- Autorisierungen für User dbuser12
--

GRANT EXECUTE ON PACKAGE NULLID.SQLC2P31 TO USER dbuser12;
GRANT SELECT ON TABLE BIBLIO.TARTIKEL TO USER dbuser12;
```
## Ueb3
The premise of this assignment is the same as Ueb2.  
To connect to a Database as a simple Database user, use this command: 
```
db2 CONNECT TO DBBW002 USER dbuser10 USING dbuser10
```
### Ueb3_GRANT_User.sql
```
--
-- Speichern Sie in diesem SQL Script die notwendigen GRANT Statements
--

--
-- Autorisierungen für User dbuser10
--

GRANT CREATETAB ON DATABASE TO USER dbuser10;
GRANT IMPLICIT_SCHEMA ON DATABASE TO USER dbuser10;
GRANT USE OF TABLESPACE USERSPACE1 TO USER dbuser10;

--
-- Autorisierungen für User dbuser11
--

GRANT CREATETAB ON DATABASE TO USER dbuser11;
GRANT IMPLICIT_SCHEMA ON DATABASE TO USER dbuser11;
GRANT USE OF TABLESPACE USERSPACE1 TO USER dbuser11;

--
-- Autorisierungen für User dbuser12
--

GRANT CREATETAB ON DATABASE TO USER dbuser12;
``` 

## Ueb4
In this assignment, you must create a database role that has certain permissions on certain tables.  
After that, you must create two UNIX users that have the newly created role (in this case: TESTER)
### Ueb4_GRANT_ROLE.sql
```
--
-- Speichern Sie in diesem SQL Script die notwendigen GRANT Statements
--

CREATE ROLE TESTER;

--
-- Autorisierungen für User dbuser10
--

GRANT SELECT, INSERT, UPDATE, DELETE ON DBUSER10.TDBS_PERSON TO TESTER;
GRANT SELECT, INSERT, UPDATE, DELETE ON DBUSER10.TDBS_ABTEILUNG TO TESTER;

--
-- Autorisierungen für User dbuser11
--

GRANT SELECT, INSERT, UPDATE, DELETE ON DBUSER11.TDBS_PERSON TO TESTER;
GRANT SELECT, INSERT, UPDATE, DELETE ON DBUSER11.TDBS_ABTEILUNG TO TESTER;

--
-- Autorisierungen für User dbuser12
--

GRANT SELECT, INSERT, UPDATE, DELETE ON DBUSER12.TDBS_PERSON TO TESTER;
GRANT SELECT, INSERT, UPDATE, DELETE ON DBUSER12.TDBS_ABTEILUNG TO TESTER;

```

Afterwards, you must assign this role to the users (in this case tester01 and tester02).

```
db2 GRANT TESTER TO USER tester01;
db2 GRANT TESTER TO USER tester02;
```

Lastly, I had to enable the Workload for the users.

```
db2 GRANT USAGE ON WORKLOAD SYSDEFAULTUSERWORKLOAD TO ROLE TESTER;
```