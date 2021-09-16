## Overview
This document describes how to view the event details in operation records and the field descriptions involved in event details in the CloudAudit console.

## Directions
### Viewing operation record
1. Log in to the CloudAudit console and select **[Operation Record](https://console.cloud.tencent.com/cloudaudit)** on the left sidebar.
2. On the operation record list page, you can view the operation records of an event in the operation record list as shown below:
![](https://main.qcloudimg.com/raw/05997e3350e76763e3efe70e6610307f.png)
The username indicates the event operator. It is divided into three types according to the following operation types:
 - **Operation by a root account**: "root" is displayed as the username.
 - **Operation by a sub-user**: the sub-user name is displayed as the username. If the sub-user has been deleted, the sub-user ID will be displayed as the username.
 - **Operation by a role**: the role name is displayed as the username. If the role has been deleted, the role ID will be displayed as the username.
To view more information of a user, you can click the username to go to the user details page.

### Viewing event details
1. If you need to view the details of an event, you can click the information in the list. You can also click `+` before the information and click **View Event** in the expanded module as shown below:
![](https://main.qcloudimg.com/raw/2e0478f26d9f947cb6929467bc20a4d9.png)
2. Then, you can view the event details in the module on the right. For more information on field descriptions, please see [Appendix](#appendix).



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
<td>ap-guangzhou</td><td>Event region</td>
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
<li>ApiCall means the request is initiated by the direct call of cloud APIs.</li>
</ul>
</td>
</tr>
<tr>
<td>eventTime</td><td>int</td>
<td>1621411761</td><td>The time when an event occurs (timestamp)</td>
</tr>
<tr>
<td>sourceIPAddress</td><td>String</td>
<td>113.*.*.*</td><td>Source IP address</td>
</tr>
<tr>
<td>resourceType</td><td>String</td>
<td>cam</td><td>Tencent Cloud service name in the request</td>
</tr>
<tr>
<td>eventName</td><td>String</td>
<td>GetPolicy</td><td>Event name in the request</td>
</tr>
<tr>
<td>eventSource</td><td>String</td>
<td>cam.ap-guangzhou.api.tencentyun.com</td><td>Request source</td>
</tr>
<tr>
<td>requestParameters</td><td>-</td>
<td>N/A</td><td>Parameter information of the request</td>
</tr>
<tr>
<td>resourceName</td><td>String</td>
<td>policy/7934***</td><td>Resource in the request</td>
</tr>
</table>

The table below displays the requester's identity descriptions.
<table>
<tr>
<th width="20%">Name</th><th width="9%">Type</th>
<th width="32%">Example</th><th width="39%">Description</th>
</tr>
<tr>
<td>principalId</td><td>String</td>
<td>100015591***</td>
<td>
<ul class="params">
Operator information:
<li>Operation by a root account: the root account ID</li>
<li>Operation by a sub-user: the sub-user ID</li>
<li>Operation by a role: the role ID</li>
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
<td>sessionContext</td><td>String</td>
<td>N/A</td><td>Error code that appears when there is an API request error</td>
</tr>
</table>

<style>
.params{margin-bottom:0px !important}
</style>
