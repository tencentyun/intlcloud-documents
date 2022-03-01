## Protection Description
"CC Protection" identifies and blocks CC attacks based on access attributes and connection status. It provides scenario-specific configurations to create protection rules, helping secure your business. It also supports the cleaning threshold setting.
>? This switch controls wether to enable CC protection. Only when it is on, all the CC protection policies take effect.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/config/port) and select **Configurations** on the left sidebar. Open the **CC Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/48b33703155d1418b3a1c3aab979e8f4.png)
3. To enable CC protection in the "CC Protection and Cleansing Threshold" section, click ![](https://qcloudimg.tencent-cloud.cn/raw/b56da8e70914bb5f6fce1900bcf81ef5.png) and set a cleansing threshold.
>?The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.

![](https://qcloudimg.tencent-cloud.cn/raw/48b33703155d1418b3a1c3aab979e8f4.png)
4. Click **Set** in the **CC Protection and Cleansing Threshold** section to enter the rule list.
5. Click **Create**, and enter the required fields and set a cleansing threshold.
>?
>- When you create CC frequency limiting rules, CC protection is enabled by default.
>- Connected Anti-DDoS Pro instances will use the default cleansing threshold, and the system will generate a baseline based on historical patterns of your application traffic. You can set a cleansing threshold for a single domain name.

![](https://qcloudimg.tencent-cloud.cn/raw/9ff82f6f7a954a392a39de161655875d.png)
6. Click **Save**.
>!Refined rules take precedence over rules at the Anti-DDoS Pro instance dimension.

7. After the rule is created, it is added to the rule list. When the defense level is "Custom", click ![](https://qcloudimg.tencent-cloud.cn/raw/5034a8bab40f77233b1c6e7654414019.png) and ![](https://qcloudimg.tencent-cloud.cn/raw/7655c41673eb4d876ab44f11c5ade35f.png) to enable CC protection and set a cleansing threshold.
![](https://qcloudimg.tencent-cloud.cn/raw/33ef39ad86b2400066b9d908cc2516c0.png)



