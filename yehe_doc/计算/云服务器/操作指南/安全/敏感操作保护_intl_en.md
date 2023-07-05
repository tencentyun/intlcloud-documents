## Overview
The sensitive operation protection feature is currently available in CVM. Once the feature is enabled, identity verification needs to be completed before performing sensitive operations.
This feature can effectively protect the security of account resources, including shutdown, restart, VNC login, password reset, instance termination, system reinstallation, configuration adjustment, key load and VPC switch.

## Enabling Operation Protection
You can enable the operation protection feature in [Security Settings](https://console.cloud.tencent.com/developer/security) console. For more information, see [Operation Protection](https://intl.cloud.tencent.com/document/product/378/10740).

## Verifying Operation Protection
Once operation protection is enabled, you need to complete identity verification before you can perform a sensitive operation:
- If you have enabled **MFA verification** for operation protection, you need to enter the 6-digit dynamic verification code displayed on the MFA device.
- If you have enabled **SMS code verification** for operation protection, you need to enter the verification code received on your phone.



