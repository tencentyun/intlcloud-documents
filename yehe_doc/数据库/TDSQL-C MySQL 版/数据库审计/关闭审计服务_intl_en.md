
This document describes how to disable the audit service in the console.
After the audit service is disabled, instances will no longer be audited, and historical audit logs will be cleared.
>

## Prerequisites
You have [enabled audit in TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/1098/44614).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. On the left sidebar, select **Database Audit**.
3. Click **Enabled** after **Audit Status** to filter instances for which the audit service is enabled.
4. Find the target instance in the audit instance list, or search for it by resource attribute in the search box, and select **More** > **Disable** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/PrZK524_13.png)
>?You can batch disable the audit service for multiple target instances by selecting them in the audit instance list and clicking **Disable Database Audit** above the list.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QDAZ795_14.png)
5. In the **Disable Database Audit** window, confirm that everything is correct and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zNpX661_15.png)
6. After confirmation, the disablement result will be displayed in the result column. You can click **View Task** to enter the task list and view the details.

