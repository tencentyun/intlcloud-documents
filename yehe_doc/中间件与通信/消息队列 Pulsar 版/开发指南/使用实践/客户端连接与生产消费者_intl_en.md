This document describes the relationship between the TDMQ for Pulsar client and connection and between the client and producer/consumer, as well as how to use the client reasonably for higher efficiency and stability.

>**Core principles:**
>- One PulsarClient is sufficient for one process.
>- Producers and consumers are thread-safe. They can be reused and are recommended to be reused for the same topic.

## Client and Connection

The TDMQ for Pulsar client (PulsarClient) is a basic unit that connects an application to TDMQ for Pulsar, and one PulsarClient corresponds to one TCP connection. Generally, one application or process on the user side uses one PulsarClient, and the number of clients is equal to the number of application nodes. If an application node of the TDMQ for Pulsar service is unused for a long time, its client should be repossessed to reduce the resource usage (currently, the connection limit in TDMQ for Pulsar is 2,000 client connections per topic).



## Client and Producer/Consumer

You can create multiple producers and consumers under one client to increase the production and consumption speeds. A common approach is to use multiple threads to create multiple producer or consumer objects for production and consumption under one client and isolate data between different producers and consumers.

Currently, the limits on the number of producers/consumers in TDMQ for Pulsar are as follows:
- Up to 1,000 producers per topic.
- Up to 500 consumers per topic.



## Best Practice

The number of producers/consumers does not necessarily depend on the business object. They can be reused and are uniquely identified by name.

### Producer

If 1,000 business objects are producing messages simultaneously, it is not necessary to create 1,000 producers. As long as the application nodes deliver messages to the same topic, they can use the same producer for production (singleton mode). In this case, one single producer can often use up the hardware configuration of each application node.

Below is the sample code in Java for message production.
<dx-codeblock>
:::  java
// Get the `serviceURL` access address, token, full topic name, and subscription name from the configuration file (all of which can be copied from the console)
@Value("${tdmq.serviceUrl}")
private String serviceUrl;
@Value("${tdmq.token}")
private String token;
@Value("${tdmq.topic}")
private String topic;

// Declare a client object and producer object
private PulsarClient pulsarClient;
private Producer<String> producer;

// Create client and producer objects in an initialization program
public void init() throws Exception {
    pulsarClient = PulsarClient.builder()
            .serviceUrl(serviceUrl)
            .authentication(AuthenticationFactory.token(token))
            .build();
    producer = pulsarClient.newProducer(Schema.STRING)
            .topic(topic)
            .create();
}
:::
</dx-codeblock>


Directly import the `producer` for message sending in the business logic of message production.
<dx-codeblock>
:::  java
// Directly import the following code into the business logic of message production. Note that the schema type declared by the producer through the paradigm must match the object passed in
public void onProduce(Producer<String> producer){
    // Add the business logic
    String msg = "my-message";// Simulate getting a message from the business logic
    try {
        // Schema verification is enabled in TDMQ for Pulsar by default. The message object must match the schema type declared by the producer
        MessageId messageId = producer.newMessage()
              .key("msgKey")
          		.value(msg)
          		.send();
        System.out.println("delivered msg " + msgId + ", value:" + value);
    } catch (PulsarClientException e) {
      	System.out.println("delivered msg failed, value:" + value);
      	e.printStackTrace();
    }
}

public void onProduceAsync(Producer<String> producer){
    // Add the business logic
    String msg = "my-asnyc-message";// Simulate getting a message from the business logic
    // Send the message asynchronously, which avoids thread jamming and improves the sending speed
    CompletableFuture<MessageId> messageIdFuture = producer.newMessage()
          .key("msgKey")
      		.value(msg)
      		.sendAsync();
    // Check whether the message has been sent successfully from the async callback
    messageIdFuture.whenComplete(((messageId, throwable) -> {
        if( null != throwable ) {
            System.out.println("delivery failed, value: " + msg );
            // You can add the logic of delayed retry here
        } else {
            System.out.println("delivered msg " + messageId + ", value:" + msg);
        }
    }));
}
:::
</dx-codeblock>


