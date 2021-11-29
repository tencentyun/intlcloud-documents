## Feature Overview
This feature allows you to manage (e.g., add, edit, or delete) users in an EMR cluster easily. New users can submit Hadoop cluster tasks.

>!
>- User management is available only for EMR-v2.6.0 and EMR-v3.2.1 and above.
>- You need to manually trigger the delivery of configuration for ranger-ugsync-site.xml and restart the RangerUsersync service for user configurations to take effect.
>- Deleting users and resetting passwords may cause a running task to fail.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of a cluster in the cluster list to enter the cluster details page.
2. Click **User Management**. On the displayed page, you can add and delete users in batches, reset passwords, and download keytabs.
 ![](https://qcloudimg.tencent-cloud.cn/raw/453da7c1b4d028a425d4f57f4c9204a6.png)
3. Click **Create User** to create a user. **Username**, **User Group**, and **Password** are required and **Remarks** is optional.
 ![](https://qcloudimg.tencent-cloud.cn/raw/8c8235f44b0937bee06b25ace837b745.png)
4. Manually trigger the delivery of configuration for ranger-ugsync-site.xml and restart the service.
 - Log in to the [EMR console](https://console.cloud.tencent.com/emr), select the target cluster in the cluster list, and click **Cluster Service** to enter the cluster service list.
 - Select **Operation > Configuration Management** in the upper-right corner of the Ranger service panel.
 - On the **Configuration Management** page, select the ranger-ugsync-site.xml configuration file, click **Modify Configuration** and make no modification. Then, click **Save Configuration** below, and select **Save and Deliver** in the pop-up window.
 - Return to the **Role Management** page, select the RangerUsersync service and click **Restart Service**.
5. Reset a password.
On the user management page, find the user whose password needs to be changed and click **Reset Password** on the right. Enter the new password and confirm, and click **Confirm**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/2e23f5a5a637bf25073b0fc414c2319c.png)
6. Download a keytab.
On the user management page, find the user for whom you want to download the keytab and click **Download Keytab**. The keytab can be used to log in to the cluster.
 ![](https://qcloudimg.tencent-cloud.cn/raw/833f681ae7ad1c40da6fd8c79084e24f.png)
>! Keytab downloading is available only for Kerberos clusters.
>
7. Delete a user.
On the user management page, find the user to be deleted and click **Delete** on the right. Then click **Delete**.
![](C:\Users\v_vwslwu\AppData\Roaming\Typora\typora-user-images\image-20211129151756297.png)
