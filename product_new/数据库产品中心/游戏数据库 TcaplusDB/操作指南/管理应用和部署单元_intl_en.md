
This document describes how to manage a TcaplusDB application or deployment unit. For more information on how to create an application or deployment unit, see [Creating Application](https://intl.cloud.tencent.com/document/product/1016/32714) or [Creating a Deployment Unit](https://intl.cloud.tencent.com/document/product/1016/32716).

## Managing an Application
### Renaming an application
1. On the [Deployment Unit](https://console.cloud.tencent.com/tcaplusdb/app) page, click an application ID to enter the application details page.
2. Click the "Modify" icon to the right of the **Application Name**. The new application name should be unique under the account.
![](https://main.qcloudimg.com/raw/1d89d9708f1041b08192be67c3718789.png)

### Changing application connection password
#### Changing connection password
1. Click **Change Password**, enter the old password and new password and confirm the new password in the pop-up dialog box, and click **Confirm**.
> For **Defer Change**, you need to select **Update password** and the expiration time of the old password.
>
![](https://main.qcloudimg.com/raw/924f7779a0cc8680f3ab3e7021537393.png)
2. Once the request is successfully submitted, the expiration time of the old password will be displayed on the application details page, before which the old password will remain valid and you cannot submit another request to update the password.
![](https://main.qcloudimg.com/raw/fd3e245776b2fec28294c49938c60465.png)

#### Updating the expiration time of the old password
> Before the old password expires, you can update its expiration time to shorten or extend the period before replacing it.
>
1. Click **Change Password**, modify the expiration time in the pop-up dialog box, and click **Confirm**.
 - **Old Password**: The old password that will expire, i.e., the old password you entered when you changed the connection password.
 - **New Password**: The new password that has not taken effect yet, i.e., the new password you entered when you changed the connection password.
 - **Defer Change**: Select **Update old password expiration time**.
 - **Old Password Expiration Time**: Select the new expiration time.
![](https://main.qcloudimg.com/raw/9a9658e9be1a0a9be09959fd7ac071f2.png)
2. Return to the application details page and you will see that the expiration time of the old password has been updated.
> After the expiration time, the old password will expire, and you can submit a new request to update the password.

### Terminating an application
> An application cannot be recovered once terminated, so please operate with caution.
>
In the application list, click **Terminate** to terminate an application. If there is a deployment unit in it, then it cannot be terminated.
![](https://main.qcloudimg.com/raw/5ec45ba252c6ab8f96191ebefb5f3e9c.png)

## Managing a Deployment Unit
### Renaming a deployment unit
In the deployment unit list, click **Modify** in the "Operation" column to change the name of a deployment unit. Its name should be unique under the application.
![](https://main.qcloudimg.com/raw/da7dfabb9f2d035ea5cab6b4d88d5ff6.png)

### Terminating a deployment unit
> A deployment unit cannot be recovered once terminated, so please operate with caution.
>
In the deployment unit list, click **Terminate** in the "Operation" column to destroy a deployment unit. If there is a table in it that is in a normal state or in the recycle bin, it cannot be terminated.
![](https://main.qcloudimg.com/raw/3613898853b8f8c3398980896efe6155.png)

