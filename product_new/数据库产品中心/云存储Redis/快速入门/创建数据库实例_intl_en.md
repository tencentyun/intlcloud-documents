## Scenario
This document describes how to create an instance in the TencentDB for Redis Console.

## Directions

1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and select **Instance List** on the left sidebar.
2. Click **Create Instance** and enter the parameters as required.

| Parameter | Remarks |
|---------|---------|
| Billing Mode | Pay-as-you-go billing is supported. |
| Network Type | The basic network and VPC cannot communicate with each other. You cannot change the network type after purchase. For more information, see [Network Environment](http://intl.cloud.tencent.com/document/product/213/5227). |
| Engine | Redis Community Edition is supported. |
| Compatible Version | Compatible with Redis 2.8 and 4.0. |
| Replica Count | <li>Redis 2.8 Standard Edition supports 0-1 replicas. <li>Redis 4.0 Standard Edition supports 1-5 replicas. <li>Redis 4.0 Cluster Edition supports 1-5 replicas. |
| Port | The custom port number needs to be between 1024 and 65535. |
| Specify Project/Security Group | Specify the project and security group for the database. |
| Instance Name/Set Password | You can directly set the instance name and password here or set them in the instance list after creation. |

3. After confirming everything is correct, click **Buy Now**. For detailed pricing of each edition, see [Pricing Descriptions](http://intl.cloud.tencent.com/document/product/239/9894).
4. Return to the instance list and wait for the instance status to become **To be initialized**.
