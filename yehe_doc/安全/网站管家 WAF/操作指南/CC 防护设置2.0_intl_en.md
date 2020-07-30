## Overview
CC protection protects access to specified URLs for your website. CC protection 2.0, as a completely upgraded version, supports intelligent and custom CC protection policies. Based on big data analysis of exceptional responses (response timeout or latency) from the real server and historical access requests to the website, intelligent CC protection intelligently generates protection policies in order to block high-frequency access requests in real time. Custom CC protection allows you to customize protection rules based on access to real IPs or session frequency to process access requests by means of alarms, CAPTCHA verification, and blocking.
>!
>- Intelligent and custom CC protection policies cannot be enabled at the same time.
>- To use a session-based CC protection policy, you must set the session first.

## Configuration Procedure
#### **Example 1: configuring intelligent CC protection**
Intelligent CC protection is disabled by default. Before you enable it, make sure that the custom CC protection policy is disabled.

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and choose **Web Application Firewall** -> **Defense settings** on the left sidebar to go to the defense settings page. In the domain name list, find the target domain name and click **Defense configuration** to go to the configuration page.
![](https://main.qcloudimg.com/raw/707a3e129709d512417e875b2ecb4809.png)
2. Click **CC Protection Settings 2.0** to configure intelligent CC protection.
![](https://main.qcloudimg.com/raw/12b9dcea8ae59f2954ceafd9e7849b43.png)
**Configuration item description:**
**Status:** when intelligent CC protection is enabled, it will be automatically triggered if your website is under high-traffic CC attack (i.e., when the website QPS is greater than 1,000), with no manual intervention required. If there is no specific protection route, we recommend that you enable intelligent CC protection. However, this may result in some false positives. You can view information for blocked IP addresses and handle them promptly in [IP Management - IP Blocking Status](https://console.cloud.tencent.com/guanjia/ip/record) in the WAF Console.
>? If you know the specific protection route, we recommend that you use custom CC rules for protection.

#### **Example 2: CC protection settings based on access to real IPs**
An IP-based CC protection policy does not need to be set in the session dimension and, so it can be directly configured.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and choose **Web Application Firewall** -> **Defense settings** on the left sidebar to enter the defense settings page. In the domain name list, find the target domain name and click **Defense configuration** to go to the configuration page.
![](https://main.qcloudimg.com/raw/b44218060a78db08eceeb22570c3582a.png)
2. Click **CC Protection Settings 2.0** to configure a CC protection rule. Click Add a Rule and enter the corresponding information.
![](https://main.qcloudimg.com/raw/cb59c16306c765f638454d96377cb307.png)
3. On the **Add CC Defense Rules** page, enter the corresponding information.
![](https://main.qcloudimg.com/raw/029f2dd3203ffd8338385fe398af2db3.png)
 - **Configuration item description:**
 - **Recognition Mode:** IP or SESSION.
 - **Condition:** Equal, Prefix Match, or Include.
 - **Advanced matching:**
 - **Access frequency:** you can set the access frequency as needed. A value 3 to 10 times the normal access frequency is recommended. For example, if the average access request frequency of your website is 20 requests/minute, you can set this value to 60 to 200 requests/minute, which can be subsequently adjusted based on the attack traffic.
 - **Action:** Observe, CAPTCHA, or Block.
 - **Penalty period:** at least 1 minute and at most 1 week.
 - **Priority:** enter an integer between 1 and 100. The lower the number, the higher the priority of this rule. For rules with the same priority, the most recently created rule has a higher priority.

4. You can select a created rule and then disable, modify, or delete it.
![](https://main.qcloudimg.com/raw/c4b3a5e23cc583009d2a319c394b1def.png)

5. Trigger CC attacks based on the rule settings.
![](https://main.qcloudimg.com/raw/381abed502dc483b2c1ebd1de14ccf26.png)
6. View real-time IP address blocking. On the left sidebar, choose **IP Management** > **IP Blocking Status** to view information on the IP addresses blocked in real time and add IP addresses to the blocklist or allowlist as needed.

#### **Example 3: session-based CC protection settings**
CC protection based on the session access frequency can effectively solve the false positive problem caused when multiple users use the same IP egress in office buildings, stores, supermarkets, and other public Wi-Fi networks.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and choose **Web Application Firewall** -> **Defense settings** on the left sidebar to go to the defense settings page. In the domain name list, find the target domain name and click **Defense configuration** to go to the configuration page.
![](https://main.qcloudimg.com/raw/a8ee54aa19968970ba6f97d39602301a.png)
2. Choose **CC Protection Settings 2.0** > **Settings** to set information in the session dimension.
![](https://main.qcloudimg.com/raw/5839e3313206a5449aeeb067f1b26d03.png)
3. Enter the **Session Settings** page. In this example, cookie is used as the test object. Its ID is security, start position is 0, and end position is 9. After configuring the settings, click **Set**.
![](https://main.qcloudimg.com/raw/602857cecf82505416e26d6566dbb61f.png)
 - **Configuration item description:**
 - **SESSION Position:** COOKIE, GET, or POST. Here, GET and POST are HTTP request content parameters rather than HTTP headers.
 - **Matching Mode:** Position Match or String Match.
 - **SESSION ID:** session ID.
 - **Start Position:** position where string or position match starts.
 - **End Position:** position where string or position match ends.
 - **GET/POST Example:**
Assume that the complete parameter content in a request is: key_a = 124&key_b = 456&key_c = 789.
 - In string match mode, if the session ID is key_b = and the end character is &, the matched content will be 456.
 - In position match mode, if the session ID is key_b, the start position is 0, and the end position is 2, the matched content will be 456.
 - **COOKIE example:**
Assume that the complete cookie content in a request is cookie_1 = 123;cookie_2 = 456;cookie_3 = 789.
 - In string match mode, if the session ID is cookie_2 = and the end character is “;”, the matched content will be 456.
 - In position match mode, if the session ID is cookie_2, the start position is 0, and the end position is 2, the matched content will be 456.

4. Click **Test** to test the session information.
![](https://main.qcloudimg.com/raw/7c5b449d0a04a4caddd2b8a1715f5639.png)
5. Enter the **Session Settings** page and set the content to security = 0123456789. Then, WAF will use the string of 10 characters after “security” as the session ID. You can also delete or reconfigure the session information.
![](https://main.qcloudimg.com/raw/b01ae5205b8b01dbdddee36670e1cff9.png)
6. Set a session-based CC protection policy as instructed in the example, but select **SESSION** as the recognition mode.
![](https://main.qcloudimg.com/raw/8dbe3f54ff0efca16d83a4731dec36b9.png)
7. After the configuration is completed, the session-based CC protection policy will take effect.
>! If you use session-based CC protection, you cannot view IP address blocking information in the IP blocking status section.

[Previous: DNS Hijacking Detection](https://intl.cloud.tencent.com/document/product/627/11708)
[Next: Tampering Protection](https://intl.cloud.tencent.com/document/product/627/11710)
