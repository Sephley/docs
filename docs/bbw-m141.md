# M141 - Admin / Betrieb DBM

### Backup database
Offline

```db2 backup database DBBW001 to /bbw/DBbackup```

Online

```db2 backup database DBBW001 online to /bbw/DBbackup```

### Restore database
The location specified after 'FROM' must be a directory, not a file.

Make sure to select the timestamp that is equivalent to the one of your desired backup.

```db2 "RESTORE DB DBBW001 FROM /bbw/DBbackup/ TAKEN AT 20230417084512"```

### Update db cfg
```db2 update db cfg for dbbw001 using NEWLOGPATH '/bbw/activelog1'

db2 update db cfg for dbbw001 using MIRRORLOGPATH '/bbw/activelog2'

db2 update db cfg for dbbw001 using LOGARCHMETH1 DISK:/bbw/archlog1

db2 update db cfg for dbbw001 using LOGARCHMETH2 DISK:/bbw/archlog2

db2 update db cfg for dbbw001 using LOG RETAIN RECOVERY

db2 update db cfg for dbbw001 using AUTO_DEL_REC_OBJ ON```