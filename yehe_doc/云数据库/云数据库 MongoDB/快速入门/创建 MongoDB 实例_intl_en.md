A TencentDB for MongoDB instance can be created in the console or through APIs.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 250px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to register a Tencent Cloud account</a></div>
- To verify your identity:
<div style="background-color:#00A4FF; width: 250px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>


## Console
1. Log in and go to the [MongoDB purchase page](https://buy.cloud.tencent.com/mongodb), select configuration items based on your actual needs, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go is supported. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/240/3550).
 - **Region** and **Availability Zone**: for more information, please see [Region and Availability Zone](https://intl.cloud.tencent.com/document/product/240/3637).
 - **Configuration Type**: **High IO (10 Gigabit)** and **Standard** are supported.
 - **Version**: v3.2, v3.6, and v4.0 are supported currently.
 - **Engine**: WiredTiger and Rocks storage engines are supported. For more information, please see [Storage Engine](https://intl.cloud.tencent.com/document/product/240/31706).
 - **Instance Type** and **Node per Shard**: instance types include replica set and sharded cluster.
    - If you select replica set, the system will configure one primary and two secondaries by default.
	 - If you select sharded cluster, you can select the number of shards and number of nodes in each shard as needed. The "one-primary-two-secondary" architecture is used in each shard by default. To improve data availability, you can increase the number of nodes in each shard. To expand the storage capacity of the cluster, you can increase the number of shards.
 - **Specification**: for more information on computing specification options, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/240/3550).
 - **Capacity**: you can select a storage specification based on the computing specification. The storage space of oplog is 10% of the selected storage capacity by default, which can be adjusted as needed in the console.
 - **Network Type**: both VPC (recommended) and classic network are supported. If you select a VPC, only devices in the current subnet can access the created database instance. If you select the classic network, only devices in the classic network can access the created database instance.
 - **Project**: you can select an appropriate project based on your business needs.
 - **Quantity**: a total of up to 30 pay-as-you-go instances can be purchased in all regions.
2. Make the payment and return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


## API 
For more information on how to create a TencentDB instance through API, please see [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/240/34704).
