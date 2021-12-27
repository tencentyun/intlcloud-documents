This document describes the feature, use cases, and usage of message filtering in TDMQ for RocketMQ.

## Feature Overview

In message filtering, a message producer configures message attributes to group messages before sending them to a topic, and a consumer subscribed to the topic uses message attributes to filter the messages so that only eligible messages are delivered to the consumer for consumption.

If a consumer sets no filter conditions when subscribing to a topic, no matter whether filter attributes are set during message sending, all messages in the topic will be delivered to the consumer for consumption.

## Use Cases

Generally, messages with the same business attributes are stored in the same topic; for example, when an order transaction topic contains messages of order placement transactions, payment transactions, and delivery transactions, and if you want to consume only one type of transaction messages in your business, you can filter them on the client, but this will waste bandwidth resources.

To solve this problem, TDMQ supports filtering on the broker. You can set one or more tags during message production and subscribe to specified tags during consumption.

![](https://main.qcloudimg.com/raw/32953b29d96dce605fa4a1598b3f5146.png)

## Usage

### Sending message

You must specify tags for each message when sending it.

```java
Message msg = new Message("TOPIC","TagA","Hello world".getBytes());                
```

### Subscribing to message

- Subscribe to all tags: 
If a consumer wants to subscribe to all types of messages under a topic, an asterisk (*) can be used to represent all tags.
```java
    consumer.subscribe("TOPIC", "*", new MessageListener() {
        public Action consume(Message message, ConsumeContext context) {
            System.out.println(message.getMsgID());
            return Action.CommitMessage;
        }
    });                
```

- Subscribe to one tag: 
If a consumer wants to subscribe to a certain type of messages under a topic, the tag should be specified clearly.
```java
    consumer.subscribe("TOPIC", "TagA", new MessageListener() {
        public Action consume(Message message, ConsumeContext context) {
            System.out.println(message.getMsgID());
            return Action.CommitMessage;
        }
    });                
```

- Subscribe to multiple tags:
If a consumer wants to subscribe to multiple types of messages under a topic, two vertical bars (||) should be added between two tags for separation.
```java
    consumer.subscribe("TOPIC", "TagA||TagB", new MessageListener() {
        public Action consume(Message message, ConsumeContext context) {
            System.out.println(message.getMsgID());
            return Action.CommitMessage;
        }
    });                      
```
