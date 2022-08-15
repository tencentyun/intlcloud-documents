Data Lake Compute allows you to configure an EMR Hive data source for multi-source federated data analysis.
## Preparations
- Get the EMR Hive address.
- Use an account with the permission to create data catalogs. For more information on permissions, see [Permission Overview](https://intl.cloud.tencent.com/document/product/1155/48665).

## Creating an EMR Hive data source
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data Explore** on the left sidebar, click **+** in the **Database & table** column, and select **Create data catalog**.
![]()
3. Select **EMR Hive (HDFS)** for **Connection type** and select the target EMR instance. The VPC information will be populated by default after the instance is selected. **EMR versions supported by EMR Hive are 2.3.5, 2.3.7, 3.1.1, and 3.1.2.**
>! Relevant permissions are required for you to select the EMR Hive instance.
>
![]()
4. Select the **Run cluster**. Currently, you can only select a private data engine of Presto. If there is no engine, create one on the **Data engine** page. For more information on the purchase process, see [Purchasing Private Data Engine](https://intl.cloud.tencent.com/document/product/1155/48682).
>! The IP range of the selected data engine cannot be the same as that of the EMR instance; otherwise, a network conflict will occur, and you cannot query or analyze data.
5. Click **Confirm**.

## Querying the EMR Hive data
After the data catalog is created, you can switch to it from the **Data catalog** menu on the **Data Explore** page.
![]()
At this point, you can query and analyze the data catalog with SQL statements.
Select the data engine bound when the data catalog is created and click **Run** to get the query result.

>! You can only query the data catalog with its bound data engine. To change the bound engine, click the set icon next to the data catalog.
>
![]()
