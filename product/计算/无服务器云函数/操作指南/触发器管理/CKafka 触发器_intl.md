You can write an SCF function to handle a message received in CKafka. The SCF backend can consume the message in CKafka as a consumer and pass it to the SCF function.

Characteristics of CKafka triggers:

- **Pull model**: The backend module of SCF acts as a consumer, connects to the CKafka instance, and consumes the message. When the backend module gets the message, it encapsulates the message into data structures and calls the specified function to pass the message data to the function.
- **Async call**: A CKafka trigger always calls a function asynchronously, and the result is not returned to the caller. For more information about calling types, see [Calling Types](https://cloud.tencent.com/document/product/583/9694#.E8.B0.83.E7.94.A8.E7.B1.BB.E5.9E.8B).

## CKafka Trigger Configurations

- CKafka instance: Configure the CKafka instance you want to connect to. It can only be an instance in the same region.
- Topic: It can be an existing topic in the CKafka instance.
- Maximum messages: The maximum number of messages that can be pulled and batch delivered to the current function in one time. According to the message size and writing speed, the number of messages delivered when the function is triggered each time may not always reach the maximum number; instead, it is a variable value between 1 and the maximum number.

## CKafka Consumption and Message Delivery

CKafka does not push messages actively. The consumer needs to pull messages and consume them. Therefore, when a CKafka trigger is configured, the SCF backend launches a CKafka consumer module as the consumer to creates an independent consumer group in CKafka to consume messages.

After consuming messages, the SCF backend consumer module encapsulates them into an event structure according to timeout, quantity of accumulated messages and maximum number of messages, and then sends it to the cloud function. In this process, the number of encapsulated messages is different in each event structure, which ranges from **1 to the maximum number**. If the maximum number of messages is too large, there may be cases where the number of messages in the event structure will never reach the maximum number.

After the event content is obtained by the function, each message is guaranteed to be handled by loop handling, and it should not be assumed that the number of messages passed each time is constant.

## Event Message Structure for CKafka Trigger

When the specified CKafka topic receives a message, the backend consumer module of SCF will consume the message and encapsulate the message into an event in JSON format like the one below, which triggers the bound function and pass the data content as input parameters to the function.

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

| Parameter name| Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list |
| Ckafka | This identifies the event source as CKafka |
| topic | Message source topic |
| partition | Partition ID of the message source |
| offset | Consumption offset number |
| msgKey | Message key |
| msgBody | Message content |
