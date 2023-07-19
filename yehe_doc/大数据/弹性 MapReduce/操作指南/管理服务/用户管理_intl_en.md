## Overview
This feature allows you to manage (add, edit, or delete) users in an EMR cluster easily. New users can submit Hadoop cluster tasks.
>!
>- User management is available only for EMR-v2.6.0 and EMR-v3.2.1 and above.
>- You need to manually trigger the delivery of configurations in `ranger-ugsync-site.xml` and restart the EnableUnixAuth service to sync user configurations.
>- Deleting users and resetting passwords may cause a running task to fail.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of a cluster in the cluster list to enter the cluster details page.
2. Click **Users**. On the displayed page, you can add and delete users in batches, reset passwords, and download keytabs.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/zKQD179_%E5%9B%BD%E9%99%8553.png)
3. Click **Create user** to create a user. **Username**, **User group**, and **Password** are required and **Remarks** is optional.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3n9T621_%E5%9B%BD%E9%99%8554.png)
4. Manually trigger the delivery of configuration for ranger-ugsync-site.xml and restart the service.
 - Log in to the [EMR console](https://console.cloud.tencent.com/emr), select the target cluster in the cluster list, and click **Cluster services* to enter the cluster service list.
 - Select **Operation > Configurations** in the upper-right corner of the Ranger service panel.
 - On the **Configurations** page, select `ranger-ugsync-site.xml`, click **Edit configuration** and make no modification. Then, click **Save configuration** below, and select **Save and deliver** in the pop-up window.
 - Return to the **Roles** page, select the EnableUnixAuth service, and click **Restart service**.
5. Reset a password.
On the user management page, find the user whose password needs to be changed and click **Reset password** on the right. Enter the new password and confirm, and click **Confirm**.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/TQtD344_%E5%9B%BD%E9%99%8555.png)
6. Download a keytab.
On the user management page, find the user for whom you want to download the keytab and click **Download keytab**. The keytab can be used to log in to the cluster.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ieg3481_%E5%9B%BD%E9%99%8556.png)
>! Keytab downloading is available only for Kerberos clusters.
>
7. Delete a user.
On the user management page, find the user to be deleted and click **Delete** on the right. Then click **Delete**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WzDx466_%E5%9B%BD%E9%99%8557.png)
