## Overview
This document describes how to view the event details in operation records and the field descriptions involved in event details in the CloudAudit console.

## Directions
### Viewing operation record
1. Log in to the CloudAudit console and select **[Operation Record](https://console.cloud.tencent.com/cloudaudit)** on the left sidebar.
2. On the operation record list page, you can view the operation records of an event in the operation record list as shown below:
![](https://main.qcloudimg.com/raw/05997e3350e76763e3efe70e6610307f.png)
The username indicates the event operator. It is divided into three types based on the following operation types:
 - **Operation by a root account**: "root" is displayed as the username.
 - **Operation by a sub-user**: The sub-user name is displayed as the username. If the sub-user has been deleted, the sub-user ID will be displayed as the username.
 - **Operation by a role**: The role name is displayed as the username. If the role has been deleted, the role ID will be displayed as the username.
You can go to the user details page by clicking the username to view more user information.
3. CloudAudit supports many filters, including time, event, username, operation read/write type, sensitive operation, resource name, key ID, request ID, and API error code. You can click **Unfold** and refer to the following to configure filters as needed:
![](https://qcloudimg.tencent-cloud.cn/raw/5272d30d498fee25060b81d83c2ac23d.png)
Filter descriptions:
 - **Time Range**: You can filter logs within a 30-day range in the past 90 days.
 - **Operation Type**: You can filter by all, read, or write.
 - **Resource Event Name**: You can filter desired logs by API name in the API documentation of each product, such as CVM - RunInstances (for instance creation). Up to ten events can be queried at a time.
<dx-alert infotype="explain" title="">
If you can't find a product event name that you want to query in the list, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
</dx-alert>
 - **Username**: You can filter logs by root account, sub-account ID, or role ID.
 - **Sensitive Operation**: You can filter all sensitive and non-sensitive operations. Sensitive operations are defined by the platform as events that may involve key operations on cloud resources. If you need to include certain operations as sensitive operations, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
 - **Resource Name**: You can enter a resource ID for search, such as `ins-fi8oxxxx`.
 - **Key ID**: You can enter a key ID for search, such as `AKIDZ0GSXSG2nT5c6Xxxxxxxxxxxxxxxxx`.
 - **Request ID**: You can enter a request ID for search, such as `a7da0568-7580-4798-88c8-xxxxxxxxxx`.
 - **API Error Code**: You can enter an API error code as listed in the corresponding API documentation for search.
4. Click **Query** to get the filtered operation records.


### Viewing event details
1. If you need to view the details of an event, you can click the information in the list. You can also click `+` before the information and click **View Event** in the expanded module as shown below:
![](https://main.qcloudimg.com/raw/2e0478f26d9f947cb6929467bc20a4d9.png)
<dx-alert infotype="explain" title="">
You can check whether the event was successfully executed through the "CAM Error Code" field. If this field is empty, the event was successfully executed; otherwise, it means the execution failed. For failure details, check the `errorCode` and `errorMessage` fields in the event details.
</dx-alert>
2. Then you can view the event details in the module on the right. For more information on field descriptions, see [Appendix](#appendix).





## Appendix[](id:appendix)
The table below displays the field descriptions of the event details in an operation record.
<table>
<tr>
<th width="20%">Name</th><th width="9%">Type</th>
<th width="32%">Example</th><th width="39%">Description</th>
</tr>
<tr>
<td>userIdentity</td><td><a href="#requester">dict</a></td>
<td>N/A</td><td>Identity information of the requester</td>
</tr>
<tr>
<td>actionType</td><td>String</td>
<td>Read</td><td>The read/write type of a request event</td>
</tr>
<tr>
<td>eventRegion</td><td>String</td>
<td>ap-guangzhou</td><td>Cluster region of a request event</td>
</tr>
<tr>
<td>eventVersion</td><td>int</td>
<td>2</td><td>Log version</td>
</tr>
<tr>
<td>errorCode</td><td>int</td>
<td>0</td><td>Error code that appears when there is an API request error</td>
</tr>
<tr>
<td>errorMessage</td><td>String</td>
<td>N/A</td><td>Error message that appears when there is an API request error</td>
</tr>
<tr>
<td>requestID</td><td>String</td>
<td>be59bbc7-e539-4b14-9d2c-eb7061e61***</td><td>Request ID. Each API request has a request ID.</td>
</tr>
<tr>
<td>apiVersion</td><td>String</td>
<td>3.0</td><td>API version</td>
</tr>
<tr>
<td>eventType</td><td>String</td>
<td>ConsoleCall</td>
<td>
<ul class="params">
<li>ConsoleCall means the request is initiated by the Tencent Cloud console.</li>
<li>ApiCall means the request is initiated by the direct call of TencentCloud API.</li>
</ul>
</td>
</tr>
<tr>
<td>eventTime</td><td>int</td>
<td>2022-04-01 11:30:36</td><td>Event occurrence time (local time at Tencent Cloud International)</td>
</tr>
<tr>
<td>sourceIPAddress</td><td>String</td>
<td>113.*.*.*</td><td>Source IP address</td>
</tr>
<tr>
<td>resourceType</td><td>String</td>
<td>cam</td><td>The requested Tencent Cloud service name</td>
</tr>
<tr>
<td>eventName</td><td>String</td>
<td>GetPolicy</td><td>The requested event name</td>
</tr>
<tr>
<td>eventSource</td><td>String</td>
<td>cam.ap-guangzhou.api.tencentyun.com</td><td>Request source</td>
</tr>
<tr>
<td>requestParameters</td><td>-</td>
<td>N/A</td><td>The requested parameter information</td>
</tr>
<tr>
<td>resourceName</td><td>String</td>
<td>policy/7934***</td><td>The requested resource name</td>
</tr>
</table>


The table below displays the requester's identity descriptions:[](id:requester)
<table>
<tr>
<th width="20%">Name</th><th width="9%">Type</th>
<th width="32%">Example</th><th width="39%">Description</th>
</tr>
<tr>
<td>principalId</td><td>String</td>
<td>100015591***</td>
<td>
Operator information:
<ul class="params">
<li>Operation by a root account: The root account ID</li>
<li>Operation by a sub-user: The sub-user ID</li>
<li>Operation by a role: The role ID</li>
</ul>
</td>
</tr>
<tr>
<td>accountId</td><td>String</td>
<td>100015591***</td><td>Root account ID</td>
</tr>
<tr>
<td>secretId</td><td>String</td>
<td>AKID4IrZ2GV***</td><td>Key ID</td>
</tr>
<tr>
<td>type</td><td>String</td>
<td>root</td>
<td>
<ul class="params">
<li>root: Tencent Cloud root account</li>
<li>CAMuser: Tencent Cloud CAM account ID (or username)</li>
<li>AssumedRole: Tencent Cloud roleUser</li>
</ul>
</td>
</tr>
<tr>
<td>userName</td><td>String</td>
<td>root</td>
<td>
<ul class="params">
<li>root: Tencent Cloud root account</li>
<li>CAMuser: Tencent Cloud CAM account ID (or username)</li>
<li>AssumedRole: Tencent Cloud roleUser</li>
</ul>
</td>
</tr>
<tr>
<td>roleName</td><td>String</td>
<td>SSA_QcsRole</td>
<td>Name of the current role, which needs to be determined together with `type`. <br>If `type` is `AssumedRole` and `userName` is `roleUser`, then `roleName` is the name of the role.
</td>
</tr>
<tr>
<td>sessionContext</td><td>String</td>
<td>N/A</td><td>Error code that appears when there is an API request error</td>
</tr>
</table>

<style>
.params{margin-bottom:0px !important}
</style>
