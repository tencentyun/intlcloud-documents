## Overview
[Beats](https://www.elastic.co/cn/products/beats) platform hosts various single-purpose data shippers which can be used as lightweight agents after installation to send collected data from hundreds or thousands of machines to the target.
![](https://main.qcloudimg.com/raw/e48ad4b5a9d1d4576bbb5f574125b8aa.png)
Beats offers a wide variety of shippers. You can download the most appropriate one based on your needs.
![](https://main.qcloudimg.com/raw/c054b3a90fbc7d8ede9082778fce5deb.png)


## Configuration File
```
#======= Filebeat prospectors ==========

filebeat.prospectors:

- input_type: log 

# Here is the path to the listener file
  paths:
    - /var/log/messages

#=======  Outputs =========

#------------------ kafka -------------------------------------
output.kafka:
  # Set as the instance address
  hosts: ["127.1.2.3:9092"]
  # Set the target topic
  topic: 'test'
  partition.round_robin:
    reachable_only: false

  required_acks: 1
  compression: none
  max_message_bytes: 1000000

  # The following information needs to be configured for SASL. If not required, they can be ignored.
  username: "instance-will#user"
  password: "password"
```

## Run
1. Run the following command to start the client.
`sudo ./filebeat -e -c filebeat.yml `
2. Add data to the listener file (the example here is a testlog file written to the listener).
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


### SASL/PLAINTEXT Mode
If you need to configure SALS/PLAINTEXT, you need to set the username and password under Kafka configuration.
```
# The following information needs to be configured for SASL. If not required, they can be ignored.
  username: "instance-will#user"
  password: "password"
```
