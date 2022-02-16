## Operation Scenarios
This document describes how to change a cluster's connection password in the TcaplusDB Console and update the expiration time of the old password.

## Prerequisites
You have created a cluster and a table group. For more information, please see [Creating Cluster](https://intl.cloud.tencent.com/document/product/1016/32714) and [Creating Table Group](https://intl.cloud.tencent.com/document/product/1016/32716).

## Directions
### Changing connection password
1. Enter the [Cluster List](https://console.cloud.tencent.com/tcaplusdb/app) page, click **Change Password** in "Connection Password" of the cluster, enter the old password and new password, confirm the new password in the pop-up dialog box, and click **Confirm**.
>For "Defer Change", you need to select **Update password** and the expiration time of the old password.
>
![](https://main.qcloudimg.com/raw/7aab39aa33e2e461e0a2e87b07abeeb6.png)
2. Once the request is successfully submitted, the expiration time of the old password will be displayed on the cluster details page, before which the old password will remain valid and you cannot submit another request to update the password.

### Updating old password expiration time
>Before the old password expires, you can update its expiration time to shorten or extend the period before replacing it.

1. Enter the [Cluster List](https://console.cloud.tencent.com/tcaplusdb/app) page, click **Change Password** in "Connection Password" of the cluster, modify the expiration time in the pop-up dialog box, and click **Confirm**.
 - **Old Password**: old password that will expire, i.e., the old password you entered when you changed the connection password.
 - **New Password**: new password that has not taken effect yet, i.e., the new password you entered when you changed the connection password.
 - **Defer Change**: select **Update old password expiration time**.
 - **Old Password Expiration Time**: select a new expiration time.
![](https://main.qcloudimg.com/raw/f603e4184231af909e48129d6cce56d4.png)
2. Return to the cluster details page and you will see that the expiration time of the old password has been updated.
>After the expiration time, the old password will expire, and you can submit a new request to update the password.
