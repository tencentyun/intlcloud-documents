## Operation Scenarios
To access CKafka over public network, you can add public routes in CKafka Console and configure SASL authentication and ACL rules to access the production and consumption messages in CKafka topics.

## Prerequisites
You have [created an instance](https://intl.cloud.tencent.com/document/product/597/32543).

## Directions

### Creating a public route

1. Click the target instance ID in the [Instance List](https://console.cloud.tencent.com/ckafka/index?rid=1) of CKafka Console to enter the instance details page.
![](https://main.qcloudimg.com/raw/047f485ed3a815974bc1f7d904e7ef14.jpg)
2. Click **Add a routing policy** on **Basic Info** -> **Access Mode** and select policy info.
 - Route type: public domain name access
 - Access mode: only SASL_PLAINTEXT is supported currently
![](https://main.qcloudimg.com/raw/46300a7b7ac8150cb033e99b1534f3d2.jpg)
3. Click **Submit**, and you will see the routing policy below the access mode.
![](https://main.qcloudimg.com/raw/75508695dfc41601ef9f98119b1decc8.jpg)




### Creating a user

1. Click **Create** on **Instance List** -> **User Management**.
![](https://main.qcloudimg.com/raw/afab16e8a50e4bbecee5b2502d0d9a9c.jpg)
2. Enter the following information in the pop-up window:
 - User Name: only contain letters, numbers, underscores, "-" and "."
 - Password: only contain letters, numbers, underscores, "-" and "."
 - Confirm Password: enter the password again
![](https://main.qcloudimg.com/raw/fa01d35b74ba9050e7e340e63b4e2efe.jpg)
3. Click **Submit**, and you will see this new user in the user management list.
![](https://main.qcloudimg.com/raw/bab585cf98974e1d3487a3b1e9084f6a.jpg)


### Adding an ACL policy

Perform ACL permission management (including read and write) on the existing topic. Only users with permissions can perform read and write permission operations on the topic.

1. Enter **Instance List** -> **ACL Policy Management**, and click **Edit ACL Policy** on the operation column of the target topic.
![](https://main.qcloudimg.com/raw/1ab398b395258a69ca2513e8c024047a.jpg)
2. Click **Create** to enter the **Add ACL Policy** page.
![](https://main.qcloudimg.com/raw/f62cf3c6262b3456440881d90710bccd.jpg)
3. Configure user and IP in the prompted **Add ACL Policy** window. If not selected, all users/hosts are supported by default.
![](https://main.qcloudimg.com/raw/647380c3617e473644eac5bae337f9b7.jpg)
4. Click **Submit**, you will see the policy show in the policy list of the target topic.
![](https://main.qcloudimg.com/raw/b1b68e42f2adafb428a593fa52d17658.jpg)

### Production and consumption over public network
After operating on the console, you can access instance resources over public network using user name and password.

#### Production
```java
Properties props = new Properties();
        //Domain name for public access, i.e. public routing address
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
        //User name and password. Note: use name is not the one on the console, but concatenated as the “instanceId#user name” instead
        props.put("sasl.jaas.config",
                "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"yourinstance#yourusername\" password=\"yourpassword\";");
        Producer<String, String> producer = new KafkaProducer<String, String>(props);
        for (int i = 0; i < 1000; i++) {
            Future<RecordMetadata> future = producer.send(new ProducerRecord<>("topic1", UUID.randomUUID().toString()));
            System.out.println("produce offset:" + future.get().offset());
        }
        producer.close();
```



#### Consumption
```java
Properties props = new Properties();
        //Domain name for public access
        props.put("bootstrap.servers", "your_public_network_route_addr");
        props.put("group.id", "yourconsumegroup");
        props.put("enable.auto.commit", "true");
        props.put("auto.commit.interval.ms", "1000");
        props.put("session.timeout.ms", "30000");
        props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
        props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
        //User name and password. Note: use name is not the one on the console, but concatenated as the “instanceId#user name” instead
        props.put("sasl.jaas.config",
                "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"yourinstance#yourusername\" password=\"yourpassword\";");

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        consumer.subscribe(Arrays.asList("foo", "bar"));
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
            for (ConsumerRecord<String, String> record : records) {
                System.out.printf("offset = %d, key = %s, value = %s", record.offset(), record.key(), record.value());
            }
        }
```

>?Except adding `sasl.jaas.config` configurations using `properties`, you can also pass in using `System.setProperty` or `-D` method.
> - System.setProperty("java.security.auth.login.config", "/etc/ckafka_client_jaas.conf");
>
```java
> KafkaClient {
> org.apache.kafka.common.security.plain.PlainLoginModule required
> username="yourinstance#yourusername"
> password="yourpassword";
> }; 
> ```

