To enable CLS to ship logs to Cloud Object Storage (COS) or CKafka, you need to grant CLS the COS or CKafka write permission. That is, you need to grant the `QcloudCOSAccessForCLSRole` or `QcloudCKAFKAAccessForCLSRole` policy permission to the unique service role `CLS_QcsRole` of CLS.

This document describes how to grant collaborators or sub-accounts the permission to configure shipping tasks.



## Granting Permissions in the Console

To enable collaborators or sub-accounts to configure a shipping task in the CLS console, you need to use the root account to grant them the necessary permissions as shown below:

| Permission                                                     | Description                                     | Use Case                                                     |
| ------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------ |
| CLS preset policy: QcloudCLSFullAccess                            | The permission for collaborator or sub-account to operate CLS         | The collaborator or sub-account must be authorized to operate CLS and configure shipping tasks  |
| CAM preset policy: `QcloudCamSubaccountsAuthorizeRoleFullAccess`    | The permission for collaborator or sub-account to authorize the service role         | When shipping logs to COS or CKafka, the collaborator or sub-account needs to confirm that the role is authorized with the CLS write permission to COS or CKafka, i.e., grant the service role `CLS_QcsRole` the policy permission `QcloudCOSAccessForCLSRole` or `QcloudCKAFKAAccessForCLSRole` |
| COS API permission: GetService (or preset policy: `QcloudCOSReadOnlyAccess`) | The permission for collaborator or sub-account to obtain the COS bucket lists | To configure a task for shipping to COS in the CLS console, the collaborator or sub-account needs to obtain the COS bucket list, and then selects the destination bucket |
| CKafka API permission: `ListInstance`, `ListTopic` (or preset policy: `QcloudCkafkaReadOnlyAccess`) | The permission for collaborator or sub-account to obtain CKafka resource list | To configure a task for shipping to CKafka in the CLS console, the collaborator or sub-account needs to obtain the CKafka resource list, and then selects the target CKafka instance topic |

### Authorization by root account

1. Log in to the CAM console with the root account and choose **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the **User List** page, click the target username to go to the user details page.
3. On the user details page, select **Associate Policy**.
4. In the **User Permissions** step on the **Add Policy** page, click **Select policies from the policy list**.

5. Select the preset policies, including `QcloudCLSFullAccess`, `QcloudCamSubaccountsAuthorizeRoleFullAccess`, `QcloudCOSReadOnlyAccess`, or `QcloudCkafkaReadOnlyAccess`, for the collaborator or sub-account.
<dx-alert infotype="notice" title="">
The root account must complete the authorization process. Otherwise, the collaborator or sub-account cannot configure shipping tasks properly.
</dx-alert>
6. Click **Next**.
7. Confirm the configuration in the **Review** step and click **OK**.




