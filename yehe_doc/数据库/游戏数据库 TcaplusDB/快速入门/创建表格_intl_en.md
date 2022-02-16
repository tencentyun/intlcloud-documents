## Operation Scenarios
This document describes how to create a table in the TcaplusDB Console.

## Prerequisites
- You have created a TcaplusDB [cluster](https://intl.cloud.tencent.com/document/product/1016/32714) and [table group](https://intl.cloud.tencent.com/document/product/1016/32716).
- You have prepared the table file according to the [sample table description file](https://intl.cloud.tencent.com/document/product/1016/36560).

## Directions
1. Log in to the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/table), select **Table List** on the left sidebar, and click **Create Table**.
2. Configure the table on the table creation page.
 -**Cluster and Table Group**: select the target cluster and table group.
 - **Table File**: you can upload a table definition file from your local file system, select a previously uploaded one, or mix and match. However, filenames must be unique. For more information, please see the sample PB table file [game_players.proto](
https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto).
 - **Remarks**: enter the table remarks.
   ![](https://main.qcloudimg.com/raw/5621a15042a9d73b4364fe19b9a9268b.png)
3. Click **Next** and the system will verify the selected table definition file.
 - If the verification fails, an error will be returned, and you should modify the file accordingly and upload it again.
 - If the verification is successful, the table metadata defined in the file will be displayed, and then you can proceed to the next step.
4. On the table configuration page, select the table to be created and enter the capacity and reserved read and write parameters. The daily fees of the table will be automatically calculated.
![](https://main.qcloudimg.com/raw/32aa5c8a292df17249a62e88b6fca4e6.png)
5. After confirming that the table information is correct, click **Create** and the system will prompt that the creation has been successful.
![](https://main.qcloudimg.com/raw/7a39640da609a65df7040fc9c1d7be3d.png)
