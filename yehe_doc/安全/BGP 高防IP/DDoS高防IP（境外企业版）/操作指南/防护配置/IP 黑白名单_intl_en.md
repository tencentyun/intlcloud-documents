Anti-DDoS supports configuring IP blocklist and allowlist to block or allow source IPs accessing the Anti-DDoS services, restricting the users accessing your business resources. If the accessing traffic exceeds the cleansing threshold, the allowed IPs will be allowed to access resources without being filtered by any protection policy; while the access requests from the blocked IPs will be directly denied.

## Prerequisites
You have purchased an Anti-DDoS Advanced (Global Enterprise Edition) instance and set your target to protect.
>?The IP blocklist and allowlist filtering take effect only when your business is under DDoS attacks.
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.


## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/d6586694f3fc6b1cbc6099b6b1498c38.png)
3. Click **Set** in the **IP Blocklist/Allowlist** section to enter the IP blocklist/allowlist.
![](https://main.qcloudimg.com/raw/547da2bb027b1a379ee82d44db8330d7.png)
4. Click **Create**.
5. In the pop-up window, select the rule type to create a rule, and click **OK**.
![](https://main.qcloudimg.com/raw/653dfbd6db8d33a70453a64cee1d66f2.png)
6. Now the new rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://main.qcloudimg.com/raw/aa6f0a3a9758bdf990b31daebd758497.png)
