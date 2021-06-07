## Generating Data
### By Java code
```
@Component
@Slf4j
public class KafkaProducer {

    @Autowired
    private KafkaTemplate<String, Object> kafkaTemplate;

    // Custom topics.
    public static final String TOPIC_TEST = "topic.test";

    //
    public static final String TOPIC_GROUP1 = "topic.group1";

    //
    public static final String TOPIC_GROUP2 = "topic.group2";

    public void send(Object obj) {
        String obj2String = JSONObject.toJSONString(obj);
        log.info("the message to send: {}", obj2String);
        // Send a message.
        ListenableFuture<SendResult<String, Object>> future = kafkaTemplate.send(TOPIC_TEST, obj);
        future.addCallback(new ListenableFutureCallback<SendResult<String, Object>>() {
            @Override
            public void onFailure(Throwable throwable) {
                // Returned result for failed sending
                log.info(TOPIC_TEST + " - the producer failed to send the message:" + throwable.getMessage());
            }

            @Override
            public void onSuccess(SendResult<String, Object> stringObjectSendResult) {
                // Returned result for successful sending
                log.info(TOPIC_TEST + " - the producer sent the message successfully:" + stringObjectSendResult.toString());
            }
        });
    }
}
```

### By command
```
bin/kafka-console-producer.sh --broker-list node86:9092 --topic t_cdr
```

## Consuming Data
### By Java code
```
@Component
@Slf4j
public class KafkaConsumer {

    @KafkaListener(topics = KafkaProducer.TOPIC_TEST, groupId = KafkaProducer.TOPIC_GROUP1)
    public void topic_test(ConsumerRecord<?, ?> record, Acknowledgment ack, @Header(KafkaHeaders.RECEIVED_TOPIC) String topic) {

        Optional message = Optional.ofNullable(record.value());
        if (message.isPresent()) {
            Object msg = message.get();
            log.info("topic_test consumed: Topic:" + topic + ",Message:" + msg);
            ack.acknowledge();
        }
    }

    @KafkaListener(topics = KafkaProducer.TOPIC_TEST, groupId = KafkaProducer.TOPIC_GROUP2)
    public void topic_test1(ConsumerRecord<?, ?> record, Acknowledgment ack, @Header(KafkaHeaders.RECEIVED_TOPIC) String topic) {

        Optional message = Optional.ofNullable(record.value());
        if (message.isPresent()) {
            Object msg = message.get();
            log.info("topic_test1 consumed: Topic:" + topic + ",Message:" + msg);
            ack.acknowledge();
        }
    }
}
```
 
### By command
```
bin/kafka-console-consumer.sh --zookeeper node01:2181 --topic t_cdr --from-beginning
```

### Adding a topic (by command)
```
bin/kafka-topics.sh --zookeeper node01:2181 --create --topic t_cdr --partitions 30  --replication-factor 2
```
For more information, see [Kafka Documentation](https://kafka.apache.org/11/documentation.html).

