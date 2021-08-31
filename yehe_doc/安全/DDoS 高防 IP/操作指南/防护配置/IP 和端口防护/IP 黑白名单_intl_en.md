
Anti-DDoS Pro supports IP blocklist and allowlist configurations to block or allow source IPs accessing the Anti-DDoS Pro service, restricting the users accessing your business resources. For the allowed IPs, they are allowed to access without being filtered by any protection policy; while the access requests from the blocked IPs are directly denied.

## Prerequisites
Purchase an [Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/36115) and set the object to be protected.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Anti-DDoS Pro (New)** -> **Configurations** on the left sidebar.
2. Select an instance ID from the left list, e.g., `bgp-000000iu`, open the **IP and Port Protection** tab, and then click **Set** in the **IP Blocklist/Allowlist** section.
![](https://main.qcloudimg.com/raw/07b8daad2b3a04be6bd6d6dc68ea9d7e.png)
3. Click **Create** to create a blocklist or allowlist rule.
![](https://main.qcloudimg.com/raw/980fe2e07d4404255a30101a206de02c.png)
4. In the pop-up window, tick **Blocklist** or **Allowlist** as the type, enter the target IP, and click **OK**.
![](https://main.qcloudimg.com/raw/e16a265499ee7762b497d1aac0370ab4.png)
5. Now the rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://main.qcloudimg.com/raw/a7f5b24ff9d6ebcdac1282297e85c432.png)
