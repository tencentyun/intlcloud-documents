## Overview

Audit logs enable you to view the information of historical operation events in the specified period of time, including basic information, operation information, and event details. Generally, audit logs can be used in scenarios such as compliance audit, project change tracking, and security analysis.

## Directions

### Step 1. Query audit logs  

The console displays the audit logs in the last 24 hours by default. You can set filters to view the desired audit logs.

>?Currently, you can search for audit logs in the last 30 days in the console. To search for earlier logs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://qcloudimg.tencent-cloud.cn/raw/bf0721e738a21159ea1874399c5be436.png)


1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and select **Management center** > **Audit log** on the left sidebar.
2. Set filters, which include:
<table>
<thead>
<tr>
<th>Field</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td><nobr>Operation time</nobr></td>
<td>You can search by operation time. You can select the preset last 5 minutes, last 15 minutes, last hour, last 6 hours, last day, last 3 days, last 7 days, last 30 days, today, yesterday, the day before yesterday, this week, last week, or a custom time period.</td>
</tr>
<tr>
<td>Username</td>
<td>You can search by username or account ID to view the audit logs of the specified user.</td>
</tr>
<tr>
<td>Project name</td>
<td>You can search by project name to view the audit logs of the specified project.</td>
</tr>
<tr>
<td>Module</td>
<td>You can search by module such as app integration, connection management, security gateway, operation monitoring, general storage, integration resource, project management, API management, or API user center.</td>
</tr>
<tr>
<td>Operation type</td>
<td>You can search by operation type such as creation, editing, deletion, publishing, stop, login, or logout.</td>
</tr>
<tr>
<td>Operation result</td>
<td>You can search by operation result such as success or failure.</td>
</tr>
<tr>
<td><nobr>Custom search box</nobr></td>
<td>You can search by entering an operation event keyword. Generally, this filter is suitable for exception tracking.</td>
</tr>
</tbody></table>
3. View logs. The audit logs meeting the specified filter conditions are displayed and sorted in reverse chronological order. The log list contains the following:[](id:loglist)
<table>
<thead>
<tr>
<th>Field</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td><nobr>Operation time</nobr></td>
<td>The time when the operation event occurred.</td>
</tr>
<tr>
<td>Username</td>
<td>The username and account ID of the user executing the operation event.</td>
</tr>
<tr>
<td>Operation result</td>
<td>Whether the operation event is executed successfully. If the result is failure, the operation is not executed, and you can view the error message.</td>
</tr>
<tr>
<td>Project name</td>
<td>The project of the operation event.</td>
</tr>
<tr>
<td>Module</td>
<td>The feature module of the operation event.</td>
</tr>
<tr>
<td>Operation type</td>
<td>The abstract operation type of the operation event.</td>
</tr>
<tr>
<td>Operation event</td>
<td>The content digest of the operation event.</td>
</tr>
<tr>
<td>Operation</td>
<td>**View details**. You can view the basic information, operation information, and event details as instructed in <a href="#step2">step 2</a>.</td>
</tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ea174bbc2d8cbf7939ec8a246ea4da5a.png">
4. Reset logs filters.
After filtering and querying logs, you can click **Reset** to quickly restore to the logs displayed by default.
![](https://qcloudimg.tencent-cloud.cn/raw/5171806e19b4335324418c64abd72e32.png)

### Step 2. View log details[](id:step2)  

For a concerning or suspicious audit log, you can click **View details** to view its details. In addition to the information on the list page, the following information is also displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/b3afff6098d505ef1a77aea2b86e28c8.png)

<table>
<thead>
<tr>
<th>Type</th>
<th>Field</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="2"><nobr>Basic info</nobr></td>
<td>Event ID</td>
<td>The unique ID of each audit log.</td>
</tr>
<tr>
<td>Source IP address</td>
<td>The source IP address of the user who executed the operation event.</td>
</tr>
<tr>
<td>Operation info</td>
<td><nobr>Error message</nobr></td>
<td>The error message displayed when the operation result is failure.</td>
</tr>
<tr>
<td>Event details</td>
<td>Event details</td>
<td>The request parameters of the operation event. For example, if the operation event is `API service{API service name} creation`, information such as API service name, protocol, description, tag, and version will be displayed here.</td>
</tr>
</tbody></table>

### Step 3. Download logs  
You can download logs on the platform. You can export audit logs in the current list as an .xlsx or .csv file for further analysis or sorting. For detailed fields, see the [log list](#loglist).
Log in to the [iPaaS console](https://console.cloud.tencent.com/ipaas), select **Audit log** on the left sidebar, click the download icon, and select **Export as .xlsx file** or **Export as .csv file**.
![](https://qcloudimg.tencent-cloud.cn/raw/b29579ca86456bddac6450f65a091d02.png)
