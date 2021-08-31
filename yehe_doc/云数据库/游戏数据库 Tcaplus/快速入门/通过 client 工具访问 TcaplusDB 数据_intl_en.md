This document describes how to use the client tool `tcaplus_client` to access TcaplusDB data.
All data operation statements must carry the `WHERE` clause, which should contain at least a primary key field. If there are multiple primary keys, separate them with `and`.

## Client Tool
`tcaplus_client` is a client tool used to access TcaplusDB tables and can be obtained at the download address in the table below.

The release package of TcaplusServiceAPI for Linux x86_64 contains the `tcaplus_client` tool for Linux 64-bit.

| Version | OS | Download Package Name |
| ------------- | -------- | ------------------------------------------------------------ |
| 3.36.0.192960 | Linux    | [TcaplusPbApi3.36.0.192960.x86_64](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz) |

>?The relevant operations need to be performed on the CVM instance in the same VPC and subnet under your Tencent Cloud account as your TcaplusDB instance.

### Installing client
After downloading the TcaplusServiceAPI installation package, you can [use the upload tool](https://intl.cloud.tencent.com/document/product/213/34821) to upload it onto the CVM instance in the same VPC and subnet as the TcaplusDB cluster.

1. After the upload, run the following command to decompress the installation package:
```
tar -xf TcaplusServiceApi3.32.0.191008.x86_64_release_20190409.tar.gz -C tcaplus
```
2. After the decompression, enter the `bin` directory in `tcaplus` and grant the tool executable permission:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. Run the `./tcaplus_client` command, and the system will prompt you to enter the parameter information required for database connection. You can enter it based on your cluster information.
>!In the sample below, `app_id` indicates the cluster access ID, `App` indicates the cluster, and `zone` indicates the table group.


```
# ./tcaplus_client
--------------------------------------------------------------------------------
 invalid parameters, please start the client as following:
    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]
    the params in [] are optional, and theire order is not important.
    -a(--ap_id)    App ID
    -z(--zone_id)    ZONE ID
	-s(--signature)    PASSWORD
    -d(--dir)    dir server addr
    -t(--table)    table to add
    -l(--log)    log file name that must be client_log.xml, and log class name be client
    -T(--tdr)    tdr filename 
    -e(--execute)    content following should be with qoutes.
    e.g. ./tcaplus_client -a 2 -z 3 -s "test@Password1" -d 172.xx.xx.181:9999 -T table_test.tdr 
--------------------------------------------------------------------------------
```

### Connecting to TcaplusDB
Run the corresponding command to connect to TcaplusDB. The access point information in the sample below is as follows, and the table `tb_online` has been created in the table group whose ID is 1:
- Cluster access ID: 2
- Connection password: test@Password1
- Private address:private port: 10.125.32.21:9999
- Table group ID: 1

```
./tcaplus_client -a 2 -z 1 -s "test@Password1" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  build at Wed Jan 18 22:08:38 CST 2017              |
|                                                                              |
|    Welcome!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

Enter `help` after the prompt, and the help information will be displayed. You can run `> help specific command` to view the detailed usage of the specific command.
```
tcaplus>help
--------------------------------------------------------------------------------
    show                 get server status related information. executing help show for details.
    dir                  add dir server url. if no dir_server_url added ,
                         commands will fail when executing.
    desc                 output current table struction description
    count                output table row count
    select               query data
    update               update record. if record does not exist then add it or update it if exists.
    insert               insert a new record (not implemented)
    delete               delete record(s)
    bson                 execute bson query
    dump                 dump records from tcaplus to file with csv format
    load                 load records from csv file and import the records to tcplus
    clean                clean table
    quit                 exit the client
    help                 follow a command to get details.
                         e.g. help show, help dir etc.
    note: tdr mode means starting client with -T, and none tdr mode starting client without -T
--------------------------------------------------------------------------------
```


## Statement Execution Method
<br>The execution methods and features of the statements above are as shown below.

#### Performing desc operation
This command is used to view the table definition information. For a nested field, you can only see that its attribute is nested type, but you cannot view the nested structure definition.
Syntax: `desc table name;`
```
tcaplus>desc game_players;
TableName:game_players
TableType:PROTOBUF
-------------------------------------------------------------------------
| Field                         Type                          Key       |
-------------------------------------------------------------------------
| player_id                     int64                         key       |
| player_email                  string                        key       |
| player_name                   string                                  |
| game_server_id                int32                                   |
| login_timestamp               string                                  |
| logout_timestamp              string                                  |
| is_online                     int8                                    |
| pay                           message                                 |
-------------------------------------------------------------------------
```

#### Performing count operation
This command is used to view the total number of table records.
Syntax: `count table name;`
```
tcaplus>count t1;
-------------------------------------------
| TableName                     COUNT(*)  |
-------------------------------------------
| t1                            15        |
-------------------------------------------
```

#### Exporting data
You can run the `dump` command to export all records of a specified table into a .json file.
Syntax: `dump * from table name into filename;`
```
tcaplus>dump * from player into player.txt;
--------------------------------------------------------------------------------
      dump from table("player") success. total record number is 4
--------------------------------------------------------------------------------
```

#### Importing data
You can run the `load` command to import the records of a specified table from a .csv file. Files exported with the `dump` command cannot be imported directly.
Syntax: `load table name from file;`
```
tcaplus>load hehe from test1;
--------------------------------------------------------------------------------
      1 records loaded successfully.
--------------------------------------------------------------------------------
```

#### Clearing table data
For the sake of security, the client tool currently does not allow you to directly clear table data. If you want to clear the data of the entire table, please use the [table clearing](https://console.cloud.tencent.com/tcaplusdb/table) feature in the console.


### Inserting data
Currently, the `INSERT` statement cannot be used; instead, you can run the `UPDATE` statement to insert a record.

### Modifying data
You can run the `UPDATE` statement to write a record. If there are no records matching the primary key field value in the `WHERE` clause, the record will be added as a new one.
Syntax: `update table set field=value[,field 2=value 2…] where primary key field=value [and primary key field 2=value 2…];`
```
tcaplus>update tb_online set gamesvrid=4099, logintime=101 where uin=1024 and name="tcaplus_user" and region=10;
--------------------------------------------------------------------------------
        success. 
--------------------------------------------------------------------------------
update time: 5593 us
```

### Reading data
You can run the `SELECT` statement to read specified field data.
Syntax: `select field[,field 2…] from table where primary key field=value [and primary key field 2=value];`
The `recDataVersion` column in the input data indicates the version number of the current record.
```
tcaplus>select gamesvrid, logintime from tb_online where uin=1024 and name="tcaplus_user" and region=10;
+------+--------------+--------+------------------+--------------+-----------+
| uin  | name         | region | recDataVersion   | gamesvrid    | logintime |
+------+--------------+--------+------------------+--------------+-----------+
| 1024 | tcaplus_user | 10     | 2                | 4099         | 101       |
+------+--------------+--------+------------------+--------------+-----------+
totally 1 record(s) responded.
query time 8686 us
```

The syntax `select * from table where primary key field=value` is supported. Below is an example:
```
tcaplus>select * from test where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 7537 us
```

The `\G` and `\P` formatted output modes are supported. `\G` indicates horizontal output by field, while `\P` indicates that data will be output as a table. Fields that are not configured with formatted output will be output in `\P` mode by default.
```
tcaplus>select * from hehe where id=1 and name=1 \G;
----------------------------------------1.row----------------------------------------
id: 1
name: 1
recDataVersion: 1
em: 1
responding record total:1
query time 3285 us
```

You can run the `SELECT` statement to export data into a file.
Syntax: `select * into [outfile] filename from table name where primary key=value [and primary key 2=value];`

```
tcaplus>select * into outfile test2.xml from hehe where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 5399 us
```

### Deleting data
You can run the `DELETE` statement to delete a written record.
Syntax: `delete from table name where primary key=value [and primary key 2=value];`
```
tcaplus>delete from hehe where id=4 and name=4;
--------------------------------------------------------------------------------
        success
--------------------------------------------------------------------------------
delete time 4280 us
```
