## Creating an Instance
1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. On the CKafka instance list page, click **Create** to enter the instance purchase page.
3. On the CKafka instance purchase page, set the configuration information for purchase.
	- Billing Mode: Monthly subscription
	- Region: Select a region nearby the physical partition
	- AZ: Select a purchasable partition
	- Product Specification: Select an appropriate model based on the peak bandwidth and disk capacity
	- Message Retention: A period in minutes ranging from 1 minute to 30 days
	>?After the message retention period is set, messages will be deleted after expiration. Messages are deleted in batches based on CKafka segments but not immediately. Currently, the segment size is 1 GB, and if a segment is less than 1 GB, it will not be deleted. Therefore, if the retention period is set to 1 minute, but the data size of the segment cannot be accumulated to 1 GB in 1 minute, this period will be invalid, and you are recommended to increase the period depending on the speed of data accumulation.
	- Quantity: 1-20
	- Purchase Duration: You can set auto-renewal by month upon expiration
4. Click **Buy Now** to complete the instance creation process.


## Creating a Topic
1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click **Topic Management** at the top.
3. On the topic management page, click **Create**.
4. In the topic editing window, set configuration information such as the number of partitions and replicas.
 - Name: The topic name, which cannot be changed once entered and can only contain letters, digits, underscores, dashes, and full stops.
 - Number of Partitions: Partition is a physical concept of partitioning. A topic can contain one or more partitions, and CKafka uses partition as the unit for allocation.
 - Number of Replicas: The number of partition replicas which are used to ensure high availability of partitions. For the sake of data reliability, you cannot create a single-replica topic currently. 2 replicas are enabled by default.
 - Whitelist: After the whitelist is enabled, the topic can be accessed only from whitelisted IPs, thus effectively guaranteeing data security. (The whitelist can be enabled on the page of creating or editing a topic.)
5. Click **Submit** to complete topic creation.

>?The number of replicas is also considered for partitions. For example, if you create 1 topic, 6 partitions, and 2 replicas, then there will be a total of 1 \* 6 \* 2 = 12 partitions.
If the maximum number of partitions allowed is exceeded during purchase, the following prompt will be displayed when you click **Submit**:
![](https://main.qcloudimg.com/raw/eeb3b9aa16ef7b5ae6370d56affed865.png)

## Viewing an Instance
1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click the **Basic Information** tab to view the configuration information, access mode, message retention period, and automatic topic creation of the instance.
Once you enable the automatic topic creation feature for the server, when you use or access metadata of a topic that does not exist, it will be automatically created with the configured number of replicas and partitions. You can view the automatically created topic in **Topic Management**.
>?
>- The total number of topics that can be automatically created varies by instance specification. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).
>- The private IP and port (such as `10.6.206.110:9092`) in **Basic Info** represents the communication address used to obtain the backend service. There may be multiple ports in a real access address. If access control is configured on your server, open all ports after 9092 to the internet on it.


### Viewing a Topic
1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click the **Topic Management** tab to view the information of a topic such as monitoring information, number of partitions, and whitelist.
