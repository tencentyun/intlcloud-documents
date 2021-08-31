## Operation Scenarios 
This document describes how to modify a table in the TcaplusDB Console. If you want to modify the structure definition of a table, you can do so by modifying the table under the condition that the new definition meets the TcaplusDB table modification rules.

## Prerequisites
You have created a table. For more information, please see [Creating Table](https://intl.cloud.tencent.com/document/product/1016/32715).

## Directions
1. Enter the [Table List](https://console.cloud.tencent.com/tcaplusdb/table) page and select the target table. Select **More** > **Modify** in the "Operation" column or select multiple tables and click **Batch Modify** at the top.
2. In the "Modify" dialog box that pops up, upload or select a new table definition file and click **Compare Difference**.
> 
>- The primary key field cannot be deleted.
>- The name and type of the primary key field cannot be modified.
>- You cannot add new primary key fields.
>- A general field marked as required cannot be deleted.
>- The name and type of fields with the same identifier cannot be modified.
>- A new general field should be named according to the naming convention.
>
![](https://main.qcloudimg.com/raw/407bf6c819bf9b60d4ebd18928904a6b.png)
3. In the pop-up dialog box, you can view the comparison result. If your new table definition does not meet the TcaplusDB table modification rules, a prompt will be displayed.
![](https://main.qcloudimg.com/raw/087642d98430e6e1d066ae5dfc202f1a.png)
4. Click **Preview** in the "Comparison Preview" column to view the comparison between the new and old table structures.
![](https://main.qcloudimg.com/raw/997d4e6cd91e2815a8534f44e2ee10de.png)
5. After confirming that everything is correct, click **Confirm** to submit your request to modify the table, and a prompt will be returned if the modification is successful.
![](https://main.qcloudimg.com/raw/53fc68f54fcbaf6726874e9af3c26463.png)
   After modification, you can view the structure of the new table on the table configuration page.
   
