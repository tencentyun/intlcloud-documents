## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Python over the public network.

## Prerequisites

- [Install Python](https://www.python.org/downloads/)
- [Install pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/pythonkafkademo/gongwang)

## Directions

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
import json
producer = KafkaProducer(
bootstrap_servers = ['$domainName:$port'],
ssl_check_hostname = False,
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = "PLAIN",
sasl_plain_username = "$instance_id#$username",
sasl_plain_password = "$password",
api_version = (0,10,0)
)
message = "Hello World! Hello Ckafka!"
msg = json.dumps(message).encode()
producer.send('topic_name',value = msg)
print("produce message " + message + " success.");
producer.close()
```

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| sasl_plain_username | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the **Instance Details** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), and the username is set when the user is created in **User Management**. |
| sasl_plain_password | User password, which is set when the user is created in **User Management** on the **Instance Details** page in the CKafka console. |
| topic_name          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |

2. Compile and run `producer.py`.
3. View the operation result.
   ![](https://main.qcloudimg.com/raw/312d264676c655838e398ab9fa03b491.png)
4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
   ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)





### Step 3. Consume the message

1. Modify the configuration parameters in the message consumption program `consumer.py`.

```python
#coding:utf8
from kafka import KafkaConsumer

consumer = KafkaConsumer(
'$topic_name',
group_id = "$group_id",
bootstrap_servers = ['$domainName:$port'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',
sasl_plain_username = "$instance_id#$username",
sasl_plain_password = "$password",
api_version = (0,10,0)
)

for message in consumer:
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
```

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| group_id | Consumer group ID, which can be customized according to the business needs. |
| sasl_plain_username | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the **Instance Details** page in the CKafka console, and the username is set when the user is created in **User Management**. |
| sasl_plain_password | User password, which is set when the user is created in **User Management** on the **Instance Details** page in the CKafka console. |
| topic_name          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |

2. Compile and run `consumer.py`.

3. View the operation result.
   ![](https://main.qcloudimg.com/raw/479f3b14e67a5f50f9d49781ab4df39f.png)

4. On the **Consumer Group** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
