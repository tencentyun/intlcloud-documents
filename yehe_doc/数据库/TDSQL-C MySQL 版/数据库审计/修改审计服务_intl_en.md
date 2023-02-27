This document describes how to modify the audit service in the console.
>?
>- If you choose to extend the log retention period, the change will take effect immediately; if you choose to shorten the log retention period, expired logs will be cleared immediately.
>- If the data of the last n days is set to be stored in frequent access storage, older data will be automatically transitioned to infrequent access storage. After the frequent access storage period is extended, the audit data that falls in the extension period will be automatically migrated back from infrequent access storage to frequent access storage.

## Prerequisites
You have enabled the audit service as instructed in [Enabling Audit Service](https://intl.cloud.tencent.com/document/product/1098/44614).

## Modifying the audit service for one instance
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Database Audit** on the left sidebar and select the region at the top.
3. Click **Enabled** after **Audit Status** to filter instances for which the audit service is enabled.
4. Find the target instance in the audit instance list, or search for it by resource attribute in the search box, and select **More** > **Modify Audit Service** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DUxM107_3.png)
5. In the **Modify Audit Service** window, modify the log retention period or frequent access storage period and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kJbh262_4.png)

## Batch modifying the audit service
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Database Audit** on the left sidebar and select the region at the top.
3. Click **Enabled** after **Audit Status** to filter instances for which the audit service is enabled.
4. Find the target instances in the audit instance list, or search for them by resource attribute in the search box, and select them. Then, click **Modify Audit Service** above the list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/FUy7405_5.png)
5. In the **Modify Audit Service** window, modify the log retention period or frequent access storage period and click **OK**.
>!The **Modify Audit Service** window displays the log retention periods both before and after the modification to make comparisons easier. The new log retention period will be applied to the selected instances. Therefore, proceed with caution.
>
