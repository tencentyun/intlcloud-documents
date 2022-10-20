## Overview
The TencentDB for MongoDB console displays the list of instances with the audit feature enabled, so you can quickly search for audit instances by instance ID or name, This helps you stay on top of various information such as audit rules, audit log volume, and retention period.

## Version description

Currently, only TencentDB for MongoDB 4.0 supports database audit.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551) and enabled database audit for it.
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **TencentDB for MongoDB** > **Database Audit** on the left sidebar.
3. Above the **Database Audit** page on the right, select the region.
4. In the top-right corner of the audit instance list, select an instance with **Audit Status** being **Enabled**.
5. Click the search box and find the target instance by **Instance ID**, **Instance Name**, **Tag Key**, or **Tag** in the drop-down list.
6. View the audit information of the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/a0cebf73189c00d71af6c96913a06ba7.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance ID/Name</td>
<td>Audit instance ID/name. Click the instance ID to enter the <strong>Instance Details</strong> page. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44179">Viewing Instance Details</a>.</td></tr>
<tr>
<td>Version and Engine</td>
<td>Version and storage engine of the audit instance. "WT" indicates the WiredTiger engine. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31706">Storage Engine and Version</a>.</td></tr>
<tr>
<td>Audit Status</td>
<td>Audit instance status, which can be **Enabled** or **Disabled**.</td></tr>
<tr>
<td>Log Retention Period</td>
<td>Audit log retention period. You can modify it as instructed in <a href="https://cloud.tencent.com/document/product/240/78933">Modifying Audit Log Retention Period</a>.</td></tr>
<tr>
<td>Log Volume</td>
<td>Audit log volume in MB. It may not be updated in real time and is for reference only. Data in the billing system shall prevail.</td></tr>
<tr>
<td>Audit Rule</td>
<td>Audit rules of the instance, including full audit and rule audit. You can modify rules as instructed in <a href="https://www.tencentcloud.com/document/product/240/50657">Modifying Audit Rule</a>.</td></tr>
<tr>
<td>Project</td><td>Project name of the instance.</td></tr>
<tr>
<td>Tag (key: value)</td><td>Tag key and value of the audit instance.</td></tr>
</tbody></table>


## More operations
For more information on database audit operations, see [Viewing Audit Log](https://intl.cloud.tencent.com/document/product/1102/47772).

