
## Overview 
This document describes how to modify a table in the TcaplusDB console. If you want to modify the structure definition of a table, you can do so by modifying the table under the condition that the new definition meets the TcaplusDB table modification rules.

## Prerequisite
You have created a table. For more information, see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

## Directions
1. On the [Table List](https://console.cloud.tencent.com/tcaplusdb/table) page, either locate the desired table and select **More** > **Modify** in the **Operation** column or select multiple tables and select **Batch Operation** > **Modify Table** at the top.
2. In the pop-up window, upload or select a new table definition file and click **Compare Difference**.
>! 
>- The primary key field cannot be deleted.
>- The name and type of the primary key field cannot be modified.
>- You cannot add new primary key fields.
>- A general field marked as required cannot be deleted.
>- The name and type of fields with the same identifier cannot be modified.
>- A new general field should be named according to the naming convention.
>
![](https://qcloudimg.tencent-cloud.cn/raw/e814beb8d7e1e21d537b4b54b7f33c35.png)
3. In the pop-up dialog box, you can view the comparison result. If your new table definition does not meet the TcaplusDB table modification rules, a prompt will appear.
![](https://qcloudimg.tencent-cloud.cn/raw/cf146c39e9873ae25823ef1ffdcf0e2c.png)
4. Click **Preview** in the **Comparison Preview** column to view the comparison between the new and old table structures.
![](https://qcloudimg.tencent-cloud.cn/raw/4a8eb927da13cfd9715c139484c3a09e.png)
5. After confirming that everything is correct, click **Modify** to submit your request to modify the table, and a prompt will be returned if the modification is successful.
![](C:\Users\v_vwslwu\AppData\Roaming\Typora\typora-user-images\image-20220303203648828.png)
After modification, you can view the structure of the new table on the **Table Configuration** page.
