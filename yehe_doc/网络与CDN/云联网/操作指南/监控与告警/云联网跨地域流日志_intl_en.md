CCN provides the flow log collection feature to collect and analyze cross-region traffic and generate logs and analysis charts. This helps you stay informed of cross-region communication and quickly locate and solve problems based on the logs, thus improving the business availability and Ops efficiency.
>?
>+ The flow log feature is in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>+ The Flow Log service is free of charge, but the data stored in CLS will be [charged at the standard prices](https://intl.cloud.tencent.com/document/product/614/37509) of CLS.
>+ As flow log data is stored in CLS, make sure that you have granted CLS access to Flow Logs.
>

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Diagnostic Tools** > **Flow Logs** on the left sidebar.
2. Select the region in the top-left corner of the **Flow Logs** page and click **+Create**.
3. Configure the following parameters in the **Create Flow Log** window.
<img src="" width="80%">
<table>
<tr>
<th width="12%">Field</th>
<th>Description</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for the flow log to be created.</td>
</tr>
<tr>
<td>Collection Range</td>
<td>Multiple collection ranges are supported currently. <b>Cross-region CCN traffic</b> is selected here.</td>
</tr>
<tr>
<td>CCN</td>
<td>CCN instance ID.</td>
</tr>
<tr>
<td>Collection Type</td>
<td>Select the type of traffic to be collected by the flow log: all traffic, or the traffic rejected or accepted by security groups or ACL.</td>
</tr>
<tr>
<td>Logset</td>
<td>Specify the storage location in CLS for flow logs. If you already have a logset, select it directly; otherwise, keep <b>Created by System</b> selected, so that the system will create one for you. You can also click <b>Create</b> to create one in the CLS console.</td>
</tr>
<tr>
<td>Log Topic</td>
<td>Specify the minimum dimension of log storage, which is used to distinguish between different types of logs, such as `Accept` log. If you already have a log topic, select it directly; otherwise, keep <b>Created by System</b>  selected, so that the system will create one for you. You can also go to the CLS console to create one.
<p><b>Note</b>: For more information on how to configure a logset, log topic, and index, see <a href="https://intl.cloud.tencent.com/document/product/682/18967">Creating Logsets and Log Topics</a>.
</td>
</tr>
<tr>
<td>Tag Key</td>
<td>Click <b>Advanced Options</b> to enter or select a tag key for the identification and management of flow logs.</td>
</tr>
<tr>
<td>Tag Value</td>
<td>Click <b>Advanced Options</b> to enter or select a tag value. It can also be left empty.</td>
</tr>
</table>
4. Click **OK**.
   <dx-alert infotype="explain" title="">
You can view the record of a newly created flow log in CLS after six minutes upon the creation (one minute for the capture window and five minutes for data publishing).
</dx-alert>
5. After about six minutes, click **Storage Location** or **View** to enter the **Search and Analysis** page of the CLS service, select the region and time period for which to view logs, and click **Search and Analyze** to view the logs.
    ![]()
>?For field descriptions, see [Appendix](#appendix). For more information on log analysis, see [Quick Analysis](https://intl.cloud.tencent.com/document/product/614/42002).

 

 ## Appendix

### Flow log records of cross-region CCN traffic[](id:appendix)
The flow logs of cross-region CCN traffic record the network flows filtered by the "quintuple + traffic source region + traffic destination region" rule in a specific capture window; that is, only flow logs that meet the rule in the capture window can be recorded as flow logs of cross-region CCN traffic.
- **Quintuple + traffic source region + traffic destination region**
  - A quintuple refers to a collection of five values: source IP address, source port, destination IP address, destination port, and transport layer protocol.
  - The traffic source region refers to the region from which cross-region CCN traffic is sent.
  - The traffic destination region refers to the region to which cross-region CCN traffic arrives.
- **Capture window**
It refers to a time period of one minute, during which FL aggregates data and takes about five minutes to publish the flow log records. Flow log records are strings separated with spaces in the following format:
`srcaddr dstregionid dstport start dstaddr version packets ccnid protocol srcregionid bytes action region-id srcport end log-status`

| Field | Data Type | Description |
|---------| |---------|
|srcaddr |text | Source IP. |
|dstregionid | text | Traffic destination region. |
|dstport | long | Traffic destination port. This field will take effect only for UDP/TCP protocols and will be displayed as "-" for other protocols. |
|start | long | The timestamp when the first packet is received in the current capture window. If there are no packets in the capture window, it will be displayed as the start time of the capture window in Unix seconds. |
|dstaddr | text| Destination IP. |
|version | text | Flow log version. |
|packets |long | Number of packets transferred in the capture window. This field will be displayed as "-" when `log-status` is `NODATA`. |
|ccnid |text  | Unique CCN instance ID. To get the information of your CCN instance, [contact us](https://intl.cloud.tencent.com/document/product/1003/41737). |
|protocol | long | IANA protocol number of the traffic. For more information, see [Assigned Internet Protocol Numbers](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml#protocol-numbers-1). |
|srcregionid | text | Traffic source region. |
|bytes | long | Number of bytes transferred in the capture window. This field will be displayed as "-" when `log-status` is `NODATA`. |
|action | text	 | Operation associated with the traffic:<br/> ACCEPT: Cross-region traffic normally forwarded over CCN.<br/>  REJECT: Cross-region traffic prevented from being forwarded due to traffic throttling. |
|region-id | text| Region where logs are recorded. |
|srcport |text  | Traffic source port. This field will take effect only for UDP/TCP protocols and will be displayed as "-" for other protocols. |
|end | long | The timestamp when the last packet is received in the current capture window. If there are no packets in the capture window, it will be displayed as the end time of the capture window in Unix seconds. |
|log-status | text | Logging status of the flow log. Valid values:<br>OK: Data is normally logged to the specified destination.<br/>NODATA: There was no inbound or outbound network flow in the capture window, in which case both the `packets` and `bytes` fields will be displayed as `-1`. |


 ## FAQs

 ### How do I view flow logs between specified regions?
If the flow log feature is enabled in the Shanghai region, all outbound traffic from Shanghai and inbound traffic to Shanghai will be collected. To collect the flow logs between two regions, you can filter out the expected flow logs by `srcregion` and `dstregion` in CLS. For more information, see [Context Search and Analysis](https://intl.cloud.tencent.com/document/product/614/39795).


