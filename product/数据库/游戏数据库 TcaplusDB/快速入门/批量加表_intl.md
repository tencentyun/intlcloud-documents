[//]: # (chinagitpath:XXXXX)

## Batch Table Creation
This document describes how to create TcaplusDB tables for your game after the service is activated.

## Prerequisites
You have activated Tcaplus for your game.
To activate Tcaplus, see [Service Activation](https://intl.cloud.tencent.com/document/product/596/10869).

## Procedure
Common table management operations in TcaplusDB include batch creation, batch modification, batch deletion, batch scaling and batch rollback.
TcaplusDB supports batch creation of tables. Follow the steps below:  
1. Click **Batch Creation** to enter the table creation page.
![](https://main.qcloudimg.com/raw/95381d456556dee21d1efd125076d7a1.png)

2. Select the deployment unit. If there is no deployment unit, you will need to create one. Click **New Deployment Unit** and enter the name as needed.
> The table structure is defined by the proto file. Before creating the table, you must understand TcaplusDB’s table definition rules. See [Proto Table Creation File](https://intl.cloud.tencent.com/document/product/1016/30286)
>
![](https://main.qcloudimg.com/raw/4fe221481d531c3495951006e8109109.png)


The following is an example of a proto file.

```
// tb_online.proto
syntax = "proto2";
package myTcaplusTable;

import "tcaplusservice.optionv1.proto";

message tb_online {
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    required int64 uin = 1; 
    required string name = 2; 
    required int32 region = 3;

    required int32 gamesvrid = 4; 
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; 
    optional bool is_available = 7 [default = false]; 
    optional pay_info pay = 8; 
}

message pay_info { 

    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { 
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```

3. Click **Local File** to select local files to upload. If you have uploaded a file, click **Import from History File** to add a file, and then click **Next**.
> ! Only Proto file format is supported and the file size  cannot exceed 2 MB.
> 
![](https://main.qcloudimg.com/raw/138c78c572216fb906338248cd2883d6.png)

4. Set the table information. Select the table to be set, set **Capacity**, **Reserved Reads** and **Reserved Writes** as needed, and click **Next**.
![](https://main.qcloudimg.com/raw/f8234f0e7431c827fa14768491f08db7.png)

5. Confirm the table information, and then click **Create**.
![](https://main.qcloudimg.com/raw/870584ad7b59bcd6fc7175e85b9384d8.png)

6. The system will return a success message when the table is successfully created. 
![](https://main.qcloudimg.com/raw/edbb79dc9fbfedb97424edd3cf9bbd46.png)



