### How do I check the fees incurred?

1. Captcha is billed based on the number of ticket verifications initiated by the server. You can log in to the [Captcha console](https://console.cloud.tencent.com/captcha/graphical) and select **CAPTCHA** -> **CAPTCHA Statistics** on the left navigation pane to view the ticket verifications trend.
2. Log in to the console and go to **Cost Center** -> **Bills** -> **Bill Details** to view the details of the generated bills.

### I am already using the Captcha service, why are no fees deducted?
Please check whether the client and server have integrated to the Captcha service as required. After TenDI Captcha is integrated into the business client, the business server needs to verify the CAPTCHA ticket. For more information, please see [Integration to Ticket Verification (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).

>! If ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs.
