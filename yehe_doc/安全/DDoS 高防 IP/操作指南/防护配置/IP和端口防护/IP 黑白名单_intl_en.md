Anti-DDoS supports configuring IP blocklist and allowlist to block or allow source IPs accessing the Anti-DDoS services, restricting the users accessing your business resources. If the accessing traffic exceeds the cleansing threshold, the allowed IPs will be allowed to access resources without being filtered by any protection policy; while the access requests from the blocked IPs will be directly denied.

## Prerequisites
- You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.
>?The IP blocklist and allowlist filtering take effect only when your business is under DDoS attacks.
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.


## Directions
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and select **Anti-DDoS Advanced (New)** > **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/9926499f6012c6a88194642aae7474e0.png)
3. Click **Set** in the **IP Blocklist/Allowlist** section to enter the IP blocklist/allowlist.
![](https://main.qcloudimg.com/raw/30e91f059daf331222b5e3cb1741b318.png)
4. Click **Create**.
5. In the pop-up window, select the rule type to create a rule, and click **OK**.
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
5. Now the new rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://main.qcloudimg.com/raw/ffe79141e64da02c47ad887b3ca23ef2.png)

