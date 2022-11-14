This topic describes the operations in **Alert Management**. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/warncenter). In the [Alert Management](https://console.cloud.tencent.com/cfw/warncenter/event) page, click **Blocked attacks** to open the **Blocked attacks** page. This page displays a trend chart of blocked attacks, blocked IPs, regions, and destination ports to help you analyze and protect your assets.

## Filtering blocked attacks [](id:xinxi)
This section describes how to find the blocked attacks you want to view through filtering.
① Select the assets and regions for which you want to view the blocked attacks;
② Select **Inbound**, **Lateral movement**, or **Outbound**.
③ Select the intrusion defense policy and resolution status. You can filter the records by specifying **Blocking history ranking**, **Page refresh frequency**, and **Blocking frequency statistics**.
![](https://qcloudimg.tencent-cloud.cn/raw/58178b26aeff8d4898e6fde82ba9b849.png)

>? The above describes the operations in the asset view. For more information about operations in the event view, please see **[Filtering alert events](https://intl.cloud.tencent.com/document/product/1160/49820#kuaisudingweijingao)**.

## Resolving blocked attacks
1. This section describes how to resolve blocked attacks. For more information about how to filter blocked attacks, please see "[Filtering blocked attacks](#xinxi)".
![](https://qcloudimg.tencent-cloud.cn/raw/7ab89a6063fa61f1d2d2d4df4089cbc5.png)
>? To modify your operation, undo the operation in [**Intrusion defense**](https://console.cloud.tencent.com/cfw/ips) -> **Blocklist**, **Allowlist**, or **Quarantined list**.

2. On the **Blocked attacks** page, you can search for different assets and IPs by selecting **Inbound**, **Lateral movement**, or **Outbound**.
  - You can pin or allow the access source IPs that have been blocked in the inbound direction. For the allowed IPs, you can select **More** -> **Block** to block them if necessary.
![](https://qcloudimg.tencent-cloud.cn/raw/63a37e0d4361517ca81e8d291f38bc43.png)
  - For the assets and IPs involving lateral movement attacks, you can view the blocking history here.
 ![](https://qcloudimg.tencent-cloud.cn/raw/4fc10f15218fa4d0c21a071ab5a3993e.png)
  - You can pin, allow, quarantine, block, or ignore the assets/IPs blocked by the **Intrusion defense** module in the outbound direction.
 ![](https://qcloudimg.tencent-cloud.cn/raw/3d5cce8050260599fdcc6ccd80cad01c.png)
3. You can perform the following operations on different assets/IP addresses:
  - **Pin to top**/**Unpin**: You can pin or unpin assets. Note: A maximum of 5 items can be pinned for **Outbound** or **Inbound**.
   - **Allow**: Click **Allow** for an IP that does not need to be blocked. Then, select **Reason**, **Direction**, and **Validity**. The IP will be in the allowlist in the [**Intrusion defense**](https://console.cloud.tencent.com/cfw/ips) module within the selected period. CFW allows traffic from the IP by skipping attack detection for the IP in **Intrusion defense** within the specified period. If you are not certain about whether the reason is "false positive", you can select **Allow for emergency**, and modify it later if necessary.
<img src="https://qcloudimg.tencent-cloud.cn/raw/861cbfb061ce6c9f8d8a54630faf9325.png" style="zoom:67%;" />
   - **Block**: For assets with a high threat level, click **Block**. Then, specify a validity period and direction to add the IP to the blocklist in [**Intrusion defense**](https://console.cloud.tencent.com/cfw/ips). CFW automatically blocks that IP from accessing all of your assets within the specified period.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e400c2a47f5a14225779d2db5823bc58.png" style="zoom:67%;" />
 - **Quarantine**: Click **Quarantine**. When an asset instance is quarantined, the system automatically publishes the blocking rule for enterprise security groups to block network access to the selected asset in the specified blocking direction. This makes the subsequent troubleshooting easy and prevents the asset from being attacked.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/d925662c3badc58074566d45770cad97.png" style="zoom:67%;" />
 - **Ignore**: For repeated or possible false alerts, you can click **Ignore**. The ignored alert events are not included in the alert list and statistics, but their logs are retained. You are no longer notified of the ignored alert events when they trigger alerts again. You can select **Ignored** in the list to view all the ignored events. **The "Ignore" operation is irreversible.**
 ![](https://qcloudimg.tencent-cloud.cn/raw/74e832e49fc52bd5cbda28414f850d37.png)


## Resolving false alerts
You can add the IP to the allowlist. On the **Blocked attacks** page, select the target asset/IP, click **Allow**, select **False positive** for **Reason**, and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/de0994abcf8a25861defde20829b9998.png)

## Searching for attack events from an IP

In the **Asset view**, place the pointer over the value of **Access destination**, **Access source**, or **Asset name**, and click **Check in intrusion defense log** to view all attack events.
![](https://qcloudimg.tencent-cloud.cn/raw/efe4143f38370ca9d5d198bc617f2cba.png)

>? The figure above shows the process.

## Viewing the blocked attacks for an asset
- Method 1: Select the specified asset in the upper-left corner to filter the records.
![](https://qcloudimg.tencent-cloud.cn/raw/999eec2bf6aa857bca54481a0c95b1e3.png)
- Method 2: Select the target asset by clicking **Event details** -> **Asset name** to view its records of blocked attacks. For more information, please see [Assets Management](https://intl.cloud.tencent.com/document/product/1160/49812).

## Viewing recently blocked attacks
The **Blocked attacks** page is automatically refreshed. Click ![](https://qcloudimg.tencent-cloud.cn/raw/fc22474131de711ae3b7747da1e5cf60.png) in the upper part of the page, select **Last blocked* for **Blocking history ranking**, and then click OK** to view the recently blocked attacks.
 ![](https://qcloudimg.tencent-cloud.cn/raw/792dbfc9901aa45ab02ff925859074d7.png)