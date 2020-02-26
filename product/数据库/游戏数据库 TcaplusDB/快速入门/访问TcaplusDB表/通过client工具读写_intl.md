[//]: # (chinagitpath:XXXXX)

This document describes how to access the TcaplusDB table through the client tool.

Tcaplus_client is a TcaplusDB table access tool in the bin directory of the TcaplusServiceAPI release package. It is also one of TcaplusServiceAPI’s app.

The TcaplusServiceAPI release package for the Linux x86_64 platform will include the 64-bit tcaplus_client tool for Linux. The TcaplusServiceAPI release package for the Windows x64 platform will include the 64-bit tcaplus_client tool for Windows. This example shows how to access using the tool for Linux x86_64.

> Operations must be performed in the CVM under your Tencent Cloud account.

In the following example, you receive the following access point information and created a table tb_online in the table group with the TableGroupID of 1.

* AccessID:2
* AppKey:3aa84dd773826cd655e9f24a249d68bb
* tcapdir Access Point:10.125.32.21:9999
* TableGroupID:1

## Permissions

Firstly, the tcaplus_client tool needs to be given executable permissions. When ./tcaplus_client is performed directly without any parameter, the parameter information needed for connection will be printed for users to enter based on their game specifications.

```
# ./tcaplus_client
--------------------------------------------------------------------------------
 invalid parameters, please start the client as following:

    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]

    the params in [] are optional, and theire order is not important.

    -a(--ap_id)    APP ID

    -z(--zone_id)    ZONE ID    -s(--signature)    PASSWORD



    -d(--dir)    dir server addr

    -t(--table)    table to add

    -l(--log)    log file name that must be client_log.xml, and log class name be client

    -T(--tdr)    tdr filename 

    -e(--execute)    content following should be with qoutes.

    e.g. ./tcaplus_client -a 2 -z 3 -s "FE6533875C8385C3" -d 172.25.40.181:9999 -T table_test.tdr 
--------------------------------------------------------------------------------
```

## Connect

Connect to TcaplusDB using commands.

```
./tcaplus_client -a 2 -z 1 -s "3aa84dd773826cd655e9f24a249d68bb" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  build at Wed Jan 18 22:08:38 CST 2017              |
|                                                                              |
|    Welcome!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

Enter "help" after the prompt, and you can see detailed help information. Use `> help commands` to view the specific usage method.

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

The following sections will walk you through how to perform write and read operations through the Update and Select commands.

## Write Operation

Write a record with the Update command.

```
tcaplus>update tb_online set gamesvrid=4099, logintime=101 where uin=1024 and name="tcaplus_user" and region=10;
--------------------------------------------------------------------------------
        success. 
--------------------------------------------------------------------------------
update time: 5593 us
```

## Read Operation

Read the written data with the Select command.

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

