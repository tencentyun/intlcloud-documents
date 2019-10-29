Login protection is an added layer of protection that Tencent Cloud provides when you log in. Users enter a credential for identity verification after the user name and password have been entered correctly.

When login protection is enabled, you must verify your identity every time you log in to the Tencent Cloud website. This prevents others from logging into your account, even if they steal your password.

## Enabling Login Protection
Log in to the Tencent Cloud Console. Go to [Security Settings](https://console.cloud.tencent.com/developer/security).  **Login Protection** can be enabled under **Account Protection Verification**.

## Login Protection Types
Log in to the Tencent Cloud Console. Go to [Security Settings](https://console.cloud.tencent.com/developer/security). Go to **Account Protection Verification** > **Login Protection**, and select from the following accordingly:

| Login Protection Types | Description                                   |
| -------- | ---------------------------------------- |
| Enable WeChat QR code verification | If you did not login via scanning your WeChat QA code, you will be sent to the identity verification page and will need to scan a QR code with WeChat to confirm your identity. The WeChat account used to scan the code must be the same as the WeChat account associated with your Tencent Cloud account. Otherwise, you cannot log in. |
| Enable multi-factor authentication (MFA)  | After logging in with your username and password, you will be sent to the MFA verification page where you will need to enter the correct MFA password to log in to your account. |
| Enable SMS verification  | After logging in with your username and password, you will be sent to the SMS verification page. Click to receive the verification code on your phone and enter it correctly to log in to your account. |
| Do not enable | Secondary verification is not required.                            |
