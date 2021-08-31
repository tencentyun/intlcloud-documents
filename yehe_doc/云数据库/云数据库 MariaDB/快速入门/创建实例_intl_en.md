
This document describes how to create an instance in the TencentDB for MariaDB console.

## Directions
1. Log in and go to the [TencentDB for MariaDB purchase page](https://console.cloud.tencent.com/mariadb/buy), select configuration items based on your actual needs, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: pay as you go.
 - **Region**: select a region where the instance will be deployed. We recommend that you use the same region as that of the CVM instance to be connected to.
 - Availability zones (AZ):
    - **Primary AZ**: the AZ where the primary node will be deployed. AZs are physical IDCs whose electric power facilities and networks are independent from each other within the same region. We recommend that you use the same AZ as that of the CVM instance to be connected to.
    - **Replica AZ**: the AZ where the replica node will be deployed. As cross-AZ access is supported, the replica AZ can be different from the primary AZ, and in this case, we recommend you select the same AZ as that of your standby business system.
 - **Network**: select a network where the instance will be deployed. We recommend that you use the same network as that of the CVM instance to be connected to. Once selected, a VPC cannot be changed. For more information on VPC operations, see [Managing VPC Instances](https://intl.cloud.tencent.com/zh/document/product/215/31805).
 - **Architecture**: for more information, see [Instance Architecture](https://intl.cloud.tencent.com/zh/document/product/237/6918). The more the replicas, the higher the availability.
 - **Database Version**: MySQL 8.0.18 (fully compatible with MySQL 8.0), Percona 5.7.17 (fully compatible with MySQL 5.7), and MariaDB 10.1.9 (fully compatible with MySQL 5.6).
 - **Instance Specs**: this represents different performance levels and basic prices. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/237/2034).
 - **Disk**: SSD disk (local disk) is used by default.
 - **Project**: if instances need to be managed by different teams, assign the instances to the projects of different teams accordingly.
 - **Quantity**: this represents the number of instances that can be purchased at a time. To avoid faulty operations, an upper limit has been set for this parameter. If you want to purchase more instances, please make multiple purchases.
2. Verify all the information is correct in the pop-up window and click **Buy Now** to purchase.
3. After making the payment, return to the instance list, wait for the instance status to become **Uninitialized**, and initialize the instance.

