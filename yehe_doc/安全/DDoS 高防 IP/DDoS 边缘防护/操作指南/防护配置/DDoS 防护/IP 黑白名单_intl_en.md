DDoS Edge Defender supports configuring IP blocklist and allowlist to block or allow source IPs accessing the DDoS Edge Defender service, restricting the users accessing your business resources. If the accessing traffic exceeds the cleansing threshold, the allowed IPs will be allowed to access resources without being filtered by any protection policy; while the access requests from the blocked IPs will be directly denied.

## Prerequisites
You have successfully purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance and set the object to protect.
>?
>- The IP blocklist and allowlist filtering take effect only when your business is under DDoS attacks.
>   - The allowed IPs will be allowed to access resources without being filtered by any protection policy.
>   -	The access requests from the blocked IPs will be directly denied.
>- DDoS Edge Defender is currently available to beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Protection Policy** on the left sidebar, and then select **DDoS Protection**.
2. Select an Edge Defender instance ID in the list on the left, such as "edge-xxxxxxx".
![](https://main.qcloudimg.com/raw/dcb8de6c5b81f6f522b25962f4ad3c11.png)
3. Click **Set** in the **IP Blocklist/Allowlist** section to enter the IP blocklist/allowlist.
![](https://main.qcloudimg.com/raw/ef1dedadf78a150fea126532b79f7f68.png)
4. Click **Create**.
5. In the pop-up window, select the rule type to create a rule, and click **OK**.
![](https://main.qcloudimg.com/raw/1c3a46e9eea39733555bec2741bedc10.png)
6. Now the new rule is added to the list. You can click **Delete** on the right of the rule to delete it.
![](https://main.qcloudimg.com/raw/ffe79141e64da02c47ad887b3ca23ef2.png)
