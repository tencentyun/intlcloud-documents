## Overview

COS offers unlimited storage and can automatically transition objects to ARCHIVE or DEEP ARCHIVE for cost reduction, making it ideal for data backup and archive.

More and more customers are backing up data in the cloud. To facilitate this, Oracle's backup module has integrated with COS so that you can back up and restore databases at a lower cost.

## Connecting OSB to COS

The Oracle Secure Backup (OSB) Cloud Module is part of the OSB product family. It enables you to directly back up Oracle databases to COS. The OSB Cloud Module has integrated with RMAN. Therefore, you can customize an RMAN script to directly back up Oracle databases to COS efficiently.

Oracle 9i or later versions support the OSB Cloud Module. For more information, please see [Oracle Documentation](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-6FCF4FD8-861C-4D52-BB41-32E6EF03789F).


## Installing OSB

1. Go to [Oracle](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-964AADD2-3405-4476-8698-E9F2133CB5B7) to obtain the latest version of OSB and install it.
2. Decompress the downloaded `osbws_installer.zip` and run the following command with the actual `SecretId`, `SecretKey`, region, and endpoint of COS to install OSB:
>!We recommend you use a sub-account key preferentially and follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to reduce risks. For information about how to obtain a sub-account key, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).
>
```
java -jar osbws_install.jar -AWSID <SecretId> -AWSKey <SecretKey> -walletDir $ORACLE_HOME/osbws_wallet -libDir $ORACLE_HOME/lib -location <Region> -awsEndPoint <endpoint>

// Replace the location with the actual directory of the package.
```
For example:
```
java -jar osbws_install.jar -AWSID AKIDxxxx -AWSKey XXXX -walletDir $ORACLE_HOME/osbws_wallet -libDir $ORACLE_HOME/lib -location ap-guangzhou -awsEndPoint cos.ap-guangzhou.myqcloud.com
```
>? Oracle 12 and later versions have the OSB cloud module by default. If the installation does not work, you can download the latest OSB module and install it by yourself or use a proxy.
>


## Backing Up Databases to COS Using RMAN

1. Log in to the database and run the following command to connect to RMAN:
```
rman target / 
```
2. Back up the databases to a COS bucket using the commands below, where `lib/libcos.so` and `cosorcl.ora` are about the database names and should be modified as needed.
```
	run {
	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	backup channel=ch1 database format='ora_%d_%I_%T_%s_%t_%c_%p.dbf' plus archivelog;
	backup channel=ch1  current controlfile  format='%d_%I_%T_%s_%t_%c_%p.conf';
	backup channel=ch1 spfile format='ora_%d_%I_%T_%s_%t_%c_%p.spf' ;
	release channel ch1;
	}
```

## Restoring a Database from COS Using RMAN

1. Shut down the database and make its status “unmount”.
 - Shut down the database:
```
shutdown immediate;
```
 - Make the database status “unmount”:
```
startup nomount;
```
2. Run the RMAN command `list backup` to list all backups and select the desired one, whose handle and tag should be recorded.
3. Run the following `restore` command to connect to the backup.
Connect to the backup whose handle is `ORACLE_1880733115_20190507_5_1007656283_1_1.conf`, which is obtained from `list backup`. `lib/libcos.so` and `cosorcl.ora` are about the database names. They should be modified as needed and be the same as those used in the backup process.
```
	run {
	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	restore controlfile from 'ORACLE_1880733115_20190507_5_1007656283_1_1.conf';
	release channel ch1;
	}
```
4. Run the `restore` command below and change the database status to `mount` with `alter database mount`:
```
	run {

	allocate channel ch1 type
	sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so,
	SBT_PARMS=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	restore database from tag='TAG20190507T163102';
	recover database from tag='TAG20190507T163102';
	release channel ch1;
	}
```
 - The tag value **TAG20190507T163102** is a backup’s ID number, which is obtained using `list backup`. Ensure that the value is the same as that obtained from the control file of the database to restore, that is, the handle of the backup should be **ORACLE_1880733115_20190507_5_1007656283_1_1.conf**.
 - `lib/libcos.so` and `cosorcl.ora` are about the database names and should be modified as needed.
5. Open the database to view the data restored from COS.


## Modifying RMAN Concurrence

>? By default, RMAN does not have concurrence. To use concurrence, you need to set it manually.
>

Log in to RMAN and modify the concurrence configuration. The following sets the number of concurrences to 15:
```
	run {
	configure channel device type sbt parms='SBT_LIBRARY=/u01/app/oracle/product/11.2.0/dbhome_1/lib/libcos.so ENV=(OSB_WS_PFILE=/u01/app/oracle/product/11.2.0/dbhome_1/dbs/cosorcl.ora)';
	configure default device type to SBT;
	configure device type SBT parallelism 15;
	}
```

## References

For more information, see [E.1 About Backup on the Cloud Using Oracle Secure Backup Cloud Module](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rcmrf/oracle-secure-backup-osb-cloud-module.html#GUID-6FCF4FD8-861C-4D52-BB41-32E6EF03789F).


