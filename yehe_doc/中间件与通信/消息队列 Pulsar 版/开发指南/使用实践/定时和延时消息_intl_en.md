## Concepts
- **Scheduled message**: After a message is sent to the server, the business may want the consumer to receive it at a later time point rather than immediately. This type of message is called "scheduled message".

- **Delayed message**: After a message is sent to the server, the business may want the consumer to receive it after a period of time rather than immediately. This type of message is called "delayed message".

Actually, scheduled message can be regarded as a special type of delayed message, which is essentially the same thing.

## Use Cases
There is no difference between implementing delay from your business code or a third-party component if your system uses a monolithic design. However, if your system has a large distributed architecture with dozens or even hundreds of microservices, implementing the delay logic through the application may result in a variety of issues, and if a node running the delay program fails, the entire delay logic will be affected.

Given this, it will be a good option to deliver delayed messages to a message queue based on their attributes, as the delay period can be calculated in a unified manner, while the retry and dead letter mechanisms ensure that messages will not get lost.


## Directions[](id:usage)
The TDMQ for Pulsar SDK provides dedicated APIs to implement scheduled and delayed messages.
- For a scheduled message, you need to specify a moment to send it.
- For a delayed message, you need to specify a period of time as the delay.

### Scheduled message
Scheduled messages are implemented by the producer's `deliverAt()` method. Below is the sample code:
```java
String value = "message content";
try {
		// You need to convert the explicit time to a timestamp first
  	long timeStamp = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").parse("2020-11-11 00:00:00").getTime();
  	// Call the producer's `deliverAt` method to implement the scheduled message
		MessageId msgId = producer.newMessage()
				.value(value.getBytes())
				.deliverAt(timeStamp)
				.send();
} catch (ParseException e) {
		// TODO: Add the method for handling the timestamp parsing failure
		e.printStackTrace();
}
```

>!
>- The time range for scheduled messages is any time point within 864,000 seconds (ten days) starting from the current time; for example, starting from 12:00 on October 1, it can be set to 12:00 on October 11 at the most.
>- Scheduled messages cannot be sent in batch mode, so you need to set the `enableBatch` parameter to `false` when creating the producer.
>- Scheduled messages can be consumed only in the shared mode; otherwise, scheduling will not work (even in the key-shared mode).

### Delayed message
Delayed messages are implemented by the producer's `deliverAfter()` method. Below is the sample code:
```java
String value = "message content";

// You need to specify the length of the delay
long delayTime = 10L;
// Call the producer's `deliverAfter` method to implement the delayed message
MessageId msgId = producer.newMessage()
    .value(value.getBytes())
    .deliverAfter(delayTime, TimeUnit.SECONDS) // You can select a unit freely
    .send();
```

>!
>- The time range for delayed messages is 0–864,000 seconds (10 days); for example, starting from 12:00 PM on October 1, it can be set to 12:00 PM on October 11 at most.
>- Delayed messages cannot be sent in batch mode, so you need to set the `enableBatch` parameter to `false` when creating the producer.
>- Delayed messages can be consumed only in the shared mode; otherwise, delaying will not work (even in the key-shared mode).


## Use Instructions and Limits
- When using scheduled and delayed messages, make sure that the time on the client is in sync with the time on the server; otherwise, there will be a time difference.

- There is a precision deviation of about 1 second for scheduled and delayed messages.

- Scheduled and delayed messages do not support batch mode (i.e., batch sending), as that mode will cause message heap. To be on the safe side, you need to set the `enableBatch` parameter to `false` when creating the producer.

- Scheduled and delayed messages can be consumed only in the shared mode; otherwise, scheduling and delaying will not work (even in the key-shared mode).

- The maximum time range for scheduled and delayed messages are both 10 days.

- When using scheduled messages, you need to set a time point after the current time; otherwise, the message will be sent to the consumer immediately.

- After the scheduled time point is set, the maximum message retention period (i.e., TTL) will still be calculated starting from the message sending time point; for example, if the message is scheduled to be sent in two days, but the TTL of the message is set to one day, then the message will be deleted after one day. In this case, you should make sure that the TTL is longer than the scheduled time (i.e., two days); otherwise, the message will be deleted after the TTL elapses. This is also the case for delayed messages.

- In general topics, you can send scheduled and delayed messages through API as instructed in [Directions](#usage) and receive them.

  

