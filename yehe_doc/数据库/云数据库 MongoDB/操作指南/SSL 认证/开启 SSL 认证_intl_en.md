## Overview
Secure Sockets Layer (SSL) authentication is a process that authenticates the connection from the user client to the TencentDB server. After SSL encryption is enabled, you can get a CA certificate and upload it to the server. Then, when the client accesses the database, the SSL protocol will be activated to establish an SSL secure channel between the client and the server. This implements encrypted data transfer, prevents data from being intercepted, tampered with, and eavesdropped during transfer, and ultimately ensures the data security for both the client and the server. 
>? The SSL authentication is being gradually released in regions. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category

## Billing Details
SSL encryption is free of charge.

##Precautions
- You need to restart the instance to enable SSL. Please perform this operation during off-peak hours, or ensure that your application has a reconnection feature.
- Enabling SSL encryption ensures the security of data access and transfer but will significantly increase CPU utilization. We recommend you enable it only when encryption is required.
- When SSL is enabled, you will receive an expiration alarm 30 days, 15 days, and 7 days before the expiration of your certificate and on its expiration date. Please refresh the SSL certificate in time, or the access authentication through SSL certificate will fail.

## Version Requirement
- New instances of TencentDB for MongoDB 4.0 and 4.2 support SSL authentication.
- Existing instances of TencentDB for MongoDB 3.6 needs to be upgraded to v4.0 to support SSL authentication 

## Prerequisites
- The database instance is in **Running** status, with no ongoing tasks.
- The operation is performed in off-peak hours, or the client has an automatic reconnection mechanism.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Instance ID/Name** column of the target instance, click the instance ID in blue font to enter the **Instance Details** page.
6. Click **Data Security** tab, and select **Access Encryption** tab
7. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/84853fe19aa340a98cc138f8d951ddb9.png" style="zoom: 25%;" /> behind **Enable SSL** tab
8. In the **Note** pop-up window, learn the impact of enabling SSL, and click **OK**
9. Wait for the **Enable SSL** status to become **Enabled** and click **Download Certificate**.
If you receive a certificate expiration warning message, and the certificate has expired, please click **Refresh Certificate** to update the certificate file.
10. In the bottom-left corner of the page, obtain certificate **MongoDB-CA.crt**
11. You can use Mongo Shell to connect to TencentDB for MongoDB. For detailed directions, see [Using Mongo Shell to Connect to Database by SSL Authentication] [https://intl.cloud.tencent.com/document/product/240/48469）
You can use multi-language SDKs to connect to TencentDB for MongoDB. For detailed directions, see [Using Multi-Language SDKs to Connect to Database by SSL Authentication] (https://intl.cloud.tencent.com/document/product/240/48470)

