The server needs to call the ticket verification API to verify the client verification result. 

>! If ticket verification is not integrated, the black market can easily forge verification results, which defeats the purpose of human verification via CAPTCHAs.

## Integration steps
### Step 1. Install the SDK in the corresponding language.
Tencent Cloud provides SDKs in multiple languages. You can install the SDK in any of the languages based on your business needs. For more information, please see [SDK Center](https://intl.cloud.tencent.com/document/product/494).

### Step 2. Obtain the TencentCloud API key.
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) and select **Access Key** -> **API Key Management** on the left navigation pane.
2. On the API key management page, if the key has been created, you can view it on this page; if the key has not been created, click **Create Key** to generate the required key.
![](https://qcloudimg.tencent-cloud.cn/raw/079738d642a10cda2f5d6a72633080e4.png)

### Step 3. Call the `DescribeCaptchaResult` API.
It is recommended to use [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=captcha&Version=2019-07-22&Action=DescribeCaptchaResult&SignVersion=) to generate code online. For more information about the API, please see [Verify CAPTCHA Ticket Result (Web and App)](https://intl.cloud.tencent.com/document/product/1159/49682).
## FAQs
For more information, please see [Integration FAQs](https://intl.cloud.tencent.com/document/product/1159/49692).
