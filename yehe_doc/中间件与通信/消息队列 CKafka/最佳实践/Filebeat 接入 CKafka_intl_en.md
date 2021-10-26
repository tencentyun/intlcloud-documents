[Beats](https://www.elastic.co/beats) platform hosts various single-purpose data shippers which can be used as lightweight agents after installation to send collected data from hundreds or thousands of machines to the target.
![](https://main.qcloudimg.com/raw/e48ad4b5a9d1d4576bbb5f574125b8aa.png)
Beats offers a wide variety of shippers, and you can download the one which best suits your needs. This document uses Filebeat, a lightweight log shipper, as an example to describe how to connect Filebeat to CKafka and handle common problems that may occur after the connection.

## Prerequisites

- Download and install Filebeat (for more information, please see [Installing Logstash](https://www.elastic.co/guide/en/logstash/7.6/installing-logstash.html))
- Download and install JDK 8 (for more information, please see [Java SE Development Kit 8 Downloads](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html))
- You have [created a CKafka instance](https://intl.cloud.tencent.com/document/product/597/39718)

## Directions

### Step 1. Get the CKafka instance access address

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar and click the **ID** of the target instance to enter its basic information page.
3. On the instance basic information page, get the instance access address in the **Access Mode** module.
     ![](https://main.qcloudimg.com/raw/fea1f55c3cf311d1393347853cf183fc.png)

### Step 2. Create a topic

1. On the instance's basic information page, select the **Topic Management** tab on the top.
2. On the topic management page, click **Create** to create a topic named `test`.
    ![](https://main.qcloudimg.com/raw/bd8fb967eb2e46f14cee52c3a34014e2.png)

### Step 3. Prepare the configuration file

Enter the installation directory of Filebeat and create the configuration monitoring file `filebeat.yml`.
<dx-codeblock>
:::  yaml
#======= For versions after Filebeat 7.x, change `filebeat.prospectors` to `filebeat.inputs` =======
filebeat.prospectors:

- input_type: log 

# This is the path to the monitoring file.
  paths:
    - /var/log/messages

#=======  Outputs =========

#------------------ kafka -------------------------------------
output.kafka:
  version:0.10.2 //Set the value to the open-source version of the CKafka instance.
  # Set to the access address of the CKafka instance
  hosts: ["xx.xx.xx.xx:xxxx"]
  # Set the name of the target topic
  topic: 'test'
  partition.round_robin:
    reachable_only: false

  required_acks: 1
  compression: none
  max_message_bytes: 1000000

  # The following parameters need to be configured for SASL. If SASL is not required, skip them.
  username: "yourinstance#yourusername"  // `username` should consist of the instance ID and username
  password: "yourpassword"
:::
</dx-codeblock>


### Step 4. Send a message in Filebeat

1. Run the following command to start the client:
	```
	sudo ./filebeat -e -c filebeat.yml 
	```
2. Add data to the monitoring file (for example: `testlog`).
	```
	echo ckafka1 >> testlog
	echo ckafka2 >> testlog
	echo ckafka3 >> testlog
	```

3. Start the consumer to consume the corresponding topic and get the following data.
	```
	{"@timestamp":"2017-09-29T10:01:27.936Z","beat":{"hostname":"10.193.9.26","name":"10.193.9.26","version":"5.6.2"},"input_type":"log","message":"ckafka1","offset":500,"source":"/data/ryanyyang/hcmq/beats/filebeat-5.6.2-linux-x86_64/testlog","type":"log"}
	{"@timestamp":"2017-09-29T10:01:30.936Z","beat":{"hostname":"10.193.9.26","name":"10.193.9.26","version":"5.6.2"},"input_type":"log","message":"ckafka2","offset":508,"source":"/data/ryanyyang/hcmq/beats/filebeat-5.6.2-linux-x86_64/testlog","type":"log"}
	{"@timestamp":"2017-09-29T10:01:33.937Z","beat":{"hostname":"10.193.9.26","name":"10.193.9.26","version":"5.6.2"},"input_type":"log","message":"ckafka3","offset":516,"source":"/data/ryanyyang/hcmq/beats/filebeat-5.6.2-linux-x86_64/testlog","type":"log"}
	```

### SASL/PLAINTEXT mode

If you want to configure SASL/PLAINTEXT, you need to set the username and password under the Kafka configuration.
<dx-codeblock>
:::  yaml
 # The following parameters need to be configured for SASL. If SASL is not required, skip them.
  username: "yourinstance#yourusername"  // `username` should consist of the instance ID and username
  password: "yourpassword"
:::
</dx-codeblock>


## FAQs

The Filebeat log file (default path: `/var/log/filebeat/filebeat`) contains a large number of INFO logs as follows:

```
2019-03-20T08:55:02.198+0800    INFO    kafka/log.go:53 producer/broker/544 starting up
2019-03-20T08:55:02.198+0800    INFO    kafka/log.go:53 producer/broker/544 state change to [open] on wp-news-filebeat/4
2019-03-20T08:55:02.198+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/4 selected broker 544
2019-03-20T08:55:02.198+0800    INFO    kafka/log.go:53 producer/broker/478 state change to [closing] because EOF
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 Closed connection to broker bitar1d12:9092
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/5 state change to [retrying-3]
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/4 state change to [flushing-3]
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/5 abandoning broker 478
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/2 state change to [retrying-2]
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/2 abandoning broker 541
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/leader/wp-news-filebeat/3 state change to [retrying-2]
2019-03-20T08:55:02.199+0800    INFO    kafka/log.go:53 producer/broker/478 shut down
```

This problem may be related to the Filebeat version. Products in the Elastic family are updated frequently, and major version incompatibility problems often occur.
For example, v6.5.x supports Kafka v0.9, v0.10, v1.1.0, and v2.0.0 by default, while v5.6.x supports Kafka v0.8.2.0 by default.

Check the version configuration in the configuration file:
<dx-codeblock>
:::  yaml
output.kafka:
  version:0.10.2 //Set the value to the open-source version of the CKafka instance.
:::
</dx-codeblock>

