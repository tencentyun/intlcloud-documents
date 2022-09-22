## FAQs about use limits

### What is the QPS limit for TenDI Captcha? What is the business impact when the limit is exceeded? Can the limit be changed?

1. **Queries Per Second** (QPS) is limited to 1,000 for ticket verification.
2. When QPS exceeds 1,000 for the ticket verification API calls, **an error is returned** (RequestLimitExceeded).
3. To change the limit, submit a ticket or contact us.

## FAQs about features

### How does TenDI Captcha block unusual requests?

During the verification, ten security protection mechanisms are used to defend against malicious activities of the black market. For more information, please see "Multi-dimensional defense" in [Overview](https://intl.cloud.tencent.com/document/product/1159/49674).

### Why can't TenDI Captcha effectively block unusual requests?

If you want to block more malicious requests from the black market, you can log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical), select the CAPTCHA to configure, and click **Security configuration**. On the CAPTCHA details page, select the **Security configuration** tab, and change the risk control level to "Strict". Then, TenDI Captcha will block unusual verification requests with stricter risk control policies.

### Does TenDI Captcha support multiple languages?

TenDI Captcha supports 23 languages. You can configure the language in the following ways:

1. Log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical), select the CAPTCHA to configure, and click "Appearance configuration". On the CAPTCHA details page, select the **Appearance configuration** tab, and set the prompt language to "Adaptive" (which means the prompt language changes with the browser language).
2. Configure relevant parameters during client integration. For more information, please see [Web Client Integration](https://intl.cloud.tencent.com/document/product/1159/49680).

### Does the prompt language first match the system language or the browser language if it is set as "Adaptive"?
TenDI Captcha matches the browser language first.

### Does TenDI Captcha support private deployment?
TenDI Captcha does not support private deployment.

## FAQs about usage

### Why are users prompted "Too many attempts. Try again later" after they correctly answer the verification questions?
Possible reasons and solutions are as follows:

- The user is in an unusual environment and deemed suspicious by the policies. They can wait for 10-20 minutes or change the network environment and try again.
- The user is malicious or in a malicious environment and is blocked by the policies. TenDI Captcha ensures secure verification using multi-dimensional policy models consisting of user environments, verification history, and device fingerprints.
- Check whether the CaptchaAppId used for the business client integration belongs to a CAPTCHA created by the console. For how to create a valid CaptchaAppId, please see [Operation Guide](https://intl.cloud.tencent.com/document/product/1159/49686).

- If this problem is reported by multiple users, the policies may be too strict. You can log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical), select the CAPTCHA in use, and click **Security configuration**. On the CAPTCHA details page, select the **Security configuration** tab, and change the risk control level to "Experience-Oriented".

### How can I grant permission to sub-accounts to use TenDI Captcha?

1. Log in to the [Cloud Access Management](https://console.cloud.tencent.com/cam/overview) console with your primary account, and click [**Policies**](https://console.cloud.tencent.com/cam/policy) on the left navigation pane to enter the policy management page.
2. Search for the QcloudCaptchaFullAccess policy, click "Associate User/User Group", select the users/user groups to associate in the "Select Users" box, and click **OK**.
