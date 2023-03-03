## Overview 
MPS needs read and write access to COS in order to download videos from COS buckets and upload files to COS buckets after transcoding. Therefore, you need to create a service role to grant MPS access to COS.

## Directions
1. Log in to the [MPS console](https://console.tencentcloud.com/mps) and select [General Settings > Authorization](https://console.tencentcloud.com/mps/auth) on the left sidebar. Click **Go to CAM**. In the CAM console, click **Grant** to create the preset service role and grant the necessary permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/7eede4a6eb36a65a4d26b49f4e7b59af.png)
>! You cannot perform further operations in the MPS console before granting the permissions.
2. After authorization, return to the Authorization page, and you will see that the role has been created successfully. To revoke the permissions granted, click **Cancel Authorization**, find the [service role](https://intl.cloud.tencent.com/document/product/598/19388) created in the CAM console, and click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/a4972ed47afa9acc4b8e1ca3bd5035b7.png)
