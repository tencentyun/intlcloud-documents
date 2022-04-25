## Overview
If you forgot or want to change your password, you can reset it directly in the console.

## Prerequisites
- You have [applied for a TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712).
- The database instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID and enter the **Reset Password** window in any of the following ways:
   - In the **Configuration** section on the **Instance Details** page, click **Reset Password** on the right of **Connection Password**.
   - In the account list on the **Account Management** page, find the **default account** or custom account for which to reset the password, and click **Reset Password** in the **Operation** column.
5. In the **Reset Password** pop-up window, enter the **New Password** and **Confirm Password**. The password:
   - Must contain 8–30 (preferably above 12) characters.
   - Cannot start with a slash (/).
   - Must contain characters in at least two of the following types:
     - Lowercase letters (a–z)
     - Uppercase letters (A–Z)
     - Digits (0–9)
     - `()~!@#$%^&*-+=_|{}[]:;<>,.?/`
6. Click **OK**, and the new password will take effect immediately.

## Related APIs
| API | Description |
| ----------------------- | ------------------------------------------------------------ |
| [ResetPassword](https://intl.cloud.tencent.com/document/product/239/32054) | Resets password |

