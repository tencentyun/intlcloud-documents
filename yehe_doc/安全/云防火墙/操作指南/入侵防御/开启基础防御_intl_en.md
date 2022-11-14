After basic protection is enabled, the north-south traffic on public IP addresses can be monitored based on intrusion defense rules.

## Directions
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips) and click **Intrusion Protection System** in the left navigation pane.
2. On the **Intrusion protection system** page, click **View rules** in the **Basic protection** module.
![](https://qcloudimg.tencent-cloud.cn/raw/5ddb46fb7d1a3f1dcdc1d10d043cc38f.png)
3. In the **Basic protection rules** window displayed, you can view the description of any rule.
![](https://qcloudimg.tencent-cloud.cn/raw/71eadb0f7c3aa968770d4e7d76946cc9.png)
4. After viewing the rules, click ![](https://qcloudimg.tencent-cloud.cn/raw/10ace5416baaa335087014f76ec37c9a.png) in the **Basic protection** module to enable this feature.
>?
>- When basic protection is disabled, the basic protection rules no longer take effect.
>- Only when basic protection and [edge firewall](https://console.cloud.tencent.com/cfw/switch/internet) are both enabled for a public IP address, CFW monitors the north-south traffic on this IP address based on intrusion defense rules.
>- In the Block mode, malicious behaviors that hit high-confidence rules are automatically blocked, and security event alerts are generated when other rules are hit.


## More information
For questions about intrusion defense, please see [Intrusion Protection System](https://intl.cloud.tencent.com/document/product/1160/49835).
