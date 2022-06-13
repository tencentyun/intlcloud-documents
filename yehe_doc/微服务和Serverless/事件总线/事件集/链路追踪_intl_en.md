## Use Cases 
With the event bus linkage tracing capability provided by EventBridge, you can view the details of each event delivered to EventBridge and the complete event processing linkage of the event in EventBridge, facilitating the tracking and management of each event.

## Prerequisites 
The linkage tracing feature reports your event processing logs to a specified CLS logset and integrates the log content into the EventBridge console for you to search and view. To ensure normal use of the feature, check that you have activated the CLS service and created related service roles. For more information, see [Permission Description](https://intl.cloud.tencent.com/document/product/614/37888).

## Feature Description
### Service dimension
Event bus: You can configure and bind related linkage tracing feature configuration to event buses.

### Reporting type
#### Default delivery	
- Event logs are reported to the default logset of EventBridge, and EventBridge automatically configures a default index for the logset.
- Data in the logset is stored for three days by default.
- Logs of all basic events are reported, including logs of Tencent Cloud service alarm events and rule-matched custom event logs that fail to be delivered to targets.

#### Custom delivery
- Event logs are delivered to a custom logset. In this case, you need to enable **full-text index**.
- You can select an appropriate delivery scheme according to your business requirements. Supported delivery schemes are as follows: 
    - After successful event rule matching, report all delivery logs (including successful and failed delivery logs).
    - After successful event rule matching, report only failed delivery logs.
    - After successful event rule matching, report only successful delivery logs.
    - After successful event rule matching, report all delivery logs (including successful and failed delivery logs) and event rule matching failure logs.
    - After successful event rule matching, report only failed delivery logs and event rule matching failure logs.
    - After successful event rule matching, report only successful delivery logs and event rule matching failure logs.

#### Remarks
- For a single event ID, if rule matching fails and related delivery is enabled, report a failure log.
- For a single event ID, if rule matching is successful, the delivery result (success or failure) will be reported in the target dimension.
- If a log fails to be reported to CLS (due to a platform error, limit exceeding error, or other causes), the log will be discarded.



## Directions 
### Creation process
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. Choose **Create event bus**. When creating an event bus, you can configure the event reporting method. You can select **Default**, **Custom**, or **Enable later** as needed.
3. After creating the event bus, you need to bind an event source connector as needed. On the event bus details page, click **Manage Event Rules** to enter the event rule page.
![](https://qcloudimg.tencent-cloud.cn/raw/6d63af96e69587d8de4ff84e65d5fe1e.png)
4. Click **Create event rule**. On the page displayed, enter information as prompted to complete rule and target binding as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/6addc1d96739cdaa11542658dd854b04.png)
5. Click **OK**. After the creation is completed, send an event, and you can view the corresponding log on the **Query events** tab page on the event bus details page.

### Log search
On the event query page, you can filter and search logs in a number of ways, as described below. 
#### Tencent Cloud service event bus
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. Click the event bus name to enter the event bus event query page.
 You can set fields to filter logs.
 <table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Time period</td>
<td>By default, event logs in the last 15 minutes are displayed. The time period can be up to three days. If you need more logs, filter logs in the CLS console.</td>
</tr>
<tr>
<td>Event filter</td>
<td>For the Tencent Cloud service event bus, you can choose to display all events or only Tencent Cloud service alarm events.</td>
</tr>
<tr>
<td>Event source &amp; Event type</td>
<td>You can select an existing Tencent Cloud service event source or enter a custom event source. If you select <strong>Custom</strong>, you need to enter a complete event type name, such as <code>cvm:ErrorEvent:GuestOom</code>, in the <code>Event type</code> field.</td>
</tr>
<tr>
<td>Event rule</td>
<td>If an event bus is bound with multiple rules, you can select a rule for filtering so that you can view the delivery logs of events that meet the selected rule.</td>
</tr>
<tr>
<td>Event ID</td>
<td>You can specify an event ID to query the track and details of the specified event.</td>
</tr>
</tbody></table>
 


#### Custom event bus
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. Click the event bus name to enter the event bus event query page.
 You can set fields to filter logs.
 <table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Time period</td>
<td>By default, event logs in the last 15 minutes are displayed. The time period can be up to three days. If you need more logs, filter logs in the CLS console.</td>
</tr>
<tr>
<td>Event type</td>
<td>For a custom event bus, you need to enter a complete event type name, such as <code>cvm:ErrorEvent:GuestOom</code>.</td>
</tr>
<tr>
<td>Event rule</td>
<td>If an event bus is bound with multiple rules, you can select a rule for filtering so that you can view the delivery logs of events that meet the selected rule.</td>
</tr>
<tr>
<td>Event ID</td>
<td>You can specify an event ID to query the track and details of the specified event.</td>
</tr>
</tbody></table>


#### Event details
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. Click the event bus name to enter the event bus event query page. Click **View details** in the event list. Then you can see the complete content, delivery result, time elapsed, and other detailed information of the event.
  - The time elapsed is the result of **the target delivery time minus the time when the event reaches the event bus**. If a retry occurs due to a delivery failure, the retry interval is added to the time elapsed.
  - For the tracing records of the same event under the same rule, up to 10 result records (the first five and last five records) are displayed.

## Free Tier
The linkage tracing capability itself is not charged. However, because logs are reported to CLS and CLS is billed separately, certain fees may incur. For the billing method details, see the [CLS billing overview](https://intl.cloud.tencent.com/document/product/614/37509). To minimize usage costs for users, EventBridge provides a free quota of 30-day storage for 1 GB of data for the **default EventBridge logset**. The quota details are as follows: 
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
