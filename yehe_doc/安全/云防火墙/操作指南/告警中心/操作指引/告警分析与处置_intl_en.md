This topic describes the operations in **Alert Management**. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/warncenter) and open the [Alert Management](https://console.cloud.tencent.com/cfw/warncenter/event) page, and then click **Attack alerts** to go to the **Attack alerts** page. On this page, you can view the trend chart of security events and the number of recent security events, and then adjust your defense policies to prevent attacks.
## Filtering alert events[](id:kuaisudingweijingao)
This section describes how to locate the alert events you want to view through filtering.
① Select the assets for which you want to view the alert events;
② Select the type of alert events.
③ Select whether to view unresolved events or resolved events;
④ Sort events in the order of occurrence time and the number of occurrences, or filter events by attack event type, severity, protocol, and source.
![](https://qcloudimg.tencent-cloud.cn/raw/d179c138aa4b2de22e2f6b741110fded.png)

>? 
>- To view all critical or high-risk events, select the level from the **④Severity** column and then view the events by clicking different types of **②alert events**.
>- You can also enter keywords in the search bar on the right to search for the events you need.

## Resolving alert events
This section describes how to resolve alert events. For more information about how to filter alert events, please see "[Filtering alert events](#kuaisudingweijingao)".
![](https://qcloudimg.tencent-cloud.cn/raw/47765326bd23edae3a46ee9ecf1491a1.png)
① You can click **Block**, **Allow**, or **Ignore** to resolve an alert.

>? To modify your operation, undo the operation in [**Intrusion defense**](https://console.cloud.tencent.com/cfw/ips) -> **Blocklist**.

  - **Block**: For security events with a higher severity or a larger number of alerts, click **Block** to add the IP to the blocklist in [Intrusion defense](https://console.cloud.tencent.com/cfw/ips). CFW automatically blocks access from this IP to all your assets within the specified period.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6148aa197793aa82b7f88a70689671b2.png" style="zoom:67%;" />
  - **Allow**: For repeated or possible false alerts, you can click **Allow** to add the IP to the allowlist in [Intrusion defense](https://console.cloud.tencent.com/cfw/ips). CFW allows traffic from the IP by skipping attack detection for the IP in **Intrusion defense** within the specified period.
    <img src="https://qcloudimg.tencent-cloud.cn/raw/395b06efb0db2330bbc03cfc5ab693e0.png" style="zoom:67%;" />
  - **Ignore**: If you do not want to take action on an alert, click **Ignore**. The log is not deleted. You can view the log in the list of ignored alerts.
>! "Ignore" operation is irreversible.

  ![](https://qcloudimg.tencent-cloud.cn/raw/bfa4c3d1fe5732b2a3094b5fd0bad898.png)

② Select multiple alert events in the area marked "②" on the left.
> ? 
>- To select alert events across pages, select the target events on the current page and then go to another page to select more events.
>- This applies to all multi-selection scenarios.

③ You can click **Block all**, **Allow**, or **Ignore** to batch resolve multiple events.

## Searching for security events of an IP
This section describes how to search for all security events of an IP. Locate a security event of the IP of your interest, and click ![](https://main.qcloudimg.com/raw/93468c10726b1e12ef8b3d0d98063cb4.png) to the right of the IP to list all security events of the IP.
![](https://qcloudimg.tencent-cloud.cn/raw/5243c6c1be8b588d1dd6f7046e611c5a.png)

>? This applies to all the scenarios where you need to filter security events of IPs, regardless of the IP types.

## Searching for security events of an asset
This section describes how to search for all security events of an asset.
 - Method 1: In the drop-down list in the upper-left corner of the view, select the target asset.
![](https://qcloudimg.tencent-cloud.cn/raw/f4b892dddc10cbacdd8c6044e18215ab.png)
 - Method 2: Locate a security event of your interest, and click ![](https://main.qcloudimg.com/raw/a6e0dab1d7ed30366506e87777c5a61e.jpg) to the right of the asset.
![](https://qcloudimg.tencent-cloud.cn/raw/d0e7a2213d37c489260955d31c89b689.png)
>? This applies to all scenarios where you need to view events by asset.

## Viewing recent security events
To view the recent security events, select all assets and all sources, and then click the arrow to the right of **Occurrence time** to sort the security events in reverse chronological order. You can switch between different alert types by clicking the tabs on the top. For more information, see **[Filtering alert events](#kuaisudingweijingao)**.
![](https://qcloudimg.tencent-cloud.cn/raw/b1ee4cc304d50064356fe6e765080a59.png)
