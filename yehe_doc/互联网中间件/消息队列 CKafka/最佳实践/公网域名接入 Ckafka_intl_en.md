## Overview

To access CKafka over the public network in case that the consumer or producer is in a self-built data center or another cloud service, you can add public routes in the CKafka console and configure SASL authentication and ACL rules to access the CKafka topics and produce/consume messages.


## Prerequisites

You have [created an instance](https://intl.cloud.tencent.com/document/product/597/39718).
You have [created a topic](https://intl.cloud.tencent.com/document/product/597/32554).

## Directions

### Creating public route

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar and click the **ID** of the target instance to enter the instance basic information page.
3. On the instance basic information page, click **Add a routing policy** in the **Access Mode** module.
   - Route Type: public domain name access
   - Access Mode: only SASL_PLAINTEXT is supported currently
  ![](https://main.qcloudimg.com/raw/65be6a54e2a2abcf1cd5c3b1507dca7d.png)
3. Click **Submit**, and you will see the routing policy below the access mode.
   ![](https://main.qcloudimg.com/raw/642337483d8e59cbdc55cb96e81faf4b.png)




### Creating user

1. On the instance basic information page, select the **User Management** tab on the top.
2. On the user management page, click **Create** and enter the username and password to create a user.
  ![](https://main.qcloudimg.com/raw/971325c47e11c07ee728f82b50d54a7b.png)
3. Click **Submit**, and you will see this new user in the user management list.
   ![](https://main.qcloudimg.com/raw/c427790899d8ff8e0d4d8f88ddd126fe.png)

### Adding ACL policy

You can manage existing topics with ACLs (including read and write permissions) so that only authorized users can perform read and write operations on the topics.

1. On the instance details page, select the **ACL Policy Management** tab at the top.
2. Click **Edit ACL Policy** in the **Operation** column of the target topic to enter the ACL policy page.
3. Click **Create** and select/enter the target users and IPs. If you don't select any, the policy will take effect for all users/hosts by default.
   ![](https://main.qcloudimg.com/raw/632c3903a52bb1c71860b1dbd40ed43a.png)
4. Click **Submit**, and the policy appears in the policy list of the target topic.
   ![](https://main.qcloudimg.com/raw/f97473b3031d97efa6ae4aeec16560d9.png)

>?For more information on SASL and ACL related to CKafka, please see [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).

### Production and consumption over public network

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
        / /Username and password. Note: the username is a combination of the instance ID and the username used for the console: instanceId#username
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
        / /Username and password. Note: the username is a combination of the instance ID and the username used for the console: instanceId#username
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
>- System.setProperty("java.security.auth.login.config", "/etc/ckafka_client_jaas.conf");
>- The content of the `ckafka_client_jaas.conf` file is as follows:

```java
KafkaClient {
	org.apache.kafka.common.security.plain.PlainLoginModule required
	username="yourinstance#yourusername"
  password="yourpassword";
}; 
```

