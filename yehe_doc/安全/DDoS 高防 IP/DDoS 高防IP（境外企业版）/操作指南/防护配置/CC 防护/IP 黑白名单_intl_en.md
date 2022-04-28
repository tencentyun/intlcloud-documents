Anti-DDoS Advanced (Global Enterprise Edition) supports IP blocklist and allowlist configurations to block and allow IPs connected to Anti-DDoS, restricting the users from accessing your resources. For the allowed IPs, they are allowed to access without being filtered by any protection policy; while the access requests from the blocked IPs are directly denied.
>?The IP blocklist and allowlist filtering takes effect only when your business is under CC attacks.
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.


## Prerequisite
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition) instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.


## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** > **Configurations** > **CC Protection**.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/a2847abc25fdf6848a669a529c8950df.png)
3. Click **Set** in the **IP Blocklist/Allowlist** section.
4. Click **Create**. On the pop-up page, enter the required fields.
![](https://qcloudimg.tencent-cloud.cn/raw/4dbda8f53e7404a6bc2e7156591ac0b6.png)
**Parameter description:**
 - For **Protocol Type**, select "http" or "https" as needed.
 - For **Domain Name**, enter the domain name under the instance.
 - For **Blocked/Allowed IPs**, enter the IP or IP range.
 - For **Type**, select "Blocklist" or "Allowlist" as needed.
5. Click **Save**.
6. (Optional) After the rule is created, it is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/e3a320a3a5f2aa400bd06bc1ea80f13b.png)
