## Operation Scenarios
This document guides you through how to create and view an instance in the CKafka Console.

## Directions
### Creating an instance
1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. On the CKafka instance list page, click **Create** to enter the instance purchase page.
3. On the CKafka instance purchase page, set the configuration information for purchase.
	- Region: select a region close to the physical partition
	- AZ: select a purchasable partition
	- Product Specification: select an appropriate model based on the peak bandwidth and disk capacity
	- Message Retention: a period in minutes ranging from 1 minute to 90 days
	>After the message retention period is set, messages will be deleted after expiration. Messages are deleted in batches based on CKafka segments but not immediately. Currently, the segment size is 1 GB, and if a segment is less than 1 GB, it will not be deleted. Therefore, if the retention period is set to 1 minute, but the data size of the segment cannot be accumulated to 1 GB in 1 minute, this period will not take effect, and you are recommended to increase the period depending on the speed of data accumulation.
	- Quantity: 1–20
4. Click **Buy Now** to complete the instance creation process.


### Viewing an instance
1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click the **Basic Info** tab to view the configuration information, access mode, message retention period, and automatic topic creation of the instance.
Once you enable the automatic topic creation feature for the server, when you use or access metadata of a topic that does not exist, it will be automatically created with the configured number of replicas and partitions. You can view the automatically created topic in **Topic Management**.
> 
>- The total number of topics that can be automatically created varies by instance specification. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).
>- The private IP and port (such as `10.6.206.110:9092`) in **Basic Info** represents the communication address used to get the backend service. There may be multiple ports in a real access address. If access control is configured on your server, open all ports after 9092 to the internet on it.

