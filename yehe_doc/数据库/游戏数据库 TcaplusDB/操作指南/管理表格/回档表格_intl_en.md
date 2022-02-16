## Operation Scenarios 
This document describes how to roll back specified records in the TcaplusDB Console.

## Prerequisites
You have created a table. For more information, please see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

## Directions
1. Enter the [Table List](https://console.cloud.tencent.com/tcaplusdb/table) page, select the target table and click **More** > **Roll back** in the "Operation" column, or select multiple tables and click **Batch Rollback** at the top.
2. In the pop-up dialog box, upload a .txt file that contains the values of the fields of the target record.
   The file is in the following format:
   Suppose your table is defined as follows, where the primary keys are `openid`, `tconndid`, and `timekey`:
```
syntax = "proto2";
package myTcaplusTable;
import "tcaplusservice.optionv1.proto";
message tb_online {
    option(tcaplusservice.tcaplus_primary_key) = "openid,tconndid,timekey";
    required int32 openid = 1; //QQ Uin
    required int32 tconndid = 2;
    required string timekey = 3;
    required string gamesvrid = 4;
	optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; 
	optional pay_info pay = 7;
	message pay_info {
		optional uint64 total_money = 1;
		optional uint64 pay_times = 2;
	}
}
```
To roll back a record with keys of `openid` = 100, `tconndid`= 1, and `timekey` = '123456', you need to prepare a file containing the keys as follows. The first row contains the names of primary keys separated by space, and the second and subsequent rows contain the primary key values of the records to be rolled back.
```
openid tconndid timekey 
100 1 123456
```
4. After the key.txt file is uploaded, select the rollback time and click **Submit**.
![](https://main.qcloudimg.com/raw/60f9532439c46ae11803a267bed79f98.png)

