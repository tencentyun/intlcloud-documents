## Overview
A Cloud Access Management (CAM) role is a virtual identity with a collection of permissions. It is used to grant the role entity the permissions to access services and resources and perform operations in Tencent Cloud. You can associate the CAM role with a CVM instance to call other Tencent Cloud APIs from the instance using the periodically updated temporary Security Token Service (STS) key. This ensures the security of your SecretKey and helps you implement refined permission control, avoiding the security risks from using persistent keys.

This document describes how to bind, modify, and delete a role.

## Advantages
Binding a CAM role to instances comes with the following features and advantages.
- You can access other Tencent Cloud services using STS temporary keys. For more information, see [STS APIs](https://intl.cloud.tencent.com/document/product/598/35840).
- You can grant roles associated with different access policies to instances so that the instances are given different access permissions to Tencent Cloud resources, which helps you implement refined permission control.
- You don’t need to save SecretKey in an instance. Instead, you can easily control the access permissions of the instance by changing the role authorization.




## Use Instructions
- The instance only allows the role entity that contains `cvm.qcloud.com` to assume the role. For more information, see [Concepts](https://intl.cloud.tencent.com/document/product/598/19421).
- The instance must reside in a VPC.
- An instance can only bind one CAM role at a time.
- You can bind, modify or delete a role without paying extra fees.


## Directions

### Binding/modifying roles
#### Binding/modifying the role of one CVM
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and click **Instances** on the left sidebar.
2. On the **Instances** page, select the CVM instance for which you want to bind or modify the role, and then click **More** > **Instance Settings** > **Bind/Modify a Role** under the **Operation** column, as shown below.
![](https://main.qcloudimg.com/raw/34d5a9866aa28fdb8a3363884918e3bb.png)
3. In the pop-up window, select the role you want to bind, and click **OK**.
#### Batch binding/modifying roles
1. On the **Instances** page, select the CVM instances for which you want to bind or modify the roles, click **More Actions** > **Instance Settings** > **Bind/Modify a Role** at the top of list, as shown below.
![](https://main.qcloudimg.com/raw/4093443ee4f5b484860f8c8eae3b3b3e.png)
2. In the pop-up window, select the role you want to bind, and click **OK**.
>?CVMs modified using this method will have the same role name.



### Deleting roles
#### Deleting the role of one CVM
1. On the **Instances** page, locate the CVM instance for which you want to delete the role, click **More** > **Instance Settings** > **Delete a Role** under the **Operation** column, as shown below.
![](https://main.qcloudimg.com/raw/8b44772763ab60fa69c404360db1ebbf.png)
2. Click **OK** in the pop-up window.
#### Batch deleting roles
1. On the **Instances** page, select the CVM instances for which you want to delete the roles, click **More Actions** > **Instance Settings** > **Delete a Role** above the list, as shown below.
![](https://main.qcloudimg.com/raw/72669a0d3bbdde1491c24b5acc0eadbf.png)
2. Click **OK** in the pop-up window.



