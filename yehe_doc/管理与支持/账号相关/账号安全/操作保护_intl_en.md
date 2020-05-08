Operation protection is an additional layer of protection that Tencent Cloud provides for sensitive operations. After operation protection is enabled, you will need to complete identity authentication before performing sensitive operations.

A verification code is often used for secondary confirmation when you perform sensitive operations in the console.

## Enabling Operation Protection
1. Log in to the Tencent Cloud Console and go to [Security Settings](https://console.cloud.tencent.com/developer/security) page. Click the edit icon next to **Operation Protection** to enable it.
![](https://main.qcloudimg.com/raw/a83e15686213f265025e41fcd4889ca3.png)
2. Complete the identity authentication as prompted.
3. You will be able to enable **Operation Protection** after you pass the identity authentication.

## Operation Protection Types
Log in to the Tencent Cloud Console and go to [Security Settings](https://console.cloud.tencent.com/developer/security). Go to **Account Protection Verification** > **Operation Protection**, and select from the following accordingly:

| Operation Protection Type | Description                                   |
| -------- | ---------------------------------------- |
| Enable MFA | To perform an operation in the console, you must enter the correct MFA password on the identity authentication page; otherwise, the operation cannot be performed. |
| Enable SMS verification | To perform an operation in the console, you must enter the verification code received on your phone on the identity authentication page; otherwise, the operation cannot be performed. |
| Do not enable | Secondary verification will not be required.                            |
