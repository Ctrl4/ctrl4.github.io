---
layout: post
title: How to replicate from RDS to local or EC2
tags: ctrl4 mysql rds
---

As being RDS a managed service, and also having a managed solution for replication (the very same RDS), it is not as straight forward to **replicate** from RDS to a local MySQL instance.
In this blog post you will find the steps needed to acomplish this.

We will assume you already've got the RDS instance and the local mysql instance you want to use as an slave.

## Prepare RDS instance
Go to RDS console. In the left menu, select "Parameter Groups". Create parameter group or modify your own.
The option that you need to care about is *binlog_format*, set it to MIXED.
If you created the parameter group you need to modify the instance and apply it. After that the instance must to be rebooted to apply changes. 

---
## Generate a dump file from the databases
After rebooting the instance you need to execute a store procedure that aws gave us to work with replication.
```mysql
CALL mysql.rds_set_configuration('binlog retention hours', 144);
```
And create a replication user
```mysql
GRANT REPLICATION CLIENT, REPLICATION SLAVE ON *.* TO 'repuser'@'%' IDENTIFIED BY 'XXXX';
```

* Take a snapshot and restore this snapshot in a temporal rds instance.
* If everything went fine you can go to "Alarms and Recent Events" in the RDS Console and check for a line like the following:
```
Binlog position from crash recovery is mysql-bin-changelog.000003 99358949
```
* After the restore is complete you can generate a dump from this instance so you'll avoid more down time in the main instance
```
mysqldump --databases database --host=host.com --single-transaction --order-by-primary -r database.sql -u <user> -p
```

This instance can be deleted after dump is complete

---
## Restore dump 
Create the database on the slave server and restore the dump in it.

Then
```mysql
CHANGE MASTER TO 
  MASTER_HOST = 'master-host.com'
  ,MASTER_PORT = 3306
  ,MASTER_USER = 'repuser' 
  ,MASTER_PASSWORD = 'XXX'
  ,MASTER_LOG_FILE = 'mysql-bin-changelog.000003'
  ,MASTER_LOG_POS = 99358949
FOR CHANNEL 'channel_xxx';
START SLAVE FOR CHANNEL 'channel_xxx'
```

Now your local instance is replicating from RDS.
 
 
