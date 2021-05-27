## Overview

This document describes how to access the SASL access point of CKafka to receive/send messages through the PLAIN mechanism in a VPC.

## Prerequisites

- [Install Python](https://www.python.org/downloads/)
- [Install pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)

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
   	ssl_check_hostname = False,
   	security_protocol = "SASL_PLAINTEXT",
   	sasl_mechanism = "PLAIN",
	sasl_plain_username = "$instance_id#$username",
   	sasl_plain_password = "$password",
	api_version = (0,10,0)
)

producer.send('$topic_name',value="Hello World! Hello Ckafka!")
producer.close()
```

| Parameters | Description |
| ------------------- | ------------------------------------------------------------ |
| bootstrap_servers | SASL access point, which can be obtained in **Basic Info** > **Access Mode** on the **Instance Details** page in the [CKafka console](https://console.cloud.tencent.com/ckafka) |
| sasl_plain_username | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the **Instance Details** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), and the username is set when the user is created in **User Management** |
| sasl_plain_password | User password, which is set when the user is created in **User Management** on the **Instance Details** page in the CKafka console |
| topic_name | Topic name, which can be created and obtained in **Topic Management** on the **Instance Details** page in the CKafka console |

#### Message consumption

```python
#coding:utf8
from kafka import KafkaConsumer

consumer = KafkaConsumer(
	'$topic_name',
	group_id = "$group_id",
	bootstrap_servers = ['$ip:$port'],
	security_protocol = "SASL_PLAINTEXT",
	sasl_mechanism = 'PLAIN',
	sasl_plain_username = "$instance_id#$username",
   	sasl_plain_password = "$password",
	api_version = (0,10,0)
)

for message in consumer:
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
```

| Parameters | Description |
| ------------------- | ------------------------------------------------------------ |
| bootstrap_servers | SASL access point, which can be obtained in **Basic Info** > **Access Mode** on the **Instance Details** page in the [CKafka console](https://console.cloud.tencent.com/ckafka) |
| group_id | Consumer group ID, which can be customized according to the business needs |
| sasl_plain_username | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the **Instance Details** page in the CKafka console, and the username is set when the user is created in **User Management** | 
| sasl_plain_password | User password, which is set when the user is created in **User Management** on the **Instance Details** page in the CKafka console |
| topic_name | Topic name, which can be created and obtained in **Topic Management** on the **Instance Details** page in the CKafka console |
