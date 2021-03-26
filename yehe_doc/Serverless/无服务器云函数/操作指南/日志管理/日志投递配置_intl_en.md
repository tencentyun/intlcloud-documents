

>? If your function was created before January 29, 2021, but you need to deliver logs, please see [Connecting SCF Logs to CLS](https://intl.cloud.tencent.com/document/product/583/34876).

SCF was fully connected to [CLS](https://intl.cloud.tencent.com/document/product/614) on January 29, 2021, invocation logs of newly created functions have been delivered to CLS since then, and logs can be output in real time.
This document describes the two log delivery methods of [default delivery](#MRTD) and [custom delivery](#ZDYTD) provided by SCF and how to configure them.



## Use Limits

Delivering function invocation logs to CLS has the following limits:
- The maximum amount of logs printed within 5 seconds for each request is 1 MB.
- The maximum number of logs printed within 5 seconds for each request is 5000.
- The maximum length of each log is 8 KB, and excessive parts will be discarded.

Please pay attention to whether the CLS configuration can meet your business needs. Exceeding the limits may cause log write failures.

## Directions
<span id ="MRTD"></span>

### Default delivery

When creating a function, if you don't specify the destination topic for log delivery, the default log delivery capability will be used. For default log delivery, SCF will activate the CLS service for you and deliver the function invocation logs to the log topic under the SCF-specific logset, which are prefixed with `SCF_logtopic` and `SCF_logset` respectively and will be created automatically if not existing. Function invocation logs will be retained for 7 days by default, and you can view and manage them in the [CLS console](https://console.cloud.tencent.com/cls/logset).



>! CLS is billed separately, and the SCF-specific log topic will consume the free tier of CLS. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509).



#### Configuring CLS

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Template** or **Custom** to create a function. This document takes **Custom** as an example.
4. In **Advanced Configuration**, select **Default publishing** in **Log Configuration** as shown below:
![](https://main.qcloudimg.com/raw/3954432a56fdc393ec4d0a72f663854f.png)
5. Click **Complete**. You can view the log configuration in **Function Management** > **Function Configuration** as shown below:
![](https://main.qcloudimg.com/raw/4148a9a9e023fb7538a8c311934e43d6.png)

#### Viewing and managing logs

You can click the logset ID in **Log Configuration** in **Function Configuration** to enter the [CLS console](https://console.cloud.tencent.com/cls/logset) to view and manage logs. The SCF-specific logset is marked with the word `SCF` in the CLS console. If you need to persistently store, deliver, or consume logs or monitor and set alarms on log content, you can complete the configuration in the CLS console.

<span id="ZDYTD"></span>


### Custom delivery

When creating a function, if you need to specify the destination log topic to deliver function invocation logs, you can use the custom log delivery capability. Before using this capability, you should make sure that the [CLS](https://intl.cloud.tencent.com/product/cls) service has been activated.


#### Creating logset and log topic

Log in to the [CLS console](https://console.cloud.tencent.com/cls) and [create a logset and log topic](https://intl.cloud.tencent.com/document/product/614/31592). This document uses the creation of the `SCF-test` logset and log topic in Guangzhou as an example as shown below:
>!For the logset region, please select the region where the SCF service is located. Cross-region log push is not supported currently.
>
![](https://main.qcloudimg.com/raw/f3ffd10aaaeb6abc2a492e5840339c9f.png)

#### Configuring CLS

1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Template** or **Custom** to create a function. This document takes **Custom** as an example.
4. In **Advanced Configuration**, select **Custom publishing** in **Log Configuration**, and select the logset and log topic already created for this function. This document uses `SCF-test` as an example as shown below:
![](https://main.qcloudimg.com/raw/53a703aee35dd6ed7967d981b139aff0.png)
5. Click **Complete**.






### Configuring index

Log search depends on the index configuration of the log topic. SCF will automatically complete the index configuration when you create a function. If the index is exceptional and logs cannot be viewed properly, please configure the index in the following steps:



1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Function Service** list page, select the name of the function whose index is exceptional to enter the **Function Management** page.
3. On the **Log Query** tab, select **Index Configuration** in **Advanced Retrieval** as shown below:
![](https://main.qcloudimg.com/raw/8d506d9d22c6c26b3e2396acb33fb499.png)
4. On the **Index Configuration** page, enable **Index Status** and **Key-Value Index** and select **Auto Configure** as shown below:
![](https://main.qcloudimg.com/raw/861138c664768aab368761d91b441e9e.png)
5. After configuring the index, click **OK**.



The configuration method in step 4 is only valid for scenarios where there are function invocation logs in the log topic; otherwise, please manually configure the **key-value index** by referring to the table below.
<table>
<thead>
<tr>
<th>Field Name</th>
<th>Field Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
<td>Function name.</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
<td>Function namespace.</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>long</td>
<td>Invocation start time.</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
<td>Log generation time.</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
<td>Request ID.</td>
</tr>
<tr>
<td>SCF_Duration</td>
<td>long</td>
<td>Function execution duration.</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
<td>Alias.</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
<td>Version.</td>
</tr>
<tr>
<td>SCF_MemUsage</td>
<td>double</td>
<td>Function runtime memory.</td>
</tr>
<tr>
<td>SCF_Level</td>
<td>text</td>
<td>Log4J log level. Default value: INFO.</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
<td>Log content.</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
<td>Log type. Platform: platform log, Custom: user log.</td>
</tr>
<tr>
<td>SCF_StatusCode</td>
<td>long</td>
<td>Function execution <a href="https://intl.cloud.tencent.com/document/product/583/35311">status code</a>.</td>
</tr>
<tr>
<td>SCF_RetryNum</td>
<td>long</td>
<td>Number of retries.</td>
</tr>
</tbody></table>


To ensure the display effect of the logs in the SCF console, please toggle on **Enable Statistics** for the field in the key-value index configuration as shown below:
![](https://main.qcloudimg.com/raw/5e34368e42bb03dd6d6be864af695fa3.png)






