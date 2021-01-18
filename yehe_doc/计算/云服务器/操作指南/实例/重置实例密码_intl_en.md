## Overview

If you forget your CVM instance login password, you can reset it on the console. This document describes how to reset your instance login password on the console.
>! 
> - You can only reset the login passwords of shutdown instances.
> - Running instances will be shut down when you reset their login passwords on the console. To avoid service interruptions and data losses, please plan ahead and reset passwords during off-peak hours.



## Directions

### Resetting the password of a single instance

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the desired CVM instance and click **More** > **Password/Key** > **Reset Password**, as shown in the following figure:
![Reset password](https://main.qcloudimg.com/raw/48b4403fe0ba2b8182915cb2d94a88f2.png)
3. Instances in different statuses have different steps for resetting passwords. Therefore, select one of the following set of steps based on the status of the instance:
 - If you need to reset the password of a **Running** instance:
    1. Select **Username** and enter the username of the selected instance. Enter the **New password**, re-enter the new password in the **Confirm Password** field, and click **Next**.
    2. Select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7fb5cbfca86cbaf9fd4cec3c15c6d86e.png)
 - If you need to reset the password of a **Shutdown** instance:
    1. Select **Username** and enter the username of the selected instance. Enter the **New password**, re-enter the new password in the **Confirm Password** field, and click **Next**.
    2. Click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/17579c2803867472f283a4afb0d824c5.png)    

### Resetting instance passwords in batches

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the CVM instances to reset password, and click **Reset Password** at the top of the instance list, as shown in the following figure:
![Batch reset password](https://main.qcloudimg.com/raw/a1f607f2f0383c9eab2cbfa800bb15be.png)
3. Instances in different statuses have different steps for resetting passwords. Therefore, select one of the following set of steps based on the status of the instance:
 - If you need to reset the password of a **Running** instance:
    1. Select **Username** and enter the username of the selected instance. Enter the **New password**, re-enter the new password in the **Confirm Password** field, and click **Next**.
    2. Select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/ab3e094af0f2ea68d0841bba98d5802a.png)
 - If you need to reset the password of a **Shutdown** instance:
    1. Select **Username** and enter the username of the selected instance. Enter the **New password**, re-enter the new password in the **Confirm Password** field, and click **Next**.
    2. Click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/17579c2803867472f283a4afb0d824c5.png)    
