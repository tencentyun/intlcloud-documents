## Protection Description
In order to improve the protection effect and reduce the risk of false blocking during protection, Anti-DDoS Advanced has three protection levels for CC attacks for your choice, and the "Medium" level is used by default.
<dx-tabs>
::: Loose
This level applies to a protected website without obviously exceptional traffic. It will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. As this CC protection policy is loose, a small number of exceptional requests may pass through the security system.
:::
::: Medium
This level is set as the default. We recommend this protection level when a protected website is under CC attacks. Compared with the Loose level, it can cover most of attack scenarios and defend against most of CC attacks. Meanwhile it will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website.
:::
::: Strict
This level applies to more complex CC attacks. It will run checks on all visitor requests by using human verification algorithm. Only the visitors who successfully authenticate are allowed to access the website. As this verification mode is strict, some normal requests may be blocked.
:::
</dx-tabs>

>!
>- The protection algorithms for the above three CC protection levels are only applicable to webpages and HMTL5 pages.
>- If the business of the visited website is an API or a native app, as such businesses generally cannot respond to algorithm-based authentication normally, there is a great risk of false blocking.
>- To protect your API or native app business from CC attacks, please [contact us](https://intl.cloud.tencent.com/contact-us) to customize protection policies.


## Prerequisites
You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Protection Configuration** on the left sidebar.
2. Select a domain name under an instance ID from the left list, e.g., **212.64.xx.xx bgpip-000002je** -> **http:80** -> **www.xxx.com**.
![](https://main.qcloudimg.com/raw/9b99b60388bd40282a34316cda196b64.png)
3. In the **CC Protection Policy** section, set the protection level to **Loose**, **Medium**, or **Strict** as needed and set the cleansing threshold.
>?
>- The cleansing threshold is the threshold for Anti-DDoS services to start cleansing traffic. If the number of HTTP requests sent to the specified domain name exceeds the threshold, CC protection will be triggered.
>- If the protection is enabled, your Anti-DDoS Advanced instance will use the default cleansing threshold after your business is connected, and the system will generate a baseline based on historical patterns of your business traffic. You can also set the cleansing threshold for your business needs.
>- If you have a clear concept about the threshold, set it as required. Otherwise please leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and generate the default threshold for you.
