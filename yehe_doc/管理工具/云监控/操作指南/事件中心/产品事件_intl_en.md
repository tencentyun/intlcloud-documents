## Event Definition
Product event records changes in instance resources and products you have purchased and used on the cloud.

Product event is directly or indirectly triggered by you during use and belongs to specific resource instance. You can control and manage the event, and determine resource instances affected by and associated with it.

Each product event record consists of the following attributes:

| Attribute | Description |
| ------------- | ----- |
| Time | Time when an event record is generated, accurate to the second. |
| Event | Event name. |
| **Event Type** | Events are divided into **exception** and **status change** based on their impact on resources and instances. |
| Product | Product type of resources associated with an event. |
| Associated Resource | Resource instance uniquely associated with an event. |
| **Status** | The triggered and recovered status of a recoverable exception of a specific resource. |
| Region (if applicable) | The region where a resource resides. |
| Project (if applicable) | The project to which a resource belongs. |
| Additional Information (if applicable) | Supplementary information for an event, which can include zero to multiple fields based on actual scenarios. |

>A recoverable exception is associated with two event records: triggered and recovered. To better locate and understand resource status through the console, the two associated event records are displayed together and the status of the exception of the specific resource is updated through `status`. The two event records are differentiated by start time and update time.


## Features
In addition to getting and storing resource instance events, the product event module provides a comprehensive event information consumption channel to drive monitoring and OPS.
The product event module provides the following features based on use cases such as display and tracing, alarm notification, data pull by API, and automated operation triggering:
- **Event overview**: displays the statistical data of key events filtered by current conditions. The **unresolved exception** and **unalarmed exception** dimensions are provided to help you quickly understand exceptions. You can click the corresponding number to load relevant event information.
- **Global event filtering**: allows you to filter events by attributes such as time span, product type to which an event belongs, event, event status, event type, alarm configuration status, project, etc. Multiple attributes can be selected for filtering. When multiple options of one attribute are used, the "OR" operation will be performed. When multiple attributes are used, the "AND" operation will be performed.
- **Searching for resource-associated events**: allows you to search for resource object IDs and multiple resource attributes in object details to get resource-associated events.
- **Viewing event alarm and setting quick configuration**: displays configured alarm policies for specific resources and event rules. In addition to creating and configuring event alarms on the alarm policy page, you can set quick configuration for specific resources and events. When you click the entry for creating and configuring specific product event records, resource instances and related event rules will be loaded to the alarm policy configuration page.

APIs for pulling data and the automated triggering capability will be publicly available in the near future.


## Scenarios
- **Locating problems through alarm messages**: if alarm policies are configured for resources, event rules can be incorporated into alarm policies. When an event triggers the alarm, an alarm message will be promptly sent to the recipient through an alarm channel.
- **Routine inspection**: you can browse the product event overview, check the health status of product resource instances in real time, and promptly view unresolved and unalarmed exceptions.
- **Exception tracing**: detailed event information records are provided to help you locate resources that have exceptions, and information on associated events can be traced.
- **Automated operation triggering**: you can configure automated triggering rules based on specific resource instance events to implement auto-recovery and automated scheduling, improving monitoring and OPS efficiency.



## Use Limits
- You can only view event information in the last 6 months.
- Event alarm messages are included in the message quota.
- The maximum number of event alarms can be configured for an account (including alarm policies of event rules) equals to the maximum number of alarm policies allowed.


## Operation Guide
### Filtering events
You can use global event filtering to get information on events with a specified attribute combination.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** on the left sidebar to enter the product event page.
3. Click the global filtering search box in the top-right corner, modify the default filtering items (**Product Type** and **Event Name**) and confirm. Alternatively, add custom filtering items (**Region**, **Event Status**, **Event Type**, **Alarm Configuration Status** and **Project**) and click to complete filtering. You can use the time filtering box in the top-left corner to customize the time range and view events updated within the time range.
4. Scroll up or down on the event list page or select a specific page to view results.

### Searching for resources-associated events
You can view information of events associated with specific resources.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** on the left sidebar to enter the product event page.
3. Click the global filtering search box in the top-right corner, select **Affected Object**, enter the resource object ID, and press **Enter**.
4. (Optional) You can search for associated events by resource object attributes. Click the corresponding product in the **Type** column. Attributes supported by the product will be displayed in the global filtering search box. For example, **Cluster ID** and **Namespace** are added for **TKE**. Press **Enter** to confirm.
5. Scroll up or down on the event list page or select a specific page to view results.


### Viewing event overview
The product event overview page allows you to quickly understand the overall status of resource instances and provides a shortcut entry to view key event information.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** on the left sidebar to enter the product event page.
3. View event data that meets the current filter conditions in event overview, including **exception** and **status change** categories. For **exception**, the system also counts the number of unresolved and unalarmed events. The number in event overview changes by filter conditions and search criteria.
4. When you click the number corresponding to an overview item, the color of the overview item turns dark and the corresponding event information will be loaded in the list. Click the overview item again to return to the previous status.

### Configuring event alarms
You can configure the recipients of alarm policies based on event information.
**Creating an alarm policy**
This procedure is the same as the existing procedure of configuring a new alarm policy. Select the corresponding rule item from the new event alarm items.

**Quick configuration**
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** on the left sidebar to enter the product event page.
3. Find the event to be configured. In the **Alarm Configuration** column, click **Add Configuration** to be redirected to the page for creating alarm policies. Enter the corresponding event rule and associated resource instance, modify the policy as needed, and then submit.
4. View alarm records in **Alarm History**.


## Supported Products
Currently, product event supports the following products and more will be supported soon. For more information, please see [Product Event List](https://intl.cloud.tencent.com/document/product/248/32823)
- Cloud Virtual Machine (CVM)
- Cloud Load Balancer (CLB)
- VPN Gateway
- Tencent Kubernetes Engine (TKE)
- TencentDB for MySQL
- TencentDB for MongoDB
- Direct Connect (Connection, Dedicated Tunnel)
