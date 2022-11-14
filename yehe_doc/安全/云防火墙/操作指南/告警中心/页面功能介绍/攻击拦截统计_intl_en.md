The **Blocked attacks** module presents all the security events blocked by CFW based on configured rules and threat intelligence, and allows you to analyze and resolve all blocked attacks.

## Visual representation of blocked attacks
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/warncenter). In the left navigation pane, click **Alert Management** -> **Blocked attacks** to open the **Blocked attacks** page.
2. In this module, you can analyze existing security alert events by **① personal assets**, **② region**, and **③ time range** (24 hours, 7 days, or a custom time range) with a graph. The left section displays the trend curve of recently blocked events, with the x-axis indicating time and the y-axis indicating the number of blocked attacks at each point in time. In addition, you can view the statistics about blocked malicious outgoing access, attacks blocked by blocklist, blocked brute-force attacks, and exploit attacks. On the right, you can view the ranking of blocked events by blocked IP, geographic location, and destination port.
>? This page is automatically refreshed at an interval. You can set **④Auto refresh rate** to **30s** or **60s**.

![](https://qcloudimg.tencent-cloud.cn/raw/070ee66606052718c42a7bec6ef4184f.png)

## List of blocked attacks
Blocked events are divided into **Inbound**, **Lateral movements**, and **Outbound** based on the traffic direction.
![](https://qcloudimg.tencent-cloud.cn/raw/af23e28386114c2e82db789ed293cc25.png)
<dx-tabs>
::: ① Batch resolve events
You can click **Block all**, **Block**, or **Ignore** for selected events.

>?These buttons are only available when one or more events are selected.

:::
::: ② Filter events by conditions
Select values from the drop-down lists marked "②" to filter blocked events. The following capabilities are supported:
- Display blocked events by intrusion defense policy and resolution status.
- Sort blocked events by blocking time, blocking statistics, and average blocking frequency.
- Record blocked events at a frequency of minutes, hours, or days.
- Filter events by keywords.
::: 
::: ③ Full-screen display
 - Click ![](https://main.qcloudimg.com/raw/3e8d19212c5f062acace92276889cf9e.png) to switch to the full-screen display mode.
 - Click ![](https://main.qcloudimg.com/raw/38aac1bda3c2ed4054d997dce9357ab3.png) to switch back to the original display mode.
:::
::: ④ Switch view
 Click **Asset view** or **Event view** to switch between the two views.
:::
</dx-tabs>

### Asset view
In this view, the blocked events from the same access source are displayed based on attacker assets.
- You can click the IP of the access source on the left to view the threat profile.
![](https://qcloudimg.tencent-cloud.cn/raw/9173cb319c7636eff252626357cef773.png)
- Click **Pin to top** or **Allow**, or click **More** -> **Quarantine/Block/Ignore** on the right to pin, allow, quarantine, block, or ignore an IP.
>? 
>- The available buttons on the right vary depending on the state of the assets.
>- The following operations also apply to batch processing and event view.
>- To modify your operation, undo the operation in **[Intrusion defense](https://console.cloud.tencent.com/cfw/ips)** -> **Blocklist**.

![](https://qcloudimg.tencent-cloud.cn/raw/70211e36e00d6b047ca027843f7e7b21.png)
 - **Pin to top**/**Unpin**: You can pin or unpin assets. Note: A maximum of 5 items can be pinned for **Outbound** or **Inbound**.
 - **Allow**: Click **Allow** for an IP that does not need to be blocked. Then, select **Reason** and **Validity**. Within the selected validity period, the IP is in the access control allowlist and is not blocked. If you are not certain about whether the reason is "false positive", you can select **Allow for emergency**, and modify it later if necessary.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e66d616641aa6a6ce9ea931788fd540c.png" style="zoom:67%;" />
 - **Quarantine**: Click **Quarantine**. When an asset instance is quarantined, the system automatically publishes the blocking rule for enterprise security groups to block network access to the selected asset in the specified blocking direction. This makes the subsequent troubleshooting easy and prevents the asset from being attacked.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/6b7701ba27d31d3b9c2eb5897a62f90b.png" style="zoom:67%;" />
 - **Block**: For assets with a high threat level, click **Block**. Then, specify a validity period to add the IP to the blocklist in [<font color=#006EFF>**Intrusion defense**</font>](https://console.cloud.tencent.com/cfw/ips). CFW automatically blocks that IP from accessing all of your assets within the specified period.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7902f55f9852b35d17e76020d8df780b.png" style="zoom:67%;" />
 - **Ignore**: For repeated or possible false alerts, you can click **Ignore**. The ignored alert events are not included in the alert list and statistics, but their logs are retained. You are no longer notified of the ignored alert events when they trigger alerts again. You can select **Ignored** in the list to view all the ignored events. **The "Ignore" operation is irreversible.**
![](https://qcloudimg.tencent-cloud.cn/raw/b18fabfddfac986e0e913293a5c1a741.png)

### Event view
For more information about operations in this view, please see [Attack alerts - Event details](https://intl.cloud.tencent.com/document/product/1160/49816#keshihua).
