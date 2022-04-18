Kafka real-time consumption allows you to send data collected by Cloud Log Service (CLS) to target applications efficiently and conveniently. It can connect to your stream computing components such as Flink and ES for stream processing of log data. After you enable this feature, CLS will provide a Kafka topic for you to consume.


## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. Click the log topic name/ID for which real-time consumption needs to be configured to go to its details page.
4. Click the **Real-time Consumption** tab to go to the real-time consumption configuration page.
5. Click **Edit** on the right, toggle **Status** on, and click **OK**.

6. Construct a consumer based on the information of the topic that CLS provides for data consumption. For more information, please see [CKafka SDK](https://intl.cloud.tencent.com/document/product/597/43839).



## Examples

Construct Consumer.py via Consumer.py
```
import uuid
from kafka import KafkaConsumer,TopicPartition,OffsetAndMetadata
consumer = KafkaConsumer(
// Your topic name. Enter the topic name in the above figure here.      
'in-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX',  
group_id = uuid.uuid4().hex,
auto_offset_reset='earliest',
// Kafka service address. Enter the access point information in the above figure here.   
bootstrap_servers = ['ckafka-lweXXXXk.ap-
guangzhou.ckafka.tencentcloudmq.com:6012'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',   
// SASL information. Concatenate the Kafka instance information and username with # and enter it here. The instance information is in the access point information.   
sasl_plain_username = "ckafka-lweXXXXk#cls-2pGgXXX",
// SASL information. Enter the password in the above figure here.   
sasl_plain_password = "8uleOOPXXX",
api_version = (0,10,0)
)
print('begin')
for message in consumer:
    print('begins')
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
    print('end')
```


>? If data cannot be consumed, your server may be configured with access restrictions. Open ports 9092 to 9192 to the internet on the server (As the brokers may be expanded automatically, more ports need to be opened to the internet after the expansion. Therefore, reserve an adequate number of ports). For more information, see [Viewing Instance](https://intl.cloud.tencent.com/document/product/597/38570).
>
