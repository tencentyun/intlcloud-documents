This document describes how to create an instance in the TencentDB for MariaDB console.

## Directions
1. Log in and go to the [TencentDB for MariaDB purchase page](https://console.cloud.tencent.com/mariadb/buy), select configuration items based on your actual needs, confirm that everything is correct, and click **Buy Now**.
 - Billing Mode: Monthly subscription and pay-as-you-go.
 - **Region**: Select a region where the instance will be deployed. We recommend that you use the same region as that of the CVM instance to be connected to.
 - AZ:
    - **Primary AZ**: The AZ where the primary node will be deployed. AZs are physical IDCs whose electric power facilities and networks are independent from each other within the same region. We recommend that you use the same AZ as that of the CVM instance to be connected to.
    - **Replica AZ**: The AZ where the replica node will be deployed. As cross-AZ access is supported, the replica AZ can be different from the primary AZ, and in this case, we recommend that you select the same AZ as that of your standby business system.
 - Network type: Select a network where the instance will be deployed. We recommend that you use the same network as the CVM instance to be connected to. Once selected, a VPC cannot be changed. For more information on VPC operations, see [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805).
 - **Architecture**: For more information, see [Instance Architecture](https://cloud.tencent.com/doc/product/237/6918). The more the replicas, the higher the availability.
 - **Database Version**: MySQL 8.0.18 (fully compatible with MySQL 8.0), Percona 5.7.17 (fully compatible with MySQL 5.7), and MariaDB 10.1.9 (fully compatible with MySQL 5.6).
 - **Instance Specs**: This represents different performance levels and basic prices. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/237/2034).
 - **Disk**: SSD disk (local disk) is used by default.
 - **Project**: If instances need to be managed by different teams, assign the instances to the projects of different teams accordingly.
 - **Quantity**: This represents the number of instances that can be purchased at a time. To avoid faulty operations, an upper limit has been set for this parameter. If you want to purchase more instances, make multiple purchases.
2. Verify all the information is correct in the pop-up window and click **Buy Now** to purchase.
3. After making the payment, return to the instance list. After the status of the instance changes to **Running**, it can be used normally.

