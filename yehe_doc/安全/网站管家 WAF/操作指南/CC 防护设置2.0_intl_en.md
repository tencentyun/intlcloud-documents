## Feature Overview
CC protection protects access to specified URLs of your website. CC protection 2.0, as a completely upgraded version, supports intelligent and custom CC protection policies. Based on big data analysis of exceptional responses (response timeout or latency) from the real server and historical access requests to the website, Intelligent CC protection can intelligently generate protection policies in order to block high-frequency access requests in real time. Custom CC protection allows you to custom protection rules based on access source IP or session frequency to process access requests by means of alarming, CAPTCHA verification, and blocking.
>
>- Intelligent and custom CC protection policies are mutually exclusive and cannot be enabled at the same time.
>- If you use a session-based CC protection policy, you should set the session first before setting the policy.

## Configuration Steps
#### **Example 1. Intelligent CC protection configuration**
Intelligent CC protection is disabled by default. Before enabling it, please make sure that the custom CC protection rule is disabled.

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Web Application Firewall** > **Protection Settings** on the left sidebar to enter the protection settings page. In the domain name list, find the domain name to be protected and click **Protection Configuration** to enter the configuration page.
![](https://main.qcloudimg.com/raw/707a3e129709d512417e875b2ecb4809.png)
2. Click **CC Protection Settings 2.0** to configure intelligent CC protection.
![](https://main.qcloudimg.com/raw/12b9dcea8ae59f2954ceafd9e7849b43.png)
**Configuration item description:**
 **Status**: when intelligent CC protection is enabled, it will be automatically triggered if your website is under large-traffic CC attacks (i.e., when the website QPS is greater than 1,000), with no manual intervention required. If there is no specific protection route, you are recommended to enable intelligent CC protection. However, there may be some false positives. You can view information of the blocked IPs and handle them promptly in **[IP Management - IP Blocking Status](https://console.cloud.tencent.com/guanjia/ip/record) in the WAF Console.
	
	> If you know the specific protection route, you are recommended to use custom CC rules for protection.

#### **Example 2. CC protection settings based on access source IP**
An IP-based CC protection policy does not need to be set in the session dimension and therefore can be directly configured.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Web Application Firewall** > **Protection Settings** on the left sidebar to enter the protection settings page. In the domain name list, find the domain name to be protected and click **Protection Configuration** to enter the configuration page.
![](https://main.qcloudimg.com/raw/b44218060a78db08eceeb22570c3582a.png)
2. Click **CC Protection Settings 2.0** to configure a CC protection rule. Click **Add Rule** and enter the corresponding information.
![](https://main.qcloudimg.com/raw/cb59c16306c765f638454d96377cb307.png)
3. On the CC protection rule adding page, enter the corresponding information.
![](https://main.qcloudimg.com/raw/029f2dd3203ffd8338385fe398af2db3.png)
 - **Configuration item description:**
	- **Recognition Mode:** `IP` or `SESSION`.
	- **Match Condition:** "Equal", "Prefix Match", or "Include".
 - **Advanced Match:**
	 - **Access Frequency:** you can set the access frequency as needed. A value 3–10 times the normal access speed is recommended; for example, if the average access request frequency of your website is 20 requests/minute, you can set this value to 60–200 requests/minute, which can be further adjusted based on the attack traffic.
	 - **Action:** observation, CAPTCHA verification, or blocking.
	 - **Blocking Period**: at least 1 minute and at most 1 week.
	 - **Priority**: enter an integer between 1 and 100. The smaller the number, the higher the priority of this rule. For rules with the same priority, the last created one will be prioritized.

4. You can select a created rule and disable, modify, or delete it.
![](https://main.qcloudimg.com/raw/c4b3a5e23cc583009d2a319c394b1def.png)

5. Conduct test CC attacks based on the rule settings.
![](https://main.qcloudimg.com/raw/381abed502dc483b2c1ebd1de14ccf26.png)
6. View real-time IP blocking. On the left sidebar, select **IP Management** > **IP Blocking Status** to view information of IPs blocked in real time and add IPs to the blacklist or whitelist as needed.

#### **Example 3. Session-based CC protection settings**
CC protection based on session access speed can effectively solve false positive problems caused when multiple users use the same IP egress in office buildings, stores, supermarket, and other public Wi-Fi networks.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Web Application Firewall** > **Protection Settings** on the left sidebar to enter the protection settings page. In the domain name list, find the domain name to be protected and click **Protection Configuration** to enter the configuration page.
![](https://main.qcloudimg.com/raw/a8ee54aa19968970ba6f97d39602301a.png)
2. Select **CC Protection Settings 2.0** > **Settings** to set information in the session dimension.
![](https://main.qcloudimg.com/raw/5839e3313206a5449aeeb067f1b26d03.png)
3. Enter the session settings page. In this example, a cookie is used as the test object, whose ID is `security`, start position is `0`, and end position is `9`. After completing the settings, click **Set**.
![](https://main.qcloudimg.com/raw/602857cecf82505416e26d6566dbb61f.png)
	- **Configuration item description:**
		- **Session Position**: `COOKIE`, `GET`, or `POST`. Here, `GET` and `POST` are HTTP request content parameters rather than HTTP header.
		- **Match Mode**: position match or string match.
		- **Session ID**: session ID.
		- **Start position**: position where string or position match starts.
		- **End position**: position where string or position match ends.
	- **GET/POST sample:**
Assume that the complete parameter content in a request is `key_a = 124&key_b = 456&key_c = 789`, then:
		- In string match mode, if the session ID is `key_b =` and the end character is `&`, then the matched content will be `456`.
		- In position match mode, if the session ID is `key_b`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.
	- **Cookie sample:**
Assume that the complete cookie content in a request is `cookie_1 = 123;cookie_2 = 456;cookie_3 = 789`, then:
		- In string match mode, if the session ID is `cookie_2 =` and the end character is `;`, then the matched content will be `456`.
		- In position match mode, if the session ID is `cookie_2`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.

4. Click **Test** to test the session information.
![](https://main.qcloudimg.com/raw/7c5b449d0a04a4caddd2b8a1715f5639.png)
5. Enter the session settings page and set the content to `security = 0123456789`. Then, WAF will use the string of 10 characters after `security` as the session ID. In addition, you can delete or reconfigure the session information.
![](https://main.qcloudimg.com/raw/b01ae5205b8b01dbdddee36670e1cff9.png)
6. Set a session-based CC protection policy as instructed in the example, but please select "SESSION" as the recognition mode.
![](https://main.qcloudimg.com/raw/8dbe3f54ff0efca16d83a4731dec36b9.png)
7. After the configuration is completed, the session-based CC protection policy will take effect.
>If you use session-based CC protection, you cannot view IP blocking information in the IP blocking status section.

[Previous Step: DNS Hijacking Detection](https://intl.cloud.tencent.com/document/product/627/11708)
[Next Step: Webpage Tampering Prevention](https://intl.cloud.tencent.com/document/product/627/11710)