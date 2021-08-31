## Operation Scenarios
This document describes how to create, enable/disable, delete, and view an API key for a root account.
## Prerequisites
You have logged in to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console as the [root account](https://intl.cloud.tencent.com/document/product/378/36004).
## Directions

### Creating API key for root account
You can create an API key for a root account. After the API key is created, the root account can use APIs, SDKs, or other development tools to manage the resources under the account.
On the API key management page, click **Create Key** in the top-left corner and complete the API key creation operations.
 >
 > - One root account can have at most two API keys.
 > - The root account API key represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.
 > - An API key is an important credential for creating TencentCloud API requests. For the security of your assets and services, please keep the keys private, change them regularly, and delete old keys promptly after creating new ones.
 
### Viewing root account API key
You can view and copy the `SecretId` and `SecretKey` information of the API key of the root account. You can use the `SecretId` and `SecretKey` to use APIs, SDKs, or other development tools to manage resources under the account.
1. On the API key management page, you can directly copy the `SecretId` in the "Operation" column.
2. Click **Show** in the "Operation" column. You will be able to get and copy the `SecretKey` after completing identity verification.


### Disabling/Enabling root account API key
You can disable the API key of the root account. Do note that Tencent Cloud will block all requests that use the API key after it is disabled.
1. On the API key management page, click **Disable** in the "Operation" column.
2. In the pop-up window, click **Disable* to disable the access key.
>You can click **Enable** in the "Operation" column to enable the key. After the key is enabled, you can use APIs, SDKs, or other development tools to manage the resources under the account.

### Deleting root account API key
1. On the API key management page, click **Disable** in the "Operation" column. If the API key that you want to delete has already been disabled, directly proceed to step 3.
2. In the pop-up window, click **Disable*.
3. On the API key management page, click **Delete** in the "Operation" column.
4. In the pop-up window, click **Delete* to delete the API key.
>Please note that an API key cannot be recovered once deleted.

