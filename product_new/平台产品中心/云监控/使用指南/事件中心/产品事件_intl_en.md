## Event Definition
Product events record the changes of resource instances and products purchased and used by a customer. These events are directly or indirectly triggered by customer behavior during use and operation. A product event belongs to a specific resource or instance, and the customer can control and manage these events.

Each product event record consists of the following attributes.

| Attribute | Description |
| ------------- | ----- |
| Time | The time when an event record occurs, accurate to second. |
| Event | Event name |
| **Event Type** | Events are divided into **exception event** and **status change** based on their impact on resources and instances. |
| Product | The product type of resources associated with an event. |
| Associated Resource | The resource instance that is uniquely associated with an event. |
| **Status** | The triggering and restoration status of a recoverable exception event of a specific resource. |
| Region (if applicable) | The region where a resource resides. |
| Project (if applicable) | The project to which a resource belongs. |
| Additional Information (if applicable) | Supplementary information about an event, including zero to multiple extra attributes based on actual scenarios. |

> A recoverable exception event is associated with triggering and restoration event records. To better locate and understand resource status via the console, the two associated event records are displayed together and the status of the exception event of the specific resource is updated according to the `status` attribute. The triggering and restoration event records differ by their start times and update times.


## Features
In addition to acquiring and storing resource instance events, the product event module provides a comprehensive event information consumption channel to drive monitoring and OPS with event information.
The product event module provides the following features based on use cases such as display rewind, alarm notification, data pull by API, and automated triggering:
- **Product Event**: displays the statistical data of key events filtered by current conditions. The **exception event not restored** and **alarm for exception events is not configured** dimensions are provided to help you quickly understand exception events. You can click the corresponding number to load relevant event information.
- **Global event filtering**: allows users to filter events by attributes, such as time span, product type to which an event belongs, event, event status, event type, alarm configuration status, and project. Multiple attributes can be selected for filtering. When multiple options of one attribute are used, the OR operation is performed. When multiple attributes are used, the AND operation is performed.
- **Searching for resource-associated events**: allows users to search for resource object IDs and multiple resource attributes in object details to acquire related resource-associated events.
- **View event alarms and quick configuration**: displays configured alarm policies for specific resources and event rules. In addition to allowing users to create and configure event alarms on the alarm policy page, it supports the quick configuration of specific resources and events. When you click the entry for creating and configuring specific product event records, resource instances and related event rules are loaded to the alarm policy configuration page.

APIs for pulling data and the automated operation triggering capability are supported and will be publicly available in the future.


## Scenarios
- **Locating problems through alarm messages**: When alarm policies are configured for resources, they can be incorporated into event rules. When an event triggers the alarm, an alarm message is promptly sent to the recipient through an alarm channel.
- **Routine Inspection**: Users can browse the product event overview, check the health status of product resource instances in real time, and promptly view alarm exception events that are not restored and configured.
- **Rewinding exception**: Detailed event information records are provided to help locate problems in abnormal resources, displaying the associated event information in reverse chronological order.
- **Automated operation triggering**: Users can configure automated triggering rules based on specific resource instance events to implement auto-recovery and automated scheduling, improving the efficiency of monitoring and OPS.



## Use Limits
- You can only view event information from the past 6 months.
- Event alarm messages are included in the message quota.
- The maximum number of event alarms that can be configured for an account (including the alarm policies of event rules) equals the alarm policy quantity limit.


## Operation Instructions
### Filtering Events
Use the global event filtering capability to acquire information about events with a specified attribute combination.
1. Log in to the [Cloud Monitoring console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** in the left sidebar to access the product event page.
3. Click the global filtering search box in the upper-right corner, modify the default filtering items **Product Type** and **Event Name**, and confirm. Alternatively, add custom filtering items such as **Region**, **Event Status**, **Event Type**, **Alarm Configuration Status**, and **Project**, and clilck to complete the filtering. By using the time filtering boxes in the upper-left corner, you can customize the time range filter to display events updated within the time range.
4. Use the scroll bar to scroll up and down the event list page or click to jump to a specific page to view the filtered results.

### Searching for resource-associated events
View information about events associated with specific resources.
1. Log in to the [Cloud Monitoring console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** in the left sidebar to access the product event page.
3. Click the global filtering search box in the upper-right corner, select **Affected Object**, enter the resource object ID, and press **Enter**.
4. (Optional) Search for associated events by resource object attribute. Click the corresponding product in the **Type** column. Attributes supported by the product are displayed in the global filtering search box. For example, **Cluster ID** and **Namespace** are added for **TKE**. After content is output, press **Enter**.
5. Use the scroll bar to scroll up and down the event list page or click to jump to a specific page to view the filtered results.


### Viewing the product event page
The product event page allows users to quickly understand the overall status of resource instances and provides a shortcut entry to view key event information.
1. Log in to the [Cloud Monitoring console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** in the left sidebar to access the product event page.
3. View the event data that meets the current filter conditions in the product event section under the filtering control, including the **exception event not restored** and **alarm for exception events is not configured** categories. The **exception event not restored** category also collects statistics about alarm events that are not restored and configured. Numbers in the product event section change based on filtering and search conditions.
4. When you click the number corresponding to an overview item, the color of the overview item turns dark and the information about the corresponding event is loaded in the list. Click the overview item again to restore the item to its previous status.

### Configuring event alarms
Configure the recipients of alarm policies based on event information.
**Creating alarm policies**
This procedure is the same as configuring an existing new alarm policy. Select the corresponding rule item in the new event alarm items.

**Quick Configuration**
1. Log in to the [Cloud Monitoring console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** in the left sidebar to access the product event page.
3. Find the event to be configured. In the **Alarm Configuration** column, click **Add Configuration** to be redirected to the page for creating alarm policies. Enter the corresponding event rule and associated resource instance, modify the policy, and then submit it.
4. View alarm records in **Alarm List**.


## Supported Products
The following products are currently supported, and other products will be available soon. Go to the event list page to [view specific event information](https://intl.cloud.tencent.com/document/product/248/32823).
- Cloud Virtual Machine (CVM)
- Cloud Load Balancer (CLB)
- VPN Gateway
- TKE

