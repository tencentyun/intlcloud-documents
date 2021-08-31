This document describes how to configure CC protection in the Web Application Firewall (WAF) console.
## Background
CC protection enables access protection for specified URLs, which supports emergency CC protection and custom CC protection policies.
>!Emergency CC protection and custom CC rules cannot be enabled at the same time.


## Directions
### Example 1: Emergency CC protection settings
>!Emergency CC protection is disabled by default. Before enabling it, please make sure that the custom CC rule feature is disabled.
>
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), and select **Web Application Firewall** -> **Defense settings** on the left sidebar to enter the protection setting page.
2. Find the target domain name in the domain name list, and click **Defense configuration** to enter the configuration page.
3. Click **CC protection settings 2.0** to configure emergency CC protection.
**Configuration item description:**
**Status switch:** after emergency CC protection is enabled, if a website is under massive CC attacks (with a website QPS of 1000 or above), the protection will be automatically triggered. If there are no specific protection paths, we recommend enabling emergency CC protection. As there may be some false alarms, you can click [**IP management** -> **IP Blocking On/Off**](https://console.cloud.tencent.com/guanjia/ip/record) on the left sidebar to view the information of blocked IPs and handle them in time.
>? If there are specific protection paths, we recommend using custom CC rules.


<span id="two"></span>
### Example 2: Access source IP-based CC protection settings
An IP-based CC protection policy can be directly configured without setting SESSION.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), and select **Web Application Firewall** -> **Defense settings** on the left sidebar to enter the protection setting page.
2. Find the target domain name in the domain name list, and click **Defense configuration** to enter the configuration page.
3. Click **CC protection settings 2.0** -> **Add a Rule**.
4. Enter the rule details in the pop-up window.
>!If **IP** is selected as the recognition mode, after the rule is triggered for blocking, the IP will be blocked across the entire website (i.e., the IP will be blocked when accessing other URLs). But if **SESSION** is selected, blocking will not be global.
> **Configuration item description:**
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


### Example 3: Session-based CC protection settings
CC protection based on session access frequency effectively resolves false positive problems that may occur when the same IP egress is used by multiple users in office buildings, stores, supermarkets, and other public Wi-Fi networks.
>!SESSION must be set before using the session-based CC protection policy. The step 1 to 4 are SESSION setting directions.

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/overview), and select **Web Application Firewall** -> **Defense settings** on the left sidebar to enter the protection setting page.
2. Find the target domain name in the domain name list, and click **Defense configuration** to enter the configuration page.
3. Click **CC protection settings 2.0** -> **Settings** to set the SESSION information.
4. On the SESSION settings page, enter the required information. In this example, a cookie is used as the test object, whose ID is `security`, start position is `0`, and end position is `9`. After completing the settings, click **Set**.
 **Configuration item description:**
 - **SESSION Position:** "COOKIE", "GET", or "POST". Here, GET and POST are HTTP request content parameters rather than HTTP header information.
 - **Note:** "Position Match" or "String Match".
 - **SESSION ID:** session ID.
 - **Start Position:** position where string or position match starts.
 - **End Position:** position where string or position match ends.
 - **GET/POST example:** Assume that the complete parameter content in a request is `key_a = 124&key_b = 456&key_c = 789`, then:
	 - In string match mode, if the session ID is `key_b =`, and the end character is `&`, then the matched content will be `456`.
	 - In position match mode, if the session ID is `key_b`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.
 - **COOKIE example:** Assume that the complete cookie content in a request is `cookie_1 = 123;cookie_2 = 456;cookie_3 = 789`, then:
	 - In string match mode, if the session ID is `cookie_2 =`, and the end character is `;`, then the matched content will be `456`.
	 - In position match mode, if the session ID is `cookie_2`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.
5. Click **Test** to test the session information.
6. Go to the SESSION settings page and set the content to `security = 0123456789`. Then, WAF will use the 10 characters following `security` as the session ID. You can also delete or reconfigure the session information.
7. Set a session-based CC protection policy as instructed in [Example 2](#two), but select "SESSION" as the recognition mode.
 >?If **GET** is selected as the session position in a rule, access with the same session information instead of the IP information will be blocked.
 >
8. After the configuration is completed, the session-based CC protection policy will take effect.
>!If you use session-based CC protection, you cannot view IP blocking information in the IP blocking status section.
