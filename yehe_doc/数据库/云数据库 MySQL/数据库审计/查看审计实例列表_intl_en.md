This document describes how to view the audit instance list as well as fields and executable operations in the list.

## Audit instance list tab
![](https://qcloudimg.tencent-cloud.cn/raw/b73ede35f5bf10b52677d289b2916fcd.png)

## Viewing the audit instance list
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance).
2. On the left sidebar, click **Database Audit**.
3. You will be redirected to the **Database Audit** > **Audit Instance** tab by default.
4. On the **Audit Instance** tab, you can view the list of tools (for quickly filtering instances, refreshing the tab, and downloading the list information), feature operations, and instance list fields.

**Tool list**

| Tool | Description | 
|---------|---------|
| Filter | You can select resource attributes such as instance ID/name, tag key, and tag in the search box above the audit instance list to filter resources. Separate multiple keywords by vertical bar "|" and separate multiple filter tags by carriage return. |
| Refresh | You can click ![](https://qcloudimg.tencent-cloud.cn/raw/7f2b69d4782d31946b52ca3330ba0521.png) to refresh the data in the audit instance list. |
| Download | You can click ![](https://qcloudimg.tencent-cloud.cn/raw/952653da73baf2763aa611d40bce4a73.png) to download the information of the filtered audit instances as a .csv file. The list fields in the file include instance ID/name, audit status, audit rule, total storage period, frequent access storage period, infrequent access storage period, total storage size, frequent access storage size, infrequent access storage size, project, tag, enablement time, and remarks. |

 **Relevant feature operations**
<table>
<thead><tr><th>Audit Status</th><th>Feature</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan="4">The audit service is enabled.</td>
<td>Disable Database Audit</td><td>You can (batch) disable the audit service as instructed in <a href="https://www.tencentcloud.com/document/product/236/56105" target="_blank">Disabling Audit Service</a>.</td></tr>
<td>Modify Audit Rule</td><td>You can (batch) modify audit rules as instructed in <a href="https://www.tencentcloud.com/document/product/236/56103" target="_blank">Modifying Audit Rule</a>.</td></tr>
<td>Modify Audit Service</td><td>You can (batch) modify the audit service items such as audit log retention period and frequent/infrequent access storage periods as instructed in <a href="https://www.tencentcloud.com/document/product/236/56104" target="_blank">Modifying Audit Service</a>.</td></tr>
<td>View Audit Log</td><td>You can query historical audit logs as instructed in <a href="https://www.tencentcloud.com/document/product/236/52087" target="_blank">Viewing Audit Log</a>.</td></tr>
<tr>
<td>The audit service is disabled</td><td>Enable Database Audit</td><td>You can (batch) enable the audit service as instructed in <a href="https://www.tencentcloud.com/document/product/236/52086" target="_blank">Enabling Audit Service</a>.</td></tr>
</tbody></table>	


 **Fields in the audit instance list**

| Field | Description |
|---------|---------|
| Instance ID/Name | ID/Name information of all instances in a region. |
| Audit Status | Audit enablement or disablement status. You can select **Enabled** or **Disabled** to filter instances in the corresponding status. |
| Audit Rule | The audit rule (full audit or rule-based audit) configured for audit-enabled instances. You can use the drop-down list to filter instances by a specific rule. |
| Log Retention Period | Total storage period and frequent/infrequent access storage periods in days for audit-enabled instances. |
| Stored Log Size | Total storage size and frequent/infrequent access storage sizes in MB for audit-enabled clusters/instances. |
| Project | Projects of instances to help you categorize and manage resources easily. You can use the drop-down list to filter instances by a specific project. |
| Tag (key:value) | Tag information of instances |
| Enablement Time | The time accurate down to the second when the audit service is enabled for instances. |
| Operation | Available operations when the audit service is enabled: <br><li>View Audit Log<li>More (Modify Audit Rule, Modify Audit Service, Disable)</li>Available operations when the audit service is disabled:<br>Enable Database Audit |
