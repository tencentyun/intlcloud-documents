## Overview
When creating a task for shipping logs to COS/CKafka, perform authorization in a corresponding way:
 - **Via CLS console**: Configure permissions according to the permission process provided in the console.
 - **Via API call**: Manually create the permissions to ship logs to COS/CKafka.
 <dx-alert infotype="notice" title="">
If you do not configure the required permissions before making an API call, log shipping will fail. Check and configure the required permissions by referring to this document.
</dx-alert>

This document describes how to check if you have the permissions to ship logs to COS/CKafka and how to create a log shipping task. If you do not have the permissions, create a log shipping task before configuring the permissions.


## Directions

### Checking whether you have the permissions to ship logs to COS/CKafka
1. Log in to the CAM console, and select **[Roles](https://console.cloud.tencent.com/cam/role)** on the left sidebar.
2. On the **Role** page, check whether you have the `CLS_QcsRole` role. You can use the search box in the top-right corner of the role list to search for the role.
![](https://qcloudimg.tencent-cloud.cn/raw/2e8a355e5901c8ece21e0f25c75af35e.png)
3. Click the role name to go to the role details page.
 - Select the **Permission** tab to see if the role has the `QcloudCOSAccessForCLSRole` and `QcloudCKAFKAAccessForCLSRole` permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/26706b34a27f744f88afbd3e6ef93e99.png)
 - Select the **Role Entity** tab to see if the role entity is `cls.cloud.tencent.com`.
![](https://qcloudimg.tencent-cloud.cn/raw/cd1a2aebfd78372764fbb70b52b830f0.png)
After confirming that you have the required role and permissions, you can create a task to ship logs to COS/CKafka. If you do not have the required role or permissions, create them as follows.


### Creating the permissions to ship logs to COS/CKafka

You can use either of the following methods to create the permissions to ship logs to COS/CKafka:

<dx-tabs>
::: Automatic Creation via CLS Console
If this is the first time you create a task to ship logs to COS/CKafka in the CLS console, follow the instructions in the console to create the required role and policies:
1. In the pop-up window that reads **This feature requires creating a service role**, click **Go to Cloud Access Management**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ed26853843fdc9cabc27bfe9bd5dbb98.png" width="70%"/>
2. On the **Role Management** page, click **Grant**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/aade131a6c18c7e93f0f712d6129ceae.png" width="70%"/>
:::
::: Manual Creation via CAM Console
1. Log in to the CAM console, and select **[Roles](https://console.cloud.tencent.com/cam/role)** on the left sidebar.
2. On the **Role** page, click **Create Role**.
3. In the **Select role entity** dialog box, click **Tencent Cloud Product Service**.
4. On the **Create Custom Role** page, perform the following operations:
 1. In the **Enter role entity info** step, select **Cloud Log Service (cls)** and click **Next**.
 2. In the **Configure role policy** step, use `clsrole` to search for data, select the `QcloudCKAFKAAccessForCLSRole` and `QcloudCOSAccessForCLSRole` policies in the search result, and click **Next**.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7b1ea04b0607e62ffc6ed7e21295d279.png)
 3. In the **Review** step, enter the role name `CLS_QcsRole` and click **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/cf1f22f7c3e30b485681da40a82cabe4.png)

:::
</dx-tabs>

Now you have created the permissions to ship logs to COS/CKafka. If you are using the root account, you can perform shipping operations directly. If you need to use a sub-account or collaborator for shipping, use the root account to grant the sub-account or collaborator with related shipping policies by referring to [Shipping Authorization](https://intl.cloud.tencent.com/document/product/614/37888) before performing shipping operations.






