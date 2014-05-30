flashback-tips
==============

Here is a list of useful commands when you come to work with Oracle flasback.

SQL commands
------------

* Is Flashback on ?

```SQL
SQL> select flashback_on from v$database;
```

* Show size of FB area + which disk it is

```SQL
SQL> show parameter db_recovery
```

* Show space occupied by logs

```SQL
SQL> select * from v$flash_recovery_area_usage;
```

* Show space occupied VS space allocated

```SQL
SQL> select space_used/(1024*1024*1024),space_limit/(1024*1024*1024) from v$recovery_file_dest;
```

* Change size of flashback area

```SQL
SQL> alter system set db_recovery_file_dest_size=46G;
```

* Show flashback retention policy

```SQL
SQL> show parameter db_flashback_retention_target
```

* set it for 2 days

```SQL
SQL> alter system set db_flashback_retention_target = 2880; 
```

* Check restore points

```SQL
SQL> select NAME,SCN,GUARANTEE_FLASHBACK_DATABASE,DATABASE_INCARNATION#, time from v$restore_point ;
```

* Delete a restore point

```SQL
SQL> DROP RESTORE POINT RP_DATE;
```

* Set flashback on

```SQL
alter database flashback on;
```

RMAN commands
-------------

* How to delete all logs with RMAN

```SQL
rman> crosscheck archivelog all;
rman> delete noprompt expired archivelog all;
```

* Set up retention policy 

```SQL
rman> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS;
```

Misc
----

Oracle Alert file: alert_MYDBNAME.log
