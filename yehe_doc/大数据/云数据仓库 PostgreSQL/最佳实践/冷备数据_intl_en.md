This document describes how to back up data regularly.

## Background
Although CDWPG has a master-standby data storage architecture, some scenarios require cold backup for all important data, such as when data is abnormally deleted. As automatic cold backup is not supported by CDWPG at the moment, manual operation is required. In CDWPG, COS is used as the storage medium for data backup. For related operations on COS data, see [Importing and Exporting COS Data at High Speed with External Table](https://intl.cloud.tencent.com/document/product/1138/45032).

## Impact
Note that backing up data as instructed in this document may have the following impact on the cluster:
1. Script execution will increase the cluster load, especially the overheads at the network layer. Therefore, we recommend you evaluate the backup time and perform it during off-peak hours of your business.
2. A COS extension will be created in each database during script execution.
3. A COS external table will be created for each table that needs to be backed up during script execution and deleted after the backup is completed.

## Issues
Note that you may encounter the following issues when backing up data as instructed in this document:

| Error Message | Solution |
|---------|---------|
| `ERROR:  permission denied for external protocol cos` | `GRANT ALL ON PROTOCOL cos TO {backup_user}` |
|`ERROR:  permission denied for schema {schame_name}` | `GRANT ALL ON SCHEMA {schame_name} to {backup_user}` |
|`ERROR:  permission denied for relation {table_name}` |`GRANT SELECT ON {table_name} to {backup_user}` |

## Directions
You can use the following `shell` script to back up all data in the CDWPG cluster and scale the cluster as needed to complete regular cold backups with crontab. You can also download and use [backup_cdw_v101.sh](https://packagedown-online-1256722404.cos.ap-guangzhou.myqcloud.com/tool/backup_cdw_v101.sh).
>!
>- Deleting a writable external table will not delete the corresponding data in COS.
>- We recommend you back up data during off-peak hours of your system, as the backup process may increase the system load.
>- The backup duration depends on the data volume and cluster specification. Simply put, the more the cluster nodes, the faster the backup.

```
#!/bin/bash

set -e

# CDWPG connection parameters that need to be entered
PWD='' # Required
HOST='' # Required
USER='' # Required
DEFAULT_DB='postgres'

# Backup parameters that need to be entered
SECRET_ID='' # Required
SECRET_KEY='' # Required
COS_URL='' # Required, such as `test-1301111111.cos.ap-guangzhou.myqcloud.com`
COMPRESS_TYPE='gzip' # Whether the files in COS are in compressed format. Valid values, gzip, none

echo -e "\n`date "+%Y%m%d %H:%M:%S"` backup task start\n"

# Step 1. Get the list of databases
db_list=`PGPASSWORD=${PWD} psql -t -h ${HOST} -p 5436 -d ${DEFAULT_DB} -U ${USER} -c "select datname from pg_database"`

# Step 2. Traverse the databases that need to be backed up
for db in $db_list
do
	# `template0`, `template1`, and `gpperfmon` are templates and system database and do not need to be backed up
        if [ "$db" = "template0" -o $db = "template1" -o $db = "gpperfmon" ];then
                continue
        fi

        echo -e "\n************************************************"
        echo -e "backup database:{$db} start"
        db_start=`date +%s`

	# Step 3. Get the current date
	# Use the date as part of the COS path to distinguish between data backed up on different dates
	cur_date=`date +%Y%m%d`	

	# Step 4. Get the list of tables that need to be backed up
	# External, virtual, temporary, and replicated tables (not supported currently) are excluded. For partitioned tables, only child tables are backed up 
	table_list=`PGPASSWORD=${PWD} psql -t -h ${HOST} -p 5436 -d ${db} -U ${USER} -c "SELECT t.schemaname||'.'||t.tablename FROM pg_class c join (SELECT a.schemaname,a.tablename,b.oid FROM pg_tables a join pg_namespace b on a.schemaname = b.nspname WHERE a.tableowner != 'gpadmincloud') as t on c.relnamespace = t.oid and c.relname = t.tablename join gp_distribution_policy d on c.oid = d.localoid WHERE c.relstorage not in('v','x') and c.relpersistence != 't' and c.relhassubclass != 't' and d.policytype != 'r'"`

	# Step 5. Create a COS extension
	PGPASSWORD=${PWD} psql -h ${HOST}  -p 5436 -d ${db} -U ${USER} -c "CREATE EXTENSION IF NOT EXISTS cos_ext SCHEMA public"

	# Step 6. Traverse the list and perform backups in sequence
	for table in $table_list
	do
		sleep 1
		table_start=`date +%s`
		echo -e "backup ${table} start"
	        # Here, a name suffix must be added in the format of `{schema}.{table}`
    		backup_table="${table}_cdw_backup_cos"

		# Step 7. Create COS backup tables
		PGPASSWORD=${PWD} psql -h ${HOST}  -p 5436 -d ${db} -U ${USER} -c "CREATE WRITABLE EXTERNAL TABLE ${backup_table} (like ${table}) LOCATION('cos://${COS_URL}/backup/${cur_date}/${db}/${table}/ secretKey=${SECRET_KEY} secretId=${SECRET_ID} compressType=${COMPRESS_TYPE}') FORMAT 'csv'"


		# Step 8. Import the data of original tables to backup tables
		PGPASSWORD=${PWD} psql -h ${HOST}  -p 5436 -d ${db} -U ${USER} -c "INSERT INTO ${backup_table} SELECT * FROM ${table}"

		# Step 9. Delete the backup external tables
		# Note: Deleting an external table will not delete the corresponding data in COS
		PGPASSWORD=${PWD} psql -h ${HOST}  -p 5436 -d ${db} -U ${USER} -c "DROP EXTERNAL TABLE ${backup_table}"

		table_end=`date +%s`
		echo -e "backup ${table} done, cost $[table_end - table_start]s\n"
	done

        db_end=`date +%s`
        echo -e "backup database:{$db} done, cost $[db_end - db_start]s"
        echo -e "************************************************\n"
done
```
