This document describes how to create a flow log for an ENI in the private network. After a flow log is created for the ENI, you can store and analyze the network traffic in real time, making it fit for troubleshooting, compliance audit, security and other use cases.


## Prerequisite
- Ensure that the CVMs are included in the FL's [Supported List](https://intl.cloud.tencent.com/document/product/682/18934).
- As the flow log data needs to be delivered to CLS, ensure that the CLS authorization has been completed before viewing the log data. For detailed directions, see [Granting FL Access to CLS](https://intl.cloud.tencent.com/document/product/682/47040).
- You have created a log topic as instructed in [Creating a log topic](https://intl.cloud.tencent.com/document/product/614/34239).

## Background
CVM A (10.16.0.22) and CVM B (10.16.0.40) reside in the same VPC. After you log in to the CVM A and run the `ping` command to connect to the CVM B, the ENI will be triggered to generate traffic. If a flow log is created for the ENI of the CVM A, the flow log also records the traffic data.
![](https://main.qcloudimg.com/raw/67866dca42fa8356b23eaf60e8bf876b.png)

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Flow Logs** > **Log List** on the left sidebar.
2. In the upper-left corner of the **Flow Logs** page, choose the target region. Click **+Create** and configure the following parameters in the pop-up dialog box.
<img src="" width="70%">
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Configuration</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for the flow log to be created.</td>
</tr>
<tr>
<td>Collection Range</td>
<td>Specify the flow log collection range. In this example, select ENI.</td>
</tr>
<tr>
<td>VPC</td>
<td>The VPC where the ENI is located. In this example, select the VPC of CVM A.</td>
</tr>
<tr>
<td>Subnet</td>
<td>The subnet where the ENI is located. In this example, select the subnet of CVM A.</td>
</tr>
<tr>
<td>Collection Type</td>
<td>Select the type of traffic to be collected by the flow log: all traffic, or the traffic rejected or accepted by security groups or ACL. In this example, select **Accepted**.</td>
</tr>
<tr>
<td>Logset</td>
<td>Select a logset that specifies the storage location in CLS for the flow log. You can also click <b>Create</b> to add a logset in the CLS console.</td>
</tr>
<tr>
<td>Log topic</td>
<td>Select a log topic that specifies the minimum dimension of log storage, which is used to distinguish log types, such as <code>Accept </code> log. You can go to the CLS console to add a log topic.</td>
</tr>
<tr>
<td>Tag key</td>
<td>Enter or select an optional tag key for the identification and management of the flow log.</td>
</tr>
<tr>
<td>Tag value</td>
<td>Enter or select an optional tag value. It can also be a null value.</td>
</tr>
</table>
3. Click **Confirm**.
<dx-alert infotype="notice" title="">
 - You can view the record of a newly created flow log in CLS after 10 minutes upon the creation (5 minutes for the capture window and 5 minutes for data publishing).
 - FL is free of charge, but the data stored in CLS is charged at standard prices.
</dx-alert>


## Result Validation
After 10 minutes, locate the flow log you’ve created on the **Flow Logs** page and click **Check** in the **Operation** column to access the **Search and Analysis** page. Select a time range and search for the IP of the CVM B.
![]()