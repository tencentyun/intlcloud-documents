## Protection Description
Anti-DDoS Pro provides three protection levels against DDoS attacks for stronger protection and less false interception. The default level is Medium.
<dx-tabs>
::: Loose
This level applies to a protected website without obviously exceptional traffic. It will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. As this CC protection policy is loose, a small number of exceptional requests may pass through the security system.
:::
::: Medium
This level is set as the default. We recommend this protection level when a protected website is under CC attacks. Compared with the Loose level, it can cover most of attack scenarios and defend against most of CC attacks. Meanwhile it will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. This level only applies to website business. If your business is about APIs or apps, protect your business with the CC frequency limit policies.
:::
::: Strict
This level applies to more complex CC attacks. It will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. As this verification mode is strict, some normal requests may be blocked. This level only applies to website business. If your business is about APIs or apps, protect your business with the CC frequency limit policies.
:::
</dx-tabs>

>!
>- The protection algorithms for the above three CC protection levels are only applicable to webpages and HMTL5 pages.
>- False blocking is highly likely to occur in a visited website for API or native app businesses, as requests to the website cannot pass the verification.
>- To protect your API or native app business from CC attacks, please [contact us](https://intl.cloud.tencent.com/contact-us) to customize protection policies.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/ddos/antiddos-native/config/port) and click **Configurations** on the left sidebar.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-0000017m", and click **Domain Name Protection** at the top on the right.
![](https://main.qcloudimg.com/raw/29f77e71117c9c4217176f19373cf44e.png)
3. Click "Cleansing Threshold" in the **CC Protection Level and Cleansing Threshold** section, and choose a cleansing threshold from the drop-down list. You can also define a cleansing threshold.
>?
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the protection is enabled, your Anti-DDoS Pro instance will use the default cleansing threshold after your business is connected, and the system will generate a baseline based on historical patterns of your business traffic. You can also set the cleansing threshold for your business needs.
>- If you have a clear concept about the threshold, set it as required. Otherwise leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and calculate the default threshold for you.
4. Click **Set** in the **CC Protection Level and Cleansing Threshold** section to enter the CC protection level and cleansing threshold rule list.
![](https://main.qcloudimg.com/raw/3c21b89cfe530036d19b1a2ba786ce77.png)
5. Click **Create** at the top on the left, and set the protection level.
>? When a new rule is created, CC protection is enabled by default and a custom cleansing threshold for a domain name is supported.

![](https://main.qcloudimg.com/raw/e7b4399a157ef5e3f08fe678422cb3ab.png)
6. Click **OK** to add the rule.
>! Refined rules take precedence over rules at the Anti-DDoS Pro instance dimension.
7. Now a CC protection domain name rule is added to the CC protection domain name list. You can click **Configuration** on the right of the rule to modify the CC protection level and cleansing threshold.
![](https://main.qcloudimg.com/raw/0646d3fe7a54afecd17d7b4c6d6880c7.png)
