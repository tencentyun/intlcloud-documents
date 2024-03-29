您可以通过 Kafka 协议实时消费，将采集到日志服务（Cloud Log Service,CLS）的数据，高效便捷地发送到目标应用中，可对接到您的 Flink、ES 等流计算组件，完成日志数据的流式处理。开启此功能后，CLS 会提供一个 Kafka Topic 供您消费。


## 操作步骤

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls) 。
2. 在左侧导航栏中，单击**日志主题**。
3. 单击需要配置实时消费的日志主题 ID/名称，进入日志主题管理页面。
4. 单击**实时消费**页签，进入实时消费配置页面。
5. 单击右侧的**编辑**，将**当前状态**的开关按钮设置为打开状态，单击**确定**。

6. 根据 CLS 给出消费的 Topic 信息，构造消费者即可。详情请参考 [Ckafka SDK](https://intl.cloud.tencent.com/document/product/597/43839)。



## 操作示例

示例：通过 Python 构造 Consumer.py
```
import uuid
from kafka import KafkaConsumer,TopicPartition,OffsetAndMetadata
consumer = KafkaConsumer(
//您的主题名称，将上图中的主题名称填写到此处      
'in-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX',  
group_id = uuid.uuid4().hex,
auto_offset_reset='earliest',
//kafka服务地址，将上图中的接入点信息填写到此处   
bootstrap_servers = ['ckafka-lweXXXXk.ap-
guangzhou.ckafka.tencentcloudmq.com:6012'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',   
//SASL信息，将kafka实例信息和用户名用#拼接填入此处，实例信息在接入点信息中   
sasl_plain_username = "ckafka-lweXXXXk#cls-2pGgXXX",
//SASL信息，将上图中的密码填入此处   
sasl_plain_password = "8uleOOPXXX",
api_version = (0,10,0)
)
print('begin')
for message in consumer:
    print('begins')
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
    print('end')
```


>? 如果数据无法消费，可能是您的服务器配置了访问限制。请在服务器上放通9092 - 9192端口（因 broker 可能会自动扩容，导致扩容后需要放通的端口增加，故需要预留充足的数量），更多详情请参考 [查看实例](https://intl.cloud.tencent.com/document/product/597/38570)。
>
