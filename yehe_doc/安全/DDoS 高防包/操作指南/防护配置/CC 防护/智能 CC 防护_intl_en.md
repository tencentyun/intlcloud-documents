Intelligent CC protection is an AI-powered protection feature leveraging Tencent Cloud's big data capability. It provides a dynamic protection model to auto-generate rules for detecting and blocking malicious attacks based on website traffic patterns and algorithm-utilized attack analysis.

## Prerequisites
- You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the object to protect.
- Only rules configured for instances accessing via domain names take effect.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/config/web). Select **Anti-DDoS Pro (New)** > **Configurations** on the left sidebar. Open the **CC Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/2dbdfc215ffe3d739eb3695f06e5385b.png)
3. In the "CC Protection and Cleansing Threshold" card, click ![](https://qcloudimg.tencent-cloud.cn/raw/b56da8e70914bb5f6fce1900bcf81ef5.png) and set a cleansing threshold before enabling intelligent CC protection.
>?
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the IP bound to the Anti-DDoS Pro instance is from WAF, you need to first enable CC protection for the IP in the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig). For more information, see [CC Protection Rules](https://intl.cloud.tencent.com/document/product/627/11709).

![](https://qcloudimg.tencent-cloud.cn/raw/9ebf3f22e757352b303cc1b0183080d2.png)
4. In the " Intelligent CC Protection" card, click **Set**.
![](https://qcloudimg.tencent-cloud.cn/raw/7eab58ff66f68d1c3b156b017aefbe47.png)
5. On the **CC AI Protection** page, click **Create**, enter the domain name to be protected, enable CC AI protection, select the defense status, and click **Save**.
>? In the observation mode, protection rules are generated intelligently but don't take effect.

![](https://qcloudimg.tencent-cloud.cn/raw/2c962326fe0c61a18da9b0b577f803b9.png)

6. When intelligent CC protection is enabled, protection rules are auto-generated and only effective for each attack. Once a single attack ends, the protection rules will automatically expire and be removed. If you need to make changes to your rules, you can click **View** on the right to edit.
![](https://qcloudimg.tencent-cloud.cn/raw/a0a3b2ad9ea98a3e74267091c3ad628b.png)
7. To delete a rule, click **Delete** on the right of the rule you want to remove.
![](https://qcloudimg.tencent-cloud.cn/raw/4b67dce0662b09048b003d6a44ca9971.png)