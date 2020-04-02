### Operation Scenarios
Anti-DDoS Pro supports the CC protection function. When the HTTP request amount calculated by Anti-DDoS Pro exceeds the set **HTTP Request Threshold**, CC protection is automatically triggered. Meanwhile, Anti-DDoS Pro supports URL whitelist, IP whitelist, and IP blacklist policies:
- For URLs in the whitelist, their access requests do not require CC attack detection and can pass directly.
- For IPs in the whitelist, their HTTP access requests do not require CC attack detection and can pass directly.
- For IPs in the blacklist, their HTTP access request will be directly denied.

You can custom the protection policy according to the features and protection needs of your business to block CC attacks more accurately.

## Directions
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgpip_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **CC Protection** tab, select the target region and Anti-DDoS Pro instance to configure CC protection.
![](https://main.qcloudimg.com/raw/8e05d9a18bb909e7badb6f97e13e643e.png)
1. Click <img src="https://main.qcloudimg.com/raw/cd0f9c22bb255091a244938a6bfbefaa.png"  style="margin:0;"> next to **CC Protection** to enable it.
>
	- By default, CC Protection is disabled.
	- You can set the HTTP request amount threshold, custom CC protection policy and blacklist/whitelist when you enable CC protection.
1. Click the drop-down list right to the **HTTP Request Threshold** to select a proper threshold.
2. Click **Add Access Control Policy**, and then set the following parameters according to the actual business demand in the **Add Access Control Policy** pop-up box. Click **OK** to complete the configuration.
![](https://main.qcloudimg.com/raw/d22693d68f47c9c83655d0b56a7e77f6.png)
 >
	- **The custom policy takes effect only when Anti-DDoS Pro is under attack.**
	- **Match mode**: Each custom policy may have up to **4** conditions for feature control, and these conditions have “and” relation, which means all conditions must be matched before the policy takes effect.
	- **Speed limit mode**: Each custom policy only allows for setting **1** policy condition.

	- **Policy Name**
Enter policy name, which consists of 1-20 characters. Character type is not restricted.
	- **Mode**
		-   Match Mode: When it detects requests matched the corresponding HTTP field, it will block the request or require human-machine recognition.
		-    Speed Limit Mode: Limits the speed of source IP access.
	- **Policy**
		-    When you select **Match Mode**, it supports a combination of multiple features such as `host`, `CGI`, `Referer`, and `User-Agent` from HTTP messages. The combination logic includes contain, not contain, and equal to. You can set up to 4 policy conditions for feature control as described below: 
		<table>
		<tr><th>Field</th><th>Description</th><th>Logic</th></tr>
		<tr><td>host</td><td>Domain name of the access request</td><td>contain, not contain, equal to</td></tr>
		<tr><td>CGI</td><td>URL of the access request</td><td>contain, not contain, equal to</td></tr>
		<tr><td>Referer</td><td>Source website of the access request, which means at which webpage the access request is generated</td><td>contain, not contain, equal to</td></tr>
		<tr><td>User-Agent</td><td>Information like browser identifier of the requester client </td><td>contain, not contain, equal to</td></tr>
		</table>
		-    When you select **Speed Limit Mode**, you limit the speed of each source IP access. You are allowed to set only one policy condition.
![](https://main.qcloudimg.com/raw/a71b5fbc1af7fb87749f21cf7e7015b3.png)

5. Click **URL Whitelist**, **IP Whitelist**, or **IP Blacklist** tab for blacklist/whitelist configuration. Addition and deletion are allowed.
> When you add a URL to the Anti-DDoS Pro whitelist, the HTTP protocol header is optional. But Anti-DDoS Pro supports only HTTP protocol. Example: `http://test.com/index.php` or `www.test.com/index.php`.
