Anti-DDoS Advanced supports HTTP/HTTPS CC protection. When the number of HTTP/HTTPS requests recorded by Anti-DDoS Advanced exceeds the set **maximum number of HTTP/HTTPS requests**, HTTP/HTTPS CC protection will be automatically triggered.
Anti-DDoS Advanced allows you to set an ACL. By enabling HTTP/HTTPS CC protection, you can use common HTTP/HTTPS packet fields (such as host, CGI, Referer, and User-Agent parameters) to set matching conditions, so as to control access requests from internet users, i.e., blocking requests that hit the conditions or triggering CAPTCHA verification. You can also set speed limit rules to limit the speed of access IPs.
Anti-DDoS Advanced also allows you to configure URL whitelist, IP whitelist, and IP blacklist.
-  For URLs in the whitelist, their access requests do not require CC attack detection and can pass directly.
-  For IPs in the whitelist, their HTTP/HTTPS access requests do not require CC attack detection and can pass directly.
-  For IPs in the blacklist, their HTTP/HTTPS access request will be directly denied.


## Enabling CC Protection
**HTTP CC protection**
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar. On the protection configuration page, click **CC Protection** and select the target instance.
1. In the **HTTP CC Protection** section, click <img src="https://main.qcloudimg.com/raw/9d7bb2c60a2b375acb45614f39e4986f.png"  style="margin:0;"> on the right of **Protection Status** to enable HTTP CC protection. Then, click the drop-down list on the right of **Maximum Number of HTTP Requests** to select an appropriate upper limit.
>CC protection is disabled by default. Only after it is enabled can the maximum number of HTTP requests be set.

**HTTPS CC protection**
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar. On the protection configuration page, click **CC Protection** and select the target instance.
2. In the **HTTPS CC Protection** section, select a protected domain name and click <img src="https://main.qcloudimg.com/raw/9d7bb2c60a2b375acb45614f39e4986f.png"  style="margin:0;"> on the right of **Protection Status** to enable HTTPS CC protection. Then, click the drop-down list on the right of **Maximum Number of HTTPS Requests** to select an appropriate upper limit.
>CC protection is disabled by default. Only after it is enabled can the HTTPS requests threshold be set.


## Customizing CC Protection Policies
> 
- **Only after HTTP/HTTPS CC protection is enabled can you customize CC protection policies. Up to 5 policies can be added.**
- **A custom policy will take effect only when your Anti-DDoS Advanced instance is under attack.**
-  In **match mode**, each custom policy may have up to **four** conditions for characteristic control, and the logical relationship between these conditions is "AND", which means all conditions must be matched before the policy will take effect.
-  In **speed limit mode**, each custom policy can have only **one** condition.
>
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar to enter the protection configuration page. Click **CC Protection**, select the region, line, and target instance, and click **Add ACL**.
2. In the **Add ACL** pop-up window, set the following parameters as needed and click **OK**.
- Policy Name
	Enter the policy name, which can contain 1–20 characters of any type.
- Protocol
	Currently, HTTP and HTTPS are supported.
- Protected Domain Name
	Only when HTTPS is selected can a protected domain name be selected accordingly. You can select the protected domain name range, i.e., HTTPS website domain names in the configured forwarding rules.
- Mode
		- Match mode: if an HTTP/HTTPS request with the specified field header is detected, it will be blocked or processed for CAPTCHA verification.
		- Speed limit mode: the speed of access requests from the source IP will be limited. **This mode is not supported for HTTPS.**
	- Policy
		- **If the **match mode** is selected and the protocol is HTTP**, multiple fields of an HTTP packet, namely, host, CGI, Referer, and User-Agent parameters, can be combined in various logical relationships such as "INCLUSIVE", "EXCLUSIVE", and "EQUAL TO", and you can set up to four policy conditions to combine the fields. **If the protocol is HTTPS**, multiple fields of an HTTPS packet, namely, CGI, Referer, and User-Agent parameters, can be combined in various logical relationships such as "INCLUSIVE", "EXCLUSIVE", and "EQUAL TO", and you can set up to three policy conditions to combine the fields. The fields are as described below:
		<table>
		<tr><th>Matched Field</th><th>Description</th><th>Applicable Logical Operators</th></tr>
		<tr><td>host</td><td>Domain name of the access request.</td><td>INCLUSIVE, EXCLUSIVE, and EQUAL TO</td></tr>
		<tr><td>CGI</td><td>URI of the access request.</td><td>INCLUSIVE, EXCLUSIVE, and EQUAL TO</td></tr>
		<tr><td>Referer</td><td>Source website address of the access request, indicating the page from which the access request is generated.</td><td>INCLUSIVE, EXCLUSIVE, and EQUAL TO</td></tr>
		<tr><td>User-Agent</td><td>Information such as browser identifier of the client that initiates the access request.</td><td>INCLUSIVE, EXCLUSIVE, and EQUAL TO</td></tr>
		</table>
		- When you select the **speed limit mode**, the speed of each source IP access request will be limited. You are allowed to set only one policy condition.
	- Run
This parameter is required only when the **match mode** is selected, indicating the action that needs to be performed after a policy is matched, such as blocking or CAPTCHA verification.

## Setting Blacklist/Whitelist
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Advanced** > **Protection Configuration** on the left sidebar to enter the protection configuration page. Click **CC Protection** and select the region, line, and target instance.
2. Select **HTTP** or **HTTPS** on the right of the page and select **URL Whitelist**, **IP Whitelist**, or **IP Blacklist** to set the blacklist/whitelist. You can add or modify entries or export/import them in batches.
