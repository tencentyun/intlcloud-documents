
Anti-DDoS supports configuring IP blocklist and allowlist to block or allow source IPs accessing the Anti-DDoS services, restricting the users accessing your business resources. If the accessing traffic exceeds the cleansing threshold, the allowed IPs will be allowed to access resources without being filtered by any protection policy; while the access requests from the blocked IPs will be directly denied.

## Prerequisites
Purchase an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to be protected.
The IP blocklist and allowlist filtering take effect only when your business is under DDoS attacks.
>?
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.
## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select the ID or port of a protected IP from the left list, e.g., **212.64.xx.xx bgpip-000002jt** or **119.28.xx.xx bgpip-000002ju** -> **tcp:8000**. Click **Set** in the **IP Blocklist/Allowlist** section to enter the IP blocklist/allowlist.
![](https://main.qcloudimg.com/raw/188d333af2cbd161c06c096c7d767531.png)
3. Click **Create**.
4. In the pop-up window, select the rule type to create a rule, and click **OK**.
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
5. Now the new rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://main.qcloudimg.com/raw/3453f2025be0bccc6429a8358986a8ed.png)
