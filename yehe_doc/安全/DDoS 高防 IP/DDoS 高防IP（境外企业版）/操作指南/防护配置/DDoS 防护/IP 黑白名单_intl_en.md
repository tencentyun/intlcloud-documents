Anti-DDoS Advanced (Global Enterprise Edition) supports configuring IP blocklist and allowlist to block or allow source IPs accessing the Anti-DDoS services, restricting the users accessing your business resources. If the accessing traffic exceeds the cleansing threshold, the allowed IPs will be allowed to access resources without being filtered by any protection policy; while the access requests from the blocked IPs will be directly denied.

## Prerequisite
- You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition)](https://intl.cloud.tencent.com/document/product/297/41154) instance and set the object to protect.
>?The IP blocklist and allowlist filtering take effect only when your business is under DDoS attacks.
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.


## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) and select **Anti-DDoS Advanced** > **Configurations** > **DDoS Protection**.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://qcloudimg.tencent-cloud.cn/raw/6865bd3d710068fc607fbe4799aef9ad.png)
3. Click **Set** in the **IP Blocklist/Allowlist** section.
4. Click **Create**. On the pop-up page, select a protocol type, enter an IP, and then click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/4dbda8f53e7404a6bc2e7156591ac0b6.png)
6. After the rule is created, it is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/e3a320a3a5f2aa400bd06bc1ea80f13b.png)
