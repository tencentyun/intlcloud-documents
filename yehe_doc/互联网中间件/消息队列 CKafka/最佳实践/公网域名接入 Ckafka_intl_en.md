## Overview
To access CKafka over a public network, you can add public routes in the CKafka console and configure SASL authentication and ACL rules to access the production and consumption messages in CKafka topics.


## Prerequisites
You have [created an instance](https://intl.cloud.tencent.com/document/product/597/40039).

## Directions

### Creating a public route

1. In the CKafka console, click your instance ID in the [Instance List](https://console.cloud.tencent.com/ckafka/index?rid=1) to enter the details page.
![](https://main.qcloudimg.com/raw/047f485ed3a815974bc1f7d904e7ef14.jpg)
2. In the **Basic Info** tab, click **Add a routing policy**, and configure the policy information as follows:
 - Route Type: Public domain name access
 - Access Mode: only SASL_PLAINTEXT is supported currently
![](https://main.qcloudimg.com/raw/46300a7b7ac8150cb033e99b1534f3d2.jpg)
3. Click **Submit**, and you will see the routing policy below the access mode.
![](https://main.qcloudimg.com/raw/75508695dfc41601ef9f98119b1decc8.jpg)




### Creating a user

1. Click your instance in the **Instance List**, select the **User Management** tab and click **Create**.
![](https://main.qcloudimg.com/raw/afab16e8a50e4bbecee5b2502d0d9a9c.jpg)
2. Enter the following information in the window that appears.
 - User Name: can contain only letters, digits, "_", "-" and "."
 - Password: can contain only letters, digits, "_", "-" and "."
 - Confirm Password: enter the password again.
![](https://main.qcloudimg.com/raw/fa01d35b74ba9050e7e340e63b4e2efe.jpg)
3. Click **Submit**, and the new user appears in the user management list.
![](https://main.qcloudimg.com/raw/bab585cf98974e1d3487a3b1e9084f6a.jpg)


### Adding an ACL policy

You can manage existing topics with ACLs (including read and write permissions) so that only authorized users can perform read and write operations on the topics.

1. Click your instance in the **Instance List**, select the **ACL Policy Management** tab, find the target topic, and click **Edit ACL Policy** in the operation column.
![](https://main.qcloudimg.com/raw/1ab398b395258a69ca2513e8c024047a.jpg)
2. Click **Create** and the ACL policy creation window appears.
![](https://main.qcloudimg.com/raw/f62cf3c6262b3456440881d90710bccd.jpg)
3. Select a user and enter an IP host. If you leave them, the policy will be applied to all users and hosts by default.
![](https://main.qcloudimg.com/raw/647380c3617e473644eac5bae337f9b7.jpg)
4. Click **Submit**, and the policy appears in the policy list of the target topic.
![](https://main.qcloudimg.com/raw/b1b68e42f2adafb428a593fa52d17658.jpg)

>? For details on SASL, ACL and user access control, see [User Access Control (User and ACL Policy Management)](https://intl.cloud.tencent.com/document/product/597/39084).

### Production and consumption over public networks
After performing the above steps, with a user name and password, you will be able to access the resources of your instance over a public network.

#### Production
```java
Properties props = new Properties();
        //Domain name for public network access, i.e. public routing address
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
        //User name and password. Note: the user name is a combination of the instance ID and the username used for the console: “`instanceId`#`username`”.
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
        //Domain name for public network access
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
        consumer.subscribe(Arrays.asList("yourtopic"));
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
            for (ConsumerRecord<String, String> record : records) {
                System.out.printf("offset = %d, key = %s, value = %s", record.offset(), record.key(), record.value());
            }
        }
```

>?Apart from adding `sasl.jaas.config` configurations using `properties`, you can also pass in configurations using `System.setProperty` or `-D`.
> - System.setProperty("java.security.auth.login.config", "/etc/ckafka_client_jaas.conf");
>- The content of the `ckafka_client_jaas.conf` file is as follows:
>
```java
KafkaClient {
	org.apache.kafka.common.security.plain.PlainLoginModule required
	username="yourinstance#yourusername"
	password="yourpassword";
}; 
```


