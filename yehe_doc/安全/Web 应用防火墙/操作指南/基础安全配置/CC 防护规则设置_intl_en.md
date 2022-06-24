## Overview
CC protection can safeguard the access to specified URLs. CC protection settings 2.0 is upgraded with emergency CC protection and custom CC rules. Emergency CC protection can perform big data analysis on websites' access history and their real servers' exceptional response such as timeout and response delay, to generate protection policies for emergencies, blocking frequent access requests in real time. Custom CC rules support customizing protection rules based on user access source IPs or SESSION frequency to handle access by blocking, setting alarms, or verifying identity with CAPTCHA.
>!
>- Emergency CC protection and custom CC rules cannot be enabled at the same time.
>- SESSION must be set before using the session-based CC protection policy.

## Directions
#### Example 1: Emergency CC protection settings
Emergency CC protection is disabled by default. Before enabling it, please make sure that the custom CC rule feature is disabled.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **CC Protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/f3944d2278c8369fd7862262ac60b1ae.png)
3. Click ![](https://qcloudimg.tencent-cloud.cn/raw/d3ac9fa840f84ca53bd0884f728d348f.png) in the emergency CC protection module and confirm the operation to configure emergency CC protection.
![](https://qcloudimg.tencent-cloud.cn/raw/6138761fc0067143a570ace892b1c322.png)

**Configuration item description:**
**Status switch:** After emergency CC protection is enabled, if a website is under massive CC attacks (with a website QPS of 1000 or above), the protection will be automatically triggered. If there are no specific protection paths, we recommend enabling emergency CC protection. As there may be some false alarms, you can click [IP Query](https://console.cloud.tencent.com/guanjia/tea-ipsearch) on the left sidebar to view the information of blocked IPs and handle them in time.

>?
>- If there are specific protection paths, we recommend using custom CC rules.
>- CLB WAF does not support emergency protection. We recommend using custom CC protection.

#### Example 2: Access source IP-based CC protection settings
An IP-based CC protection policy can be directly configured without setting SESSION.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **CC Protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/493439bbad9043b362fb215720a01e1d.png)
2. On the CC protection page, click **Add rule**, and the rule adding window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/9652ef553c44b1fc6b7d288854c154d9.png)
3. In the pop-up window, configure relevant parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/795e268a42b569308051ecd7aa823a59.png)

**Field description:**
 - **Rule name**: Name of the CC protection rule. It can contain up to 50 characters.
 - **Recognition mode**: It supports two modes: IP recognition (default) and SESSION recognition. To use SESSION recognition, you need to set the SESSION position first.
 - **Match method**: It specifies the match parameter, logical operator and match content to control access frequency. The match parameter defaults to URL. For the same rule, you can set up to 10 conditions with the logical AND operator, which should contain at least one URL condition. The fields are described as follows:
 <table>
<thead>
<tr>
<th>Match Field</th>
<th>Match Parameter</th>
<th>Logical Operators</th>
<th>Match Content Description</th>
</tr>
</thead>
<tbody><tr>
<td>URL</td>
<td>N/A</td>
<td><ul><li>Equal to</li><li>Include</li><li>Prefix match</li></ul></td>
<td>Required. The URL prefixed with "/" can contain up to 128 characters, which can be a directory or specific path.</td>
</tr>
<tr>
<td>Method</td>
<td>N/A</td>
<td><ul><li>Equal to</li><li>Include</li><li>Not equal to</li></ul></td>
<td>Values: `HEAD`, `GET`, `POST`, `PUT`, `OPTIONS`, `TRACE`, `DELETE`, `PATCH` and `CONNECT`. You can specify a method as needed.</td>
</tr>
<tr>
<td>Query</td>
<td>Key value in the `Query` parameter</td>
<td><ul><li>Equal to</li></ul></td>
<td>Required. The key value can contain up to 512 characters, which can be set multiple times.</td>
</tr>
<tr>
<td>Referer</td>
<td>N/A</td>
<td><ul><li>Equal to</li><li>Include</li><li>Prefix match</li></ul></td>
<td>The value can contain up to 512 characters.</td>
</tr>
<tr>
<td>Cookie</td>
<td>Key value in the `Cookie` parameter</td>
<td><ul><li>Equal to</li><li>Include</li><li>Not equal to</li></ul></td>
<td>Required. The key value can contain up to 512 characters.</td>
</tr>
<tr>
<td>User-Agent</td>
<td>N/A</td>
<td><ul><li>Equal to</li><li>Include</li><li>Not equal to</li></ul></td>
<td>The value can contain up to 512 characters.</td>
</tr>
<tr>
<td>Custom request header</td>
<td>Request header key value, such as Accept, Accept-Language, Accept-Encoding, and Connection.</td>
<td><ul><li>Equal to</li><li>Include</li><li>Not equal to</li><li>Blank</li><li>Not exist</li></ul></td>
<td>The key value can contain up to 512 characters, which can be set multiple times. If the matching content is blank or does not exist, you can directly enter the matching parameter.</td>
</tr>
</tbody></table>

 - **Access frequency:** sets the access frequency based on actual business requirements. We recommend setting a value 3 to 10 times the normal access frequency. For example, if your website is accessed 20 times per minute per visitor, you can set the access frequency to 60 to 200 times per minute, which can be further adjusted based on the attack severity.
 - **Action**: Defaults to "Block". You can set this field as needed. The detailed field description is as follows:
 <table>
