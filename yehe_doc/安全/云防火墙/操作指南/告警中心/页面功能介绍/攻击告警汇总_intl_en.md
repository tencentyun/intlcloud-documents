The **Attack alerts** module displays all monitored risk events and allows you to analyze and resolve all events detected by CFW.

## Visual representation of attack alerts
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/warncenter). In the left navigation pane, click **Alert Management** -> **Attack alerts** to open the **Attack alerts** page.
2. In this module, you can analyze existing security alert events by **①personal assets** and **②time range** (24 hours, 7 days, or a custom time range) with a graph. The left section displays the trend curve of recent security events, with the x-axis indicating time and the y-axis indicating the number of alerts at each point in time. In addition, you can view the statistics about compromised servers, pending events, network scans, and exploit attacks. The right section displays the list of the top 10 IPs with the most attack alerts so that you can take early action to prevent attacks of those IPs.

## Attack alert list
In this module, you can analyze alert events under different **① event types**, **② batch resolve events**, **③ filter events by conditions**, and **④ specify custom keywords**.
<dx-tabs>
::: ① Alert event type
Click the tabs in the area marked "①" to view the details of the alerts of different types.

>? The relevant security event types are displayed only after you configure the security policies required by CFW in [Intrusion defense](https://www.tencentcloud.com/document/product/1160/49856), and [Security baseline](https://console.cloud.tencent.com/cfw/secline).

:::
::: ② Batch resolve events
You can click **Block all** for all selected events, or **Allow** or **Ignore** them in batch mode.
>?These buttons are only available when one or more events are selected.

:::
::: ③ Filter events by conditions
Select values from the drop-down lists marked "③" to filter the alert events. The following capabilities are supported:
- View the information of unresolved, blocked, allowed, and ignored alert events.
- Filter alert events by severity.
- Filter alert events by security event type, protocol, and source.
- Filter events by keywords.
:::
::: ④ Specify custom keywords
Click the icon marked "④" to specify custom keywords. A maximum of 10 keywords are allowed.

:::
</dx-tabs>

### [Event details](id:keshihua)
- Click ![](https://main.qcloudimg.com/raw/5bd2ce213f9b7119211793e39ab46eea.png) next to a malicious IP to filter out all security events of that IP under the current type.
- Click ![](https://main.qcloudimg.com/raw/7db35c3a6e1a5ed4832ae18db6fff300.png) on the left to view the details of an event.
>? You need to purchase [CWPP](https://intl.cloud.tencent.com/document/product/296) to use the enhanced detection features of CWPP.

- Click **Learn more** to view the threat profile.
- Click **Block**, **Allow**, or **Ignore** on the right to resolve alert events individually.
>?
>- The following operations also apply to batch processing and events for other types of IPs.
>- To modify your operation, undo the operation in **[Intrusion defense](https://console.cloud.tencent.com/cfw/ips)** -> **Blocklist**.

 - **Block**: For security events with a higher severity or a larger number of alerts, click **Block** to add the IP to the blocklist in [Intrusion defense](https://console.cloud.tencent.com/cfw/ips). CFW automatically blocks that IP from accessing all of your assets within the specified period.
  - **Allow**: For repeated or possible false alerts, you can click **Allow** to add the IP to the allowlist in [Intrusion defense](https://console.cloud.tencent.com/cfw/ips). CFW allows traffic from the IP by skipping attack detection for the IP in **Intrusion defense** within the specified period.
  - **Ignore**: If you do not want to take action on an alert, click **Ignore**. The log is not deleted. You can view the log in the list of ignored alerts.