This document describes how to quickly connect to the bot traffic management feature and defend against malicious traffic during routine operations.

## Prerequisites
To connect to bot traffic management, you need to purchase an [extra pack](https://intl.cloud.tencent.com/document/product/627/47799) of WAF.
>? Currently, WAF Enterprise and Ultimate users are offered a free trial of the bot traffic management feature to observe how bots affect websites.

## Parsing CAPTCHA
When you use applications, mini programs, and clients as well as cross-domain scheduling, the CAPTCHA issued by the WAF instance cannot be parsed and recognized. Therefore, the bot traffic management feature cannot parse and pop up the CAPTCHA for verification. After multiple CAPTCHAs are triggered, the access requests of normal users will be blocked, affecting the business.

Therefore, when configuring a CAPTCHA action, you need to modify the frontend/client business accordingly as instructed in [Connecting Frontend-Backend Separated Site to WAF CAPTCHA](https://intl.cloud.tencent.com/document/product/627/47522).

## General Business Connection
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/dff646fbcf6d799bd878a9a5f74354b1.png)

### Enabling bot traffic analysis
On the **Bot management** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/180f2bd28c577185924e76f8a19396fe.png) in the **Rules** section.
![](https://qcloudimg.tencent-cloud.cn/raw/23feb01af222d3cb91b9d583fecb6bf0.png)

### Setting browser bot defense module
1. In **Browser bot defense module** on the **Bot management** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/180f2bd28c577185924e76f8a19396fe.png).

>!
>- Make sure that your client is a WeChat Official Account, HTML5 page, application, mini program, or PC client.
>- When you only have a browser, WeChat Official Account, or HTML5 page as the client and need cross-domain scheduling, enable the browser bot defense module to achieve the best protection.
>- After the browser bot defense module is enabled, when its protection path is accesses, the system will check whether the client is capable of parsing JavaScript. A JavaScript code snippet will be issued to verify whether the client is a real browser. For mini programs, applications, and API calls, the query issued by WAF will not be actively parsed, so the client cannot perform parsing normally.

 ![](https://qcloudimg.tencent-cloud.cn/raw/95a38ae64d1a8064a9f8c7518a1212af.png)
2. In the browser bot defense module, click **Configure now** to configure protection for key pages.
>?For more information, see [Bot Management](https://cloud.tencent.com/document/product/627/65688).

![](https://qcloudimg.tencent-cloud.cn/raw/7a2e16f35117cfd474279b0b52d3067f.png)
### Setting threat intelligence module
1. In **Threat intelligence module** on the **Bot management** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/f3f8be1cf90fd16cb762064d1bc2bf57.png). When the module is enabled for the first time, all recognition items will be enabled. After you enable corresponding items, you can recognize the access sources at different malicious levels from the threat intelligence module and IDC.
![](https://qcloudimg.tencent-cloud.cn/raw/9b5320153cfd83babd35bd2212db1af0.png)

2. In the threat intelligence module, click **Configure now** to set the IDC network and threat intelligence library.

>?The current business callback API is in the IDC domain:
>- If you are not sure about a source IP, [contact us](https://intl.cloud.tencent.com/contact-us) to add the IDC to the allowlist, that is, to disable the IDC option in the threat intelligence module for the business.
>- If you are sure about the current business callback IP, add the source IP to the allowlist in **Custom rules**. For more information, see [Precise Allowlist Management](https://intl.cloud.tencent.com/document/product/627/47523).

![](https://qcloudimg.tencent-cloud.cn/raw/6153585eb5b81a6d93ef11fc70571149.png)

### Enabling AI evaluation module
 In **AI evaluation module** on the **Bot management** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/25ee88daf408bcac2a80287e314e669c.png).
![](https://qcloudimg.tencent-cloud.cn/raw/f10a95cb63b967c95f24394beb13fd9e.png)

### Enabling bot flow statistics module
In **Bot flow statistics module** on the **Bot management** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/f05a86c4176526c2846a61f2a2207a37.png).
![](https://qcloudimg.tencent-cloud.cn/raw/bce147ee99af061f5d36fe3adf6aca39.png)

### Setting action score
1. In the **Action setting** section on the **Bot management** page, click **Action score**.
![](https://qcloudimg.tencent-cloud.cn/raw/d408b9166acea71c42dc531053453f91.png)
2. On the **Action setting** tab, you can configure the score and action to precisely block risky access requests.
![](https://qcloudimg.tencent-cloud.cn/raw/69a1bd85122d64107667db288f204ae4.png)

**Use instructions**
 - **Mode**: By default, there are loose, moderate, strict, and custom modes. The first three modes are preset, representing different recommended categories and handling policies for bots at different malicious levels in bot traffic management. Once modified, they become the custom mode.
 - **Score range**: A score ranges from 0 to 100. Ten score entries can be added to each range, which is left-closed and right-open and cannot be overlapped. You can set a range to null, and then no action will be processed in it.
 - **Action**: You can set an action to **Trust**, **Monitor**, **Redirect** (to a certain website URL), **CAPTCHA** (verification code), or **Block**.
 - **Tag**: You can set the tag to **Friendly bots**, **Malicious bots**, **Normal traffic**, or **Suspicious bots**.
    - **Friendly bots**: The bot is friendly and legal for the website by default.
    - **Suspicious bots**: The system finds the access source traffic suspicious but cannot determine if it is malicious to the website.
    - **Normal traffic**: The access traffic is regarded as from a real user.
    - **Malicious bots**: The bot has malicious traffic and is unfriendly to the website.
3. After completing the configuration, click **Publish** in the bottom-left corner of the page.
