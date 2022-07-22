NAT Gateway provides the flow log collection feature to collect and analyze NAT Gateway traffic and generate logs and analysis charts. This helps you stay informed of cross-region communication and quickly locate and solve problems based on the logs, thus improving the business availability and Ops efficiency.
>?
>+ The flow log feature is in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>+ The Flow Log service is free of charge, but the data stored in CLS will be [charged at the standard prices](https://intl.cloud.tencent.com/document/product/614/37509) of CLS.
>+ The flow log data is stored in CLS. Make sure that you have [granted the Flow Log service permissions to access CLS](https://intl.cloud.tencent.com/document/product/682/47040) before querying log data in CLS.
>

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **Flow Logs** > **Log List** in the left sidebar.
2. Select the region in the top-left corner of the **Flow Logs** page and click **+Create**.
3. Configure the following parameters in the **Create flow log** window.</br>
<img src="" width="60%">
<table>
<tr>
<th width="15%">Field</th>
<th>Description</th>
</tr>
<tr>
<td>Name</td>
<td>The name of the flow log.</td>
</tr>
<tr>
<td>Collection range</td>
<td>Select “NAT Gateway”.</td>
</tr>
<tr>
<td>NAT gateway</td>
<td>The information about the NAT gateway.</td>
</tr>
<tr>
<td>Collection type</td>
<td>Specify the type of traffic to be collected by the flow log: All traffic, or the traffic rejected or accepted by security groups or ACL.</td>
</tr>
<tr>
<td>Logset</td>
<td>Specify the storage location in CLS for flow logs. If you already have a logset, select it directly; otherwise, keep **Created by system** selected, so that the system will create one for you. You can also click <b>Create</b> to create one in the CLS console.</td>
</tr>
<tr>
<td>Log topic</td>
<td>Specify the minimum dimension of log storage, which is used to distinguish between different types of logs, such as `Accept` log. If you already have a log topic, select it directly; otherwise, keep **Created by system** selected, so that the system will create one for you. You can also go to the CLS console to create one.
<p>
<dx-alert infotype="explain" title="">
For more information on how to configure a logset, log topic, and index, see <a href="https://intl.cloud.tencent.com/document/product/682/18967">Creating Logsets and Log Topics</a>.
</dx-alert>
</td>
</tr>
<tr>
<td>Tag key</td>
<td>Click <b>Advanced options</b> to enter or select a tag key for the identification and management of the flow log.</td>
</tr>
<tr>
<td>Tag value</td>
<td>Click <b>Advanced options</b> to enter or select a tag value. It can also be left empty.</td>
</tr>
</table>
4. Click **OK**.
   <dx-alert infotype="explain" title="">
You can view the record of a newly created flow log in CLS after six minutes upon the creation (one minute for the capture window and five minutes for data publishing).
</dx-alert>
5. After about six minutes, click **Storage location** or **View** to enter the **Search and analysis** page of the CLS service, select the region and time period for which to view logs, and click **Search and analyze** to view the logs.
    ![]()
	Below are sample logs:
![]()
>?For fields description, see [Flow Log Record](https://intl.cloud.tencent.com/document/product/682/18933). For log analysis, see [Quick Analysis](https://intl.cloud.tencent.com/document/product/614/42002).
