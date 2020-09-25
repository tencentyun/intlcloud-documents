## Overview
The Cloud Access Management (CAM) role is a virtual identity with a collection of permissions. It is used to grant the permissions to access services and resources and perform operations in Tencent Cloud to the role entity. This document describes how to bind, modify, and delete a role.


## Notes
CVM only allows the role entity that contains `cvm.qcloud.com` to assume the role, as shown below. For more information, see [Concepts](https://intl.cloud.tencent.com/document/product/598/19421).
![](https://main.qcloudimg.com/raw/e47a9bc5103e3c1f342e009429e44c3a.png)


## Directions

### Binding/modifying one role
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and click **Instances** in the left sidebar.
2. On the **Instances** page, locate the CVM instance for which you want to bind or modify the role, click **More** -> **Instance Settings** -> **Bind/Modify a Role**.
3. In the pop-up window, select the role you want to bind, and click **OK**.


### Batch binding/modifying roles
1. On the **Instances** page, select the CVM instances for which you want to bind or modify the roles, click **More Actions** -> **Instance Settings** -> **Bind/Modify a Role** at the top of list.
2. In the pop-up window, select the role you want to bind, and click **OK**.
>?The CVMs using this method to modify roles will have the same role name.

### Deleting one role
1. On the **Instances** page, locate the CVM instance for which you want to delete the role, click **More** -> **Instance Settings** -> **Delete a Role**.
2. Click **OK** in the pop-up window.

### Batch deleting roles
1. On the **Instances** page, select the CVM instances for which you want to delete the roles, click **More Actions** -> **Instance Settings** -> **Delete a Role** at the top of list.
2. Click **OK** in the pop-up window.
