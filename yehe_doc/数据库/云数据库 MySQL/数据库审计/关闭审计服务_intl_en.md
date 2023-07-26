This document describes how to disable the audit service in the console.
After the audit service is disabled, instances will no longer be audited, and historical audit logs will be cleared.
>

## Prerequisite
You have enabled the audit service. For more information, see [Enabling Audit Service](https://www.tencentcloud.com/document/product/236/52086).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance).
2. On the left sidebar, click **Database Audit**.
3. Select **Region** at the top, click **Audit Instance** tab, click **Audit Status**, and click **Enabled** to filter the audit-enabled instances.
4. Find the target instance in the **Audit Instance** list, or search for it by resource attribute in the search box, and select **More** > **Disable** in the **Operation** column.
>?You can batch disable the audit service for multiple target instances by selecting them in the audit instance list and clicking **Disable Database Audit** above the list.
>
5. In the **Disable Database Audit** window, confirm that everything is correct and click **OK**.
6. After confirmation, the disablement result will be displayed in the result column. You can click **View Task** to enter the task list and view the details.
