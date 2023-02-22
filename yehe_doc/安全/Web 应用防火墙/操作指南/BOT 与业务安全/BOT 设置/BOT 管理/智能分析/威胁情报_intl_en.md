This document describes how to set the threat intelligence module in the bot analytics section of bot traffic management. This feature is built on Tencent's nearly 20 years of experience in cybersecurity and big data intelligence. It determines the status of an IP in real time and uses a scoring mechanism to quantify a risk. It precisely identifies the access from a malicious dynamic IP and IDC. In addition, it intelligently identifies the characteristics of a malicious crawler to cope with risky access requests from malicious crawlers, distributed crawlers, proxies, credential stuffing, and bargain hunting.

## Prerequisites
You have purchased a WAF instance and [bot traffic management extra pack](https://intl.cloud.tencent.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E) and enabled bot analysis for WAF-connected domain names.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/8e955224b55d59779e4609fb4d12c930.png)
3. In **Global settings**, click **Configure now** in the **Threat intelligence module** section.
![](https://qcloudimg.tencent-cloud.cn/raw/d1b8815b56676c6aa15d825e1efc578f.png)
4. On the configuration page, enable or disable an identification item or enable or disable all the items.
![](https://qcloudimg.tencent-cloud.cn/raw/08442eb247e679c3b494b307c3a97ed4.png)

**Parameter description:**
   - **Enable/Disable all**: Enable/Disable all the rules of the current type.
   - **IDC type**: IPs belong to IP libraries of the corresponding type. These IP ranges are often exploited by attackers to deploy bots or proxies rather than normal users. When this item is enabled, the threat intelligence module will identify the access source from this IDC.
   - **Threat intelligence library**:
     - Bot: The IPs tagged by this intelligence provided by Tencent Security Threat Intelligence and the bot IPs detected by WAF in real time will not be exploited by normal users. After this item is enabled, the threat intelligence module will identify the access sources of bots in Tencent Security Threat Intelligence.
     - Web attacks: The IPs tagged by this inbound threat intelligence provided by Tencent Security Threat Intelligence launch a large number of attacks containing malicious scans within the intelligence validity. Such IPs will not be exploited by normal users. After this item is enabled, the threat intelligence module will identify the access sources of web attacks in Tencent Security Threat Intelligence.
     - Web proxy: The IPs tagged by this intelligence provided by Tencent Security Threat Intelligence are exploited by attackers rather than normal users. After this item is enabled, the threat intelligence module will identify the access sources of bots in Tencent Security Threat Intelligence.
     - Scanner: The IPs tagged by this intelligence provided by Tencent Security Threat Intelligence launch malicious scans on the entire network. After this item is enabled, the threat intelligence module will identify the access sources of scanners in Tencent Security Threat Intelligence.
     - Account takeover: The IPs tagged by this intelligence launched online identity theft, account blasting, credential stuffing, and other attacks in the past period of time. After this item is enabled, the threat intelligence module will identify the access sources of account takeover attacks in Tencent Security Threat Intelligence.

5. After the configuration, click the configuration page of a certain scenario, and click ![](https://qcloudimg.tencent-cloud.cn/raw/93db9ce05a5cea306d98674d07747142.png) in the **Threat intelligence module** section. When the module is enabled for the first time, all the identification items will be enabled. If you enable certain items, you can identify the access sources at different risk levels from the threat intelligence module and IDC.

## Best Practices in Configuring Threat Intelligence Module for B2C Website
#### Overview
B2C feature: B2C faces a large number of users, and user businesses are mainly launched from residential/base station IPs.
>!
>- Some businesses have callback APIs that initiate access requests from the IDC side. The number of callback APIs is the collection of multiple users.
>- Business scheduling APIs may initiate access requests from specific IPs/IDCs.
>- Users at some of the enterprise egresses will initiate access requests from the IDC.

#### Configuration process
<dx-steps>
- Enable the threat intelligence module.
- Configure a session policy to identify proxy/IDC access requests through a CAPTCHA.
- Configure a session policy and set callback API address/business IDC address to **Trust**. This is to avoid blocking business APIs by mistake and thus affecting the business while ensuring the website security.
- Enable CAPTCHA for applications or sites as needed.
</dx-steps>



## Best Practices in Configuring Threat Intelligence Module for B2B Website

B2B feature: B2B faces a large number of businesses, and customer businesses are mainly launched from the IDC/enterprise egress. A few access sources are from residential/base station IPs.

>!
>- Some businesses have callback APIs that initiate access requests from the IDC side. The number of callback APIs is the collection of multiple users.
>- Business scheduling APIs initiate access requests from specific IPs/IDCs.
>- Users at some of the enterprise egresses will launch access requests from residential IPs.


#### Configuration process
<dx-steps>
- Enable the threat intelligence module and disable the expected IDC.
- Configure a session policy to identify residential IP access requests through a CAPTCHA.
- Configure a session policy and set callback API address/business IDC address to **Trust**. This is to avoid blocking business APIs by mistake and thus affecting the business while ensuring the website security.
- Enable CAPTCHA for applications or sites as needed.
</dx-steps>