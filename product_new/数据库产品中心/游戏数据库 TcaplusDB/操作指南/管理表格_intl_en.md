
This document describes how to manage a TcaplusDB table. For more information on how to create a table, see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

## Viewing Table Information
On the [Table List](https://console.cloud.tencent.com/tcaplusdb/table) page, you can view the information of the created tables. Each table is assigned a unique table ID.

Click a table ID to enter the table management page, which consists of **Table Details**, **Table Configuration**, **Table Monitoring**, and **Table Rollback** tabs.
![](https://main.qcloudimg.com/raw/5dd8aaecae4a2093bd5cdbbfb0dea2ff.png)
- The **Table Details** tab displays the information of table, network, and reserved configuration. You can click the "Modify" icon next to the remarks to modify the remarks.
- The **Table Configuration** tab displays the field definition information of a table.
- The **Table Monitoring** tab displays table monitoring information. You can select the monitoring data for different periods and at different granularities and compare data for different periods.
- The **Table Rollback** tab provides the table rollback feature.

## Clearing a Table
> If you clear a table, all its data will be completely cleared and cannot be recovered, so please operate with caution.
>
1. Select the desired table from the table list and select **More** > **Clear** in the "Operation" column, or select multiple tables and click **Batch Clear** at the top.
![](https://main.qcloudimg.com/raw/3d5f34cb30c29fc00b198598e6c8424b.png)
2. In the "Clear" dialog box that pops up, click **OK** to clear the table.
3. After the table is successfully cleared, the link to the task performed will be returned. Click the task ID in the "Result Remarks" column to view the task details.
![](https://main.qcloudimg.com/raw/13dccb9f78a80ce5b91c17ecc450e21d.png)

## Deleting a Table
> If you delete a table completely, all its data will be completely cleared and cannot be recovered, so please operate with caution.
>
A table which is in **RUNNING** status can be deleted. Once deleted, it will be moved to the recycle bin, and its data still exists.
1. Select the desired table from the table list, and select **More** > **Delete** in the "Operation" column, or select multiple tables and click **Batch Delete** at the top.
![](https://main.qcloudimg.com/raw/4698c628245093b1597caa2166f68cae.png)
2. In the "Delete" dialog box that pops up, click **OK**, and the table will be moved to the recycle bin.
3. In the recycle bin, you can **delete** a table completely from your system or **restore** it to the **RUNNING** status.
![](https://main.qcloudimg.com/raw/f752d04243ff5bdf7aff655d493781fa.png)

## Modifying a Table
If you want to modify the structural definition of a table, you can do so by modifying the table under the condition that the new definition meets the TcaplusDB table rules.
1. Select the desired table from the table list and select **More** > **Modify** in the "Operation" column, or select multiple tables and click **Batch Modify** at the top.
2. In the "Modify" dialog box that pops up, upload or select a new table definition file and click **Compare difference**.
> 
>- A `key` field (required) cannot be deleted.
>- The name and type of a `key` field cannot be changed.
>- No new `key` fields can be added.
>- A `value` field marked as required cannot be deleted.
>- The name and type of fields with the same tagid cannot be changed.
>- A new `value` field should be named according to the value naming convention.
>- A new `value` field should not be named the same as an existing `key` or `value` field.
>
![](https://main.qcloudimg.com/raw/407bf6c819bf9b60d4ebd18928904a6b.png)
4. In the pop-up dialog box, you can view the comparison result. If your new table definition does not meet the TcaplusDB table rules, a prompt will appear.
![](https://main.qcloudimg.com/raw/087642d98430e6e1d066ae5dfc202f1a.png)
5. Click **Preview** in the "Comparison preview" column to view the comparison between the new and old table structures.
![](https://main.qcloudimg.com/raw/997d4e6cd91e2815a8534f44e2ee10de.png)
5. After confirming that everything is correct, click **OK** to submit your request to modify the table, and a prompt will be returned if the modification is successful.
![](https://main.qcloudimg.com/raw/53fc68f54fcbaf6726874e9af3c26463.png)
After modification, you can view the structure of the new table on the "Table Configuration" page.

## Expanding a Table
1. Select the desired table from the table list and click **Expand** in the "Operation" column, or select multiple tables and click **Batch Expand** at the top.
2. In the pop-up dialog box, determine the capacity and reserved read and write parameters, and click **OK** to submit your request.
![](https://main.qcloudimg.com/raw/7809d2d5b414991d9e5d1f400f2a4cc7.png)

## Rolling back a Table
1. Select the desired table from the table list and click **Rollback** in the "Operation" column, or select multiple tables and click **Batch Rollback** at the top.
2. In the pop-up dialog box, upload a .txt file that contains the key values of the primary keys of the target record.
The file is in the following format:
Assume that your table is defined as follows, where the primary keys are openid, tconndid, and timekey.
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
To roll back a record with keys of openid=100, tconndid=1, and timekey='123456', you need to prepare a file containing the keys as follows. The first row contains the names of `key` fields separated by space, and the second and subsequent rows contain the key values to be rolled back to.
```
openid tconndid timekey
100 1 123456
```
4. After the key.txt file is uploaded, select the rollback time and click **Submit**.
![](https://main.qcloudimg.com/raw/60f9532439c46ae11803a267bed79f98.png)
