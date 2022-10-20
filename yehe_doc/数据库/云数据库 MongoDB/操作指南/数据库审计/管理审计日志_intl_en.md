## Overview

After database audit is enabled, the system will record relevant operations on TencentDB for MongoDB instances. You can view audit logs at any time, including the database access time, client IP, account ID, executed statement, and statement execution time.

## Notes

- Currently, you can download audit log files of a database instance only at the Tencent Cloud private network address by using a CVM instance in the same region.
- Log files are valid for 24 hours. Download them promptly.
- Up to 30 log files can be retained for one database instance. Delete files promptly after download.
- If the status is `Failed`, there may be too many logs. You can download them in batches by narrowing down the time range.

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551) and enabled database audit for it.
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Viewing an audit log

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **TencentDB for MongoDB** > **Database Audit** on the left sidebar.
3. Above the **Database Audit** page on the right, select the region.
4. In the top-right corner of the audit instance list, select an instance with **Audit Status** being **Enabled**.
5. Click the instance ID to enter the **Audit Log** tab and view audit logs.
6. In the time box, select the time period of audit logs. In the search box, search for audit logs by key information such as **Client IP**, **Account ID**, **Operation Type**, **Policy Name**, **Execution Time**, **Affected Rows**, and **Task Status Code**.
>?
> - The audit log display time is down to milliseconds, facilitating more precise sorting and problem analysis of SQL commands.
> - You can select any time period with data for search. Up to the first 60,000 eligible records can be displayed.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/140ebfe4af084d101f59bab2bd4bd4b7.png)
Audit log fields are as described below:
<table>
<thead><tr><th>No.</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>1</td>
<td>Time</td>
<td>The time when the database is accessed.</td></tr>
<tr>
<td>2</td>
<td>Client IP</td>
<td>The client IP from which the database is accessed.</td></tr>
<tr>
<td>3</td>
<td>Account ID</td>
<td>The account ID accessing the database.</td></tr>
<tr>
<td>4</td>
<td>Operation Type</td>
<td>The type of the operation statement executed to access the database. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/1a6b89dced3db00397b31e7be029c907.png" style="zoom:67%;"> to select the target type in the drop-down list.</td></tr>
<tr>
<td>4</td>
<td>Executed Statement</td>
<td>The request statement executed to access the database.</td></tr>
<tr>
<td>5</td>
<td>Affected Rows</td>
<td>The number of database rows changed after statement execution.</td></tr>
<tr>
<td>6</td>
<td>Task Status Code</td>
<td>The status code returned after statement execution. <ul><li>`0`: Executed successfully.</li><li>`-1`: Execution failed.</li><li>`18`: Identity verification failed.</li><li>`334`: MongoDB authentication protocol unavailable.</li></ul></td></tr>
<tr>
<td>7</td>
<td>Execution Time</td>
<td>The time taken to execute the statement.</td></tr>
</tbody></table>

## Generating and downloading an audit log file

1. In the top-right corner of the audit log list, click <img src="https://qcloudimg.tencent-cloud.cn/raw/9667d5a4436c73db2d01621458e64cdb.png" style="zoom:60%;" />.
![](https://qcloudimg.tencent-cloud.cn/raw/8a6061a69a6abb22254648b39bdf10f1.png)
2. In the **Create Log File** pop-up window, click **Generate File** to start a log file generation task.
3. In the **Create Log File** pop-up window, click **File List**.
![](https://qcloudimg.tencent-cloud.cn/raw/d28632a05f7be94de5ae6fc49f6ec026.png)
4. On the **Audit Log File List** page, view audit log files.
> ?
> - Currently, you can download audit log files of a database instance only at the Tencent Cloud private network address by using a CVM instance in the same region.
> - Log files are valid for 24 hours. Download them promptly.
> - Up to 30 log files can be retained for one database instance. Delete files promptly after download.
> - If the status is `Failed`, there may be too many logs. You can download them in batches by narrowing down the time range.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/625e0655fbafa5d48dd6f899f4fb8004.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td>File Name</td>
<td>The audit log file name, which is generated automatically by the system.</td></tr>
<tr>
<td>Creation Time</td>
<td>The time when the audit log is generated.</td></tr>
<tr>
<td>Status</td>
<td>The status of the audit log generation task, which can be **Generating** or **Generated**.</td></tr>
<tr>
<td>Size</td>
<td>The audit log file size.</td></tr>
<tr>
<td>Private Network Download Address</td>
<td>You can copy the private network address to download the log file.</td></tr>
<tr>
<td>Operation</td>
<td>Click <strong>Delete</strong> to delete the audit log file.</td></tr>
</tbody></table>

## More operations
You can manage the audit log list with the following operations:
![](https://qcloudimg.tencent-cloud.cn/raw/8a6061a69a6abb22254648b39bdf10f1.png)
- Click <img src="https://qcloudimg.tencent-cloud.cn/raw/4af2681313e814b5eb715a7515c137fa.png" style="zoom: 15%;" /> to customize fields in the audit log list.
- Click <img src="https://qcloudimg.tencent-cloud.cn/raw/6895bf17f6b486a67b680f0e6ea05252.png" style="zoom: 33%;" /> to refresh the audit log list.
- Click <img src="https://qcloudimg.tencent-cloud.cn/raw/deb8b3b9a8b6a2b9d4ec9a8b213bd785.png" style="zoom:33%;" /> to enter the audit log file list page.

   
