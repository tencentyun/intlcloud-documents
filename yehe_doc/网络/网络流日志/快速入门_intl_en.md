After a flow log is created for the ENI, you can store and analyze the network traffic in real time, making FL fit for troubleshooting, compliance audit, security and other use cases. This document describes how to create a flow log in the private network.

## Prerequisites
- The FL service is currently in beta. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Ensure that the CVM is included in the FL’s [supported list](https://intl.cloud.tencent.com/document/product/682/18934).
- You have created a logset and log topic. For more information on how to add a logset and log topic, please see [Logset Actions](https://intl.cloud.tencent.com/document/product/614/34238) and [Log Topic Actions](https://intl.cloud.tencent.com/document/product/614/34239).

## Background
CVM A (10.16.0.22) and CVM B (10.16.0.40) reside in the same VPC. If you log in to the CVM A and run the ping command to connect the CVM B, the CVM A will receive the following response. If a flow log is created for the ENI on the CVM A, the flow log also records the response to the ping operation.
![](https://main.qcloudimg.com/raw/67866dca42fa8356b23eaf60e8bf876b.png)

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Diagnostic Tools** -> **Flow Log** in the left sidebar.
2. At the top left of the **Flow Log** page, choose the region where you want to create a flow log. Click **+New** and configure the following parameters in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/b8c6d0e2ed450622f9ef00922cfbfc8e.png)
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>The name of the flow log to be created</td>
</tr>
<tr>
<td>Collection Range</td>
<td>Only **ENI** is supported currently</td>
</tr>
<tr>
<td>VPC</td>
<td>VPC where the source CVM resides</td>
</tr>
<tr>
<td>Subnet</td>
<td>Subnet where the source CVM resides</td>
</tr>
<tr>
<td>Collection Type</td>
<td>Specifies the type of traffic to be collected by the flow log: all traffic, or the traffic rejected or accepted by security groups or ACL.</td>
</tr>
<tr>
<td>Logset</td>
<td>Specifies the storage location in CLS for flow logs. Select an existing logset, or click **Create** to add a logset in the CLS console.</td>
</tr>
<tr>
<td>Log topic</td>
<td>Specifies the minimum dimension of log storage, which is used to distinguish log types, such as `Accept` log. Select an existing log topic, or go to the CLS console to add a log topic.</td>
</tr>
<tr>
<td>Tag key</td>
<td>You can enter or select a tag key for the identification and management of the flow log.</td>
</tr>
<tr>
<td>Key value</td>
<td>You can enter or select a key value, or leave it empty.</td>
</tr>
</table>
3. Click **OK**.
>!
>- You can view the record of a newly created flow log in CLS after 15 minutes upon the creation (10 minutes for the capture window and 5 minutes for data publishing).
>- FL is free of charge, but the data stored in CLS is charged at standard prices.

## Result Validation
After 15 minutes, locate the flow log you’ve created on the **Flow Log** page and click **Check** to access the **Search Analysis** page. Select a time range and enter the IP of the CVM B in the search bar to search. The result is the same as the response received by the CVM A.

