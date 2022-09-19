Threat intelligence is a module provided in bot traffic management. Relying on Tencent's nearly 20 years of network security experience and big data intelligence, this feature accurately identifies malicious IP and IDC access by monitoring the IP status in real time and adopting a risk scoring system, while intelligently identifying malicious bot characteristics to block access initiated by malicious bots, distributed bots, proxies, credential stuffing, and bargain hunting.

## Prerequisites
You have purchased a WAF plan and subscribed to the [bot traffic management](https://intl.cloud.tencent.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E) service.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig) and select **Configuration Center** > **Bot and Application Secuirty** on the left sidebar.
2. On the page that appears, select a domain name in the top left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/8e955224b55d59779e4609fb4d12c930.png)
3. On the bot management page, click the threat intelligence switch ![](https://qcloudimg.tencent-cloud.cn/raw/f3f8be1cf90fd16cb762064d1bc2bf57.png). If you toggle on the switch for the first time, all items in the setting will be enabled. You can disable the items if you do not want WAF to identify their IDC access sources and IPs whether to hit the threat intelligence library and calculate a bot score.
![](https://qcloudimg.tencent-cloud.cn/raw/d1b8815b56676c6aa15d825e1efc578f.png)
4. Click **Configure now** in the threat intelligence module.
5. On the pop-up page, configure the required items in the setting. If you want to configure all items, you can click **Enable all** or **Disable all**.
![](https://qcloudimg.tencent-cloud.cn/raw/08442eb247e679c3b494b307c3a97ed4.png)

**Parameter description:**
 - Enable all/Disable all: It allows you to enable/disable all items provided.
 - IDC type: It displays the IP library to which the IP belongs. These IPs are often exploited by attackers to deploy bots or proxies rather than normal users. When it is enabled, the IDC access source will be identified.
 - Threat intelligence library:
    - Bot: The bot IPs tagged based on Tencent Security Threat Intelligence and those detected by WAF in real time will not be exploited by normal users. When it is enabled, the access source will be identified.
    - Web attack: The IPs tagged based on Tencent Security Threat Intelligence launched a large number of attacks containing malicious scans within the intelligence validity, and such IPs will not be exploited by normal users. When it is enabled, the access source will be identified.
    - Web proxy: The IPs tagged based on the proxy threat intelligence from Tencent Security Threat Intelligence are exploited by attackers rather than normal users. When it is enabled, the access source will be identified.
    - Scanner: The IPs tagged based on Tencent Security Threat Intelligence are the attacker IPs that launch malicious scans on the entire network. When it is enabled, the access source will be identified.
    - Account takeover: The IPs tagged by this intelligence launched identity theft, account blasting, credential stuffing and other attacks in the past period of time. When it is enabled, the access source will be identified.


## Best Practices for Customer-centric Business
#### Overview
Customer-centric business is a business model based on a large number of users, which is mainly initiated by residential IPs or base station IPs.
>!
>- Some businesses use callback APIs that initiate access from an IDC. These callback APIs are used by a large number of users.
>- Business scheduling APIs may initiate access from an IP or IDC.
>- Some business egresses initiate access from an IDC.


#### Configuration process
<dx-steps>

 - Enable the threat intelligence switch.
 - Create custom session policies to perform CAPTCHA to identify access from proxies or IDCs.
 - When the website security is ensured, add the trusted callback API addresses or IDC addresses to the custom session policies to prevent false blocking from affecting the service.
 - Connect your app or site as needed and run CAPTCHA.
</dx-steps>



## Best Practices for Business-centric Business

Business-centric business is a business model that focuses on a large number of business organizations, which is mainly initiated by IDCs and egresses. A few businesses are initiated by residential IPs and base station IPs.

>!
>- Some businesses use callback APIs that will initiate access from an IDC. These APIs are used by a large number of users.
>- Business scheduling APIs may initiate access from an IP or IDC.
>- Some business egresses will initiate access from a residential IP.


#### Configuration process
<dx-steps>
- Enable the threat intelligence switch and turn off the IDC switch.
- Create custom session policies to perform CAPTCHA to identify access from residential IPs.
- When the website security is ensured, add the trusted callback API addresses or IDC addresses to the custom session policies to prevent false blocking from affecting the service.
- Connect an app or site as needed and run CAPTCHA.
</dx-steps>




