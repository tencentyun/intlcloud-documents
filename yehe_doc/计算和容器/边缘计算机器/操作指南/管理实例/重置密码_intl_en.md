## Overview

This document describes how to reset your instance login password in the ECM console.

## Notes
- The server will be shut down during password reset. Schedule the time in advance to avoid data loss. We recommend you perform the operation during off-peak hours to minimize the impact.
- Requirements of the new password for Linux instance: the password must contain 8–30 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols and cannot start with "/".
- Requirements of the new password for Windows instance: the password must contain 12–30 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols and cannot start with "/" or contain the username.

## Directions

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview).
2. On the left sidebar, select **Instance List**.
3. On the instance list page, select the target instance and click **More** > **Reset Password**.
![](https://main.qcloudimg.com/raw/57e03c1e0d2745534ee1513b3d4bb6c5.png)
4. In the pop-up window, confirm the username for which you want to reset the password (for example, the username is `root` in a Linux instance and is `Administrator` in a Windows instance), enter the new password in **New Password** and **Confirm Password**, and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/0d07a69d2aae080c34dde6170bd974cc.png)
5. Select **Agree to a forced shutdown** and click **Reset Password** as shown below:
![](https://main.qcloudimg.com/raw/cb85dfa6ef987bbae382a29ea1e51926.png)


