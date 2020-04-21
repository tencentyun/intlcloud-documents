You can write an SCF function to handle messages received in CKafka. The SCF backend can consume the messages in CKafka as a consumer and pass them to the function.

Characteristics of CKafka triggers:

- **Pull model**: the backend module of SCF acts as a consumer, connects to the CKafka instance, and consumes messages. When the backend module gets the message, it will encapsulate the message into data structures and invoke the specified function to pass the message data to the function.
- **Sync invocation**: a CKafka trigger always invokes a function synchronously. For more information on invocation types, please see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).
>If an error such an overrun or platform exception occurs while invoking a function, the CKafka trigger will continue to retry the exceptional event in an exponential backoff manner until it succeeds.


## CKafka Trigger Attributes

- **CKafka instance**: configure the CKafka instance you want to connect to. It can only be an instance in the same region as the function.
- **Topic**: it can be an existing topic in the CKafka instance.
- **Maximum messages**: the maximum number of messages that can be pulled and batch delivered to the current function at a time. According to the message size and writing speed, the number of messages delivered when the function is triggered each time may not always reach the maximum number; instead, it is a variable value between 1 and the maximum number.

## CKafka Consumption and Message Delivery

CKafka does not push messages actively. The consumer needs to pull messages and consume them. Therefore, if a CKafka trigger is configured, the SCF backend will launch a CKafka consumption module as the consumer to create an independent consumer group in CKafka for message consumption.

After consuming messages, the SCF backend consumption module will encapsulate them into event structures according to timeout, quantity of accumulated messages, and maximum number of messages, and then send them to the function. In this process, the number of encapsulated messages is different in each event structure, which ranges from **1 to the maximum number**. If the maximum number of messages is too high, there may be cases where the number of messages in an event structure will never reach the maximum number.

After the event content is obtained by the function, each message will be guaranteed for processing by loop handling, and it should not be assumed that the number of messages passed each time is constant.

## Event Message Structure for CKafka Trigger

When the specified CKafka topic receives a message, the backend consumption module of SCF will consume the message and encapsulate it into an event in JSON format like the one below, which will trigger the bound function and pass the data content as input parameters to the function.
```
{
  "Records": [
    {
      "Ckafka": {
        "topic": "test-topic",
        "partition":1,
        "offset":36,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka!"
      }
    },
    {
      "Ckafka": {
        "topic": "test-topic",
        "partition":1,
        "offset":37,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka again!"
      }
    }
  ]
}
```

The data structures are detailed as below:

| Structure Name| Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list |
| Ckafka | Identifies the event source as CKafka |
| topic | Message source topic |
| partition | Partition ID of message source |
| offset | Consumption offset number |
| msgKey | Message key |
| msgBody | Message content |
