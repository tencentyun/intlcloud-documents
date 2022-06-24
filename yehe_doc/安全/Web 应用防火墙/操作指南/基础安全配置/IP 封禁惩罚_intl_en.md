This document describes Web Application Firewall (WAF) attacker IP penalty, which can quickly block malicious attacker IPs and defeat attacks and threats from malicious scanners, proxies and webs to improve defense efficiency.

## Overview
Attacker IP penalty can automatically block repeated web attacks the client IP suffered in a short period of time. You can view [attack logs](https://intl.cloud.tencent.com/document/product/627/35649) for attack details.

## Prerequisites
- You have purchased a [WAF plan](https://intl.cloud.tencent.com/pricing/waf).
- You have added a protected domain name, and ensured the domain name is in normal protection. For detailed directions, see [Getting Started](https://intl.cloud.tencent.com/document/product/627/18635).
- Currently, IPs can be blocked by domain name. Domain names can have different blocking durations, which are calculated separately.

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig) and select **Configuration Center** > **Basic Security** > **Web Security** on the left sidebar.
2. On the web security page, select the target domain name in the top-left corner and click ![](https://qcloudimg.tencent-cloud.cn/raw/3b613bd9116dad1a919f320663da42d0.png) next to **IP blocking** to enable IP blocking.
![](https://qcloudimg.tencent-cloud.cn/raw/1d17a6e7b02de73eb292aaa08005025a.png)
3. On the web security page, click ![](https://qcloudimg.tencent-cloud.cn/raw/36d7cbd5a4d608136e4c77dff95f54dc.png) next to **IP blocking** to modify default parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/217deb2f63414f045ac1ff8ab43ed6ed.png)

**Field description:**
 - **Web attacks**: It records the number of web attacks from a malicious IP in a specified period. The attacks will trigger the rule engines against web attacks excluding AI engine, custom policies and CC protection.
 - **Detection duration**: It specifies the duration to detect the attacker IP.
 - **Blocking duration**: It specifies the duration to block the attacker IP.

