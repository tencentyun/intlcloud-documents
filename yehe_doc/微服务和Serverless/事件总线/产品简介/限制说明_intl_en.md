EventBridge has certain quota limits for each user account. This document describes such quota limits.


## Quota Limit

The quota limits for each user account are as follows:

<table>
<thead>
<tr>
<th>Content</th>
<th>Default Quota Limit</th>
</tr>
</thead>
<tbody><tr>
<td>`Put Event` API call limit in one region</td>
<td>1,000 QPS</td>
</tr>
<tr>
<td rowspan="2">Maximum number of event buses in one region</td>
<td>10<br></td>
</tr>
<tr>
</tr>
<tr>
<td>Maximum number of rules that can be bound to one event bus</td>
<td>10</td>
</tr>
<tr>
<td>Maximum number of targets that can be configured in one event rule</td>
<td>5</td>
</tr>
<tr>
<td>Maximum size of event message body</td>
<td>64 KB</td>
</tr>
<tr>
<td>Maximum number of connectors supported by one event bus</td>
<td>5</td>
</tr>

</tbody></table>



>! 
>- EventBridge currently supports 10,000-level concurrency, which can effectively support scenarios with high concurrency demand such as ecommerce promotions and parallel processing of medical and biological data. To request an increase in quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>- You can specify the relevant limits by region, event bus, etc. If your business requires higher quotas, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.


## Rule Limits

- **Event bus**
Event bus name: it can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.
Event bus description: it can contain up to 200 characters of any type.

- **Event rule**
Event rule name: it can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.
Event rule description: it can contain up to 200 characters of any type.

- **Connector**
Connector name: it can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.



## Exception Handling

### Delivery exception

An event may fail to be delivered to a target from EventBridge for various reasons, and the delivery exception processing logic varies by target. Below is the default policy for failed delivery.

#### SCF 

- **Overrun error** (error code: 432/429): 	when an error of this type occurs during delivery, the EventBridge platform will retry for the default maximum waiting time (which is 6 hours by default) at intervals of one minute. If a DLQ is configured, events that still fail after the maximum waiting time elapses will be sent to it for further processing on your own; otherwise, they will be discarded by the EventBridge platform.
- **System error**: when an SCF platform error occurs during delivery, EventBridge will retry for the default maximum waiting time (which is 6 hours by default), and the retry interval will increase to 5 minutes by exponential backoff. If a DLQ is configured, events that still fail after the maximum waiting time elapses will be sent to it for further processing on your own; otherwise, they will be discarded by EventBridge.
- **Execution error**: when an execution failure occurs on the SCF platform, EventBridge will not perceive it and will not retry.



### Deletion exception

- **Event bus deletion**: to delete an event bus, you need to delete all its trigger rules and connectors first; otherwise, the error message "An event rule/connector has been bound to this event bus. Please try again after deleting the bound event rule" will be displayed. After the event bus is deleted from the data flow, all corresponding resource information will also be deleted.
- **Event rule deletion**: to delete an event rule, you need to delete all its targets first; otherwise, the error message "An event target has been bound to this event rule. Please try again after deleting the bound event target" will be displayed. After the event rule is deleted from the data flow, delivery of events related to the rule to the corresponding event bus will also stop.
- **Event target deletion**: the component resources of the relevant delivery logic will be deleted from the data flow.
- **Connector deletion**: the connector resources will be deleted from the data flow, and messages will no longer be delivered to the corresponding event bus.



