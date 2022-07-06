## Overview
Secure Sockets Layer (SSL) authentication is a process that authenticates the connection from the user client to the TencentDB server. After SSL encryption is enabled, you can get a CA certificate and upload it to the server. Then, when the client accesses the database, the SSL protocol will be activated to establish an SSL secure channel between the client and the server. This implements encrypted data transfer, prevents data from being intercepted, tampered with, and eavesdropped during transfer, and ultimately ensures the data security for both the client and the server.
>?The SSL encryption feature is being gradually released in various regions. If you want to try it out earlier, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Billing Details
SSL encryption is free of charge.

## Notes
- Enabling SSL encryption ensures the security of data access and transfer but may slightly affect the instance performance. We recommend you enable it only when encryption is required.
- If the password exemption access feature is not enabled, both SSL and non-SSL connection methods are supported. After this feature and SSL encryption are enabled, the database can be accessed only over SSL. 
- After the SSL encryption feature is disabled, clients using encrypted connections will not be able to connect properly.
- The SSL certificate is valid for 20 years.

## Version and Architecture Requirements
- Version description
 - New instances: If the compatible version is 4.0, 5.0, or 6.0, SSL encryption can be enabled directly. To use it on v6.0, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
 - Existing instances:
   - If the compatible version is 2.8, SSL encryption can be enabled after the version is upgraded to version 4.0, 5.0, or 6.0. For more information, see [Upgrading Instance Version](https://intl.cloud.tencent.com/document/product/239/37710).
   - If the compatible version is 4.0, 5.0, or 6.0, the feature can be enabled after the proxy version is upgraded to 5.6.0. For more information, see [Upgrading Proxy](https://intl.cloud.tencent.com/document/product/239/47582).
- Architecture description
Both standard architectures and cluster architecture support SSL encryption.

## Prerequisites
- The database instance is in **Running** status, with no ongoing tasks.
- The operation is performed in off-peak hours, or the client has an automatic reconnection mechanism.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. In the **Instance ID/Name** column of the target instance, click the instance ID to enter the **Instance Details** page.
5. Click the **SSL Encryption** tab. If the system prompts you to upgrade the version under **SSL Encryption Settings**, click **Upgrade Version**, and wait until the version is successfully upgraded.
6. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/84853fe19aa340a98cc138f8d951ddb9.png" style="zoom: 25%;" /> next to **Encryption Status** and **Updating SSL Status** will be displayed.
7. Wait for **Encryption Status** to become **Enabled** and click **Download Certificate**.
8. Wait for the **Enable SSL** status to become **Enabled** and click **Download Certificate**.
9. In the bottom-left corner of the page, upload the obtained certificate **-crt.zip** to the server, and then you can access the database over SSL.
For client connection code samples, see [Java Connection Sample](https://intl.cloud.tencent.com/document/product/239/7043) and [Python Connection Sample](https://intl.cloud.tencent.com/document/product/239/7045).
