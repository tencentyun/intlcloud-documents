Browser bot defense is a feature that is used for client risk identification and protects your websites with the dynamic verification technique. A unique ID will be generated for each client to detect potential malicious bots in the client access to web or H5 pages.

## Overview
- Compatibility: Browser bot defense is suitable for protecting web and H5 pages. It generates a dynamic client ID and token to detect and identify malicious bot requests. In certain scenarios, it may be incompatible with POST requests (the content-type of the response body cannot be `text/html`, and the response body does not contain the <html> tag), resulting in abnormal dynamic detection. In this case, you can add the request path or the response request to the allowlist.
- User-sensible browser bot defense: It verifies requests via CAPTCHA (such as slider, puzzle, and character verification) to distinguish humans and bots. If verification attempts fail too many times, the request will be blocked. Therefore, it is suitable for protecting the core APIs of your website (such as shopping cart, payment, and SMS APIs). This capability has been integrated in the action setting (Observe, CAPTCHA, Redirect and Block) of WAF modules. You can configure this feature as needed.
- User-insensible browser bot defense: It completes verification without affecting user experience, which is suitable for user-friendly scenarios. Using dynamic security technology, it generates a unique client ID for each client to detect whether malicious bot behaviors happen in the client access to web or H5 pages. You can also take actions to combat malicious access behaviors if necessary.
>! Bot flow defense is limited to web and H5 applications. Mobile terminals and mini programs are not supported.

## Prerequisites
- You have purchased a WAF plan and subscribed to the [bot traffic management](https://intl.cloud.tencent.com/document/product/627/47799) service.
- You have added a protected domain name and ensured the domain name is in normal protection. Meanwhile, bot management rules has been enabled. For detailed directions, see [Getting Started](https://intl.cloud.tencent.com/document/product/627/18635).

>?
>- For domain names added to CLB WAF, browser bot defense is not supported.
>- For wildcard domain names added to SaaS WAF, browser bot defense is not supported neither.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the page that appears, select a domain name and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/14d6fbd6133a0bf3be5bd65d1315c5c5.png)
3. On the bot management page, click **Configure now** in the browser bot defense module.
![](https://qcloudimg.tencent-cloud.cn/raw/dc5dbbe48ba378587e1c890d79894102.png)
4. Toggle on the switches of the settings, such as page anti-debugging and automated identification, and specify the protected path and defense mode.
![](https://qcloudimg.tencent-cloud.cn/raw/51961b8a74494930511dbedc2ac3811e.png)

**Field description**
 - On/Off: It is off by default. When it is on, WAF will perform browser bot defense on the pages specified by the domain name, identify possible crawler behaviors in client requests, and take different actions on crawler behaviors identified. Apps and mini programs are not supported currently.
 - Automated identification: It is on by default. When it is on, it provides assistance with dynamic threat detection.
 - Page anti-debugging: It is on by default. This feature is enabled to stop users from tracking the logic underlying pages with a browser's developer tool.
 - Protected path: The default is `/` , which is a site-wide setting. Up to 5 paths (directory or URL) can be entered and each of them should be separated by commas.
>! You can use this feature to specify a path that you want to protect.

 - Defense mode: When the browser bot defense switch is on, you can set actions to combat crawler behaviors that are detected. The following actions are supported: Monitor, CAPTCHA, Redirect, and Block.




## Configuring Allowlist Policy
### Adding a rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the page that appears, select a domain name and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/0de7561c0dc8e1ae22fbf99180a134f2.png)
3. On the bot management page, click **Configure now** in the browser bot defense module.
4. On the pop-up page, click **Add rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/3a7e5ffb4f41b4b23a2021fbb51c24b5.png)
4. In the pop-up window, configure the required parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/227d4b0db648f4296639f4e5741cc882.png)

**Field description**
 - **Type**
 - **Request allowlist**: Pages of the allowed website URLs do not require dynamic security detection.
 - **Response allowlist**: By default, WAF will insert a JavaScript into the response page according to the business situation. If you need to improve website compatibility, you can configure WAF to not insert a JavaScript into the specified page.
 - **Condition**: It provides "Suffix match" (default setting), "Prefix match", "Equal to" and "Include" options.
 - **Content**: When the condition is **Suffix match**, the file suffixes to be allowed are given by default. Supported file suffixes include: ico, gif, bmp, htc, jpg, jpeg, png, tiff, swf, js, css, rm , rmvb, wmv, avi, mkv, mp3, mp4, ogg, wma, zip, exe, rar, eot, woff, woff2, ttf, and svg. It can be modified according to the actual situation. When the condition is set to other options, enter the path to be allowed.
 - **Rule description (optional)**: Enter a description of the rule.
 - **On/Off**: The switch is off by default. You can enable it as needed.

### Editing a rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the page that appears, select a domain name in the top left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/6ed6108619081c7c64a324e78cc8a018.png)
3. On the bot management page, click **Configure now** in the browser bot defense module.
4. On the pop-up page, select a rule to modify and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/71fec41e3614b4e5a90c35acc4239766.png)
5. In the pop-up window, modify the required parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/bb9800fc0039935f98c126c8e7297992.png)

### Deleting a rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the page that appears, select a domain name in the top left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/6a150c69b41c0926028dd6972b70ac58.png)
3. On the bot management page, click **Configure now** in the browser bot defense module.
4. On the pop-up page, select a rule to modify and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/68c040a34611a5a07c32999404322a34.png)
4. In the pop-up window asking you to confirm the operation, click **OK**.
