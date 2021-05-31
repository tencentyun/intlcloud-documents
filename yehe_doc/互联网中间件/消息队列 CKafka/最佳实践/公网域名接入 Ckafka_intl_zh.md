## 操作场景
如果您需要通过公网访问消息队列 CKafka 服务，可以通过控制台增加公网路由，并通过配置 SASL 鉴权和 ACL 规则实现公网访问 CKafka Topic 的生产和消费消息。


## 前提条件
已 [创建实例](https://intl.cloud.tencent.com/document/product/597/40039)。

## 操作步骤

### 创建公网路由

1. 在 CKafka 控制台的 [实例列表](https://console.cloud.tencent.com/ckafka/index?rid=1) 中，单击目标实例 ID，进入实例详情页。
![](https://main.qcloudimg.com/raw/047f485ed3a815974bc1f7d904e7ef14.jpg)
2. 在基本信息 - 接入方式中，单击【添加路由策略】，选择策略信息：
 - 路由类型：公网域名接入
 - 接入方式：目前只支持 SASL_PLAINTEXT
![](https://main.qcloudimg.com/raw/46300a7b7ac8150cb033e99b1534f3d2.jpg)
3. 单击【提交】，接入方式下将显示该路由策略。
![](https://main.qcloudimg.com/raw/75508695dfc41601ef9f98119b1decc8.jpg)




### 创建用户

1. 【实例列表】>【用户管理】中，单击【新建】。
![](https://main.qcloudimg.com/raw/afab16e8a50e4bbecee5b2502d0d9a9c.jpg)
2. 在新建用户的弹窗中，填写以下信息：
 - 用户名：只能包含字母、数字、下划线、“-”、“.”
 - 密码：只能包含字母、数字、下划线、“-”、“.”
 - 确认密码：再次输入密码
![](https://main.qcloudimg.com/raw/fa01d35b74ba9050e7e340e63b4e2efe.jpg)
3. 单击【提交】，新增的用户将显示在用户管理列表中。
![](https://main.qcloudimg.com/raw/bab585cf98974e1d3487a3b1e9084f6a.jpg)


### ACL 策略授权

对现有 Topic 进行 ACL 权限管理（包括读写），只有拥有权限的用户才能对 Topic 进行相关读写权限操作。

1. 【实例列表】>【ACL策略管理】中，单击目标 Topic 操作列的【编辑ACL策略】。
![](https://main.qcloudimg.com/raw/1ab398b395258a69ca2513e8c024047a.jpg)
2. 单击【新建】，进入新增 ACL 策略页面。
![](https://main.qcloudimg.com/raw/f62cf3c6262b3456440881d90710bccd.jpg)
4. 在新增 ACL 策略的弹窗中，填选配置用户及 IP，不选为默认所有用户/host 都支持。
![](https://main.qcloudimg.com/raw/647380c3617e473644eac5bae337f9b7.jpg)
5. 单击【提交】，该策略将显示在目标  Topic  的策略列表中。
![](https://main.qcloudimg.com/raw/b1b68e42f2adafb428a593fa52d17658.jpg)

>?CKafka 相关 SASL 和 ACL，用户管理访问控制详情见 [用户访问控制（ACL 与用户管理）](https://intl.cloud.tencent.com/document/product/597/39084) 文档。

### 公网生产和消费
控制台操作完成后，即可使用用户名和密码在公网访问实例资源。

#### 生产
```java
Properties props = new Properties();
        //公网接入域名地址,即公网路由地址
        props.put("bootstrap.servers", "your_public_network_route_addr");
        props.put("acks", "all");
        props.put("retries",0);
        props.put("batch.size", 16384);
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("request.timeout.ms", 10000);
        props.put("max.block.ms", 30000);
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
        props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
        //用户名密码，注：用户名是需要拼接，并非管控台的用户名：instanceId#username
        props.put("sasl.jaas.config",
                "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"yourinstance#yourusername\" password=\"yourpassword\";");
        Producer<String, String> producer = new KafkaProducer<String, String>(props);
        for (int i = 0; i < 1000; i++) {
            Future<RecordMetadata> future = producer.send(new ProducerRecord<>("topic1", UUID.randomUUID().toString()));
            System.out.println("produce offset:" + future.get().offset());
        }
        producer.close();
```



#### 消费
```java
Properties props = new Properties();
        //公网接入域名地址
        props.put("bootstrap.servers", "your_public_network_route_addr");
        props.put("group.id", "yourconsumegroup");
        props.put("enable.auto.commit", "true");
        props.put("auto.commit.interval.ms", "1000");
        props.put("session.timeout.ms", "30000");
        props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
        props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
        //用户名密码，注：用户名是需要拼接，并非管控台的用户名：instanceId#username
        props.put("sasl.jaas.config",
                "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"yourinstance#yourusername\" password=\"yourpassword\";");

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        consumer.subscribe(Arrays.asList("yourtopic"));
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
            for (ConsumerRecord<String, String> record : records) {
                System.out.printf("offset = %d, key = %s, value = %s", record.offset(), record.key(), record.value());
            }
        }
```

>?除了使用 properties 添加 sasl.jaas.config 配置的方式，您也可以通过 System.setProperty 或 -D 的方式传入。
>- System.setProperty("java.security.auth.login.config", "/etc/ckafka_client_jaas.conf");
>- `ckafka_client_jaas.conf` 文件的内容如下：
>
```java
KafkaClient {
	org.apache.kafka.common.security.plain.PlainLoginModule required
	username="yourinstance#yourusername"
	password="yourpassword";
}; 


