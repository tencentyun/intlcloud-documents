## Overview

CKafka allows you to dump messages to another CKafka cluster to sync data between CKafka clusters.

## Prerequisites

Currently, this feature relies on the SCF and CKafka services, which should be activated first before you can use this feature.

## Directions

### Dumping message[](id:1)

Message dump to CKafka will be performed with the CKafka trigger in SCF to sync messages to another CKafka cluster.

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select the **Topic Management** tab and click **Message Dump** in the **Operation** column.
4. Click **Add Message Dump** and select **CKafka** as the dump type.
    - Dump Type: select CKafka.
    - Dump Instance: pull the list of CKafka instances in the current region. If you want to dump data to an instance in another region or self-built Kafka, see [Custom dump settings](#2).
    - Dump Topic: pull the CKafka topic information of the selected instance.
    - Starting Position: the topic offset of historical messages when dumping.
    - Role Authorization: to use the SCF service, you need to grant a third-party role to perform access to related products for you.
    - SCF Authorization: indicate your consent to activating SCF and create a function. Then, you need to go to the function settings to set more advanced configuration items and view monitoring information.
5. After configuring the dump task, click **Submit**. After it is successfully created, dump will not start immediately; instead, you need to manually enable dump in the console.

### Custom dump settings

In the general creation process, dump cannot be performed directly across regions or in self-built Kafka. For such dump, you need to configure the network or delivery information for the function. The cross-region dump process is as follows:

1. [Create a CKafka dump template](#1), go to the SCF console, and configure the delivery instance and topic as needed.
   
2. Modify **Environment Variable** and **Network** settings in the function configuration.
   
   Environment variable configuration description:
   kafka_address: Kafka IP address.
   kafka_topic_name: Kafka topic name.
   
   > ?
   > - To dump CKafka data across regions, simply modify the relevant environment variables. You need to configure a **[peering connection](https://intl.cloud.tencent.com/document/product/553/18836)** for VPC.
   > - For a CVM-based self-built Kafka instance, you need to change them to the VPC and Kafka topic of the instance.
   > - For other self-built Kafka instances, you need to change the IP and topic in the environment variable to the information of the instance. If there is no Direct Connect, data needs to be transferred over the SCF public network.
   
3. Save the configurations and enable the dump feature.


## Notes

#### Access methods

SCF supports two CKafka access methods: `PLAINTEXT` and `SASL_PLAINTEXT`, which can be modified in the SCF code.

- `PLAINTEXT` access method:
```
kafka_to_kafka = KafkaToKafka(kafka_address)
```

- `SASL_PLAINTEXT` access method:
 ```
 kafka_to_kafka= KafkaToKafka(    
    kafka_address    
    security_protocol = "SASL_PLAINTEXT",     
    sasl_mechanism="PLAIN",     
    sasl_plain_username="ckafka-80o10xxx#Taborxx",     
    sasl_plain_password="Taborxxxx",     
    api_version=(0, 10, 2)     
  )    
 ```

 >?`sasl_plain_username` consists of **Instance ID** and **username** concatenated with **#**.

#### Viewing dump log and troubleshooting

CKafka dump capabilities are implemented based on SCF, and you can find relevant dump information and status in the SCF log.

## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings.
- The `CKafkaToCKafka` scheme uses the CKafka trigger. For more information on related settings such as retry policy and maximum number of messages, see [CKafka Trigger](https://intl.cloud.tencent.com/document/product/583/17530).
- When the dump to CKafka feature is used, the dumped messages are the `offset` and `msgBody` data of the CKafka trigger by default. If you want to process the logic by yourself, see [Event Message Structure for CKafka Trigger](https://intl.cloud.tencent.com/document/product/583/17530#ckafka-.E8.A7.A6.E5.8F.91.E5.99.A8.E7.9A.84.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF.E7.BB.93.E6.9E.84). 
- This feature is provided based on the SCF service that provides a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). For more information on the fees for excessive usage, see the [billing rules](https://intl.cloud.tencent.com/document/product/583/17299) of SCF.
