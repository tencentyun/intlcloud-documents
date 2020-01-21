## Operation Scenarios
This document guides you through how to create and view a topic under an existing instance in the CKafka Console.

Topic is the name of a category where messages can be stored and published. CKafka uses the concept of topic externally, that is, a producer writes messages to a topic, while a consumer read messages from it. To implement horizontal scaling, a topic actually consists of multiple [partitions](https://intl.cloud.tencent.com/document/product/597/32275). When a performance bottleneck occurs, you can scale out the topic by adding more partitions.

## Prerequisites
You have [created an instance](https://intl.cloud.tencent.com/document/product/597/32543).

## Directions
### Creating a topic
1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click **Topic Management** at the top.
3. On the topic management page, click **Create**.
4. In the topic editing window, set configuration information such as the number of partitions and replicas.
 - Name: the topic name, which cannot be changed once entered and can only contain letters, digits, underscores, "-", and ".".
 - Number of Partitions: partition is a physical concept of partitioning. A topic can contain one or more partitions, and CKafka uses partition as the unit for allocation.
 - Number of Replicas: the number of partition replicas which are used to ensure high availability of partitions. For the sake of data reliability, you cannot create a single-replica topic currently. 2 replicas are enabled by default.
 - Whitelist: after the whitelist is enabled, the topic can be accessed only from IPs in the whitelist, thus effectively protecting data security. (The whitelist can be enabled either on the topic creation page or topic editing page.)
5. Click **Submit** to complete topic creation.

>The number of replicas is also considered for partitions. For example, if you create 1 topic, 6 partitions, and 2 replicas, then there will be a total of 1 \* 6 \* 2 = 12 partitions.
If the maximum number of partitions allowed is exceeded during purchase, the following prompt will be displayed when you click **Submit**:
![](https://main.qcloudimg.com/raw/eeb3b9aa16ef7b5ae6370d56affed865.png)

### Viewing a topic
1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click the **Topic Management** tab to view the information of a topic such as monitoring metrics, number of partitions, and whitelist.

### Deleting a topic
>
>- Once a topic is deleted, messages stored in it will also be deleted. Please do so with caution.
>- Topic deletion is an async operation. After deletion is successfully configured, the ZooKeeper configuration will take effect after 1 minute. If you create a topic with the same name as the deleted topic in this period, the system will return error code [4000]10011. In this case, please wait and try again later.

1. On the CKafka instance list page, click the "ID/Name" of the target instance to enter the instance details page.
2. On the instance details page, click **Topic Management** at the top.
3. On the topic management page, click **Delete** in the "Operation" column. Or, use the [DeleteTopic](https://cloud.tencent.com/document/product/597/10099) API to delete the instance. 

