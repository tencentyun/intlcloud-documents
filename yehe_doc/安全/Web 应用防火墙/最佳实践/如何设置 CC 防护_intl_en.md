This document describes how to configure CC protection in the WAF console.
## Overview
CC protection enables access protection for specified URLs, which supports emergency CC protection and custom CC protection policies.
>! Emergency CC protection and custom CC rules cannot be enabled at the same time.


## Directions
### Example 1: Emergency CC protection settings
>!Emergency CC protection is disabled by default. Before enabling it, make sure that the custom CC rule feature is disabled.

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Basic security** on the left sidebar.
2. On the **Basic security** page, select the target domain name in the top-left corner and click **CC protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/22cf5db65e04a8c06e96dc4141e2830b.png)
3. In the emergency CC protection module, click ![](https://qcloudimg.tencent-cloud.cn/raw/b7881ceb022cdf653b379e111af23c1e.png) on the right of the status and confirm the operation to enable emergency CC protection.
>?
>- After emergency CC protection is enabled, if a website is under massive CC attacks (with a website QPS of 1000 or above), the protection will be automatically triggered. If there are no specific protection paths, we recommend enabling emergency CC protection. As there may be some false alarms, you can enter the blocklist/allowlist in the console to add blocked IPs to the allowlist.
>- If there are specific protection paths, we recommend using custom CC rules.

![](https://qcloudimg.tencent-cloud.cn/raw/c1b49e55a63ef40c3ee547a54edbfbb7.png)



[](id:two)
### Example 2: Access source IP-based CC protection settings
An IP-based CC protection policy can be directly configured without setting SESSION.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Basic security** on the left sidebar.
2. On the **Basic security** page, select the target domain name in the top-left corner and click **CC protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/2b39f900513af7925c311a29763d2552.png)
3. On the **CC protection** page, click **Add rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/4dc2b4e91adad36b0c98b3fe9cd60c67.png)
4. In the **Add rule** pop-up window, enter the rule details.
>!If **IP** is selected as the recognition mode, after the rule is triggered for blocking, the IP will be blocked across the entire website (i.e., the IP will be blocked when accessing other URLs). But if **SESSION** is selected, blocking will not be global.

![](https://qcloudimg.tencent-cloud.cn/raw/85b604df7ccb09ddcffbd72ee3d72892.png)

 **Parameter description:**
 - Rule name: Custom name, which can contain up to 50 characters.
 - Identification method: **IP** or **SESSION**.
 - Match method: **Equal to**, **Prefix match**, or **Include**.
 - Advanced match: Filters access with GET and POST form parameters to control the frequency in a more refined manner and increase the hit rate.
	 - Match field: Specifies the request method, which can be GET or POST.
	 - Parameter name: Parameter name in a request field, which can contain up to 512 characters.
	 - Parameter value: Parameter value in a request field, which can contain up to 512 characters.
	 Note: The three test entries for GET request are as follows: a=1&b=11, a=2&b=12, a=&b=13.
		- If the parameter name of a GET configuration is `a`, and the parameter value is `1`, then `1` will be hit.
		- If the parameter name of a GET configuration is `a`, the parameter value is `\*`, then `1`, `2`, and `3` will be hit.
 - Access frequency: Set the access frequency based on your business, for which a value 3 to 10 times the common number of access requests is recommended. For example, if your website is accessed averagely 20 times per minute, you can configure the value to 60 to 200 times per minute or adjust it according to the attack severity.
 - Action: **Observe**, **CAPTCHA**, or **Block**.
 - Penalty duration: One minute to one week.
 - Priority: Enter an integer between 1 to 100. A smaller integer indicates a higher action priority for a rule. When the priority is the same, the later a rule is created, the higher its priority.


### Example 3: Session-based CC protection settings
CC protection based on session access frequency effectively resolves false positive problems that may occur when the same IP egress is used by multiple users in office buildings, stores, supermarkets, and other public Wi-Fi networks.
>!SESSION must be set before using the session-based CC protection policy. The step 1 to 4 are SESSION setting directions.

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Basic security** on the left sidebar.
2. On the **Basic security** page, select the target domain name in the top-left corner and click **CC protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/851a838dbc3c420ce10fae9fbe2cb03a.png)
2. In the **Session setting** module, click **Set** to set the session dimension information.
![](https://qcloudimg.tencent-cloud.cn/raw/27ef35acbe7613a2f316fedd0d317b88.png)
3. In the **Session setting** pop-up window, enter the required information. In this example, a cookie is used as the test object, whose **Session ID** is `security`, **Session start** is `0`, and **Session end** is `9`. After completing the settings, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/efa08768c7ced8180d8a408a15510a6b.png)

 **Parameter description:**
 - Session location: **COOKIE**, **GET**, or **POST**. Here, **GET** and **POST** are HTTP request content parameters rather than HTTP header information.
 - Match: **Location match** or **String match**.
 - Session ID: Session ID of up to 32 characters.
 - Session start: Location where string or location match starts. It is an integer between 0 and 2048.
 - Session end: Location where string or location match ends. It is an integer between 1 and 2048 and can contain up to 128 characters.
 - GET/POST example: Assume that the complete parameter content in a request is `key_a = 124&key_b = 456&key_c = 789`, then:
	 - In string match mode, if the session ID is `key_b =`, and the end character is `&`, then the matched content will be `456`.
	 - In location match mode, if the session ID is `key_b`, the session start is `0`, and the session end is `2`, then the matched content will be `456`.
 - Cookie example: Assume that the complete cookie content in a request is `cookie_1 = 123;cookie_2 = 456;cookie_3 = 789`, then:
	 - In string match mode, if the session ID is `cookie_2 =`, and the end character is `;`, then the matched content will be `456`.
	 - In location match mode, if the session ID is `cookie_2`, the session start is `0`, and the session end is `2`, then the matched content will be `456`.

4. Click **Test** to test the session information.
![](https://qcloudimg.tencent-cloud.cn/raw/f8264b19e96aa3049dbe4a3b406f44c4.png)
5. Go to the SESSION settings page and set the content to `security = 0123456789`. Then, WAF will use the 10 characters following `security` as the session ID. You can also delete or reconfigure the session information.
![](https://qcloudimg.tencent-cloud.cn/raw/df7f060b839b8dadf885bd44fee423ff.png)
6. Set a session-based CC protection policy as instructed in [Example 2](#two), but select "SESSION" as the recognition mode.
>?If **GET** is selected as the session location in a rule, access with the same session information instead of the IP information will be blocked.

![](https://qcloudimg.tencent-cloud.cn/raw/e111459593dcd460eceda220acc3622c.png)
7. After the configuration is completed, the session-based CC protection policy will take effect.
>!If you use session-based CC protection, you cannot view IP blocking information in the IP blocking status section.
