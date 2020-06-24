## Overview

If you forget your CVM instance login password, you can reset it on the Console. This document describes how to reset your instance login password on the Console.
> 
> - You can only reset your instance login password when the instance status is “Shut down”.
> - Running instances will be shutdown when you reset their login passwords on the Console. To avoid service interruptions and data losses, please plan ahead and reset passwords during off-peak hours.

## Directions

### Resetting the password of a single instance

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, select the desired CVM instance and click **More** -> **Password/key** -> **Reset Password**, as shown in the following figure:
![Reset password](https://main.qcloudimg.com/raw/48b4403fe0ba2b8182915cb2d94a88f2.png)
3. Instances in different statuses have different steps for resetting passwords. Therefore, select one of the following set of steps based on the status of the instance:
 - If you need to reset the password of a **Running** instance:
    1. Select a **Username** type and enter the desired username. Enter the **New password** and re-enter the new password in the **Confirm password** field. Then, click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/293d27f27b37defa9f6f7cd07f921dc6.png)
    2. Select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
    ![Reset Password](https://main.qcloudimg.com/raw/7fb5cbfca86cbaf9fd4cec3c15c6d86e.png)
 - If the instance is **Shut down**, select the **Username** type and enter the desired username. Enter the **New password** and re-enter the new password in the **Confirm password** field. Click **Reset Password** to complete the process, as shown in the following figure:
![](https://main.qcloudimg.com/raw/17579c2803867472f283a4afb0d824c5.png)

### Resetting instance passwords in batches

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, select the desired CVM instances and click **Reset Password** at the top of the instance list, as shown in the following figure:
![Batch reset password](https://main.qcloudimg.com/raw/a1f607f2f0383c9eab2cbfa800bb15be.png)
3. Instances in different statuses have different steps for resetting passwords. Therefore, select one of the following set of steps based on the statuses of the instances:
 - If the selected instances include a **Running** instance:
    1. Select a **Username** type and enter the desired username. Enter the **New password** and re-enter the new password in the **Confirm password** field. Then, click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5fc5e0a1bde21458fe6f77d91ba8ec6e.png)
    2. Select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
    ![Reset Password](https://main.qcloudimg.com/raw/ab3e094af0f2ea68d0841bba98d5802a.png)
 - If all of the selected instances are **Shut down**, select a **Username** type and enter the desired username. Enter the **New password** and re-enter the new password in the **Confirm password** field. Then, click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/17579c2803867472f283a4afb0d824c5.png)

