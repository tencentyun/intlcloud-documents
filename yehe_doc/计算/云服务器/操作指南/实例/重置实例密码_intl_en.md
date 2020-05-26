## Use Cases

If you forget your CVM instance login password, you can use the console to reset it. This article describes how to reset your instance login password through the console.
> 
>- You can only reset your instance login password when the instance status is shutdown.
>- Running instances are shutdown when you reset their login passwords through the console, which may cause service interruption and data loss. Plan ahead and perform password resets during off hours to minimize the impact.

## Directions

### Resetting the password of a single instance

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page select the desired CVM instance and click **More** -> **Password/key** -> **Reset Password**, as shown in the following figure:
![Reset password](https://main.qcloudimg.com/raw/48b4403fe0ba2b8182915cb2d94a88f2.png)
3. Instances in different statuses have different steps for resetting passwords. Pick one of the following:
 - If you need to reset the password of a **Running** instance:
    1. Select a **user name type** and enter the desired user name. Enter the **New password** and **Confirm password**. Click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/293d27f27b37defa9f6f7cd07f921dc6.png)
    3. Select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
    ![Reset Password](https://main.qcloudimg.com/raw/7fb5cbfca86cbaf9fd4cec3c15c6d86e.png)
 - If the instance is **Stopped**, select **user name type** and enter the desired user name. Enter **New password** and **Confirm password**. Click **Reset Password** to complete the process, as shown in the following figure:
![](https://main.qcloudimg.com/raw/17579c2803867472f283a4afb0d824c5.png)

### Resetting passwords in batches

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, select desired CVM instances and click **Reset Password** at the top of the instance list. The **Reset Password** page appears.
![Batch reset password](https://main.qcloudimg.com/raw/a1f607f2f0383c9eab2cbfa800bb15be.png)
3. In the “Reset Password” pop-up window, the password reset operation is different for instances with different statuses. Select one of the following:
 - If the selected instances include a **Running** instance:
    1. Select a **user name type** and enter the desired user name. Enter **New password** and **Confirm password** and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5fc5e0a1bde21458fe6f77d91ba8ec6e.png)
    2. Select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
    ![Reset Password](https://main.qcloudimg.com/raw/ab3e094af0f2ea68d0841bba98d5802a.png)
 - If all selected instances are **Stopped**, select a **user name type** and enter the desired user name. Enter **New password** and **Confirm password** and click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/17579c2803867472f283a4afb0d824c5.png)

