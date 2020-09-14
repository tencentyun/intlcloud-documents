This document describes how to create an instance in the TencentDB for MariaDB Console.

## Directions
1. Log in to [MariaDB purchase page](https://console.cloud.tencent.com/mariadb/buy), specify the instance information based on your needs and click **Buy Now**.
 - Billing mode: only pay-as-you-go is supported.
 - Region: select a region where the instance will be deployed. We recommend that you use the same region as the CVM instance to be connected to.
 - Availability zone: physical IDCs whose electric power facilities and networks are independent from each other within the same region. We recommend that you use the same availability zone as the CVM instance to be connected to.
 - Network type: select a network where the instance will be deployed. We recommend that you use the same network as the CVM instance to be connected to. Once selected, a VPC cannot be changed. For more information on VPC operations, see [Managing VPC Instances](https://intl.cloud.tencent.com/document/product/215/31805).
 - Instance version: for more information, please see [Instance Architecture](https://intl.cloud.tencent.com/document/product/237/6918?from_cn_redirect=1). The more the replicas, the higher the availability.
 - Database version: for MariaDB database kernel versions, there are differences between the features of [10.0.10](https://mariadb.com/kb/en/mariadb/mariadb-10010-changelog/) and [10.1.9](https://mariadb.com/kb/en/mariadb/mariadb-1019-changelog/). For more information, please see [MariaDB official instructions](https://mariadb.org/).
 - Instance specification: this represents different performance levels and basic prices. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/237/2034).
 - Disk: SSD disk (local disk) is used by default.
 - Project: if different databases need to be managed by different teams, please specify projects accordingly.
 - Quantity: this represents the number of instances that can be purchased at a time. To avoid faulty operations, an upper limit has been set for this parameter. If you want to purchase more instances, please make multiple purchases.
2. Verify all the information is correct on the pop-up window and click **Buy Now** to purchase.
3. You will be returned to the MariaDB instance list after purchase. Wait for the instance status to be created. When the status changes to **Uninitialized**, you can initialize the instance.

