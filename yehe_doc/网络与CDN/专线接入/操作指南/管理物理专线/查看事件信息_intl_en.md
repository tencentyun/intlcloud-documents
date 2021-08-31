Connection exception information at the port level can be reported. When a physical port under your account is exceptional, or the port is not properly connected (transfer over the connection linkage is interrupted or exceptional), the exception information will be reported to Cloud Monitor. After the port is recovered, the event status will be updated accordingly.

| Event | Event Name | Event Type | Dimension | Recoverable<br> | Event Description | Solution and Suggestion |
|---------|---------|---------|---------|---------|---------|---------|
| Connection down	 | DirectConnect<br>Down	 | Exception event | Connection	 | Yes | Transfer over the connection linkage is interrupted or exceptional	 | 1. Check whether the physical line is exceptional or interrupted (for example, the fiber cable is cut off, the line is unplugged, etc.). <br>2. Check whether the opposite interface and optical/electrical modules are normal. <br>3. Check whether the network device interface is turned off. |

You can subscribe to and query relevant event information on the [product event page in the Cloud Monitor Console](https://console.cloud.tencent.com/monitor/event/product) in the following steps:

## Subscribing to Product Event
You can configure alarm channels by subscribing to product events. When a connection product event occurs, the system will automatically push it to the monitoring system of your Tencent Cloud account.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Alarm Configuration** > **Alarm Policy** on the left sidebar to enter the alarm configuration page.
3. Click **Add** in the top-left corner to create an alarm policy.
4. On the "Create Policy" page, set the following configuration items:
 - Policy Name: enter a policy name, which can contain 1–20 characters or underscores.
 - Remarks: enter the policy remarks, which can contain 1–100 characters or underscores.
 - Policy Type: select **Direct Connect** > **Connection**.
 - Project: use the default option.
 - Alarm Object: select the connection instance object to be configured.
 - Trigger Condition: select **Configure Trigger Condition** and check **Event Alarm** only.	
 - Alarm Channel: select the target recipients, valid time period, and receipt channel.
 - API Callback: if you need callback, enter a URL accessible over the public network as the callback API address (domain name or IP[:port][/path]), and Cloud Monitor will push alarm messages to this address promptly.
5. After completing the configuration, click **Complete**.

## Querying Product Event
You can view connection exceptions by querying connection product events.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** on the left sidebar to enter the product event page.
3. Double-click "All" in "Product Type: All" in the search box on the right, select **Connection** as the product type in the drop-down list, and click **Complete**.
4. Event information of all connections under the current account in the last 7 days will be displayed in the list by default.


