Anti-DDoS supports IP blocklist and allowlist configurations to block and allow IPs connected to Anti-DDoS, restricting the users from accessing your resources. For the allowed IPs, they are allowed to access without being filtered by any protection policy; while the access requests from the blocked IPs are directly denied.
>?The IP blocklist and allowlist filtering takes effect only when your business is under CC attacks.
>- The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>- The access requests from the blocked IPs will be directly denied.


## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.


## Directions
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and select **Anti-DDoS Pro (New)** > **Configurations** on the left sidebar. Open the **CC Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/3db9584e9adc4c083500f47612012d77.png)
3. Click **Set** on the **IP Blocklist/Allowlist** section.
![](https://qcloudimg.tencent-cloud.cn/raw/a2847abc25fdf6848a669a529c8950df.png)
4. Click **Create**, and enter the required fields before you click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/4dbda8f53e7404a6bc2e7156591ac0b6.png)
5. Now the rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/e3a320a3a5f2aa400bd06bc1ea80f13b.png)
