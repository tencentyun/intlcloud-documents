## Overview
This document describes how to view the event details in operation records and the field descriptions involved in event details in the CloudAudit console.

## Directions
### Viewing operation record
1. Log in to the CloudAudit console and select **[Operation Record](https://console.cloud.tencent.com/cloudaudit)** on the left sidebar.
2. On the operation record list page, you can view the operation records of an event in the operation record list.
![](https://main.qcloudimg.com/raw/05997e3350e76763e3efe70e6610307f.png)
The operator indicates the event operator. It is divided into three types based on the following operation types:
 - **Operation by a root account**: The name “root” is displayed as the operator.
 - **Operation by a sub-user**: The sub-user name is displayed as the operator. If the sub-user has been deleted, the sub-user ID will be displayed instead.
 - **Operation by a role**: The role name is displayed as the operator. If the role has been deleted, the role ID will be displayed as the operator.
You can click an operator to go to the **User List** page in the CAM console to view the detailed user information.
3. CloudAudit supports many filters, including time, event, username, operation read/write type, sensitive operation, resource tag, resource name, key ID, request ID, and API error code. You can click **Unfold** and configure filters as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/5272d30d498fee25060b81d83c2ac23d.png)
Filter descriptions:
 - **Time Range**: You can filter logs within a 30-day range in the past 90 days.
 - **Operation Type**: You can filter by **All**, **Read-only**, or **Write-only**.
 - **Resource Event Name**: You can filter desired logs by API name in the API documentation of each product, such as CVM - RunInstances (for instance creation). Up to ten events can be queried at a time.
<dx-alert infotype="explain" title="">
If you can't find a product event name that you want to query in the list, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
</dx-alert>
 - **Username**: You can filter logs by root account, sub-account ID, or role ID.
 - **Operation Query**: You can filter all sensitive and non-sensitive operations. Sensitive operations are defined by the platform as events that may involve key operations on cloud resources. If you need to include certain operations as sensitive operations, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
 - **Resource Tag**: You can filter logs by resource tag. For more information on tags, see [ Tag Overview](https://intl.cloud.tencent.com/document/product/651/13334).
 - **Resource Name**: You search by resource ID, such as `ins-fi8oxxxx`.
 - **Key ID**: You can search by key ID, such as `AKIDZ0GSXSG2nT5c6Xxxxxxxxxxxxxxxxx`.
 - **Request ID**: You can search by request ID, such as `a7da0568-7580-4798-88c8-xxxxxxxxxx`.
 - **API Error Code**: You can enter an API error code as listed in the corresponding API documentation for search.
4. Click **Query** to get the filtered operation records.


### Viewing event details
1. If you need to view the details of an event, you can click the information in the list. You can also click the `+` icon before the information and click **View Event** in the expanded module.
![](https://main.qcloudimg.com/raw/2e0478f26d9f947cb6929467bc20a4d9.png)
<dx-alert infotype="explain" title="">
You can check whether the event was successfully executed through the “CAM Error Code” field. If this field is empty, the event was successfully executed; otherwise, it means the execution failed. For failure details, check the `errorCode` and `errorMessage` fields in the event details.
</dx-alert>
2. Then you can view the event details in the module on the right. For more information on field descriptions, see [Appendix](#appendix).





## Appendix[](id:appendix)
The table below displays the field descriptions of the event details in an operation record.
<table>
<thead>
<tr>
<th width="20%">Name</th><th width="9%">Type</th>
<th width="32%">Example</th><th width="39%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">userIdentity</td>
<td align="left"><a href="#requester">dict</a></td>
<td align="left">N/A</td>
<td align="left">Identity information of the requester</td>
</tr>
<tr>
<td align="left">eventRegion</td>
<td align="left">String</td>
<td align="left">ap-guangzhou</td>
<td align="left">Cluster region of the requested Tencent Cloud service</td>
</tr>
<tr>
<td align="left">eventVersion</td>
<td align="left">int</td>
<td align="left">2</td>
<td align="left">Event version</td>
</tr>
<tr>
<td align="left">errorCode</td>
<td align="left">int</td>
<td align="left">0</td>
<td align="left">Error code returned when an error occurred while requesting the signature or authentication</td>
</tr>
<tr>
<td align="left">errorMessage</td>
<td align="left">String</td>
<td align="left">N/A</td>
<td align="left">Error message returned when an error occurred while requesting the signature or authentication</td>
</tr>
<tr>
<td align="left">requestID</td>
<td align="left">String</td>
<td align="left">be59bbc7-e539-4b14-9d2c-eb7061e61***</td>
<td align="left">Request ID, which is the ID of each API request</td>
</tr>
<tr>
<td align="left">eventID</td>
<td align="left">String</td>
<td align="left">e2c8694c-12e6-4da9-a1e1-48bb703c0892</td>
<td align="left">Event ID, which is the event GUID generated by CloudAudit</td>
</tr>
<tr>
<td align="left">apiVersion</td>
<td align="left">String</td>
<td align="left">3.0</td>
<td align="left">API version</td>
</tr>
<tr>
<td align="left">eventType</td>
<td align="left">String</td>
<td align="left">ConsoleCall</td>
<td align="left">Source type of the event request. Valid values:
<ul style="margin-bottom:0px">
<li>ConsoleCall: The request is initiated by the Tencent Cloud console.</li>
<li>ApiCall: The request is initiated by the direct call of TencentCloud API.</li>
<li>MiniProgramCall: The request is initiated by the Tencent Cloud Assistant mini program.</li>
</ul>
</td>
</tr>
<tr>
<td align="left">actionType</td>
<td align="left">String</td>
<td align="left">Read</td>
<td align="left">Read/write type of the request event. Valid values:
<ul style="margin-bottom:0px">
<li>Write: Write</li>
<li>Read: Read</li>
</ul>
</td>
</tr>
<tr>
<td align="left">apiErrorCode</td>
<td align="left">int</td>
<td align="left">0</td>
<td align="left">Error code returned for an API request error</td>
</tr>
<tr>
<td align="left">apiErrorMessage</td>
<td align="left">String</td>
<td align="left">N/A</td>
<td align="left">Error message returned for an API request error</td>
</tr>
<tr>
<td align="left">userAgent</td>
<td align="left">String</td>
<td align="left">SDK_GO_1.0.374</td>
<td align="left">The client proxy that sends the API request</td>
</tr>
<tr>
<td align="left">eventTime</td>
<td align="left">int</td>
<td align="left">2022-04-01 11:30:36</td>
<td align="left">Event occurrence time</td>
</tr>
<tr>
<td align="left">sensitiveAction</td>
<td align="left">int</td>
<td align="left">0</td>
<td align="left">Whether the event is a sensitive operation. Valid values:
<ul style="margin-bottom:0px">
<li>1: Sensitive operation</li>
<li>0: Non-sensitive operation</li>
</ul>
</td>
</tr>
<tr>
<td align="left">eventPlatform</td>
<td align="left">int</td>
<td align="left">0</td>
<td align="left">Whether the event is a platform event. Valid values:
<ul style="margin-bottom:0px">
<li>1: Platform event</li>
<li>0: Non-platform event</li>
</ul>
</td>
</tr>
<tr>
<td align="left">sourceIPAddress</td>
<td align="left">String</td>
<td align="left">113.<em>.</em>.*</td>
<td align="left">Source IP address</td>
</tr>
<tr>
<td align="left">resourceType</td>
<td align="left">String</td>
<td align="left">cam</td>
<td align="left">The requested Tencent Cloud service name</td>
</tr>
<tr>
<td align="left">eventName</td>
<td align="left">String</td>
<td align="left">GetPolicy</td>
<td align="left">The requested event name</td>
</tr>
<tr>
<td align="left">eventSource</td>
<td align="left">String</td>
<td align="left">cam.ap-guangzhou.api.tencentyun.com</td>
<td align="left">Request source</td>
</tr>
<tr>
<td align="left">requestParameters</td>
<td align="left">-</td>
<td align="left">N/A</td>
<td align="left">Input parameters of the request</td>
</tr>
<tr>
<td align="left">requestElements</td>
<td align="left">-</td>
<td align="left">N/A</td>
<td align="left">Response information of the request</td>
</tr>
<tr>
<td align="left">resources</td>
<td align="left">String</td>
<td align="left">qcs:id/0:cos:ap-shanghai:uid/1252081001:prefix//1252081001/pdd-open-api/images/2018-07-02/6cff3fee97bbf0d2c930fb4ddd5658c4.jpeg</td>
<td align="left">Resource information of the event, which is the value of the `qcs` segment in the six-segment resource description.</td>
</tr>
<tr>
<td align="left">resourceName</td>
<td align="left">String</td>
<td align="left">policy/7934***</td>
<td align="left">Resource name of the event</td>
</tr>
<tr>
<td align="left">tags</td>
<td align="left">String</td>
<td align="left">{"key":"projectId","value":"0"}</td>
<td align="left">Resource tag</td>
</tr>
</tbody></table>

The table below displays the requester’s identity descriptions.
<table>
<tr>
<th width="20%">Name</th><th width="9%">Type</th>
<th width="32%">Example</th><th width="39%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">principalId</td>
<td align="left">String</td>
<td align="left">100015591***</td>
<td align="left">Operator account ID. Valid values:
<ul  class="params">
<li>Operation by a root account: The root account ID</li>
<li>Operation by a sub-user: The sub-user ID</li>
<li>Operation by a role: The role ID</li>
</ul>
</td>
</tr>
<tr>
<td align="left">accountId</td>
<td align="left">String</td>
<td align="left">100015591***</td>
<td align="left">ID of the root account to which the operator belongs</td>
</tr>
<tr>
<td align="left">secretId</td>
<td align="left">String</td>
<td align="left">AKID4IrZ2GV***</td>
<td align="left">Key ID of the operator</td>
</tr>
<tr>
<td align="left">type</td>
<td align="left">String</td>
<td align="left">root</td>
<td align="left">Operator type. Valid values:
<ul  class="params">
<li>root: Tencent Cloud CAM root account</li>
<li>user: Tencent Cloud CAM account ID (or username)</li>
<li>AssumedRole: Tencent Cloud role (roleUser)</li>
</ul>
</td>
</tr>
<tr>
<td align="left">userName</td>
<td align="left">String</td>
<td align="left">root</td>
<td align="left">Operator name</td>
</tr>
<tr>
<td align="left">sessionContext</td>
<td align="left">String</td>
<td align="left">N/A</td>
<td align="left">Error code returned for an API request error</td>
</tr>
</tbody></table>

<style>
.params{margin-bottom:0px !important}
</style>
