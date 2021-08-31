## Operation Scenarios
This document describes how to view the API key information of the currently logged-in account.
## Prerequisites
Enter the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console.
## Directions
Root accounts and sub-accounts who have the permissions of the **`QcloudCollApiKeyReadOnlyAccess` policy** can view and copy the `SecretId` and `SecretKey` information of the API key of the current account. They can use the `SecretId` and `SecretKey` to use APIs, SDKs, or other development tools to manage resources under the root account within the scope of the configured permissions.
1. Enter the [API Key Management](https://console.cloud.tencent.com/cam/capi) page. You can directly view and copy the `SecretId` in the "Key Pair" column.
2. Click **Show** in the "Key Pair" column. You will be able to get and copy the `SecretKey` after completing identity verification.

>If your sub-account needs self-service management of API keys, please grant it permission of the **QcloudCollApiKeyManageAccess policy**.

## Related Documents
For more information on how to log in as a root account, please see [Logging in to Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/36004).
For more information on how to log in as a collaborator, please see [Logging in as Collaborator](https://intl.cloud.tencent.com/document/product/598/32659).
For more information on how to log in as a sub-user, please see [Logging in as Sub-user](https://intl.cloud.tencent.com/document/product/598/34006).
For more information on how to grant sub-account permissions, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
For more information on how to manage access keys of sub-accounts, please see [Sub-account Access Key Management](https://intl.cloud.tencent.com/document/product/598/32675).
