Dedicated tunnel exception information at the tunnel linkage level can be reported. When a tunnel linkage under your account is exceptional (for example, transfer over the connection linkage is interrupted or exceptional, BGP session is disconnected, the number of BGP session tunnel routes exceeds the limit, or BFD is interrupted), the exception information will be reported to Cloud Monitor. After the exception is recovered, the event status will be updated accordingly.

| Event | Event Name | Event Type | Dimension | Recoverable<br> | Event Description | Solution and Suggestion |
|---------|---------|---------|---------|---------|---------|---------|
| Dedicated tunnel down		 | DirectConnectTunnel<br>Down		 | Exception event | Dedicated tunnel		 | Yes | Transfer over the connection linkage is interrupted or exceptional	 | 1. Check whether the physical line is exceptional or interrupted (for example, the fiber cable is cut off, the line is unplugged, etc.). <br>2. Check whether the opposite interface and optical/electrical modules are normal. <br>3. Check whether the network device interface is turned off. |
| Dedicated tunnel BGP session down 			 | DirectConnectTunnel<br>BGPSessionDown	 | Exception event | Dedicated tunnel		 | Yes | 	BGP session of the dedicated tunnel is disconnected	 | 1. Check whether the BGP process of the network device is normal. <br>2. Check whether the dedicated tunnel is normal. <br>3. Check whether the physical line is normal. |
| Alarm of excessive BGP tunnel routes			 | DirectConnectTunnel<br>RouteTableOverload			 | Exception even | Dedicated tunnel		 | No	 | The number of BGP session tunnel routes of the dedicated tunnel exceeds 80% of the upper limit		 | Check whether the routes published by the dedicated tunnel's BGP session reaches 80% of the upper limit (the default value is 100. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/216/546) of Direct Connect). |
| Dedicated tunnel BFD down			 | DirectConnectTunnel<br>BFDDown			 | Exception event | Dedicated tunnel		 | Yes | The dedicated tunnel's bidirectional forwarding detection (BFD) is interrupted		 | 1. Check whether the dedicated tunnel is normal.<br>2. Check whether the physical line is normal. |

You can subscribe to and query relevant event information on the [product event page in the Cloud Monitor Console](https://console.cloud.tencent.com/monitor/event/product) in the following steps:

## Subscribing to Product Event
You can configure alarm channels by subscribing to product events. When a dedicated tunnel product event occurs, the system will automatically push it to the monitoring system of your Tencent Cloud account.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Alarm Configuration** > **Alarm Policy** on the left sidebar to enter the alarm configuration page.
3. Click **Add** in the top-left corner to create an alarm policy.
4. On the "Create Policy" page, set the following configuration items:
 - Policy Name: enter a policy name, which can contain 1–20 characters or underscores.
 - Remarks: enter the policy remarks, which can contain 1–100 characters or underscores.
 - Policy Type: select **Direct Connect** > **Dedicated Tunnel**.
 - Project: use the default option.
 - Alarm Object: select the dedicated tunnel instance object to be configured.
 - Trigger Condition: select **Configure Trigger Condition**, check **Event Alarm** only, and select alarm events. To configure multiple alarm events, you can click **Add** to add more events.
 - Alarm Channel: select the target recipients, valid time period, and receipt channel.
 - API Callback: if you need callback, enter a URL accessible over the public network as the callback API address (domain name or IP[:port][/path]), and Cloud Monitor will push alarm messages to this address promptly.
5. After completing the configuration, click **Complete**.

## Querying Product Event
You can view dedicated tunnel exceptions by querying dedicated tunnel product events.
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Event Center** > **Product Event** on the left sidebar to enter the product event page.
3. Double-click "All" in "Product Type: All" in the search box on the right, select **Dedicated Tunnel** as the product type in the drop-down list, and click **Complete**.
4. Event information of all dedicated tunnels under the current account in the last 7 days will be displayed in the list by default.
