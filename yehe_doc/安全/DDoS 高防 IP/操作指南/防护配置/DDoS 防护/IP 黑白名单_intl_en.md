
Anti-DDoS supports configuring IP blocklist and allowlist to block or allow source IPs accessing the Anti-DDoS services, restricting the users accessing your business resources. If the accessing traffic exceeds the cleansing threshold, the allowed IPs will be allowed to access resources without being filtered by any protection policy; while the access requests from the blocked IPs will be directly denied.

## Prerequisites
You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.
>? The IP blocklist/allowlist will take effect after being created.
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) and select **Anti-DDoS Advanced (New)** > **Configurations** on the left sidebar. Open the **DDoS Protection** tab.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "bgpip-xxxxxx".
![](https://main.qcloudimg.com/raw/9926499f6012c6a88194642aae7474e0.png)
3. Click **Set** in the "IP blocklist/allowlist" section.
![](https://qcloudimg.tencent-cloud.cn/raw/6865bd3d710068fc607fbe4799aef9ad.png)
4. Click **Create**. In the pop-up window, tick **Blocklist** or **Allowlist** as the type, enter the target IP, and click **OK**.
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
5. (Optional) After the rule is created, it is added to the rule list. To delete it, click **Delete** in the "Operation" column on the right.
![](https://main.qcloudimg.com/raw/ffe79141e64da02c47ad887b3ca23ef2.png)