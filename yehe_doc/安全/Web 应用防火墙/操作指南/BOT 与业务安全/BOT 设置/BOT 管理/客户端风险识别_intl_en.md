This document describes the browser bot defense module in client risk identification. With the dynamic identity verification technology, it will generate a unique ID for each client's business request to detect possible malicious bots and crawlers in access to websites or HTML5 pages.

## Background
- Compatibility description: The browser bot defense module is applicable to the protection for websites or HTML5 pages. It will dynamically generate client IDs and tokens and identify malicious and crawler requests by detecting the IDs and tokens. In some cases, it may have compatibility issues with POST requests (the content of the `content-type` response body is not `text/html`, and the `<html>` tag is not included). This may cause an exception in the detection. As a countermeasure, you can add the request path or response request to the allowlist.
- Perceptible bot defense: The system pops up a CAPTCHA (slider, puzzle, or character comparison) for client requests that meet the conditions to differentiate between access requests from a real person and a bot. Multiple verification failures will lead to blocking. This is applicable to protecting core website APIs (such as shopping cart, payment, and SMS). This capability has been integrated into the actions (observe, CAPTCHA, redirect, and block) of each WAF module for you to use.
- Imperceptible bot defense: Client behavior detection is imperceptible to users, applicable to use cases with high requirements for the user experience. This feature leverages the dynamic security technology to generate a unique ID for each client and detect possible click farming and malicious crawling in the access to websites or HTML5 pages. You can perform an action on malicious behaviors as needed.
>!The browser bot defense module is applicable to websites and HTML5 pages but not mobile terminals or mini programs.

## Prerequisites
- You have purchased a WAF instance and [bot traffic management extra pack](https://intl.cloud.tencent.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E).
- You have added a protected domain name, the domain name is in normal protection, and bot management rules are on. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/627/18635).
>?
>- The browser bot defense module is not supported for domain names added to CLB WAF instances.
>- The browser bot defense module is not supported for wildcard domain names added to SaaS WAF instances.

## Protection Configuration
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/14d6fbd6133a0bf3be5bd65d1315c5c5.png)
3. In **Global settings**, click **Configure now** in the **Browser bot defense module** section.
4. Set the automated identification, page anti-debugging, and allowlist policy.
![](https://qcloudimg.tencent-cloud.cn/raw/dc5dbbe48ba378587e1c890d79894102.png)
5. On the **Browser bot defense module** page, configure page anti-debugging and automated identification.
![](https://qcloudimg.tencent-cloud.cn/raw/51961b8a74494930511dbedc2ac3811e.png)
6. Click the configuration page of a certain scenario, click **Browser bot defense module**, toggle on or off the **On/Off** switch of the **Browser bot defense module**, and select the **Defense mode**.

**Field description**
  - **On/Off**: It is off by default. When it is on, WAF will protect the page specified by the domain name through the browser bot defense module to identify possible crawlers in the client request and take different actions after identification. It is not applicable to applications or mini programs.
 - **Automated identification**: It is enabled by default to assist with dynamic threat detection.
  - **Page anti-debugging**: It is enabled by default to prevent users from tracking the page logic when they call the developer tool page of the browser.
>! We recommend you enable this feature for the sensitive directory to be protected.

 - **Defense mode**: It is **Monitor** by default and can be configured to perform an action on the crawlers detected by the browser bot defense module, such as monitor, CAPTCHA, redirect, or block.


## Configuring Allowlist Policy
### Adding rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner. In **Global settings**, click **Configure now** in the **Browser bot defense module** section.
![](https://qcloudimg.tencent-cloud.cn/raw/0de7561c0dc8e1ae22fbf99180a134f2.png)
3. On the **Browser bot defense module** page, click **Add rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/3a7e5ffb4f41b4b23a2021fbb51c24b5.png)
4. In the **Add allowlist rule** pop-up window, configure parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/227d4b0db648f4296639f4e5741cc882.png)

**Field description**
 - **Type**
    - **Request allowlist**: Dynamic security detection is not required for allowed website URLs.
    - **Response allowlist**: By default, WAF will insert JavaScript code into a responding page according to the business conditions. It can be configured not to insert JavaScript code into a specified website so as to improve the website compatibility.
 - **Match condition**: **Suffix match** (default), **Prefix match**, **Equal to**, and **Include** are supported.
 - **Match content**: The current match condition is **Suffix match**. By default, the suffixes of files to be allowed are offered, including ico, gif, bmp, htc, jpg, jpeg, png, tiff, swf, js, css, rm, rmvb, wmv, avi, mkv, mp3, mp4, ogg, wma, zip, exe, rar, eot, woff, woff2, ttf, and svg. You can modify the suffix as needed. If another match condition is selected, enter the allowlist path according to the actual business conditions.
 - **Rule description (optional)**: Enter the rule description.
 - **On/Off**: It is off by default and can be changed as needed.

### Editing rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner. In **Global settings**, click **Configure now** in the **Browser bot defense module** section.
![](https://qcloudimg.tencent-cloud.cn/raw/6ed6108619081c7c64a324e78cc8a018.png)
3. On the **Browser bot defense module** page, select the target rule and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/71fec41e3614b4e5a90c35acc4239766.png)
4. In the **Edit allowlist rule** pop-up window, configure parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/bb9800fc0039935f98c126c8e7297992.png)

### Deleting a rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner. In **Global settings**, click **Configure now** in the **Browser bot defense module** section.
![](https://qcloudimg.tencent-cloud.cn/raw/6a150c69b41c0926028dd6972b70ac58.png)
3. On the **Browser bot defense module** page, select the target rule and click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/68c040a34611a5a07c32999404322a34.png)
4. In the pop-up window, click **OK**.