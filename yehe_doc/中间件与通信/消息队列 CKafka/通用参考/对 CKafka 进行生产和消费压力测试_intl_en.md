## Testing Tool
The open-source script of the Kafka client can be used for Kafka producer and consumer performance testing. Test results are displayed mainly based on the size of messages sent per second (MB/second) and the number of messages sent per second (records/second).
- Kafka producer test script: `$KAFKA_HOME/bin/kafka-producer-perf-test.sh`
- Kafka consumer test script: `$KAFKA_HOME/bin/kafka-consumer-perf-test.sh`


## Testing Command
>?The `ckafka vip:vport` in the following sample commands should be replaced by the actual IP and port assigned for your instance.

Sample command for production testing:
```
bin/kafka-producer-perf-test.sh   
--topic test 
--num-records 123 
--record-size 1000  
--producer-props bootstrap.servers= ckafka vip : port 
--throughput 20000   
```

Sample command for consumption testing:
```
bin/kafka-consumer-perf-test.sh   
--topic test 
--new-consumer  
--fetch-size 10000 
--messages 1000  
--broker-list bootstrap.servers=ckafka vip : port
```

## Suggestions
- We recommend you create three or more partitions to increase throughput. This is because there must be at least three CKafka cluster nodes at the backend. If only one partition is created, it will be distributed in a single broker, which will affect CKafka performance.     
- As messages in each CKafka partition are ordered, the production performance will be affected if there are too many partitions. We recommend you create up to six partitions.
- It is necessary to simulate concurrency with multiple clients to ensure the testing effect. We recommend you use multiple test servers as the pressure test clients (producers) and start multiple pressure test programs on each test server to increase concurrency. To avoid the high load of test servers, you are also recommended to start one producer every second rather than all producers simultaneously.  

