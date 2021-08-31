## Overview

This document describes how to access the default access point of CKafka to receive/send messages with the SDK for Python in a VPC.

## Prerequisites

- [Install Python](https://www.python.org/downloads/)
- [Install pip](https://pip-cn.readthedocs.io/en/latest/installing.html)


## Directions
### Step 1. Add the Python dependency library
Run the following command to install:
```bash
pip install kafka-python
```

### Step 2. Modify the configuration

#### Message production

```python
#coding:utf8
from kafka import KafkaProducer

producer = KafkaProducer(
   bootstrap_servers = ['$ip:$port'],
   api_version = (0,10,0)
)

producer.send('$topic_name',value = "Hello World! Hello Ckafka!")
producer.close()
```

| Parameters | Description |
| ----------------- | ------------------------------------------------------------ |
| bootstrap_servers | Default access point, which can be obtained in **Basic Info** > **Access Mode** or **Private IP and Port** on the **Instance Details** page in the [CKafka console](https://console.cloud.tencent.com/ckafka) |
| topic_name | Topic name, which can be created and obtained in **Topic Management** on the **Instance Details** page in the CKafka console |

#### Message consumption

```python
#coding:utf8
from kafka import KafkaConsumer

consumer = KafkaConsumer(
    '$topic_name',
    group_id = "$group_id",
    bootstrap_servers = ['$ip:$port'],
    api_version = (0,10,0)
)

for message in consumer:
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
```

| Parameters | Description |
| ----------------- | ------------------------------------------------------------ |
| bootstrap_servers | Access point, which can be obtained in **Basic Info** > **Access Mode** or **Private IP and Port** on the **Instance Details** page in the [CKafka console](https://console.cloud.tencent.com/ckafka). |
| group_id | Consumer group ID, which can be customized according to the business needs. |
| topic_name | Topic name, which can be created and obtained in **Topic Management** on the **Instance Details** page in the CKafka console |