When a producer is not used for a long time, you need to call the `close` method to disable it so as to avoid resource usage. When a client instance is not used for a long time, you also need to call the `close` method to disable it; otherwise, the connection pool may be used up.
<dx-codeblock>
:::  java
public void destroy(){
    if (producer != null) {
        producer.close();
    }
    if (pulsarClient != null) {
        pulsarClient.close();
    }
}
:::
</dx-codeblock>


### Consumer

Like producers, consumers are recommended to be used in singleton mode, and a single consumption node needs only one client instance and one consumer instance. Generally, the consumption performance bottleneck of a message queue lies in the process where the consumer handles messages according to its own business logic, but not in the action of receiving messages. Therefore, when the consumption performance is insufficient, check the consumer's network bandwidth usage first. If the upper limit is not reached as seen from the trend, you should analyze the message processing duration based on the logs and message trace information first.


>!
>- In shared or key-shared mode, the number of consumers is not necessarily less than or equal to the number of partitions. A module on the server responsible for delivering messages will deliver the messages to all consumers in a particular way (round robin by default in shared mode and round robin in the same key by default in key-shared mode).
>- In shared mode, if production is suspended on the producer, messages at the end may be distributed unevenly.
>- When multithreaded consumption is used, even if one consumer object is reused, the order of messages cannot be guaranteed.

Below is the complete sample code in Java for multithreaded consumption by using a thread pool based on the Spring Boot framework.
<dx-codeblock>
:::  java
import org.apache.pulsar.client.api.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

@Service
public class ConsumerService implements Runnable {

    // Get the `serviceURL` access address, token, full topic name, and subscription name from the configuration file (all of which can be copied from the console)
    @Value("${tdmq.serviceUrl}")
    private String serviceUrl;
    @Value("${tdmq.token}")
    private String token;
    @Value("${tdmq.topic}")
    private String topic;
    @Value("${tdmq.subscription}")
    private String subscription;

    private volatile boolean start = false;
    private PulsarClient pulsarClient;
    private Consumer<String> consumer;
    private static final int corePoolSize = 10;
    private static final int maximumPoolSize = 10;

    private ExecutorService executor;
    private static final Logger logger = LoggerFactory.getLogger(ConsumerService.class);

    @PostConstruct
    public void init() throws Exception {
        pulsarClient = PulsarClient.builder()
                .serviceUrl(serviceUrl)
                .authentication(AuthenticationFactory.token(token))
                .build();
        consumer = pulsarClient.newConsumer(Schema.STRING)
                .topic(topic)
                //.subscriptionType(SubscriptionType.Shared)
                .subscriptionName(subscription)
                .subscribe();
        executor = new ThreadPoolExecutor(corePoolSize, maximumPoolSize, 0, TimeUnit.SECONDS, new ArrayBlockingQueue<>(100),
                new ThreadPoolExecutor.AbortPolicy());
        start = true;
    }

    @PreDestroy
    public void destroy() throws Exception {
        start = false;
        if (consumer != null) {
            consumer.close();
        }
        if (pulsarClient != null) {
            pulsarClient.close();
        }
        if (executor != null) {
            executor.shutdownNow();
        }
    }

    @Override
    public void run() {
        logger.info("tdmq consumer started...");
        for (int i = 0; i < maximumPoolSize; i++) {
            executor.submit(() -> {
                while (start) {
                    try {
                        Message<String> message = consumer.receive();
                        if (message == null) {
                            continue;
                        }
                        onConsumer(message);
                    } catch (Exception e) {
                        logger.warn("tdmq consumer business error", e);
                    }
                }
            });
        }
        logger.info("tdmq consumer stopped...");
    }

    /**
     * Write the consumption business logic here
     *
     * @param message
     * @return return true: message ack; return false: message nack
     * @throws Exception Message nack
     */
    private void onConsumer(Message<String> message) {
        // Business logic of delay operation
        try {
            System.out.println(Thread.currentThread().getName() + " - message receive: " + message.getValue());
            Thread.sleep(1000);// Simulate business logic processing
            consumer.acknowledge(message);
            logger.info(Thread.currentThread().getName() + " - message processing succeed:" + message.getValue());
        } catch (Exception exception) {
            consumer.negativeAcknowledge(message);
            logger.error(Thread.currentThread().getName() + " - message processing failed:" + message.getValue());
        }
    }
}
:::
</dx-codeblock>





