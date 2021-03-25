## Overview
CC protection can safeguard the access to specified URLs. CC protection settings 2.0 is upgraded with emergency CC protection and custom CC rules. Emergency CC protection can perform big data analysis on websites' access history and their real servers' exceptional response such as timeout and response delay, to generate protection policies for emergencies, blocking frequent access requests in real time. Custom CC rules support customizing protection rules based on user access source IPs or SESSION frequency to handle access by blocking, setting alarms, or verifying identity with CAPTCHA.
>!
>- Emergency CC protection and custom CC rules cannot be enabled at the same time.
>- SESSION must be set before using the session-based CC protection policy.

## Directions
#### **Example 1: Emergency CC protection settings**
Emergency CC protection is disabled by default. Before enabling it, please make sure that the custom CC rule feature is disabled.

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), select **Web Application Firewall** -> **Defense settings** in the left sidebar to enter the defense settings page, and click the target domain name to enter the configuration page.
![](https://main.qcloudimg.com/raw/707a3e129709d512417e875b2ecb4809.png)
2. Click **CC protection settings 2.0** to configure emergency CC protection.
![](https://main.qcloudimg.com/raw/12b9dcea8ae59f2954ceafd9e7849b43.png)
**Configuration item description:**
**Status switch:** after emergency CC protection is enabled, if a website is under massive CC attacks (with a website QPS of 1000 or above), the protection will be automatically triggered. If there are no specific protection paths, we recommend enabling emergency CC protection. As there may be some false alarms, you can click [**IP management** -> **IP Blocking On/Off**](https://console.cloud.tencent.com/guanjia/ip/record) on the left sidebar to view the information of blocked IPs and handle them in time.
>? If there are specific protection paths, we recommend using custom CC rules.

#### **Example 2: Access source IP-based CC protection settings**
An IP-based CC protection policy can be directly configured without setting SESSION.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), select **Web Application Firewall** -> **Defense settings** in the left sidebar to enter the defense settings page, and click the target domain name to enter the configuration page.
![](https://main.qcloudimg.com/raw/b44218060a78db08eceeb22570c3582a.png)
2. Click **CC protection settings 2.0** -> **Add a Rule**.
![](https://main.qcloudimg.com/raw/cb59c16306c765f638454d96377cb307.png)
3. Enter the rule details in the pop-up window.
<img src="https://main.qcloudimg.com/raw/029f2dd3203ffd8338385fe398af2db3.png" style="zoom:80%;" /><br>
**Configuration item description:**
 - **Recognition Mode:** "IP" or "SESSION".
 - **Condition:** "equal", "prefix matches with", or "includes".
 - **Advanced Match:** filters access with GET and POST form parameters to control the frequency in a more refined manner and increase the hit rate.
	 - **Field:** specifies the request method, which can be GET or POST.
	 - **Parameter Name:** parameter name in a request field, which can contain up to 512 characters.
	 - **Parameter Value:** parameter value in a request field, which can contain up to 512 characters.
	 **Note:** the 3 test entries for GET request are as follows: a=1&b=11, a=2&b=12, a=&b=13.
		- If the parameter name of a GET configuration is `a`, and the parameter value is `1`, then `1` will be hit.
		- If the parameter name of a GET configuration is `a`, the parameter value is `\*`, then `1`, `2`, and `3` will be hit.
 - **Access Frequency:** sets the access frequency based on actual business requirements. We recommend setting a value 3 to 10 times the normal access frequency. For example, if your website is accessed 20 times per minute per visitor, you can set the access frequency to 60 to 200 times per minute, which can be further adjusted based on the attack severity.
 - **Action:** "Observation", "Verify identity", or "Block".
 - **Punishment Period:** 1 minute to 1 week.
 - **Priority:** enter an integer between 1 to 100. A smaller integer indicates a higher action priority for this rule. When the priority is the same, the later a rule is created, the higher its priority.
4. You can select a created rule to disable, modify, or delete it.
![](https://main.qcloudimg.com/raw/c4b3a5e23cc583009d2a319c394b1def.png)
5. Conduct test CC attacks based on the rule settings.
![](https://main.qcloudimg.com/raw/381abed502dc483b2c1ebd1de14ccf26.png)
6. View real-time IP blocking information. Click **IP management** -> **IP Blocking On/Off** on the left sidebar to view the information of blocked IPs in real time and add these IPs to the blocklist or allowlist as needed.

#### **Example 3: Session-based CC protection settings**
CC protection based on session access frequency effectively resolves false positive problems that may occur when the same IP egress is used by multiple users in office buildings, stores, supermarkets, and other public Wi-Fi networks.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), select **Web Application Firewall** -> **Defense settings** in the left sidebar to enter the defense settings page, and click the target domain name to enter the configuration page.
![](https://main.qcloudimg.com/raw/a8ee54aa19968970ba6f97d39602301a.png)
2. Click **CC protection settings 2.0** -> **Settings** to set the SESSION information.
![](https://main.qcloudimg.com/raw/5839e3313206a5449aeeb067f1b26d03.png)
3. On the SESSION settings page, enter the required information. In this example, a cookie is used as the test object, whose ID is `security`, start position is `0`, and end position is `9`. After completing the settings, click **Set**.
![](https://main.qcloudimg.com/raw/602857cecf82505416e26d6566dbb61f.png)
 - **Configuration item description:**
 - **SESSION Position:** "COOKIE", "GET", or "POST". Here, GET and POST are HTTP request content parameters rather than HTTP header information.
 - **Note:** "Position Match" or "String Match".
 - **SESSION ID:** session ID.
 - **Start Position:** position where string or position match starts.
 - **End Position:** position where string or position match ends.
 - **GET/POST example:**
Assume that the complete parameter content in a request is `key_a = 124&key_b = 456&key_c = 789`, then:
	 - In string match mode, if the session ID is `key_b =`, and the end character is `&`, then the matched content will be `456`.
 	- In position match mode, if the session ID is `key_b`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.
 - **COOKIE example:**
Assume that the complete cookie content in a request is `cookie_1 = 123;cookie_2 = 456;cookie_3 = 789`, then:
 	- In string match mode, if the session ID is `cookie_2 =`, and the end character is `;`, then the matched content will be `456`.
 	- In position match mode, if the session ID is `cookie_2`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.

4. Click **Test** to test the session information.
![](https://main.qcloudimg.com/raw/7c5b449d0a04a4caddd2b8a1715f5639.png)
5. Go to the SESSION settings page and set the content to `security = 0123456789`. Then, WAF will use the 10 characters following `security` as the session ID. You can also delete or reconfigure the session information.
![](https://main.qcloudimg.com/raw/b01ae5205b8b01dbdddee36670e1cff9.png)
6. Set a session-based CC protection policy as instructed in Example 1, but select "SESSION" as the recognition mode.
![](https://main.qcloudimg.com/raw/8dbe3f54ff0efca16d83a4731dec36b9.png)
7. After the configuration is completed, the session-based CC protection policy will take effect.
>!If you use session-based CC protection, you cannot view IP blocking information in the IP blocking status section.

[Tamper Protection](https://intl.cloud.tencent.com/document/product/627/11710)

