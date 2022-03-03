Kafka real-time consumption allows you to send data collected by Cloud Log Service (CLS) to target applications efficiently and conveniently. It can connect to your stream computing components such as Flink and ES for stream processing of log data. After you enable this feature, CLS will provide a Kafka topic for you to consume.


## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. Click the log topic name/ID for which real-time consumption needs to be configured to go to its details page.
4. Click the **Real-Time Consumption** tab to go to the real-time consumption configuration page.
5. Click **Edit** on the right, toggle **Status** on, and click **OK**.

6. Construct a consumer based on the information of the topic that CLS provides for data consumption. For more information, please see [CKafka SDK](https://intl.cloud.tencent.com/document/product/597/40453).



## Example

Construct Consumer.py via Consumer.py

```
import uuid
from kafka import KafkaConsumer,TopicPartition,OffsetAndMetadata
consumer = KafkaConsumer(
'in-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX', // Topic name
group_id = uuid.uuid4().hex,
auto_offset_reset='earliest',
bootstrap_servers = ['ckafka-lweXXXXk.ap-
guangzhou.ckafka.tencentcloudmq.com:6012'], // Access point information
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',
sasl_plain_username = "ckafka-lweXXXXk#cls-2pGgXXX", // Instance ID#Username. You can obtain the instance ID in the access point information.
sasl_plain_password = "8uleOOPXXX", // Password
api_version = (0,10,0)
)
print('begin')
for message in consumer:
    print('begins')
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
    print('end')

```


>? If data cannot be consumed, your server may be configured with access restrictions. Open ports 9092 to 9192 to the internet on the server (As the brokers may be expanded automatically, more ports need to be opened to the internet after the expansion. Therefore, reserve an adequate number of ports). For more information, please see [Viewing Instance](https://intl.cloud.tencent.com/document/product/597/38570).
>
