# Prüfung 19.06.2023

## Ueb1

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
To run a script as a simple Database user, use this command: 
```
db2 CONNECT TO DBBW002 USER dbuser10 USING dbuser10
```
### 