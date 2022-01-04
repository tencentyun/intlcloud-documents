## Overview

This document describes how to access CKafka to receive/send messages with the SDK for Python through SASL_PLAINTEXT over public network.

## Prerequisites

- [Install Python](https://www.python.org/downloads/)
- [Install pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/pythonkafkademo/PUBLIC_SASL)

## Directions

### Step 1. Make preparations
1. Create an access point.
	1. On the **[Instance List](https://console.cloud.tencent.com/ckafka/index)** page in the CKafka console, click the target instance ID to enter the instance details page.
	2. In **Basic Info** > **Access Mode**, click **Add a routing policy**. In the pop-up window, select `Route Type: Public domain name access`, `Access Mode: SASL_PLAINTEXT`.
	![](https://qcloudimg.tencent-cloud.cn/raw/4ac0033364e13d3f2c81d464c878d7f4.png)

2. Create a role.
On the **User Management** tab page, create a role and set the password.
![](https://qcloudimg.tencent-cloud.cn/raw/b4fd547ddb7d4fdac1c24d59bb4806bc.png)

3. Create a topic.
Create a topic on the **Topic Management** tab page as instructed in [Creating a topic](https://intl.cloud.tencent.com/document/product/597/32554).

4. Add the Python dependent library.
Run the following command to install the dependent library:
```bash
pip install kafka-python
```

### Step 2. Produce messages

1. Modify the configuration parameters in the message production program `producer.py`.
```python
producer = KafkaProducer(
    bootstrap_servers = ['xx.xx.xx.xx:port'],
    api_version = (1, 1),

    #
    # Public network access through SASL_PLAINTEXT
    #
    security_protocol = "SASL_PLAINTEXT",
    sasl_mechanism = "PLAIN",
    sasl_plain_username = "instanceId#username",
    sasl_plain_password = "password",
)

message = "Hello World! Hello Ckafka!"
msg = json.dumps(message).encode()
producer.send('topic_name', value = msg)
print("produce message " + message + " success.")
producer.close()
```

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| `bootstrap_servers` | Accessed network, which can be copied from the **Network** column in the **Access Mode** section in **Basic Info** on the instance details page in the console. <br/>![img](https://main.qcloudimg.com/raw/c5cf200a66f6dcf627d2ca6f1c747ecf.png) |
| `sasl_plain_username` | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), and the username is set when the user is created in **User Management**. |
| `sasl_plain_password` | User password, which is set when the user is created in **User Management** on the instance details page in the CKafka console. |
| `topic_name`          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |

2. Compile and run `producer.py`.
   
3. View the execution result.
![](https://main.qcloudimg.com/raw/312d264676c655838e398ab9fa03b491.png)

4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the target topic, and click **More** > **Message Query** to view the message just sent.
![](https://main.qcloudimg.com/raw/ec5fbf218cf50ff3d760be15f6331867.png)


### Step 3. Consume messages

1. Modify the configuration parameters in the message consumption program `consumer.py`.
```python
consumer = KafkaConsumer(
    'topic_name',
    group_id = "group_id",
    bootstrap_servers = ['xx.xx.xx.xx:port'],
    api_version = (1,1),

    #
    # Public network access through SASL_PLAINTEXT
    #
    security_protocol = "SASL_PLAINTEXT",
    sasl_mechanism = 'PLAIN',
    sasl_plain_username = "instanceId#username",
    sasl_plain_password = "password",
)

for message in consumer:
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" %
    (message.topic, message.partition, message.offset, message.value))

```

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| `bootstrap_servers` | Accessed network, which can be copied from the **Network** column in the **Access Mode** section in **Basic Info** on the instance details page in the console. <br/>![img](https://main.qcloudimg.com/raw/c5cf200a66f6dcf627d2ca6f1c747ecf.png) |
| `group_id`          | Consumer group ID, which can be customized based on business requirements.                            |
| `sasl_plain_username` | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the instance details page in the CKafka console, and the username is set when the user is created in **User Management**. |
| `sasl_plain_password` | User password, which is set when the user is created in **User Management** on the instance details page in the CKafka console. |
| `topic_name`          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |

2. Compile and run `consumer.py`.

3. View the running result.
![](https://main.qcloudimg.com/raw/479f3b14e67a5f50f9d49781ab4df39f.png)

4. On the **Consumer Group** tab page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name, and click **View Details** to view the consumption details.  
![](https://main.qcloudimg.com/raw/27775267907600f4ff759e6a197195ee.png)