<thead>
<tr>
<th align="left">Action Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Observe</td>
<td align="left">Session requests that meet the specified conditions will be monitored and logged. You can check the records in <a href="https://console.cloud.tencent.com/guanjia/tea-attacklog">Attack Logs</a>.</td>
</tr>
<tr>
<td align="left">CAPTCHA</td>
<td align="left">This is applicable only to the access through browsers. Session requests that match the specified conditions will be verified through CAPTCHA. If they fail, they will be blocked. Otherwise, they can normally access within the penalty period. CAPTCHA logs will be observed.</td>
</tr>
<tr>
<td align="left">Precise block</td>
<td align="left">Access requests that match the specified frequency control rules will be blocked precisely, indicating that the specific IP, instead of the domain name, will be blocked from accessing the protected URL within the penalty period ranging from 5 minutes to 10,080 minutes (7 days). You can view the blocking results in <a href="https://console.cloud.tencent.com/guanjia/tea-attacklog">Attack Logs</a>.</td>
</tr>
<tr>
<td align="left">Block</td>
<td align="left">Access requests that match the set frequency control rules will be blocked, indicating that the specific IP will be blocked from accessing all URLs within the penalty period ranging from 5 minutes to 10,080 minutes (7 days). You can view the blocking results in <a href="https://console.cloud.tencent.com/guanjia/tea-attacklog">Attack Logs</a> and check the blocked IPs in real time in <a href="https://console.cloud.tencent.com/guanjia/tea-ipsearch">IP Query</a>.</td>
</tr>
</tbody></table>

 - **Penalty duration**: It ranges from 1 minute to 1 week. Default: 10 minutes.
 - **Priority:** Enter an integer from 1 to 100 (default: 50). The smaller the value, the higher the priority of this rule. For rules with the same priority, the last created one will be used.
5. You can select a created rule to disable, modify, or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/4057c2fff6c6dd4132b831b39dfc0fc0.png)
6. Conduct test CC attacks based on the rule settings.
![](https://qcloudimg.tencent-cloud.cn/raw/81ea498d65a545f33d540132042b0711.png)
7. You can add IPs to the blocklist/allowlist on the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist) and view the blocking information on the [IP query page](https://console.cloud.tencent.com/guanjia/tea-ipsearch).

#### Example 3: Session-based CC protection settings
CC protection based on session access frequency effectively resolves false positive problems that may occur when the same IP egress is used by multiple users in office buildings, stores, supermarkets, and other public Wi-Fi networks.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **CC protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/801b5f3304a817e32f3a47ce5a098249.png)
3. Click **Settings** in SESSION settings and the SESSION settings window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/ad10d68367dd24be0120354b28fcc28d.png)
4. In the pop-up window, enter the required information. In this example, a cookie is used as the test object, whose ID is `security`, start position is `0`, and end position is `9`. After completing the settings, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/c7e711768bb87eb49f33dd311e1bc7a5.png)

 **Field description:**
 - **Session position:** "COOKIE", "GET", or "POST". GET and POST are HTTP request content parameters rather than HTTP header information.
 - **Match mode:** It supports two modes: position match and string match.
 - **Session ID:** ID of the session.
 - **Start position:** Position where string or position match starts.
 - **End position:** Position where string or position match ends.
 - **GET/POST example:**
Assume that the complete parameter content in a request is `key_a = 124&key_b = 456&key_c = 789`, then:
	 - In string match mode, if the session ID is `key_b =`, and the end character is `&`, then the matched content will be `456`.
     - In position match mode, if the session ID is `key_b`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.
 - **COOKIE example:**
Assume that the complete cookie content in a request is `cookie_1 = 123;cookie_2 = 456;cookie_3 = 789`, then:
 	 - In string match mode, if the session ID is `cookie_2 =`, and the end character is `;`, then the matched content will be `456`.
 	 - In position match mode, if the session ID is `cookie_2`, the start position is `0`, and the end position is `2`, then the matched content will be `456`.
 - **HEADER example:**
Assume that the complete header content in a request is `X-UUID: b65781026ca5678765`, then:
     - In position match mode, if the session ID is `X-UUID`, the start position is `0`, and the end position is `2`, then the matched content will be `b65`.
5. Click **Test**, enter relevant content, and click **OK** to test the session information.
![](https://qcloudimg.tencent-cloud.cn/raw/c48548e60b129dde438518f296053fe7.png)
6. Go to the SESSION settings page and set the content to `security = 0123456789`. Then, WAF will use the 10 characters following `security` as the session ID. You can also delete or reconfigure the session information.
![](https://qcloudimg.tencent-cloud.cn/raw/c301dc4f96bdcfea738cf43a32a5f3a0.png)
7. Set a session-based CC protection policy as instructed in Example 1, but select "SESSION" as the recognition mode.
![](https://qcloudimg.tencent-cloud.cn/raw/eecc3c1d8d0f4fe3398f9c8e6574fe72.png)
8. After the configuration is completed, the session-based CC protection policy will take effect.
>!If you use session-based CC protection, you cannot view IP blocking information in the IP blocking status section.


