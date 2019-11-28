## Introduction
This document describes how to create, enable/disable, and delete sub-users and collaborators API keys, and how to view the API key information.
## Prerequisites
Log in to the CAM console and go to the [User List](https://console.cloud.tencent.com/cam) page. Find the sub-user or collaborator that needs to be configured, and click the **User Name** to go to **User Details**.
## Directions

### Creating an API Key
You can create an API key for sub-users and collaborators. After creating the API key, the sub-user or collaborator can use API, SDK or other developer tools to manage the resources under the root account to the extent allowed by the configured permissions.
1. In the **User Details** page, click **API Key** to go to the **API Key Management** page.
2. In the **API Key Management** page, click **Create Key** and complete the API key creation operations.
 >
 > - Each sub-user/collaborator can have at most two API keys.
 > - An API key is an important credential for creating TencentCloud API requests. To keep your assets and services secure, save your keys appropriately and change them regularly. Delete old keys when new ones are created.
 
### Viewing Sub-User/Collaborator API Keys
You can view and copy the SecretId and SecretKey information of the API keys of sub-users and collaborators. Sub-users/collaborators can use the SecretId and SecretKey to use APIs, SDKs, or another developer tools to manage resources under the primary account to the extent allowed by the configured permissions.
1. In the **User Details** page, click **API Key** to go to the **API Key Management** page.
2. In the **API Key Management** page, perform the following operations to view and copy the SecretId and SecretKey information of the API key. An API key is an important credential for creating Tencent Cloud API requests. To keep your assets and services secure, save your keys appropriately and change them regularly. Delete old keys when new ones are created.
 > - SecretId: This can be directly viewed in the **Key** column. Click ![](https://main.qcloudimg.com/raw/f76547dfc5a0b8982a714011026f3244.png) to copy and save.
 > - SecretKey: Click **Show** under the **Key** column. You will be able to view this after completing identity verification. Click ![](https://main.qcloudimg.com/raw/f76547dfc5a0b8982a714011026f3244.png) to copy and save.

### Viewing the API Keys of the Current Account
Users who have the **QcloudCollApiKeyReadOnlyAccess Policy** permissions can view and copy the SecretId and SecretKey information of the API key of the current account. They can use the SecretId and SecretKey to use APIs, SDKs, or another developer tools to manage resources under the root account to the extent allowed by the configured permissions.
1. Go to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page. You can view and copy the SecretId from the **Key** column.
2. Click **Show** under the **Key** column. You will be able to obtain and copy the SecretKey after completing identity verification.

### Enabling/Disabling API Keys
You can disable the API keys of sub-users and collaborators. Do note that Tencent Cloud will block all requests that use the API key after it is disabled. 
1. In the **User Details** page, click **API Key** to go to the **API Key Management** page.
2. In the **API Key Management** page, click **Disable** in the **Operations** column.
3. In the confirmation window that pops up, click **Confirm* to disable the access key.
>Click **Enable** in the **Operations** column to enable the key. After the key is enabled, the sub-user/collaborator can manage the resources of the root account by using APIs, SDKs or other developer tools.

### Deleting API Keys
1. In the **User Details** page, click **API Key** to go to the **API Key Management** page.
2. In the **API Key Management** page, click **Disable** in the operations column. If the API key that you want to delete has already been disabled, go straight to Step 4.
3. In the confirmation box that pops up, click **Confirm**.
4. In the API Key Management page, click **Delete** in the operations list to delete the API key.
> Please note that an API key that has been deleted cannot be retrieved. 

