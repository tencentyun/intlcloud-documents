This document describes how to use the client tool tcaplus_client to access data.

All DML statements must use the `WHERE` clause which should contain at least a primary key field. If there are multiple primary keys, separate them with `and`.

## Accessing TcaplusDB through Client Tool
tcaplus_client is a client tool used to access TcaplusDB tables and can be obtained at the download address in the table below.

The release package of TcaplusServiceAPI for Linux x86_64 contains the tcaplus_client tool for Linux 64-bit.

| Version          | Release Date   | OS     | Package Download Address                                                     |
| ------------- | ---------- | ------------ | ------------------------------------------------------------ |
| 3.46.0.199033 | 2020/12/28 | Linux x86_64 | [Download](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/release/3-46/TcaplusPbApi3.46.0.199033.x86_64_release_20201210.tar.gz) |

>?
>- The following operations need to be performed on the CVM instance in the same VPC and subnet under your Tencent Cloud account as your TcaplusDB cluster.
>- You can download TcaplusServiceAPI v3.36.0.192960 [here](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz).

### Installing client
After downloading the TcaplusServiceAPI installation package, you can [use the upload tool](https://intl.cloud.tencent.com/document/product/213/34821) to upload it onto the CVM instance in the same VPC and subnet as the TcaplusDB cluster.

1. After the upload, run the following command to decompress the installation package:
```
tar -xf TcaplusPbApi3.46.0.199033.x86_64_release_20201210.tar.gz -C tcaplus
```
2. After the decompression, enter the `bin` directory in `tcaplus` and grant the tool executable permission:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. Run the `./tcaplus_client` command, and the system will prompt you to enter the parameter information required for database connection. You can enter it based on your cluster information.
>!In the sample below, `app_id` indicates the cluster access ID, `App` indicates the cluster, and `zone` indicates the table group.


```
## ./tcaplus_client
--------------------------------------------------------------------------------
  invalid parameters, please start the client as following:

    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]

    the params in [] are optional, and their order is not important.

    -a(--ap_id)    APP ID

    -z(--zone_id)    ZONE ID

    -s(--signature)    PASSWORD

    -d(--dir)    dir server addr

    -t(--table)    table to add

    -l(--log)    log file name that must be client_log.xml, and log class name be client

    -T(--tdr)    tdr filename 

    -e(--execute)    SQL command need to execute, the content should be in quotes.

    e.g. ./tcaplus_client -a 2 -z 3 -s "FE6533875C8385C3" -d 172.25.40.181:9999 -T table_test.tdr -e "select a, b from table where key = 1;" 
--------------------------------------------------------------------------------
```

### Connecting to TcaplusDB (default scenario)
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

Enter `help` after the prompt, and you can see detailed help information. Enter `> help` to view how to use related commands.
```
tcaplus>help
--------------------------------------------------------------------------------
      help: show usage of commands, example: "help select;".
      show: get server status related information. executing "help show;" for details.
      exit/quit: exit the client.
     count: print record number in the database.
 
      desc: print table field name and type.
    select: query records from database.
    insert: insert a new record into database.
   replace: replace a record into the database.
    update: update a record in the database.
    delete: delete record(s) from database.
 
      dump: dump records from database.
      load: load records into the database.
--------------------------------------------------------------------------------
```

### Parameter description
| Parameter | Description                                          | Required |
| ---- | --------------------------------------------- | -------- |
| -a   | Access ID                                       | Yes       |
| -z   | Table group ID                                     | Yes       |
| -s   | Cluster password                                      | Yes       |
| -d   | Cluster IP and port                            | Yes       |
| -t   | Table name                                        | No       |
| -l   | The output setting of log files. The file name must be "client_log.xml". | No       |
| -T   | TDR file path                                  | No       |
| -e   | The SQL statements to execute                           | No       |
| -v   | The version to query                                      | No       |
| <    | Redirect SQL statements to client to execute.                 | No       |

### Connecting to TcaplusDB (using TDR)
To connect to TcaplusDB via TDR, you must use the client launch parameters to specify the TDR file path. You can use the [TDR tool](#tdrgj) to convert multiple XML metadatabases into binary format. If there are dependencies between multiple XML files, the dependent XML file must be placed in front of the parameter list.

Sample:
```
[root@test-PC0 /opt]# ./tcaplus_client -a 2 -z 3 -s C12901752D0D3347 -d 8.x.x.8:9999 -T /mnt/e/tdr/2.3.table_list.tdr
 
====== Welcome to use tcaplus_client, use "help" to show usage ======
tcaplus > exit

[root@test-PC0 /opt]# ./tcaplus_client -a 2 -z 3 -s C12901752D0D3347 -d 8.x.x.8:9999 -T /mnt/e/tdr/2.3.table_list.tdr -e "show tables;"
-------------------------------------------
| Table Name                    Type      |
-------------------------------------------
| MTownRoleInfo                 GENERIC   |
| table_generic                 GENERIC   |
| table_generic_xiahuaxian      GENERIC   |
| table_list                    LIST      |
| test_table                    GENERIC   |
-------------------------------------------
```

<span id = "tdrgj"></span>

#### TDR tool
You need to use the TDR tool to generate a TDR file, which is mainly generated by the data definition file (TDR structure in XML format). Download the tool [here](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tdr).

Sample:
```
tdr -B -o ov_res.tdr ov_res.xml
        # Convert XML metadatabases to TDR binary databases.
tdr -C -o ov_res.c --old_xml_tagset  ov_res.xml
        # Convert metadatabases in old XML format (using the old tag set) to .c files.
tdr -H -O "include" --add_custom_prefix="m_" --no_type_prefix
        # Convert XML metadatabases to .h files which are saved in the "include" directory.
        # Add the prefix "m_" to the member name of struct/union, but not add a type prefix.
tdr -G -m Pkg -x ATTR -o Pkg.xml net_protocol.xml
        # Generate a configuration file in XML format through package (a data structure package customized by user).
tdr -T -u prefixfile
        # Export the prefix table of the data member used when generating the .h file to the file "prefixfile".
tdr -A --indent-size=8 net_protocol.xml
        # Generate ActionScript3 class files according to the protocol described in "net_protocol.xml". The generated class files are all indented with 8 spaces.
tdr -P --indent-size=8 net_protocol.xml
        # Generate C++ class files according to the protocol described in "net_protocol.xml". The generated class files are all indented with 8 spaces.
tdr -S --indent-size=8 net_protocol.xml
        # Generate C# class files according to the protocol described in "net_protocol.xml". The generated class files are all indented with 8 spaces.
tdr -E 0x83010404
        # Query the error information of error code 0x83010404.
```

#### tdr2xml tool
The tdr2xml tool can decompile the binary metadata file to an XML metadata file. Download the tool [here](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tdr2xml).

Syntax:
```
tdr2xml   [-o --out_file=FILE] [-h --help] [-v --version] DRFILE
The description of each parameter is as follows:
-o, --out_file=FILE: specify the name of the output file. Default value: a.xml.
-h, --help: output help.
-v, --version: output the version information.
```

Sample:
```
tdr2xml –o net_cs.xml  net_cs.tdr
```
Convert the metadata description file in binary custom format saved in the "net_cs.tdr" file into a description file in XML format.
