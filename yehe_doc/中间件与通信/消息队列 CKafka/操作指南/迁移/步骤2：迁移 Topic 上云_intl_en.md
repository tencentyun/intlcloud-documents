## Overview
This document describes how to use the migration tool provided by CKafka to migrate topics from a self-built Kafka cluster to a CKafka instance.

## Prerequisites

- You have already [purchased a CKafka instance](https://intl.cloud.tencent.com/document/product/597/41379).
- You have [downloaded Python 2](https://www.python.org/downloads/).


## Directions
1. Download the [migration tool](https://ckafka-1300957330.cos.ap-guangzhou.myqcloud.com/ckafka-demo/migrateToCkafkaTool.zip) and decompress it on a server that can connect to the broker and ZooKeeper of the self-built instance.
2. Enter the configuration parameters in the `ckafka-migrate.py` file.
>?
>- Please make sure that the networks of the server where the subsequent migration operation is performed, the CKafka instance, and the self-built Kafka cluster are interconnected.
>- The user corresponding to the key of TencentCloud API needs to have the write permission of CKafka. We recommend using the key pair of the root account.
<dx-codeblock>
:::  python
   # your local broker ip:port list
   # Broker list of the self-built instance ["broker1:port1","ip2:port2"]
   bootstrapServers = ["$ip:$port"]

   # your local zk ip:port list
   # ZooKeeper list of the self-built instance ["zk1:port1","zk2:port2"]
   sourceZk = ["$ip:$port"]

   # your cloud instanceId
   # CKafka instance ID "ckafka-xxx"
   instanceId = "$yourinstanceId"

   # topic regex,just migrate match topics
   # Regular expression of topic name. If it is not empty, only matched topics will be migrated
   topicRegex = ""

   # your secretId and secretKey
   # Account key pair
   secretId = "$yoursecretId"
   secretKey = "$yoursecretKey"

   # your cloud instance region
   # CKafka instance region and code:
   # Guangzhou ap-guangzhou; Shanghai ap-shanghai; Nanjing ap-nanjing; Beijing ap-beijing; Chengdu ap-chengdu; Chongqing ap-chongqing;
   # Hong Kong (China) ap-hongkong; Singapore ap-singapore; Mumbai ap-mumbai; Tokyo ap-tokyo; Silicon Valley na-siliconvalley;
   # Virginia na-ashburn; Toronto na-toronto; Taipei (China) ap-taipei; Tianjin ap-tianjin;
   # Shenzhen ap-shenzhen; Frankfurt eu-frankfurt; Seoul ap-seoul; Qingyuan ap-qingyuan;
   # Moscow eu-moscow; Bangkok ap-bangkok; Changsha ap-changsha-ec; Jakarta ap-jakarta
   region = "ap-changsha-ec"

   # if you make sure the migrate topic List,please modify checkFlag = 1
   # Check flag. If it is 0, the list of topics to be migrated will only be displayed, but not be actually migrated. Please set it to 0 first to check the list of topics, confirm that everything is correct, and change it to 1 to start migration
   # 0: lists the topics to be migrated and then stops the script
   # 1: lists the topics to be migrated and then starts migration
   checkFlag = 0

   # force transfor your topic config to cloude
   # If the value is 0, a local topic will not be migrated to CKafka if its attributes do not match those of CKafka. If the value is 1, the topic attribute values out of the value range of CKafka will be forcibly converted to the closest values within the value range
   # For example, if the CKafka topic supports only 2 or 3 replicas, but a local topic has 5 replicas, it will not be migrated to CKafka. If you set the parameter to 1, then a 3-replica topic, which is closest to the original number of replicas (5), will be created for the CKafka topic
   # 0: skips the unmatched topic or topic attributes if the numbers of replicas or attributes of the local and CKafka topics do not match
   # 1: forcibly migrates all topics to CKafka and changes the number of replicas or attributes for unmatched topics in CKafka if the numbers of replicas or attributes of the local and CKafka topics do not match (data in the local self-built Kafka cluster will not be modified)
   force = 0
:::
</dx-codeblock>


   | Parameter             | Description                                                         |
   | ---------------- | ------------------------------------------------------------ |
   | bootstrapServers | List of brokers of the self-built instance, such as `["ip1:port1","ip2:port2"]`.            |
   | sourceZk         | List of ZooKeepers of the self-built instance, such as `["zk1:port1","zk2:port2"]`.        |
   | instanceId       | ID of the [purchased CKafka instance](https://intl.cloud.tencent.com/document/product/597/41379), which can be copied on the **Instance List** page in the console. |
   | secretId         | ID in the account key pair.                                            |
   | secretKey        | Password in the account key pair.                                          |
   | region           | Deployment region selected during [CKafka instance purchase](https://intl.cloud.tencent.com/document/product/597/41379). All region codes are as listed in the script comment.   |
   | checkFlag        | Check flag. If it is 0, the list of topics to be migrated will be displayed only and migration will not start. If it is not 0, the topics will start to be migrated. |
   | topicRegex       | Regular expression of topic name. If it is empty, all topics will be migrated. If it is not empty, only matched topics will be migrated. |
   | force            | Specifies whether to forcibly migrate. If the value is 0, a local topic will not be migrated to CKafka if its attributes do not match those of CKafka. If the value is 1, the topic attribute values out of the value range of CKafka will be forcibly converted to the closest values within the value range. |

3. Set the `checkFlag` parameter in `ckafka-migrate.py` to 0, run `python ckafka-migrate.py` to execute the script, and check the list of topics that need to be migrated based on the output result.
>?If some self-built topics are missing, this may be because that their names are non-compliant, or the number of topic replicas or topic attribute values are out of the CKafka value range.
>
![](https://main.qcloudimg.com/raw/4566352387f69b71e6fb7ab1b44780b9.png)

4. Set the `checkFlag` parameter in `ckafka-migrate.py` to 1 and run `python ckafka-migrate.py` to execute the script to start migrating the topics.
   ![](https://main.qcloudimg.com/raw/eed68b25e287092fc370b7b91b09a35c.png)

5. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka), view the task list on the **Cloud Migration** page, and wait for the topics to be completely migrated.
	The topic list is as shown below:
	<img src="https://main.qcloudimg.com/raw/1c9a76e32926abf8cb296f9622b67a23.png" width="600px">
	
	The result of successful migration is as shown below:
	<img src="https://main.qcloudimg.com/raw/574f0dd1ead9397a7da91f26f82c9bc8.png" width="600px">

