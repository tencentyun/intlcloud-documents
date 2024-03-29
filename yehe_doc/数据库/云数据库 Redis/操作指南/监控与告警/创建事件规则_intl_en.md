## Overview
TencentDB for Redis has been connected to [Cloud Monitor (CM)](https://intl.cloud.tencent.com/document/product/248) to report cloud monitoring events. All events will be automatically delivered to the [Event Bus](https://intl.cloud.tencent.com/document/product/1108/42284) in [EventBridge](https://intl.cloud.tencent.com/document/product/1108/42267).

### Cloud Monitor Event
Currently, the following **events** can be reported:

| Event Name | Event Type | Dimension | Recoverable | Description | Troubleshooting and Suggestions |
 | ------------------- | -------- | ---------------------- | ------------ | ------------------- | ------------------------------ |
| Master/Replica switch | MasterSlaveSwitched | Status change | TencentDB for Redis instance | No | A failover occurs in TencentDB for Redis. | The failure will cause the TencentDB for Redis service to become inaccessible and momentarily unavailable. Make sure that your business has an automatic reconnection mechanism for quick business recovery. |
| Unavailable service | ServiceNotAvailable | Abnormal event | TencentDB for Redis instance | Yes | The TencentDB for Redis service is unavailable due to a failure. | We will recover the service as soon as possible and send a service recovery notification. If you have a disaster recovery instance, try switching your business to it. |
| Read-only replica failover | ReadonlyReplicaSwitched | Status change | TencentDB for Redis instance | Yes | A failover occurs in the TencentDB for Redis read-only replica. | We will recover the service as soon as possible and send a service recovery notification. If you have a disaster recovery instance, try switching your business to it or add more read-only replicas. |
| Unavailable read-only replica | ReadonlyReplicaNotAvailable | Abnormal event | TencentDB for Redis instance | Yes | A failure occurs in the TencentDB for Redis read-only replica. | We will recover the service as soon as possible and send a service recovery notification. If you have a disaster recovery instance, try switching your business to it or add more read-only replicas. |
| Instance migration due to server failure | ServerfailureInstanceMigration | Status change | TencentDB for Redis instance | Yes | A failover occurs in TencentDB for Redis. | The system detects that there is hardware risks in the server. The automatic migration time is subject to the maintenance window. Change the time promptly if needed. |


### Event Target
An event rule can have multiple event targets. Before creating an event rule, plan the event target types first. Currently, EventBridge supports the following event targets.

- [Message Push Target](https://intl.cloud.tencent.com/document/product/1108/46779) (supported by rules only in the Tencent Cloud service event bus)
- [CLS Log Target] (https://intl.cloud.tencent.com/document/product/1108/46992)
- [SCF Target](https://intl.cloud.tencent.com/document/product/1108/46254)
- [CKafka Target](https://intl.cloud.tencent.com/document/product/1108/46249)

## Billing Details
EventBridge is **pay-as-you-go**. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/1108/43288).

| **Billing mode** | **Pay-as-you-go** |
| :----------- | :----------------------------------------------------- |
| **Payment mode** | Fees are charged hourly by the number of events actually delivered to the event bus. |
| **Billing unit** | USD/million events |
|**Use cases**| Low or fluctuating message volumes |

## Directions
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb), and select **Event Rule** (https://console.cloud.tencent.com/eb/rule) on the left sidebar.
2. At the top of the page on the right, select **Guangzhou** for **Region** and select **default** in the **Event Bus** drop-down list.
  - The Tencent Cloud service event bus collects monitoring and audit events generated by Tencent Cloud services in all regions. It is created in Guangzhou region by default and cannot be deleted. 
  - Select **Event Bus** on the left sidebar. In the event bus list, click **default**, and you can see that the **default** event bus already contains TencentDB for Redis. For detailed directions, see [Tencent Cloud Service Event Source](https://intl.cloud.tencent.com/document/product/1108/46250).
![](https://qcloudimg.tencent-cloud.cn/raw/9e6fc950b148f3d83ee58d909d1ebb4e.png)
3. Click **Create Event Rule**. On the **Event Pattern** page, configure parameters by referring to the following descriptions:
![](https://qcloudimg.tencent-cloud.cn/raw/d3c784dcfdd5f1dd2dd3a90ff6283df9.png)
   
   <table class="table-striped">
   <tbody>
   <tr><th>Section</th><th>Parameter</th><th>Description</th></tr>
   <tr>
   <td rowspan="4"><b> Basic Info</b></td>
   <td>Region</td>
   <td>The region where to create an event rule.</td></tr>	
   <tr>
   <td>Event bus</td>
   <td>Information of the event bus to which the event rule belongs.</td></tr>
   <tr>
   <td>Rule name</td><td>Event rule name, which can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.</td></tr>
   <tr>
   <td>Rule description</td><td>Brief description of the event rule.</td></tr> 
   <tr>
   <td rowspan="4"><b>Event matching</b></td>
   <td>Event pattern</td><td>Select <b>Default</b>.</td></tr>
   <tr>
   <td>Tencent Cloud service</td><td>Select <b>TencentDB for Redis</b> in the drop-down list.</td></tr>
   <tr>
   <td>Event type</td><td>Select a supported event type.</td></tr>
   <tr>
   <td>Rule pattern preview</td><td>You can preview the event rule.</td></tr>
   </tbody></table>
4. Click **Test Event Matching** and select an event template in the drop-down list after **Template**. The fields of this event type are displayed in **Event fields**. Click **Test** to test the network connectivity of the defined event type.
![](https://qcloudimg.tencent-cloud.cn/raw/083860db3b0fb131e390cbfbd8587570.png)
5. (Optional) To convert the data format, select **Enable data conversion** to enter the event transformation page as shown below. Configure the data conversion formats and fields according to the parameter descriptions in the following table and click **OK** to start parsing the data. After data parsing is completed, set the filter rule and data processing method. For detailed directions, see [Configuring Data Conversion](https://intl.cloud.tencent.com/document/product/1108/46247).
> ? EventBridge provides simple data processing capabilities. After you pass in data and configuration items to EventBridge, EventBridge formats the data and distributes the structured data obtained after processing to downstream targets, creating a bridge between data sources and data processing systems. 
> 
![](https://qcloudimg.tencent-cloud.cn/raw/0c8dcc531b78a0de4c33919f24ef4465.png)
<table>
<thead><tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr>
<td><strong>Rule pattern preview</strong></td>
<td>If you select <strong>Sample event</strong>, you can use an event template. If you select <strong>Manually input</strong>, you can customize the event fields in the input box below.</td></tr>
<tr>
<td><strong>Event template</strong></td>
<td>This parameter will be displayed if you select <strong>Sample event</strong> for <strong>Rule pattern preview</strong>. You can search for "Redis" in the drop-down list and select the TencentDB for Redis event template. Then, the specific field information of the event template will be displayed in the input box below.</td></tr>
<tr>
<td><strong>Target switch</strong></td>
<td><ul><li><strong>All events</strong>: The complete structure of event fields will be routed to the delivery target.</li><li><strong>Specified events</strong>: EventBridge will extract event parameters according to the event fields configured in `JSONPath` to route the specified event fields to the delivery target.</li></ul></td></tr>
<tr>
<td><strong>JSONPath</strong></td>
<td>This parameter will be displayed if **Specified events** is selected for **Target**. Enter the event fields to be converted in the input box.</td></tr>
<tr>
<td><strong>Parsing mode</strong></td>
<td>Select a parsing mode, which can be <strong>JSON</strong>, <strong>Separator</strong>, or <strong>Extract with regex</strong>.</td></tr>
</tbody></table>
6. Click **Next** to select the delivery target bound to the rule. You can deliver collected events to the specified target to process and consume them. In the figure below, **Notification message** is selected for **Trigger method** as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/5208e601e90094504f68a96e7ac8ac52.png)
7. To make the event rule take effect immediately, select **Enable event rules now** and click **Complete**.

## Event Rule APIs

| API | Description |
| :----------------------------------------------------------- | :--------------- |
| [CheckRule](https://intl.cloud.tencent.com/document/product/1108/45818) | Checks a rule |
| [CreateRule](https://intl.cloud.tencent.com/document/product/1108/45817) | Creates an event rule |
| [DeleteRule](https://intl.cloud.tencent.com/document/product/1108/45816) | Deletes an event rule |
| [GetRule](https://intl.cloud.tencent.com/document/product/1108/45815) | Gets the details of an event rule |
| [ListRules](https://intl.cloud.tencent.com/document/product/1108/45814) | Gets the list of event rules |
| [UpdateRule](https://intl.cloud.tencent.com/document/product/1108/45813) | Updates an event rule |

## More Operations
- You can view, modify, or delete an event rule. For more information, see [Managing Event Rule](https://intl.cloud.tencent.com/document/product/1108/42290).

## FAQs
For questions about event rule concepts and billing, see [FAQs](https://intl.cloud.tencent.com/document/product/1108/42292).

