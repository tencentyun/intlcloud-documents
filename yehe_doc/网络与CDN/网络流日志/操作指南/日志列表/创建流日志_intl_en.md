This document describes how to create a flow log policy to collect flow logs of ENIs, NAT gateway and CCN cross-region connections.
>? The FL service for NAT gateway and CCN cross-region connections is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Prerequisites
+ You have created a logset and log topic:
  + The Advanced analysis dashboard is only available for “flowlog_logset” logsets marked with “Flowlog” and the log topics under them. For more information, see [Configuring Logsets and Log Topics](https://intl.cloud.tencent.com/document/product/682/47038).
  + If you do not use the advanced analysis dashboard, you can select any logset and log topic. You can [Create Logsets and Log Topics](https://intl.cloud.tencent.com/document/product/682/18967) without the “Flowlog” mark via the CLS console, or [Configure Logsets and Log Topics](https://intl.cloud.tencent.com/document/product/682/47038) with the “Flowlog” mark via the FL console.


## Directions

### Creating a flow log policy
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Flow Log** > **Flow Log** in the left sidebar.
2. In the upper-left corner of the **Flow Logs** page, choose the target region. Click **+ New** and configure the following parameters in the pop-up dialog box.
<img src="" width="70%">
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>The name of the flow log policy.</td>
</tr>
<tr>
<td>Collection range</td>
<td>This specifies the collection range of the flow log policy. ENI, NAT gateway and CCN are supported.</td>
</tr>
<tr>
<td>VPC</td>
<td>The VPC where the flow logs are collected.</td>
</tr>
<tr>
<td>Subnet</td>
<td>The subnet where the flow logs are collected.</td>
</tr>
<tr>
<td>Collection type</td>
<td>This specifies the type of traffic to be collected by the flow log: All traffic, or the traffic rejected or accepted by security groups or ACL.</td>
</tr>
<tr>
<td>Logset</td>
<td>This specifies the storage location in CLS for the flow log.<p>
</td>
</tr>
<tr>
<td>Log topic</td>
<td>This specifies the minimum dimension of log storage, which is used to distinguish log types, such as “Accept” log.</td>
</tr>
<tr>
<td>Tag key</td>
<td>An optional parameter. You can create a tag key or select an existing one. It is used for locating and managing flow logs.</td>
</tr>
<tr>
<td>Tag value</td>
<td>An optional parameter. You can create a tag value or select an existing one. You can also leave it empty.</td>
</tr>
</table>
3. Click **OK**.
<dx-alert infotype="notice" title="">
 - You can view the record of a newly created flow log in CLS after several minutes upon the creation (for example, for a flow log of an ENI, 5 minutes for the capture window and 5 minutes for data publishing).
 - FL service is free of charge, but your need to pay for the data stored in CLS. See [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509).
</dx-alert>

### Viewing log information
1. About 10 minutes after the flow log is created, click **View** at the right of the target flow log to enter the **Search and analysis** page in CLS.
    ![]()
2. On this page, you can select the region, logset, log topic and time. You can also customize the filter conditions. Click **Search and analysis** to query the log information under specified conditions.
>! Click **Index configuration** to confirm that the index has been enabled. If it is disabled, you are unable to search the collected log data.
>
 ![]()
