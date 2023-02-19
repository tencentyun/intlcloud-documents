CLB supports storing health check logs to CLS where you can view the logs, reporting at a minute granularity and querying online by multiple rules, helping you identify the causes of health check failures.

<dx-alert infotype="explain" title="">
The health check logging feature is currently in beta test. To try it out, [submit a ticket](https://console.tencentcloud.com/workorder/category).
</dx-alert>

Health check logging includes log reporting, storage and query:
- Log reporting: Processes service forwarding first, and then log reporting.
- Log storage and query: Provides SLA support based on the storage service currently in use.

## Restrictions
- CLB layer-4 and layer-7 protocols can be used for storing health check logs to CLS.
- Storing CLB health check logs to CLS is now free of charge. You only need to pay for the CLS service.
- This feature is only available to application CLBs.
- Only IPv4 and IPv6 NAT64 CLB instances support health check logging.
- Currently, this feature is supported only in certain regions as displayed in the console.


## Step 1. Add a Role Permission[](id:step1)
To add a role permission, make sure you have activated the CLS service.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and select **Health Check Logs** on the left sidebar.
2. On the **Health Check Logs** page, click **Activate Now**. Click **Authorize and Activate** in the pop-up dialog box.
<img src="" width="50%"/>
3. Switch to the **Role Management** page on the [CAM console](https://console.cloud.tencent.com/cam/role), and click **Grant**.

## Step 2. Create Logsets and Log Topics[](id:step2)
To store health check logs to CLS, you need to first create a logset and log topic.
You can directly jump to [Step 3](#step3) if you have created a logset and log topic.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and select **Health Check Logs** on the left sidebar.
2. On the **Health check logs** page, select a region for the logset, and then click **Create logset** in the **Logset information** section.
3. In the pop-up **Create logset** dialog box, set the retention period and click **Save**.
4. Click **Create topic name** in the **Log topic** section of the **Health check logs** page.
5. In the pop-up window, select a storage class and log retention period, select a CLB instance to add to the list on the right, and then click **Save**.
>?
>- Storage Class: STANDARD or STANDARD_IA. For more information, see [Storage Class Overview](https://www.tencentcloud.com/document/product/614/42003).
>- Logs can be retained permanently or for a specified time period.
>- When creating a log topic, you can add a CLB instance as needed. To add one, select a log topic in the list and click **Manage** in the operation column. Each CLB instance can only be added to one log topic.
>- A logset can contain multiple log topics. You can categorize CLB logs into various log topics which will be marked with "CLB".
>
![]()
6. (Optional) To disable health check logging, just click **Disable**.


## Step 3. View Health Check Logs[](id:step3)
Without any manual configurations, CLB has been automatically configured with index search by health check log valuable. You can directly query health check logs through search and analysis.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb) and select **Health Check Logs** on the left sidebar.
2. On the **Health Check Logs** page, select the region of the logset you want to view. In the "Log Topic" section, click **Search** on the right of the log topic you select to switch to the [CLS console](https://console.cloud.tencent.com/cls/search).
3. On the CLS console, click **Search Analysis** on the left sidebar.
4. On the **Search Analysis** page, enter the search syntax in the input box, select a time range, and then click **Search Analysis** to search for health check logs reported by CLB to CLS.
>?See [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/37803) for more information on search syntax.
>


## Health Check Log Format and Variable
### Log format
```	
[$protocol][$rsport][$rs_vpcid][$vport][$vpcid][$time][$vip][$rsip][$status][$domain][$url]
```

## Log variable description
<table class="table"><thead><tr><th>Variable</th><th>Description</th></tr></thead>Field Type</th></tr></thead>
<tbody>
<tr><td>protocol</td><td> Protocol type(HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>rsport</td><td>Real server port.</td><td>long</td></tr>
<tr><td>rs_vpcid</td><td>VPC ID of a real server; the `vip_vpcid` of a public network CLB instance is `-1`.</td><td>long</td></tr>
<tr><td>vport</td><td>CLB VPort, i.e., the listening port.</td><td>long</td></tr>
<tr><td>vpcid</td><td>VPC ID of a CLB VIP; the `vip_vpcid` of a public network CLB instance is `-1`.</td><td>long</td></tr>
<tr><td>time</td><td> Access time and time zone, such as "01/Jul/2019:11:11:00 +0800" where "+0800" represents UTC+8, i.e., Beijing time.</td><td>text</td></tr>
<tr><td>vip</td><td>CLB VIP. </td><td>text</td></tr>
<tr><td>rsip</td><td>Real server IP.</td><td>text</td></tr>
<tr><td>status</td><td>Health check status.<ul><li>`true`: healthy</li><li>`false`: unhealthy</li></ul></td><td>text</td></tr>
<tr><td>domain</td><td>Domain name to be checked. This parameter is left empty if a layer-4 listener is used.</td><td>text</td></tr>
<tr><td>url</td><td>URL to be checked. This parameter is left empty if a layer-4 listener is used.</td><td>text</td></tr>
</tbody></table>

## References
[Getting Started in 5 Minutes](https://intl.cloud.tencent.com/document/product/614/31592)
