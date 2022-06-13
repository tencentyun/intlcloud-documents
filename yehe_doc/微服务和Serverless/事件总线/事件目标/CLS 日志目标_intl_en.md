As an event delivery pipeline on the cloud, EventBridge only filters, routes, and distributes events. If you need to log or store events, you can configure **CLS as the delivery target**.


## Permission Description

To ensure normal log viewing, your account must have at least the read-only permission `QcloudCLSReadOnlyAccess` of CLS if you are using a sub-account. For how to use the root account to grant permissions for a sub-account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).


## Feature Description

Currently, EventBridge supports two delivery methods: **default logset delivery** and **custom logset delivery**.

<dx-tabs>
::: Default Logset Delivery
When creating a delivery target, if you do not specify the destination topic for log delivery, the default log delivery capability will be used. For default log delivery, EventBridge will activate the CLS service for you and deliver the function invocation logs to the log topic under the EventBridge's default logset. The EventBridge's default logset and log topic are prefixed with `EB_logset` and `EB_logtopic` respectively, and will be created automatically if they do not exist. Function invocation logs will be stored for 30 days by default, and you can view and manage them in the [CLS console](https://console.cloud.tencent.com/cls/logset).
![](https://qcloudimg.tencent-cloud.cn/raw/f1e9cef0678acfd6050cdb50bdb6e721.png)

#### Billing
CLS is billed separately. Starting from October 22, 2021, EventBridge's default logset was provided with an exclusive free quota of 1 GB of data for 30 days of storage. Details are as follows. 
<table>
<thead>
<tr>
<th>Billable Item</th>
<th>Quota/Day</th>
</tr>
</thead>
<tbody><tr>
<td>Write traffic</td>
<td>256 MB</td>
</tr>
<tr>
<td>Index traffic</td>
<td>1 GB</td>
</tr>
<tr>
<td>Log storage</td>
<td>7.5 GB</td>
</tr>
<tr>
<td>Index storage</td>
<td>30 GB</td>
</tr>
<tr>
<td>Partition</td>
<td>1 partition</td>
</tr>
</tbody></table>
This free quota is exclusive for EventBridge's default logset. The fee deduction sequence is as follows: <b>Global default free quota > Free quota exclusive for EventBridge's default logset > Normal pay-as-you-go fee deduction</b>.
:::
::: Custom Logset Delivery
When creating a delivery target, if you need to specify the destination log topic for log delivery, you can use the custom log delivery capability. Before using this capability, you need to make sure that the [CLS](https://intl.cloud.tencent.com/products/cls) service has been activated for your account.
![](https://qcloudimg.tencent-cloud.cn/raw/5a57cd1c90ec1cfd5c66a1d6ad6427e6.png)

#### Billing
CLS is billed separately. After a custom logset is bound, the fee deduction rule on the CLS side prevails. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509).
:::
</dx-tabs>









## Configuration Instructions

1. **View and manage logs**
After creating a delivery target, you can choose **Event Rule** > **Event Target** to view the bound logset and log topic, and click the log topic to go to the CLS console to view and manage logs.
EventBridge's default logset is marked with "EB" in the CLS console. If you have requirements such as persistent event storage, perform further configuration and management in the CLS console.
2. **Manage indexes**
Log searching depends on the index configuration of the log topic. For the default logset, EventBridge automatically performs index configuration for you. Currently, the following index fields are supported: 
>! If you select a custom logset, **ensure that the logset is also configured with the following indexes**. Otherwise, events cannot be queried on the CLS side after being delivered.
<table>
<thead>
<tr>
<th>Field Name</th>
<th>Field Type</th>
<th>Delimiter</th>
<th>Allow Chinese Characters</th>
</tr>
</thead>
<tbody><tr>
<td>sourceType</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>caller</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>eventbusId</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>status</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>specversion</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>id</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>type</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>source</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>subject</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>region</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>datacontenttype</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>tags</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>data</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr>
<td>time</td>
<td>text</td>
<td>N/A</td>
<td>No</td>
</tr>
</tbody></table>
