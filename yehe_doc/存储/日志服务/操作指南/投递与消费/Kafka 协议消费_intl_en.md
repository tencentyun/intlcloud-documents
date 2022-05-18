You can consume the data collected by CLS to downstream big data components or data warehouses over the Kafka protocol, such as self-built Kafka clusters, open-source ClickHouse, Hive, and Flink, as well as Tencent Cloud EMR and Oceanus.

## Consumption over private or public network

- Definitions of consumption over the private network and consumption over the private network: For example, if your log topics in the Guangzhou region use the Kafka consumption protocol, then consumption to EMR-Hive in Guangzhou is regarded as over the private network, while consumption to EMR-Hive in Shanghai is regarded as over the public network.
- Billing differences: The private network traffic is priced at 0.032 USD/GB, while the public network traffic is priced at 0.141 USD/GB.
- Consumption service domain name differences: The private and public network service domain names are as listed in the console for your choice as needed.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** on the left sidebar.
3. Click the ID/name of the log topic that needs to be consumed over the Kafka protocol to enter the log topic management page.
4. Click the **Consumption over Kafka** tab.
5. Click **Edit** on the right.

6. Set **Current Status** to **On** and click **OK**.

7. Construct the consumer according to the topic information given by CLS.



## Examples

Example: Construct Consumer.py in Python
```
import uuid
from kafka import KafkaConsumer,TopicPartition,OffsetAndMetadata
consumer = KafkaConsumer(
// Enter the topic name in the above figure here, and you will use this topic for consumption.    
'out-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX',  
group_id = uuid.uuid4().hex,
auto_offset_reset='earliest',
// Kafka protocol service address. Enter the service access information in the above figure here. If you consume over the public network, enter
the public network service domain name + port. If over the private network, enter the private network service domain name + port. The example uses the private network service.
bootstrap_servers = ['kafkaconsumer-ap-guangzhou.cls.tencentyun.com:9096'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',   
// SASL information. Enter the logset ID of the log topic here.   
sasl_plain_username = "ca5cXXXX-dd2e-4ac0-af12-92d4b677d2c6",
// SASL information. #Enter the string of your secretid#secrectkey. Be sure to keep it confidential.#
sasl_plain_password = "AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac",
api_version = (0,10,0)
)
print('begin')
for message in consumer:
    print('begins')
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
    print('end')
```



