## Overview

When creating shipping to COS/CKafka tasks, you need to grant the CLS service role the permissions to access COS/CKafka. If you perform operations in the console, the system will guide you through the authorization process. If you directly call APIs, manual authorization will be required. Before manual authorization, check whether the CLS service role has been authorized in the following steps.

## Checking CLS Authorization

1. Log in to the CAM console, and select **[Role](https://console.cloud.tencent.com/cam/role)** on the left sidebar.
2. On the **Role** page, check whether you have the `CLS_QcsRole` role. You can use the search box in the top-right corner of the role list to search for the role.
3. Click the role name to go to the role details page.
 - Select the **Permission** tab to see if the role has the `QcloudCOSAccessForCLSRole` and `QcloudCKAFKAAccessForCLSRole` permissions.
 - Select the **Role Entity** tab to see whether the role entity is `cls.cloud.tencent.com`.
If there is no such role or permission, create one as instructed below.

## Directions

### Granting CLS access permissions

You can use either of the following methods to grant CLS the permissions to ship logs to COS/CKafka:

<dx-tabs>
::: Automatic Creation via CLS Console
If this is the first time you create a task to ship logs to COS/CKafka in the CLS console, follow the instructions in the console to create the required role and policies:
1. In the pop-up window that reads **This feature requires creating a service role**, click **Go to Cloud Access Management**.
2. On the **Role Management** page, click **Grant**.
:::
::: Manual Creation via CAM Console
1. Log in to the CAM console, and select **[Role](https://console.cloud.tencent.com/cam/role)** on the left sidebar.
2. On the **Role** page, click **Create Role**.
3. In the **Select role entity** dialog box, click **Tencent Cloud Product Service**.
4. On the **Create Custom Role** page, perform the following operations:
 1. In the **Enter role entity info** step, select **Cloud Log Service (cls)** and click **Next**.
 2. In the **Configure Role Policy** step, use `clsrole` to search for data, select the `QcloudCKAFKAAccessForCLSRole` and `QcloudCOSAccessForCLSRole` policies in the search result, and click **Next**.
 3. In the **Review** step, enter the role name `CLS_QcsRole` and click **Complete**.

:::
</dx-tabs>

At this point, you have authorized the CLS service role to access COS/CKafka. If you are using a root account, you can directly ship logs. If you are using a sub-account or collaborator account, you need to be authorized by the root account. For more information on granting permissions, see [CAM Access Management](https://intl.cloud.tencent.com/document/product/614/32854). For more information on copying authorization policies, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).




