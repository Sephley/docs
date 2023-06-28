# This assignment is about federated datasources
Note that you will also need to hand in a documentation for this assignment.

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
