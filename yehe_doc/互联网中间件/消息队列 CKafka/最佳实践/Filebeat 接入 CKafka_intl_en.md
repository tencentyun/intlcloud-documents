## Filebeat Overview
[Beats](https://www.elastic.co/beats) platform hosts various single-purpose data shippers which can be used as lightweight agents after installation to send collected data from hundreds or thousands of machines to the target.
![](https://main.qcloudimg.com/raw/e48ad4b5a9d1d4576bbb5f574125b8aa.png)
Beats offers a wide variety of shippers, and you can download the one which best suits your needs. This document uses Filebeat, a lightweight log shipper, as an example to describe how to connect Filebeat to CKafka and handle common problems that may occur after the connection.


## Directions
### File configuration
Follow the steps below to configure the monitoring file:
```
#======= Filebeat prospectors ==========
filebeat.prospectors:

- input_type: log 

# This is the path to the monitoring file.
  paths:
    - /var/log/messages

#=======  Outputs =========

#------------------ kafka -------------------------------------
output.kafka:
  version:0.10.2 //Set the value to the open-source version of the CKafka instance.
  # Set to the instance address.
  hosts: ["127.1.2.3:9092"]
  # Set the target topic.
  topic: 'test'
  partition.round_robin:
    reachable_only: false

  required_acks: 1
  compression: none
  max_message_bytes: 1000000

  # The following parameters need to be configured for SASL. If SASL is not required, skip them.
  username: "instance-will#user"
  password: "password"
```

### File execution
1. Run the following command to start the client.
`sudo ./filebeat -e -c filebeat.yml`
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
If you need to configure SALS/PLAINTEXT, you need to set the username and password under Kafka configuration.
```
# The following parameters need to be configured for SASL. If SASL is not required, skip them.
  username: "instance-will#user"
  password: "password"
```

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
For example, by default, Filebeat 6.5.x runs against Kafka 0.9, 0.10, 1.1.0, or 2.0.0, while Filebeat 5.6.x runs against Kafka 0.8.2.0.

Check the version configuration in the configuration file:
```
output.kafka:
  version:0.10.2 //Set the value to the open-source version of the CKafka instance.
```
