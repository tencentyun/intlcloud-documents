After a metric or event alarm policy is configured for a connection, dedicated tunnel, or direct connect gateway, you can view the alarm history and details on the Cloud Monitor console.

## Prerequisites
- You have [configured an alarm policy](https://intl.cloud.tencent.com/document/product/216/38402).

## Viewing Alarm History

1. Log in to the [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm List** on the left sidebar to view alarm records.
2. Select a period during which alarms are generated.
   The **Alarm Records** page displays the alarm details, including alarm object, alarm content, duration, and alarm status.
   
## Viewing Product Event

Tencent Cloud provides the automatic exception detection for connections and dedicated tunnels such as disconnected port or link, and syncs the information to the Cloud Monitor console. These product events in the last 30 days can be viewed on the console. You can also configure an alarm policy for the product event as needed.
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) and select **Event Center** -> **Product Event** on the left sidebar.
2. At the top of the **Product Event** page, double-click **All** of **Product Type: All** in the search bar, select Connection or Dedicated Tunnel in the drop-down list, and click **OK**.
>? By default, the product event lists all the connection/dedicated tunnel events under the current account during the custom period. The fields including Event, Affected Object, Object Details, Status, and Start Time are displayed.

3. To create an alarm policy for the selected product event, click **Add Configuration** in its **Alarm Configuration** column to access **Create Policy**. Complete the configurations and click **Complete**.
