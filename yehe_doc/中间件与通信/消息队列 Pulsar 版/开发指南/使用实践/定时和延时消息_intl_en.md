## Concepts
- **Scheduled message**: after a message is sent to the server, the business may want the consumer to receive it at a later time point rather than immediately. This type of message is called "scheduled message".

- **Delayed message**: after a message is sent to the server, the business may want the consumer to receive it after a period of time rather than immediately. This type of message is called "delayed message".

Actually, scheduled message can be regarded as a special type of delayed message, which is essentially the same thing.

## Use Cases
There is no difference between implementing delay from your business code or a third-party component if your system uses a monolithic design. However, if your system has a large distributed architecture with dozens or even hundreds of microservices, implementing the delay logic through the application may result in a variety of issues, and if a node running the delay program fails, the entire delay logic will be affected.

Given this, it will be a good option to deliver delayed messages to a message queue based on their attributes, as the delay period can be calculated in a unified manner, while the retry and dead letter mechanisms ensure that messages will not get lost.

Below are some sample use cases:
- After a WeChat red packet is sent, the producer sends a message with a delay of 24 hours, and the consumer receives the message after 24 hours and determines whether the user has opened the red packet; if not, the consumer returns the red packet to the original account.
- After an order is placed for an item on a mini program, a message with a delay of 30 minutes is stored on the backend, and the consumer receives the message after 30 minutes to determine the payment result; if the order has not been paid, the consumer cancels it. This implements the logic of canceling orders not paid within 30 minutes.
- After a WeChat user sets a message as a to-do, a scheduled message can be sent, and the server receives the message and reminds the user about the to-do.



## Directions
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
		// TODO adds the method for handling the timestamp parsing failure
		e.printStackTrace();
}
```

>!
>- The time range for scheduled messages is any time point within 864,000 seconds (10 days) starting from the current time; for example, starting from 12:00 on October 1, it can be set to 12:00 on October 11 at the most.
>- Scheduled messages cannot be sent in batch mode, so you need to set the `enableBatch` parameter to `false` when creating the producer.

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
>- The time range for delayed messages is 0–864,000 seconds (0 seconds–10 days); for example, starting from 12:00 on October 1, it can be set to 864,000 seconds at the most. If a greater value is set, it will be counted as 864,000 directly, and the message will be delivered then.
>- Delayed messages cannot be sent in batch mode, so you need to set the `enableBatch` parameter to `false` when creating the producer.




## Use Instructions and Limits
- When using scheduled and delayed messages, make sure that the time on the client is in sync with the time on the server (UTC+8 Beijing time in all regions); otherwise, there will be a time difference.

- There is a precision deviation of about 1 second for scheduled and delayed messages.

- Scheduled and delayed messages do not support batch mode (i.e., batch sending), as that mode will cause message retention. To be on the safe side, you need to set the `enableBatch` parameter to `false` when creating the producer.

- The maximum number of concurrent scheduled and delayed messages in a single topic is 100,000, and after this number is exceeded, the server will stop the producer from producing these two types of messages. To prevent this, you need to pay attention to the scheduled and delayed message monitoring metrics in the console.

- The maximum time range for scheduled and delayed messages are both 10 days.

- When using scheduled messages, you need to set a time point after the current time; otherwise, the message will be sent to the consumer immediately.

- After the scheduled time point is set, the maximum message retention period will be calculated from it on; for example, if a message is scheduled for delivery after 3 days and the maximum message retention period is 7 days, then the message will be deleted if it is not consumed by the 10th day. This is also the case for delayed messages.

  

