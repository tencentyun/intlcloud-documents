This document describes the configuration for login with a password.

> Requirements for passwords:
> - For a Linux CVM, the password must be 8 to 30 characters in length; password with more than 12 characters is recommended. It cannot begin with "/", and must contain at least one character from three of the following categories, uppercase letter (A-Z), lowercase letter (a-z), digit (0-9), and special character (()`~!@#$%^&*-+=_|{}[]:;'<>,.?/).
> - For a Windows CVM, the password must be 12 to 30 characters in length. It cannot begin with "/", and must contain at least one character from three of the following categories, uppercase letter (A-Z), lowercase letter (a-z), digit (0-9), and special character (()`~!@#$%^&*-+=_|{}[]:;'<>,.?/). The password cannot contain your username.

## Setting initial password

> 
> - If you select **Random Password**, you will receive an auto-generated initial password through email and [Internal Message](https://console.cloud.tencent.com/message).
> - If you select **Set Password**, the initial password will be the one defined by yourself.

1. If you select to customize the configuration of a CVM, you will be able to choose a login method. **Set Password** will be selected by default.
2. Enter a password according to the password requirements and confirm it. Go to next step to confirm all your configuration and enable the CVM. The initial password will be set successfully. Please wait for the CVM instance to be assigned.

## Viewing Password

An auto-generated password will be sent to your email and [Internal Message](https://console.cloud.tencent.com/message). Click the corresponding message to view the initial password.
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/), and click the envelope icon in the upper right corner to go to [Internal Message](https://console.cloud.tencent.com/message).
  ![](https://main.qcloudimg.com/raw/648d5ea37b192bc1eb384878a79c2453.png)

## Resetting Password

> You can only reset the password of a CVM when it is shut down. If you reset the password while a CVM is running, a forced shutdown may result in data loss or file system corruption.

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Shut down the CVM whose password you want to reset.
3. Open the password resetting box.
  - If you want to reset the password of a single shut-down instance, click **More** > **Password/Key** > **Reset Password** in the Operation column on the right.
  - If you want to reset the passwords of multiple instances all at once, select all the CVMs whose passwords you want to reset, and click **Reset Password** at the top of the list to modify their login passwords all at the same time. If the passwords of some instances cannot be reset, the reasons will be displayed.
4. Enter a new password in the Reset Password pop-up box, confirm the password, and click “Next”.
5. After the password is reset successfully, you will receive a confirmation message via [Internal Message](https://console.cloud.tencent.com/message), and then you can use the new password to log in to the CVM.
