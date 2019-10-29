Operation protection is an added layer of protection that Tencent Cloud provides when you perform sensitive operations. Once operation protection has been enabled, users will need to complete identity authentication before performing sensitive operations.

A verification code is often used for secondary confirmation when you perform sensitive operations on the console.

## Enabling Operation Protection
Log in to the Tencent Cloud Console. Go to [Security Settings](https://console.cloud.tencent.com/developer/security). **Operation Protection** can be enabled under **Account Protection Verification**.

## Operation Protection Types
Log in to the Tencent Cloud Console. Go to [Security Settings](https://console.cloud.tencent.com/developer/security). Go to **Account Protection Verification** > **Operation Protection**, and select from the following accordingly:

| Operation Protection Types | Description                                   |
| -------- | ---------------------------------------- |
| Enable WeChat QR code verification | To perform an operation in the console, you must use WeChat to scan the QR code and confirm your identity in the identity verification page. The WeChat account used to scan the code must be the same as the account associated with the account. Otherwise, the operation cannot be performed. |
| Enable multi-factor authentication (MFA) | To perform an operation on the console, you must enter the correct MFA password in the identity verification page. Otherwise, the operation cannot be performed. |
| Enable SMS verification | To perform an operation on the console, you must enter the verification code received on your phone in the identity verification page. Otherwise, the operation cannot be performed. |
| Do not enable | Secondary verification is not required.                            |
