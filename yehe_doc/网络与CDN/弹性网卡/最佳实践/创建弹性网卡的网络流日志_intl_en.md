[Flow Logs](https://intl.cloud.tencent.com/document/product/682/18931) provides a full-time, full-flow and non-intrusive traffic collection service. It enables you to store and analyze the collected network traffic in real time for troubleshooting, compliance auditing, architecture optimization, and security detection.

You can create a flow log for an ENI to collect the inbound/outbound traffic. The collected traffic will be stored and analyzed in Tenceng Cloud CLS. This document describes how to create a flow log for an ENI.


## Prerequisites
- The CVM to which the ENI is bound is supported by Flow Logs. See [Supported List](https://intl.cloud.tencent.com/document/product/682/18934).
- You have granted permissions to FL to access CLS.
- You have created a log topic. See [Creating a Log Topic](https://intl.cloud.tencent.com/document/product/614/34239).

## Sample Case
CVM A (10.16.0.22) and CVM B (10.16.0.40) reside in the same VPC. After you log in to the CVM A and run the `ping` command to the CVM B, the ENIs on both CVMs will be triggered to generate traffic. If a flow log is created for the ENI on CVM A, the flow log also records the traffic.
![](https://main.qcloudimg.com/raw/67866dca42fa8356b23eaf60e8bf876b.png)

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Flow Logs** > **Log List** in the left sidebar.
2. In the upper-left corner of the **Flow Logs** page, choose the target region. Click **+ New** and complete the configuration.
![]()
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>The name of the flow log.</td>
</tr>
<tr>
<td>Collection range</td>
<td>This specifies the collection range of the flow log. Select "ENI" in this example.</td>
</tr>
<tr>
<td>VPC</td>
<td>The VPC where the ENI resides. Select the VPC of CVM A in this example.</td>
</tr>
<tr>
<td>Subnet</td>
<td>The subnet where the ENI resides. Select the subnet of CVM A in this example.</td>
</tr>
<tr>
<td>Collection type</td>
<td>This specifies the type of traffic to be collected by the flow log: All traffic, or the traffic rejected or accepted by security groups or ACL. Select "Accept" in this example.</td>
</tr>
<tr>
<td>Logset</td>
<td>This specifies the storage location in CLS for the flow log. Please select an existing logset. You can also click <b>Create</b> to add a logset in the CLS console.</td>
</tr>
<tr>
<td>Log topic</td>
<td>This specifies the minimum dimension of log storage, which is used to distinguish log types, such as <code>Accept</code> log. You can go to the CLS console to add a log topic.</td>
</tr>
<tr>
<td>Tag key</td>
<td>(Optional) It is used for locating and managing flow logs. You can create a tag key or select an existing one. </td>
</tr>
<tr>
<td>Tag value</td>
<td>(Optional) You can create a tag value, select an existing one, or just leave it empty.</td>
</tr>
</table>
3. Click **OK**.
<dx-alert infotype="notice" title="">
 - For the first creation of a flow log, it takes about 10 minutes before you can see he logs in the CLS console.
 - The Flow Logs service is free of charge, but you need to pay for the data stored in CLS.
</dx-alert>


## Result Validation
After 10 minutes, locate the flow log you’ve created on the **Flow logs** page and click **View** in the **Operation** column to access the **Search and analysis** page. Select a time range and search for the IP of the CVM B.
![]()