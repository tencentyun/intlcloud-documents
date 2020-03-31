
mysqldump is easy to use for data import but needs long downtime, so it is only suitable for small amounts of data or situations that allow relatively long downtime.

1. Use mysqldump to export data from the local database to a data file.
>Do not update data during the export. This step only exports data excluding stored procedures, triggers, and functions.
>
```
mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName --skip-triggers > /tmp/dbName.sql
```
Parameter description:
 - localIp: IP address of the local database server.
 - userName: migration account of the local database.
 - dbName: name of the database that needs to be migrated.
 - /tmp/dbName.sql: name of the generated backup file.
2. Use mysqldump to export stored procedures, triggers, and functions.
>If the database does not use stored procedures, triggers, or functions, you can skip this step. During the export, you need to remove the definer in order to make the data compatible with TencentDB.
>
```
mysqldump -h localIp -u userName -p --opt --default-character-set=utf8 --hex-blob dbName -R | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' > /tmp/triggerProcedure.sql
```
Parameter description:
 - localIp: IP address of the local database server.
 - userName: migration account of the local database.
 - dbName: name of the database that needs to be migrated.
 - /tmp/triggerProcedure.sql: name of the generated backup file.
3. Upload the data file and stored procedure file to a CVM instance. Please make sure that the CVM and TencentDB instances can be properly connected and there is sufficient available storage capacity in the CVM instance.
4. Log in to CVM and import the data file and stored procedure files to the target TencentDB instance. Please make sure that you have the database account with corresponding permissions; otherwise, you need to generate an account in the console.
```
mysql -h xxx.xxx.xxx.xxx:xxxx –u userName -p dbName < /tmp/dbName.sql
mysql -h xxx.xxx.xxx.xxx:xxxx -u userName -p dbName < /tmp/triggerProcedure.sql
```
Parameter description:
 - xxx.xxx.xxx.xxx:xxxx: instance connection address. In this document, a private network address is used as an example.
 - userName: migration account of the TencentDB instance.
 - dbName: name of the database that needs to be imported to.
 - /tmp/dbName.sql: name of the data file that needs to be imported.
 - /tmp/triggerProcedure.sql: name of the stored procedure file that needs to be imported.
