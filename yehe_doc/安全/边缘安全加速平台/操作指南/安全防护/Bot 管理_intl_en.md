## Overview
Based on request and session characteristics, client reputation intelligence, and smart behavior analysis, the Bot Management feature identifies and restricts access from bot clients (non-browser clients such as proxies, crawlers, scanners, search engine bots, and API clients), identifies and handles high-risk malicious requests (such as malicious scans, botnets, ATO attack sources, high-risk proxies, and brute force attacks), and reduces false positives and blocking for low-risk crawlers and legitimate APIs.


We recommend you optimize bot management rule configurations in the following steps:
<dx-steps>
- Change the rule action to **Observe**. In this way, the bot management feature allows matched requests and records a rule match log.
- Send a known normal or need-to-block request.
- Check the bot management rule match log. For normal requests, set the action to **Observe** or **Ignore**; for need-to-block requests, set the action to **CAPTCHA** (**JavaScript challenge** or **Managed challenge**) or **Block**.
</dx-steps>


## Basic Bot Protection Settings
EdgeOne can process requests by characteristic, such as UA, search engine, and IDC.
>? Configuration suggestion: The feature identifies bot requests based on the characteristics of static client requests.
>- UA Feature Rules: Identifies clients of a specific type. It's applicable to most general scenarios. Configure the rule, set the Action to **Observe** first and then adjust it according to the result.
>- Search Engine Rules: Identifies bot clients of search engines. It's applicable to non-webpage sites (such as API services). If your business is open to the search engines, we recommend you disable it.
>- IDC Rules: Identifies clients from specified IDCs or ISPs. Configure the rule, set the Action to **Observe** first and then adjust it according to the result.


1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone), select **Security** > **Bot Management** on the left sidebar, and select the desired site and subdomain name.
2. In the **Basic bot protection settings** section, click **Set** to adjust the rule configuration.
3. On the **Basic bot protection settings** page, you can set a single rule category or batch set rule categories.
   - Set a single rule category
      1. Click **Rule setting** on the target rule category card to configure its rules.
           ![](https://qcloudimg.tencent-cloud.cn/raw/d53e9ecef4f0633b8d8abcf60cbc18d3.png)
      2. Select a **Rule ID**, click the **Action** drop-down list, and select an action.
    ![](https://qcloudimg.tencent-cloud.cn/raw/c22dfa608371b6d13753ace90e9c08b7.png)
      3. Click **Apply**.
   - Batch set rule categories
     1. On the **Basic bot protection settings** page, click **Batch setting** and select one or more rule categories.
     2. In batch setting mode, select all the categories you want.
>? In batch setting mode, you can **Select all** or **Deselect all** category cards at once.

![](https://qcloudimg.tencent-cloud.cn/raw/b432c9d3e2fd396bb59c088f6385b474.png)
    3. Click the **Action** drop-down list and select an action.
		 ![](https://qcloudimg.tencent-cloud.cn/raw/98a41bb8ce2a218e5cd6249d11a604dd.png)
        4. Click **Apply**.

4. Click **OK** at the bottom to complete.



## Custom Rule
This feature allows you to create custom rules for a number of business use cases, such as allowing/blocking specific traffic.

### Adding a rule
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone), select **Security** > **Bot Management** on the left sidebar, and select the desired site and subdomain name.
![](https://qcloudimg.tencent-cloud.cn/raw/1f28be03af575f6c8fa7aca2e7adc5ec.png)
2. In the **Custom rules** section, click **Set**.
3. On the custom rule page, click **Add rule**. Set the rule name, matching method, action, and priority.
![](https://qcloudimg.tencent-cloud.cn/raw/73497ee33b83ad9f87aebdfb1c8e411e.png)

**Parameter description:**
 - Rule name: It contains letters, digits, and underscores. A rule name will be generated automatically if this parameter is left empty. Note that a rule name must be unique.
 - Matching method: It consists of configuration items such as the protocol field (http/https) and the logical operator (include/equal to). Up to 5 conditions per rule are allowed, and the relation among conditions is "AND". Note that the same field can only be configured once in each rule.
 - Action: Select as needed.
 - Priority: Execution order of a rule. Custom rules with higher priority (a larger priority value) take precedence over those with lower priority (a smaller priority value). For custom rules with the same priority, the later-added one will be executed first.

3. Click **OK**.

### Enabling a rule
On the **Custom rules** page, you can enable a single rule or multiple rules.
  - To enable a single rule, select the target **Rule ID** and toggle on the switch ![](https://qcloudimg.tencent-cloud.cn/raw/171fbbf6fe32c80aba5be84541814e23.png).
![](https://qcloudimg.tencent-cloud.cn/raw/1d0ccf947d5423281e6d4f10ed27f841.png)
  - To enable multiple rules, click **Enable** after you select rules you want to enable.
![](https://qcloudimg.tencent-cloud.cn/raw/3621f94947c9dc38c35bfaec48bdebbb.png)

### Disabling a rule
On the **Custom rules** page, you can disable a single rule or multiple rules.
  - To disable a single rule, turn off the switch ![](https://qcloudimg.tencent-cloud.cn/raw/057134e300a8daaed49b0d60348921e3.png) on the right of the rule.
  - To disable multiple rules, click **Disable** after you select rules you want to disable.
![](https://qcloudimg.tencent-cloud.cn/raw/02d00aa6ca32cc679efc996dcb3a5016.png)

### Deleting a rule
1. On the custom rule page, select a rule you want to delete, and click **Delete** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/3b77dbf5b2574c2689689848382fd131.png)
2. In the **Delete rule** pop-up window, click **Delete**.


## Client Reputation
The client IP reputation is profiled based on the malicious access request and intelligence data collected recently. You can configure the action according to the confidence of the malicious client.
>? Client reputation confidence: Under each type of client reputation rules, each confidence value corresponds to a client address list and reflects the frequency and consistency of a certain type of malicious behaviors performed from client addresses in the list.
>- High confidence: Malicious behaviors are performed constantly and highly frequently from the client address. It is almost certain that requests from this address are malicious. We recommend you configure the rule as **Block**.
>- Medium confidence: Malicious behaviors are performed frequently from the client address. It is highly probable that requests from this address are malicious; however, false positives may occur. We recommend you configure the rule to **JavaScript challenge** or **Managed challenge**.
>- General confidence: Malicious behaviors are performed constantly from the client address. This address is more likely to send malicious requests than others; however, false positives may occur. We recommend you configure the rule to **Observe** and change it to **JavaScript challenge** or **Managed challenge** as needed.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone), select **Security** > **Bot Management** on the left sidebar, and select the desired site and subdomain name.
![](https://qcloudimg.tencent-cloud.cn/raw/7fe5587ddbeee79de769dcf7e803b7ab.png)
2. In the **Client reputation** section, toggle on or off the switch on the right.
>?
>- After the client reputation feature is disabled, related rules no longer take effect. Requests are allowed by default, and no logs are recorded.
>- When the client reputation feature is enabled for the first time, we recommend you configure the detailed rule before enabling the rule. This is to prevent normal business access from being affected.

![](https://qcloudimg.tencent-cloud.cn/raw/7fe5587ddbeee79de769dcf7e803b7ab.png)
3. In the **Client reputation** section, click **Set** to configure a rule in the module.
4. On the **Client reputation** page, click the **Action** drop-down list in the target malicious behavior category section and select an action.
![](https://qcloudimg.tencent-cloud.cn/raw/8c8d0da46e004207bee9feadd4afb397.png)
5. Click **OK** to complete.
