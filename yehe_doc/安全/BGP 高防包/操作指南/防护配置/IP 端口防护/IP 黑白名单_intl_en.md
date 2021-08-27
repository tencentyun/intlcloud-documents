
Anti-DDoS Pro supports IP blocklist and allowlist configurations to block or allow source IPs to access the Anti-DDoS service, restricting the users from accessing your business resources. For the allowed IPs, they are allowed to access without being filtered by any protection policy; while the access requests from the blocked IPs are directly denied.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.
>?
>- The IP blocklist and allowlist filtering take effect only when your business is under DDoS attacks.
>  - The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>  - The access requests from the blocked IPs will be directly denied.


## Directions
1. Log in to the [Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and select **Configurations** on the left sidebar.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://main.qcloudimg.com/raw/07b8daad2b3a04be6bd6d6dc68ea9d7e.png)
3. Click **Set** in the **IP Blocklist/Allowlist** section to enter the IP blocklist/allowlist.
![](https://main.qcloudimg.com/raw/980fe2e07d4404255a30101a206de02c.png)
4. Click **Create** to create an IP blocklist/whitelist.
5. In the pop-up window, tick **Blocklist** or **Allowlist** as the type, enter the target IP, and click **OK**.
![](https://main.qcloudimg.com/raw/e16a265499ee7762b497d1aac0370ab4.png)
6. Now the new rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://main.qcloudimg.com/raw/a7f5b24ff9d6ebcdac1282297e85c432.png)
