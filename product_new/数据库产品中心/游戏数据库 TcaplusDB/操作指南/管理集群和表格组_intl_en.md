
This document describes how to manage a TcaplusDB cluster or table group. For more information on how to create a cluster or table group, see [Creating Cluster](https://intl.cloud.tencent.com/document/product/1016/32714) or [Creating a Table Group](https://intl.cloud.tencent.com/document/product/1016/32716).

## Managing a Cluster
### Renaming a cluster
1. On the [Table Group](https://console.cloud.tencent.com/tcaplusdb/app) page, click a cluster ID to enter the cluster details page.
2. Click the "Modify" icon to the right of the **Cluster Name**. The new cluster name should be unique under the account.
![](https://main.qcloudimg.com/raw/6e962819e86afe233d9c481e4f7bb4e4.png)

### Changing cluster connection password
#### Changing connection password
1. Click **Change Password**, enter the old password and new password and confirm the new password in the pop-up dialog box, and click **Confirm**.
> For **Defer Change**, you need to select **Update password** and the expiration time of the old password.
>
![](https://main.qcloudimg.com/raw/924f7779a0cc8680f3ab3e7021537393.png)
2. Once the request is successfully submitted, the expiration time of the old password will be displayed on the cluster details page, before which the old password will remain valid and you cannot submit another request to update the password.
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
2. Return to the cluster details page and you will see that the expiration time of the old password has been updated.
> After the expiration time, the old password will expire, and you can submit a new request to update the password.

### Terminating a cluster
> A cluster cannot be recovered once terminated, so please operate with caution.
>
In the cluster list, click **Terminate** to terminate a cluster. If there is a table group in it, then it cannot be terminated.
![](https://main.qcloudimg.com/raw/5ec45ba252c6ab8f96191ebefb5f3e9c.png)

## Managing a Table Group
### Renaming a table group
In the table group list, click **Modify** in the "Operation" column to change the name of a table group. Its name should be unique under the cluster.
![](https://main.qcloudimg.com/raw/6ced0ca63b18b4f569321a7d9d7627d2.png)

### Terminating a table group
> A table group cannot be recovered once terminated, so please operate with caution.
>
In the table group list, click **Terminate** in the "Operation" column to destroy a table group. If there is a table in it that is in a normal state or in the recycle bin, it cannot be terminated.
![](https://main.qcloudimg.com/raw/d4397bc74149092495c083087cd7acc7.png)

