TencentDB for MongoDB can be purchased in the console or through APIs.

## Purchase in Console
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click **Create Instance** to enter the purchase page.
![](https://main.qcloudimg.com/raw/24f2aa83ab3171731caeb975652b312b.png)
2. Select various configuration items on the purchase page, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go is supported. For more information, please see [Billing Overview](https://intl.intl.cloud.tencent.com/document/product/240/3550).
 - **Region and AZ**: for more information, please see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/240/3637).
 - **Configuration Type**: High-IO and Ten-Gigabit High-IO are supported.
 - **Version**: v3.2, v3.6, and v4.0 are supported currently.
 - **Engine**: WiredTiger and Rocks storage engines are supported. For more information, please see [Storage Engine](https://intl.cloud.tencent.com/document/product/240/31706).
 - **Instance Type and Node Count**: instance types include replica set and sharding cluster.
    If you select replica set, the system will configure one master and two slaves by default.
		If you select sharding cluster, you can select the number of shards and number of nodes in each shard as needed. The "one-master-two-slave" architecture is used in each shard by default. To improve data availability, you can increase the number of nodes in each shard. To expand the storage capacity of the cluster, you can increase the number of shards.
 - **Specification**: for more information on computing specification options, please see [Billing Overview](https://intl.intl.cloud.tencent.com/document/product/240/3550).
 - **Capacity**: you can select a storage specification based on the computing specification. The storage space of Oplog is 10% of the selected storage capacity by default, which can be adjusted as needed in the console.
 - **Network Type**: both VPC and basic network are supported. If you select a VPC, only devices in the current subnet can access the created database instance. If you select the basic network, only devices in the basic network can access the created database instance.
 - **Project**: you can select an appropriate project based on your business needs.
 - **Purchase Quantity**: a total of up to 30 pay-as-you-go instances can be purchased in all regions.
3. After making the payment, return to the instance list, wait for the instance status to become **to be uninitialized**, and initialize the instance.

## Purchasing via API
For more information on how to purchase a TencentDB instance via API, please see [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/240/34704).
