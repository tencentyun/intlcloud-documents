## Sequence diagram of calling Captcha

### Web and app

The sequence diagram of the web and app calling Captcha is as follows:

- Business client: needs to integrate to Captcha to display the verification page on the client.
- Business server: needs to call the ticket verification API to verify the client verification result. 

![](https://qcloudimg.tencent-cloud.cn/raw/6cb8455c3891dc4574fa72144366013d.png)

## Quick integration

### Step 1. Create CAPTCHA and obtain the CAPTCHA key.

1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **Image CAPTCHA** -> **Manage CAPTCHA** on the left navigation pane to go to the Manage CAPTCHA page.
2. Click **Create CAPTCHA** and set parameters such as CAPTCHA name according to your business requirements.
3. Click **OK** to complete the CAPTCHA creation. Then you can view the CAPTCHA key (CaptchaAppId and AppSecretKey) in the CAPTCHA list.

>! After a CAPTCHA is created, you can modify the verification method, risk control level, and appearance style. For more information, please see [Console Operation Guide](https://intl.cloud.tencent.com/document/product/1159/49686).

### Step 2. The client integrates to Captcha and displays the verification page.

You need to dynamically introduce the Captcha JS into the web and app codes. When the business requires behavior verification, it calls and renders the Captcha JS for verification. For more information, please see [Web Integration](https://intl.cloud.tencent.com/document/product/1159/49680) and [App Integration](https://intl.cloud.tencent.com/document/product/1159/49681).

>! TCaptcha-global.js must be loaded dynamically. If you use other methods to avoid dynamic loading, CAPTCHAs cannot be updated and consequently some legitimate requests rather than malicious requests might be blocked.

### Step 3. The server connects to Captcha and calls the ticket verification API to perform a second verification.

The server needs to call the ticket verification API (DescribeCaptchaResult) to verify the client verification result. For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).

>! If ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs.

## More features

The Captcha console also supports the following features:
- **Statistics**: View data such as requests, passed ticket verifications, failed ticket verifications, and ticket verifications.
- **Verification Configuration**: Adjust the configuration of CAPTCHA security, appearance, and others.

For more information, please see [Console Operation Guide](https://intl.cloud.tencent.com/document/product/1159/49686).

## FAQs

For more information, please see [Integration FAQs](https://intl.cloud.tencent.com/document/product/1159/49692).
