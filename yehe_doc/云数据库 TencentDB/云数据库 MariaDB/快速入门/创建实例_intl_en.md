## Operation Scenario
This document describes how to create an instance in the TencentDB for MariaDB Console.

## Directions
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql) and click **Create** to enter the purchase page.
2. Specify the database instance information based on your needs and click **Buy Now**.
 - Billing Mode: pay-as-you-go billing is supported.
 - Region: this is the region where the instance will be deployed. You are recommended to use the same region as the CVM instance to be connected to.
 - AZ: this is a physical IDC in a region with independent power supply and network resources. You are recommended to use the same AZ as the CVM instance to be connected to.
 - Network Type: this is the network where the instance is located. You are recommended to use the same network as the CVM instance to be connected to. Once selected, a VPC cannot be changed. For more information on VPC operations, please see [Managing VPCs](https://cloud.tencent.com/document/product/215/20121).
 - Instance Edition: for more information, please see [Instance Editions](https://cloud.tencent.com/doc/product/237/6918). The more the slaves, the higher the availability.
 - Database Version: this is the TencentDB for MariaDB (TDSQL) database kernel version. The features of versions [10.0.10](https://mariadb.com/kb/en/mariadb/mariadb-10010-changelog/) and [10.1.9](https://mariadb.com/kb/en/mariadb/mariadb-1019-changelog/) are different. For more information, please see [MariaDB's official website](https://mariadb.org/).
 - Instance Specification: this represents different performance levels and basic prices. For more information, please see [Billing Overview](https://cloud.tencent.com/document/product/237/2034).
 - Disk: SSD disk (local disk) is used by default.
 - Project: if different databases need to be managed by different teams, please specify projects accordingly.
 - Quantity: this represents the number of instances that can be purchased at a time. To avoid faulty operations, an upper limit has been set for this parameter. If you want to purchase more instances, please make multiple purchases.
4. After confirming that everything is correct on the information confirmation page, click **Buy Now** and make the payment.
![](https://main.qcloudimg.com/raw/eca110496c3fe48e9c7a895690ea09c6.png)
5. After making the payment, return to the TencentDB for MariaDB instance list, wait for the instance status to become **uninitialized**, and initialize the instance.

