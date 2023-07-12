To ship CLS(Cloud Log Service) logs to COS(Cloud Object Storage) or Ckafka, you need to grant CLS the write permission to COS or Ckafka. In other words, you need to grant the unique CLS service role `CLS_QcsRole` the policy permission `QcloudCOSAccessForCLSRole` or `QcloudCKAFKAAccessForCLSRole`. This document describes how to configure the authorization under different use cases.

## Console: Configuring Shipping Task by Collaborator or Sub-account

If you want to use collaborator or sub-account to successfully configure a shipping task on the CLS console, root account needs to grant them the necessary permissions as shown below:

| Permission                                                     | Description                                     | Use Case                                                     |
| :----------------------------------------------------------- | :------------------------------------------- | :----------------------------------------------------------- |
| CLS preset policy: QcloudCLSFullAccess                            | The permission for collaborator or sub-account to operate CLS         | The collaborator or sub-account must be authorized to operate CLS and configure shipping tasks  |
| CAM preset policy: QcloudCamSubaccountsAuthorizeRoleFullAccess    | The permission for collaborator or sub-account to authorize the service role         | When shipping logs to COS or Ckafka, the collaborator or sub-account needs to confirm that the role is authorized with the CLS write permission to COS or Ckafka, i.e, grant the service role `CLS_QcsRole` the policy permission `QcloudCOSAccessForCLSRole` or `QcloudCKAFKAAccessForCLSRole` |
| COS API permission: GetService (or preset policy: QcloudCOSReadOnlyAccess) | The permission for collaborator or sub-account to obtain the COS bucket lists | To configure shipping task to COS on the CLS console, the collaborator or sub-account needs to obtain the COS bucket list, and then selects the destination bucket |
| CKafka API permission: ListInstance, ListTopic (or preset policy:QcloudCkafkaReadOnlyAccess) | The permission for collaborator or sub-account to obtain CKafka resource list | To configure shipping task to Ckafka on the CLS console, the collaborator or sub-account needs to obtain the Ckafka resource list, and then selects the target Ckafka instance topic |

#### Root account authorization

1. Log in to the [CAM](https://console.cloud.tencent.com/cam/overview) console with root account, select **Users** -> **User List** in the left sidebar to enter the **User List** page. Select the target user and enter the details page.
2. In the **Permissions** tab, click **Associate Policy** and select the **Select policies from the policy list** tab.
3. Check the preset policies including QcloudCLSFullAccess, QcloudCamSubaccountsAuthorizeRoleFullAccess, QcloudCOSReadOnlyAccess and QcloudCkafkaReadOnlyAccess for collaborator or sub-account.

#### Configuring shipping task by collaborator or sub-account


>! 
Collaborator or sub-account must be authorized by root account to configure shipping task.

1. Log in to the [CLS](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou) console with collaborator or sub-account and select **Logset** in the left sidebar. Select a target logset to see the log topic list.
2. Click **Go to CAM Console** when prompted for service role authorization for shipping configuration on the **Ship to COS** or **Ship to Ckafka** page.
3. Click **Grant**, and then proceed with shipping configuration.

## API: Configuring Shipping Task

If you want to configure a shipping task via API, grant the CLS service role `CLS_QcsRole` the policy permission `QcloudCOSAccessForCLSRole` or `QcloudCKAFKAAccessForCLSRole`.

#### Authorization steps

1. Log in to the [CAM](https://console.cloud.tencent.com/cam/overview) console and click **Roles** in the left sidebar.
2. Click **Create Role**, select **Tencent Cloud Product Service** as the role entity, and then check **Cloud Log Service** on the **Enter role entity info** page.
3. Associate the role with policies, for example, associate QcloudCOSAccessForCLSRole for shipping to COS, and QcloudCKAFKAAccessForCLSRole for shipping to Ckafka.

#### Configuring shipping task via API



>! The service role must be authorized for CLS log shipping.

Configure the shipping task parameters as instructed in the [Creating Shipping Task](https://intl.cloud.tencent.com/document/product/614/16890) or shipping to Kafka documentation.
