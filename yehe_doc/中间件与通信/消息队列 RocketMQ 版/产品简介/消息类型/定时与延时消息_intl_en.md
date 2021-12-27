This document describes the concepts and usage of scheduled message and delayed message in TDMQ for RocketMQ.

## Concepts

- **Scheduled message**: after a message is sent to the server, the business may want the consumer to receive it at a later time point rather than immediately. This type of message is called "scheduled message".
- **Delayed message**: after a message is sent to the server, the business may want the consumer to receive it after a period of time rather than immediately. This type of message is called "delayed message".

Actually, delayed message can be regarded as a special type of scheduled message, which is essentially the same thing.

## Usage

Apache RocketMQ does not provide an API for you to freely set the delay time. In order to ensure compatibility with the open-source RocketMQ client, TDMQ for RocketMQ has designed a method to specify the message sending time by adding the property key-value pair to the message. You only need to add the `__STARTDELIVERTIME` property value to the `property` of the message that needs to be sent at a scheduled time (within 40 days). For delayed messages, you can first calculate the time point for scheduled sending and then send them as scheduled messages.

A code sample is given below to show how to use scheduled and delayed messages in TDMQ for RocketMQ. You can also [view the complete sample code >>](https://github.com/streamnative/rop/blob/master/examples/src/main/java/org/streamnative/rocketmq/example/delaymessage/DelayProduceDemo.java)

### Scheduled message

To send a scheduled message, simply write a standard millisecond timestamp to the `__STARTDELIVERTIME` property before sending it.

```java
Message msg = new Message("test-topic", ("message content").getBytes(StandardCharsets.UTF_8));
// Set the message to be sent at 00:00:00 on 2021-10-01
try {
    long timeStamp = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").parse("2021-10-01 00:00:00").getTime();
    // Set `__STARTDELIVERTIME` into the property of `msg`
    msg.putUserProperty("__STARTDELIVERTIME", String.valueOf(timeStamp));
    SendResult result = producer.send(msg);
    System.out.println("Send delay message: " + result);
} catch (ParseException e) {
    // TODO adds the method for handling the timestamp parsing failure
    e.printStackTrace();
}
```

### Delayed message

For a delayed message, its scheduled sending time point is first calculated by `System.currentTimeMillis() + delayTime`, and then it is sent as a scheduled message.

```java
Message msg = new Message("test-topic", ("message content").getBytes(StandardCharsets.UTF_8));

// Set the message to be sent after 10 seconds
long delayTime = System.currentTimeMillis() + 10000;
// Set `__STARTDELIVERTIME` into the property of `msg`
msg.putUserProperty("__STARTDELIVERTIME", String.valueOf(delayTime));

SendResult result = producer.send(msg);
System.out.println("Send delay message: " + result);
```



## Use Limits

- When using delayed messages, make sure that the time on the client is in sync with the time on the server (UTC+8 Beijing time in all regions); otherwise, there will be a time difference.
- There is a precision deviation of about 1 second for scheduled and delayed messages.
- The maximum time range for scheduled and delayed messages are both 40 days.
- When using scheduled messages, you need to set a time point after the current time; otherwise, the message will be sent to the consumer immediately.
- Delayed message in TMDQ for RocketMQ is not compatible with delayed message of RocketMQ ONS client, but they achieve the same results.
