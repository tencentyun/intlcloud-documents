Intelligent CC protection is an AI-powered protection feature leveraging Tencent Cloud's big data capability. It provides a dynamic protection model to auto-generate rules for detecting and blocking malicious attacks based on website traffic patterns and algorithm-utilized attack analysis.

## Prerequisites
- You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.
- Only rules configured for instances accessing via domain names take effect.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port). Select **Anti-DDoS Advanced (New)** > **Configurations** on the left sidebar. Open the **CC Protection** tab.
2. Select a domain name from the IP list on the left.
![](https://qcloudimg.tencent-cloud.cn/raw/4751fcbaaa957df96ddc3f231efd65cb.png)
3. In the "CC Protection and Cleansing Threshold" card, click ![](https://qcloudimg.tencent-cloud.cn/raw/b56da8e70914bb5f6fce1900bcf81ef5.png) and set a cleansing threshold before enabling intelligent CC protection.
>?
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the IP bound to the Anti-DDoS Pro instance is from WAF, you need to first enable CC protection for the IP in the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig). For more information, see [CC Protection Rules](https://intl.cloud.tencent.com/document/product/627/11709).

![](https://qcloudimg.tencent-cloud.cn/raw/c412b2951b9f094f6cfdb236bc09488c.png)
4. In the **Intelligent CC protection** card, toggle on ![](https://qcloudimg.tencent-cloud.cn/raw/9795d7ce17dc03f5be0daae4ef488f98.png) the switch.
![](https://qcloudimg.tencent-cloud.cn/raw/7319818d35265c8ef08cad415e177988.png)
5. Click **View** to view the auto-generated protection rules. You can make changes to these rules if necessary.
>!
>- When intelligent CC protection is enabled, the protection rules are auto-generated when an attack occurs.
>- Protect mode: Apply auto-generated protection rules to defend against each specific attack. After the attack ends, the rules are automatically deleted.
>- Observe mode: Attacks are observed only.

![](https://qcloudimg.tencent-cloud.cn/raw/05c94576d64fd977aad5ee8d7270a56b.png)
6. To delete a rule, click **Delete** on the right of the rule you want to remove.
![](https://qcloudimg.tencent-cloud.cn/raw/eb76d5ebd36b1340f9c6cd986c0ce64a.png)
