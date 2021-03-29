## Overview

This document describes how to create, enable/disable, delete, and view API keys of the root account.

## Prerequisites

You have logged in to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM console as the [root account](https://intl.cloud.tencent.com/document/product/378/36004).

## Directions

### Creating an API key for a root account

You can create an API key for a root account. After the API key is created, the root account can use APIs, SDKs, or other development tools to manage the resources under the account.
Click **Create Key** on the left of the [API Key Management](https://console.cloud.tencent.com/cam/capi) page, as shown below:
![](https://main.qcloudimg.com/raw/0eaec6ab40a4904e136d9e63c7335684.png)

 > ?
 >
 > - One root account can create up to 2 API keys.
 > - The root account API key represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.
 > - An API key is an important credential for creating Tencent Cloud API requests. To keep your assets and services secure, store your keys appropriately, change them regularly, and delete old keys after creating new ones.

### Viewing an API key of a root account

You can view and copy the `SecretId` and `SecretKey` of the API key of the root account. You can use the `SecretId` and `SecretKey` to use APIs, SDKs, or other developer tools to manage resources under the account.

1. Enter the [API Key Management](https://console.cloud.tencent.com/cam/capi) page. You can directly view and copy the `SecretId` from the **Key** column.
2. Click **Show** in the "Key" column. You can get and copy the `SecretKey` after completing identity verification.
![](https://main.qcloudimg.com/raw/e328ad7cca684908f01041935a21b381.png)


### Disabling/enabling root account API key

You can disable an API key of the root account. Tencent Cloud will block all requests that use the API key after it is disabled.

1. Click **Disable** in the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
![](https://main.qcloudimg.com/raw/deefbfdc98bd794daa399af0ff8a9f7a.png)
2. In the pop-up window, click **Confirm** to disable the access key.

> ?You can click **Enable** in the "Operation" column to enable the key. After the key is enabled, you can use APIs, SDKs, or other developer tools to manage the resources under the account.

### Deleting root account API key

1. Click **Disable** in the [API Key Management](https://console.cloud.tencent.com/cam/capi) page. If the target API key was disabled, you can directly perform step 3.
2. In the pop-up window, click **Disable**.
3. On the API Key Management page, click **Delete** in the "Operation" column.
4. In the pop-up window, click **Delete**.

> ?Please note that a deleted API key cannot be retrieved.
