flashback-tips
==============

Flashback useful commands:

* Is Flashback on ?

SQL> select flashback_on from v$database;

* Show size of FB area + which disk it is

SQL> show parameter db_recovery

* show space occupied by logs

SQL> select * from v$flash_recovery_area_usage;

* show space occupied VS space allocated

SQL> select space_used/(1024*1024*1024),space_limit/(1024*1024*1024) from v$recovery_file_dest;

* Change size of flashback area

SQL> alter system set db_recovery_file_dest_size=46G;

* Show flashback retention policy

SQL> show parameter db_flashback_retention_target

* set it for 2 days

SQL> alter system set db_flashback_retention_target = 2880; 

* Check restore points

SQL> select NAME,SCN,GUARANTEE_FLASHBACK_DATABASE,DATABASE_INCARNATION#, time from v$restore_point ;

* Delete a restore point

SQL> DROP RESTORE POINT RP_DATE;

* set flashback on

alter database flashback on;

---

* How to delete all logs with RMAN

rman> crosscheck archivelog all;

rman> delete noprompt expired archivelog all;

* Set up retention policy 

rman> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS;

---

Oracle Alert file: alert_MYDBNAME.log
