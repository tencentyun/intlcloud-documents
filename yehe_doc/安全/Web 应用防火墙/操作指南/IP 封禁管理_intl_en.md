
This document describes Web Application Firewall (WAF) attacking IP penalty, which can quickly block malicious attack source IPs and defeat attacks and threats from malicious scanners, proxies and webs to improve defensive efficiency.
## Background
Attacking IP penalty can automatically block repeated web attacks the client IP suffered in a short period of time. You can view [attack logs](https://intl.cloud.tencent.com/document/product/627/35649) for attack details.

## Prerequisites
- You have [purchased a WAF package](https://buy.cloud.tencent.com/buy/waf) and added the protected domain name, which is in normal protection.
- Intelligence IP blocking is now in beta. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us) for a free trial. After official launch, you will be charged on the published prices.

## Directions
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia), and select **IP Management** > **IP Blocking Management** on the left sidebar.
2. Configure the attacking IP penalty settings.
![](https://main.qcloudimg.com/raw/1e2b32f4d3b2e61d4bc80164ca1e7310.png)
Field and operation descriptions:
 - **Blocking Switch**: specifies whether to enable attacking IP penalty. It is disabled by default.
 - **Web Attacks**: specifies the number of web attacks triggered by the attack source IP (which will trigger rules engine excluding AI engine, custom strategies, and CC attacks) within a period of time. Default: 20.
 - **Detection Duration**: specifies the detection duration of the attack source IP. Default: 20 minutes.
 - **Blocking Duration**: specifies the blocking duration of the attack source IP. Default: 20 minutes.
 - **Operation**: edits the default setting. You can click **Settings** in the top right corner of the attacking IP penalty page.
![](https://main.qcloudimg.com/raw/593f63b9f26a31d65231c15758d1d8b9.png)
