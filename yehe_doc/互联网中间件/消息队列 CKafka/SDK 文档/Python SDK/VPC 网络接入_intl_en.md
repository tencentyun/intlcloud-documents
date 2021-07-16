## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Python in a VPC.

## Prerequisites

- [Install Python](https://www.python.org/downloads/)
- [Install pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/pythonkafkademo/VPC)

## Directions

Upload the `pythonkafkademo` in the downloaded demo to the Linux server, log in to the server, and enter the `pythonkafkademo` directory.

### Step 1. Add the Python dependency library

Run the following command to install:
```bash
pip install kafka-python
```


### Step 2. Produce a message

1. Modify the configuration parameters in the message production program `producer.py`.

```python
#coding:utf8
from kafka import KafkaProducer

producer = KafkaProducer(
   bootstrap_servers = ['$domainName:$port'],
   api_version = (0,10,0)
)
message = "Hello World! Hello Ckafka!"
msg = json.dumps(message).encode()
producer.send('topic_name',value = msg)
print("produce message " + message + " success.");
producer.close()
```

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png) |
| topic_name          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |

2. Compile and run `producer.py`.
3. View the operation result.
![](https://main.qcloudimg.com/raw/312d264676c655838e398ab9fa03b491.png) 
4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
	![](https://main.qcloudimg.com/raw/ec5fbf218cf50ff3d760be15f6331867.png)




### Step 3. Consume the message

1. Modify the configuration parameters in the message consumption program `consumer.py`.
```python
#coding:utf8
from kafka import KafkaConsumer

consumer = KafkaConsumer(
    '$topic_name',
    group_id = "$group_id",
    bootstrap_servers = ['$domainName:$port'],
    api_version = (0,10,0)
)

for message in consumer:
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
```

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png) |
| group_id | Consumer group ID, which can be customized according to the business needs. |
| topic_name          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |

2. Compile and run `consumer.py`.

3. View the operation result.
   ![](https://main.qcloudimg.com/raw/479f3b14e67a5f50f9d49781ab4df39f.png)

4. On the **Consumer Group** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/27775267907600f4ff759e6a197195ee.png)
