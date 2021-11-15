## Protection Description
DDoS Edge Defender provides three protection levels against CC attacks for stronger protection and less false blocking. The default level is Medium.
<dx-tabs>
::: Loose
This level applies to a protected website without obviously exceptional traffic. It will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. As this CC protection policy is loose, a small number of exceptional requests may pass through the security system.
:::
::: Medium
This level is set as the default. We recommend this protection level when a protected website is under CC attacks. Compared with the Loose level, it can cover most of attack scenarios and defend against most of CC attacks.

Meanwhile it will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. This level only applies to website applications. If your application is related to APIs or apps, configure CC frequency limiting rules for protection.
:::
::: Strict
This level applies to more complex CC attacks. It will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. As this verification mode is strict, some normal requests may be blocked. This level only applies to website applications. If your application is related to APIs or apps, configure CC frequency limiting rules for protection.
:::
</dx-tabs>

>!
>- The protection algorithms for the above three CC protection levels are only applicable to webpages and HMTL5 pages.
>- False blocking is highly likely to occur in a visited website for API or native app businesses, as requests to the website cannot pass the verification.
>- To protect your API or native app business from CC attacks, please [contact us](https://intl.cloud.tencent.com/contact-us) to customize protection policies.



## Prerequisites
You have successfully purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance and set the object to protect.

>? DDoS Edge Defender is currently available to beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Protection Policy** on the left sidebar, and then select the tab **CC Protection**.
2. Select an Edge Defender instance ID, such as "edge-xxxxxxx".
![](https://main.qcloudimg.com/raw/dcb8de6c5b81f6f522b25962f4ad3c11.png)
3. Click **Set** in the **CC Protection Level and Cleansing Threshold** section on the right.
![](https://main.qcloudimg.com/raw/3c21b89cfe530036d19b1a2ba786ce77.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields, set the protection level and click **OK**.
>?
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the protection is enabled, your instance will use the default cleansing threshold after your business is connected, and the system will generate a baseline based on historical patterns of your business traffic. You can also set the cleansing threshold for your business needs.
>- If you have a clear concept about the threshold, set it as required. Otherwise leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and calculate the default threshold for you.

![](https://main.qcloudimg.com/raw/e7b4399a157ef5e3f08fe678422cb3ab.png)
6. Now a CC domain name protection rule is added to the CC protection level and cleansing threshold list. You can click **Configuration** on the right of the rule to modify the CC protection level and cleansing threshold.
![](https://main.qcloudimg.com/raw/0646d3fe7a54afecd17d7b4c6d6880c7.png)
