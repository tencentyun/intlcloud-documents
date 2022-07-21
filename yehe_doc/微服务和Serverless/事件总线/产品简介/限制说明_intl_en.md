EventBridge has certain quota limits for each user account. This document describes such quota limits.


### Quota Limits

The quota limits for each user account are as follows:

<table>
<thead>
<tr>
<th>Content</th>
<th>Default Quota Limit</th>
</tr>
</thead>
<tbody><tr>
<td>`PutEvents` API call limit per region</td>
<td>5000 TPS</td>
</tr>
<tr>
<td>Number of custom event buses per region</td>
<td>10<br></td>
</tr>
<tr>
</tr>
<tr>
<td>Maximum number of rules that can be bound to one custom event bus</td>
<td>10</td>
</tr>
<tr>
<td>Maximum number of rules that can be bound to Tencent Cloud service event bus</td>
<td>200</td>
</tr>
<tr>
<td>Maximum number of targets that can be configured in one event rule</td>
<td>10</td>
</tr>
<tr>
<td>Maximum size of event message body</td>
<td>64 KB</td>
</tr>
<tr>
<td>Maximum number of connectors supported by one event bus</td>
<td>10</td>
</tr>

</tbody></table>


<dx-alert infotype="notice" title="">
- EventBridge currently supports 10,000-level concurrency, which can effectively support scenarios with high concurrency demand such as ecommerce promotions and parallel processing of medical and biological data. To request an increase in quota, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
- You can specify the relevant limits by region, event bus, etc. If your business requires higher quotas, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
</dx-alert>




#### Rule Limits

- **Event bus**
Event bus name: It can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.
Event bus description: It can contain up to 200 characters of any type.

- **Event rule**
Event rule name: It can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.
Event rule description: It can contain up to 200 characters of any type.

- **Connector**
Connector name: It can contain 2–60 letters, digits, underscores, and hyphens and must start with a letter and end with a digit or letter.



### Deletion Exceptions

- **Event bus deletion**: To delete an event bus, you need to delete all its trigger rules and connectors first; otherwise, the error message "An event rule/connector has been bound to this event bus. Try again after deleting the bound event rule" will be displayed. After the event bus is deleted from the data flow, all corresponding resource information will also be deleted.
- **Event rule deletion**: To delete an event rule, you need to delete all its event targets first; otherwise, the error message "An event target has been bound to this event rule. Try again after deleting the bound event target" will be displayed. After the event rule is deleted from the data flow, delivery of events related to the rule to the corresponding event bus will also stop.
- **Event target deletion**: The component resources of the relevant delivery logic will be deleted from the data flow.
- **Connector deletion**: The connector resources will be deleted from the data flow, and messages will no longer be delivered to the corresponding event bus.


