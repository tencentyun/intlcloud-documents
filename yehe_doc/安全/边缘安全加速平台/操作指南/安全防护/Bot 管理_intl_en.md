## Bot Management
### Overview
Based on request and session characteristics, client reputation intelligence, and smart behavior analysis, the Bot Management feature identifies and restricts access from bot clients (non-browser clients such as proxies, crawlers, scanners, search engine bots, and API clients), identifies and handles high-risk malicious requests (such as malicious scans, botnets, ATO attack sources, high-risk proxies, and brute force attacks), and avoids false positives for legitimate crawlers and API clients.

>?The EdgeOne console is now only available to beta users. [Contact us](https://intl.cloud.tencent.com/contact-us) to join the beta.


**Optimizing bot management rules**
We recommend you optimize rule configurations in the following steps:
- Change the rule action to **Observe**. In this way, the bot management feature allows matched requests and records a rule match log.
- Send a known normal or need-to-block request.
- Check the bot management rule match log. For normal requests, set the action to **Observe** or **Ignore**; for need-to-block requests, set the action to **CAPTCHA** or **Block**.

## Basic Bot Protection Settings

EdgeOne can process requests by characteristic, such as UA, search engine, and IDC.
**Configuration suggestions**
The feature identifies bot requests based on the characteristics of static client requests. 

- UA Feature Rules: Identifies clients of a specific type. It’s applicable to most general scenarios. Configure the rule, set the Action to **Observe** first and then adjust it according to the result.
- Search Engine Rules: Identifies bot clients of search engines. It’s applicable to non-webpage sites (such as API services). If your business is open to the search engines, we recommend you disable it. 
- IDC Rules: Identifies clients from specified IDCs or ISPs. Configure the rule, set the Action to **Observe** first and then adjust it according to the result.


1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **Bot Management** on the left sidebar.
2. On the **Bot management** page, select the target site and subdomain name. In the **Basic bot protection settings** section, click **Set** to adjust the rule configuration.
3. On the **Basic bot protection settings** page, click **Rule settings** on the target rule category card to configure its rules.

**Batch configuring categories**
On the **Basic Bot Management** page, click **Batch setting** and select multiple category cards. The steps are as follows:
1. In batch setting mode, select all the categories you want.
2. Click the **Action** drop-down list and select an action.
3. Click **Apply**.

>! In batch setting mode, you can **Select all** or **Deselect all** category cards at once.

4. On the **Basic Bot Management** > **Rule setting** configuration page, click the **Action** drop-down list of the target rule and select a handling method.

**Batch configuring rules**
On the **Basic Bot Management** > **Rule setting** page, configure multiple rules in a batch. The steps are as follows:

1. Select all the rules you want.
2. Click the **Action** drop-down list and select an action.
3. Click **Apply**.
>?
>- In batch setting mode, you can click **Select all** or the checkbox at the top of the rule column to select all the rules at once.
>! In batch setting mode, you can **Select all** or **Deselect all** rules at once.

4. Click **OK** at the bottom to complete.


## Custom Rule
See the configuration method for custom web protection rules.

## Client Reputation
The client IP reputation is profiled based on the malicious access request and intelligence data collected recently. You can configure the action according to the confidence of the malicious client.
**Client reputation confidence**
Under each type of client reputation rules, each confidence value corresponds to a client address list and reflects the frequency and consistency of a certain type of malicious behaviors performed from client addresses in the list:
- High confidence: Malicious behaviors are performed constantly and highly frequently from the client address. It is almost certain that requests from this address are malicious. We recommend you configure the rule as **Block**.
- Medium confidence: Malicious behaviors are performed frequently from the client address. It is highly probable that requests from this address are malicious; however, false positives may occur. We recommend you configure the rule to **JavaScript challenge** or **Managed challenge**.
- General confidence: Malicious behaviors are performed constantly from the client address. This address is more likely to send malicious requests than others; however, false positives may occur. We recommend you configure the rule to **Observe** and change it to **JavaScript challenge** or **Managed challenge** as needed.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **Bot Management** on the left sidebar.
2. On the **Bot management** page, select the target site and subdomain name and click the ![](https://qcloudimg.tencent-cloud.cn/raw/7d363152eb0ea6c823ae278c4d118dc6.png) in the **Client reputation** section to enable or disable the feature.

>? 
>- After the client reputation feature is disabled, related rules longer take effect. Requests are allowed by default, and no logs are recorded.
>- When the client reputation feature is enabled for the first time, we recommend you configure the detailed rule before enabling the rule. This is to prevent normal business access from being affected.

3. On the **Bot management** page, select the target site and subdomain name and click **Set** in the **Client reputation** section to configure a rule in the module.
4. On the **Client reputation** page, click the **Action** drop-down list in the target malicious behavior category section and select an action.
5. Click **OK** to complete.
