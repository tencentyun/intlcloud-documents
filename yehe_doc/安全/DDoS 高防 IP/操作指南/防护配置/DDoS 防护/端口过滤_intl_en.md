Anti-DDoS Advanced enables you to block or allow inbound traffic by ports. With port filtering enabled, you can customize port settings against inbound traffic, including the protocol type, source port and destination port ranges and set the protection action (allow/block/discard) for the matched rule.

## Prerequisites
You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) and select **Anti-DDoS Advanced (New)** > **Configurations** on the left sidebar. Open the **DDoS Protection** tab.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "bgpip-xxxxxx".
![](https://main.qcloudimg.com/raw/dcb8de6c5b81f6f522b25962f4ad3c11.png)3. Click **Set** in the **Port Filtering** section to enter the page.
![](https://qcloudimg.tencent-cloud.cn/raw/f49c805c5fbf89de4e5cd8ab8bf941ab.png)
4. Click **Create**, enter the required fields based on the action you select, and then click **Save**.
>?
>- Multiple instances can be created at a time. For instances without protected resources, you cannot create rules.
>- For **Priority**, enter an integer between 1-1000. A rule with a lower number has higher priority and is listed higher. Default: 10.

![](https://qcloudimg.tencent-cloud.cn/raw/a9133be52adb1193a8bc2bf8e0ec78b9.png)
6. After the rule is created, it is added to the rule list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/3c0af9d892ef890d41c61c2add90b15f.png)
