## Operation Scenarios
Anti-DDoS Pro supports the CC protection function. When the HTTP request amount calculated by Anti-DDoS Pro exceeds the set **HTTP Request Threshold**, CC protection is automatically triggered. Meanwhile, Anti-DDoS Pro supports URL whitelist, IP whitelist, and IP blacklist policies:
- For URLs in the whitelist, their access requests do not require CC attack detection and can pass directly.
- For IPs in the whitelist, their HTTP access requests do not require CC attack detection and can pass directly.
- For IPs in the blacklist, their HTTP access request will be directly denied.

You can custom the protection policy according to the features and protection needs of your business to block CC attacks more accurately.

## Steps
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **CC Protection** tab, select the target region and Anti-DDoS Pro instance to configure CC protection.
![](https://main.qcloudimg.com/raw/ec16ed5e0a454ed99be648fc901054f5.png)
1. Click <img src="https://main.qcloudimg.com/raw/cd0f9c22bb255091a244938a6bfbefaa.png"  style="margin:0;"> next to **CC Protection** to enable it.
>- By default, CC Protection is disabled.
	- You can set the HTTP request amount threshold, custom CC protection policy and blacklist/whitelist when you enable CC protection.
1. Click the drop-down list right to the **HTTP Request Threshold** to select a proper threshold.
2. Click **Add Policy**, and then set the following parameters according to the actual business demand in the **Add Custom Policy** pop-up box. Click **OK** to complete the configuration.
![](https://main.qcloudimg.com/raw/cdea67ab2e4201c88f20cf95b6597c6b.png)

 >- **The custom policy takes effect only when Anti-DDoS Pro is under attack.**
	- **Match mode**: Each custom policy may have up to **4** conditions for feature control, and these conditions have “and” relation, which means all conditions must be matched before the policy takes effect.
	- **Speed limit mode**: Each custom policy only allows for setting **1** policy condition.

	- **Policy Name**
Enter policy name, which consists of 1-20 characters. Character type is not restricted.
	- **Mode**
		-   Match Mode: Requests matched to the corresponding HTTP field. It performs blocking or verification code operation.
		-    Speed Limit Mode: Limits the speed of source IP access.
	- **Policy**
		-    When you select **Match Mode**, it supports a combination of multiple features such as `host`, `CGI`, `Referer`, and `User-Agent` from HTTP messages. The combination logic includes contain, not contain, and equal to. You can set up to 4 policy conditions for feature control.  
		-    When you select **Speed Limit Mode**, you limit the speed of each source IP access. You are allowed to set only one policy condition.
![](https://main.qcloudimg.com/raw/4722af1ff5b4eed7da5448d09a18f1f0.png)

1. Click **URL Whitelist**, **IP Whitelist**, or **IP Blacklist** tab for blacklist/whitelist configuration. Addition and deletion are allowed.
