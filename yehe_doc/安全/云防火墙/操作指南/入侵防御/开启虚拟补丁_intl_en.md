After virtual patching is enabled, CFW automatically identifies and blocks north-south traffic that may exploit vulnerabilities to launch attacks, preventing CVM vulnerabilities from being exposed to the Internet.

## Directions
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips) and click **Intrusion Protection System** in the left navigation pane.
2. On the **Intrusion protection system** page, click **View rules** in the **Virtual patching** module.
![](https://qcloudimg.tencent-cloud.cn/raw/ae80c990f36c3309ac11f450cb8bdd19.png)
3. In the **Virtual patch rules** window displayed, you can view all the patches applied and the description of corresponding vulnerabilities.
![](https://qcloudimg.tencent-cloud.cn/raw/8818a2b5d6d6524f1812f13a7357174c.png)
4. After viewing patch rules, click ![](https://qcloudimg.tencent-cloud.cn/raw/4030f9442689ec668ab21620a72d6b57.png) next to **Virtual patching** in the **Virtual patching** module to enable this feature.
>!
>- When virtual patching is enabled, the virtual patch rules take effect for public IP addresses with this feature enabled.
>- When virtual patching is disabled, the virtual patch rules do not take effect.
>- In the Block mode, all intrusions are automatically blocked.

## More information
For questions about intrusion defense, please see [Intrusion Protection System](https://intl.cloud.tencent.com/document/product/1160/49835).
