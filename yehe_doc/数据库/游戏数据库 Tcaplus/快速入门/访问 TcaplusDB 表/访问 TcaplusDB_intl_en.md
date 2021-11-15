TcaplusDB data can be accessed and read through multiple means such as client tool, SDK toolkits for various programming languages, and RESTful APIs.

## Accessing TcaplusDB Data Through Client Tool
`tcaplus_client` is a client tool used to access TcaplusDB tables and can be obtained at the download address in the table below.

The release package of TcaplusServiceAPI for Linux x86_64 contains the `tcaplus_client` tool for Linux 64-bit.

| Version | OS | Download Package Name | 
|---------|---------|---------|
| 3.36.0.192960 | Linux |[TcaplusPbApi3.36.0.192960.x86_64](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz) |

>The relevant operations need to be performed on the CVM instance in the same VPC and subnet under your Tencent Cloud account as your TcaplusDB instance.

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
>In the sample below, `app_id` indicates the cluster access ID, `App` indicates the cluster, and `zone` indicates the table group.
>

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


The execution methods and features of the statements above are as shown below.

#### Performing desc operation
This command is used to view the table definition information. For a nested field, you can only see that its attribute is nested type, but you cannot view the nested structure definition.
The syntax is `desc table name;`
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
This command is used to view the total number of table records. The syntax is `count table name;`.
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
The syntax is `dump * from table name into filename;`
```
tcaplus>dump * from player into player.txt;
--------------------------------------------------------------------------------
      dump from table("player") success. total record number is 4
--------------------------------------------------------------------------------
```

#### Importing data
You can run the `load` command to import the records of a specified table from a .csv file. Files exported with the `dump` command cannot be imported directly.
The syntax is `load table name from file;`
```
tcaplus>load hehe from test1;
--------------------------------------------------------------------------------
      1 records loaded successfully.
--------------------------------------------------------------------------------
```

#### Clearing table data
For the sake of security, the client tool currently does not allow you to directly clear table data. If you want to clear the data of the entire table, please use the [table clearing](https://console.cloud.tencent.com/tcaplusdb/table) feature in the console.


## Accessing TcaplusDB Data Through SDK for C++ API
You can use the SDK for [C++](https://intl.cloud.tencent.com/document/product/1016/30289) tool to access TcaplusDB data.

## Accessing TcaplusDB Data Through RESTful API
For more information, please see [RESTful API Description](https://intl.cloud.tencent.com/document/product/1016/30290).
