After creating a flow log for an ENI, you can store and analyze the network traffic in real time, making the Flow Logs service fit for troubleshooting, compliance audit, security test and other use cases. This document describes how to create a flow log over the private network.

## Prerequisites
- The FL service is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Ensure that the CVMs are included in the FL’s [supported list](https://intl.cloud.tencent.com/document/product/682/18934).
- You have created a log topic as instructed in [Adding Log Topic](https://intl.cloud.tencent.com/document/product/614/34239).

## Background
CVM A (10.16.0.22) and CVM B (10.16.0.40) reside in the same VPC. After you log in to the CVM A and run the `ping` command to connect to the CVM B, the CVM A will receive the following response. If a flow log is created for the ENI on the CVM A, the flow log also records the response to the ping operation.
![](https://main.qcloudimg.com/raw/67866dca42fa8356b23eaf60e8bf876b.png)

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Diagnostic Tools** > **Flow Log** on the left sidebar.
2. In the upper-left corner of the **Flow Log** page, choose the target region. Click **+New** and configure the following parameters in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/7357cc77440d826478bd35716283eddb.png)
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for the flow log to be created.</td>
</tr>
<tr>
<td>Collection Range</td>
<td>Only <b>ENI</b> is supported currently.</td>
</tr>
<tr>
<td>Virtual Private Cloud</td>
<td>Select the VPC where the source CVM resides.</td>
</tr>
<tr>
<td>Subnet</td>
<td>Select the subnet where the source CVM resides.</td>
</tr>
<tr>
<td>Collection Type</td>
<td>Select the type of traffic to be collected by the flow log: all traffic, or the traffic rejected or accepted by security groups or ACL.</td>
</tr>
<tr>
<td>Log set</td>
<td>Select a log set that specifies the storage location in CLS for the flow log. You can also click <b>Create</b> to add a logset in the CLS console.</td>
</tr>
<tr>
<td>Log topic</td>
<td>Select a log topic that specifies the minimum dimension of log storage, which is used to distinguish log types, such as <code>Accept </code> log. You can go to the CLS console to add a log topic.</td>
</tr>
<tr>
<td>Tag key</td>
<td>Enter or select a tag key for the identification and management of the flow log.</td>
</tr>
<tr>
<td>Tag value</td>
<td>Enter or select a key value, or leave it empty.</td>
</tr>
</table>
3. Click **OK**.
>!
 - You can view the record of a newly created flow log in CLS after 15 minutes upon the creation (10 minutes for the capture window and 5 minutes for data publishing).
 - FL is free of charge, but the data stored in CLS is charged at standard prices.

## Result Validation
After 15 minutes, locate the flow log you’ve created on the **Flow Log** page and click **Check** in the **Operation** column to access the **Search and Analysis** page. Select a time range and search for the IP of the CVM B. The result is the same as the response received by the CVM A.
![](https://main.qcloudimg.com/raw/26fd7de53cea591b26169319ab31834d.png)


