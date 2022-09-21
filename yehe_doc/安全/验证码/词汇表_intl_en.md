### CaptchaAppId

CAPTCHA app ID. This parameter is required to integrate to Captcha. When your business client calls the Captcha service, the Captcha server can obtain the verification type, risk control level, and other parameters configured on the console with CaptchaAppId. CaptchaAppId and AppSecretKey can be found on the CAPTCHA list page in the [Captcha console](https://console.cloud.tencent.com/captcha/graphical).

### SecretKey

SecretId and SecretKey collectively refer to the TencentCloud API key, which is the security credential required for authentication when you access TencentCloud API. SecretKey is used to encrypt signature strings and verify them on the server. You can create multiple TencentCloud API keys for one APPID.

### CAPTCHA ticket

The user verification ticket returned by the callback function after the business client initiates verification. CAPTCHA ticket is required when the business server calls the ticket verification API.
