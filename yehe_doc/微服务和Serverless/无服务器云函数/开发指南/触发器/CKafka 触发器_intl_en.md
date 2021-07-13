You can write an SCF function to process messages received in the specific CKafka instance. The SCF backend can consume the messages in CKafka as a consumer and pass them to the function.

Characteristics of CKafka triggers:

- **Pull model**: the backend module of SCF acts as a consumer, connects to the CKafka instance, and consumes messages. When the backend module gets the message, it will encapsulate the message into data structures and invoke the specified function to pass the message data to the function.
- **Sync invocation**: a CKafka trigger always invokes a function synchronously. For more information on invocation types, please see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).
>?
>- For execution errors (including user code errors and runtime errors), the CKafka trigger will retry according to the configured retry times, which is 10,000 by default.
>- For system errors, the CKafka trigger will continue to retry in an exponential backoff manner until it succeeds.


## CKafka Trigger Attributes

- **CKafka instance**: configure the CKafka instance you want to connect to. It can only be an instance in the same region as the function.
- **Topic**: it can be an existing topic in the CKafka instance (only topics without ACL are supported).
- **Maximum messages**: the maximum number of messages that can be pulled and batch delivered to the current function at a time, which can be up to 10,000 currently. According to the message size and writing speed, the number of messages delivered when the function is triggered each time may not always reach the maximum number; instead, it is a variable value between 1 and the maximum number.
- **Start Point**: the start position from which the trigger consumes messages. Valid values: latest (default), oldest, specified time point.
- **Retry Attempts**: the maximum number of retries when an error occurs during function execution (including user code errors and runtime errors).


## CKafka Consumption and Message Delivery

CKafka does not push messages actively. The consumer needs to pull messages and consume them. Therefore, if a CKafka trigger is configured, the SCF backend will launch a CKafka consumption module as the consumer to create an independent consumer group in CKafka for message consumption.

After consuming messages, the SCF backend consumption module will encapsulate them into event structures according to the **timeout period**, **accumulated messages**, and **maximum messages** and then initiate function invocation (sync invocation). Applicable limits are as follows:
- **Timeout period**: the current timeout period of the consumption module on the backend of SCF is 60 seconds, which avoids waiting for too long before consuming. For example, if the CKafka topic has very few messages written in, and the consumption module fails to collect the configured maximum number of messages in 60 seconds, then the function invocation will still be initiated.
- **Event size limit for sync invocation**: 6 MB. For more information, please see [Limits](https://intl.cloud.tencent.com/document/product/583/11637). If the messages in the CKafka topic are large (for example, one single message is over 6 MB in size), then due to the 6 MB limit for sync invocation, there will be only one message in the event structure passed to the function instead of the user-configured maximum number of messages.
- **Maximum messages**: this is the same as the user-defined CKafka trigger attribute, which can be up to 10,000 currently.

The consumption module on the backend of SCF will loop this process and ensure the order of message consumption, that is, the next batch of messages will be consumed only after the previous batch is completely consumed (sync invocation).
>?
>- In this process, the number of encapsulated messages is different in each event structure, which ranges from **1 to the maximum number**. If the maximum number of messages is too high, there may be cases where the number of messages in an event structure will never reach the maximum number.
>- After the event content is obtained by the function, each message can be guaranteed for processing by loop handling, and it should not be assumed that the number of messages passed each time is constant.




## Event Message Structure for CKafka Trigger

When the specified CKafka topic receives a message, the backend consumption module of SCF will consume the message and encapsulate it into an event in JSON format like the one below, which will trigger the bound function and pass the data content as input parameters to the function.
```
{
  "Records": [
    {
      "Ckafka": {
        "topic": "test-topic",
        "Partition":1,
        "offset":36,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka!"
      }
    },
    {
      "Ckafka": {
        "topic": "test-topic",
        "Partition":1,
        "offset":37,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka again!"
      }
    }
  ]
}
```

The data structures are as detailed below:

| Structure | Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list |
| Ckafka | Identifies the event source as CKafka |
| topic | Message source topic |
| partition | Partition ID of message source |
| offset | Consumption offset number |
| msgKey | Message key |
| msgBody | Message content |

## FAQs
### What should I do if a lot of CKafka messages heap up?
If a CKafka trigger is configured, the SCF backend will launch a CKafka consumption module as the consumer to create an independent consumer group in CKafka for message consumption. In addition, the number of consumption modules is equal to the number of partitions in the CKafka topic.

If a lot of CKafka messages heap up, you need to increase the consumption capability in the following ways:
* Increase the number of partitions of the CKafka topic. The consumption capability of the function is proportional to the number of partitions. The CKafka consumption modules on the backend of the function will automatically match the number of CKafka topic partitions, that is, the consumption capability can be improved by adding partitions.
* Optimize the execution duration of the function. The shorter the duration, the higher the consumption capability. If the duration becomes longer (for example, the database in the function needs to be written but the response of the database becomes slower), the consumption speed will decrease.
