## Operation Scenario
This document describes how to create a TcaplusDB table in the console.

## Prerequisites
You have created a TcaplusDB [application](https://intl.cloud.tencent.com/document/product/1016/32714) and [deployment unit](https://intl.cloud.tencent.com/document/product/1016/32716).

## Directions
1. Log in to the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/table), select **Table List** on the left sidebar, and click **Create Table**.
2. Configure the table on the table creation page.
 - **Application and Deployment Unit**: Select the target application and deployment unit.
 - **Table File**: You can upload a table definition file from your local file system, select a previously uploaded one, or mix and match. However, filenames must be unique.
![](https://main.qcloudimg.com/raw/05faf2ee7fe0d3ed536b7b3db92cde64.png)
Below is a sample .proto file:
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
3. Click **Next** and the system will check the selected table definition file.
 - If the check fails, an error will be returned, and you should modify the file accordingly and upload it again.
 - If the check is successful, the table metadata defined in the file will be displayed, and then you can proceed to the next step.
4. On the table configuration page, select the table to be created and enter the capacity and reserved read and write parameters. The daily fees of the table will be automatically calculated.
![](https://main.qcloudimg.com/raw/053be2ade8302028afda597b7d712a3f.png)
5. After checking that the table information is correct, click **Create** and the system will prompt that the creation has been successful.
![](https://main.qcloudimg.com/raw/24534e9f9d35dde777aa6c25b20d4732.png)
