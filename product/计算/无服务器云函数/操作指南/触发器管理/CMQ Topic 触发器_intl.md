You can write an SCF function to handle a message received in a CMQ topic. The CMQ topic can pass the message to the function and call the function by using the message content and related information as parameters.

Characteristics of CMQ topic triggers:

- **Push model**: The CMQ topic will push the message to all subscribers of the topic after receiving the message. If it's configured to trigger an SCF function, the function will also receive the push as a subscriber from the queue. In the push model, the CMQ topic retains the event source mapping for the SCF function.
- **Async call**: A CMQ topic always calls a function asynchronously, and the result is not returned to the caller. For more information about calling types, see [Calling Types](https://cloud.tencent.com/document/product/583/9694#.E8.B0.83.E7.94.A8.E7.B1.BB.E5.9E.8B).

## CMQ Topic Trigger Configurations

- CMQ topic (required): Configure a CMQ topic . It can only be a CMQ queue in the same region.

## CMQ Topic Trigger Binding Limit
 
One CMQ topic supports up to 100 subscribers. You can bind multiple SCF functions to one single topic within the limit.

CMQ Topic trigger only works to CMQ topic in the same region, that is, when you configure a CMQ Topic trigger for an SCF cloud created in Guangzhou region, you can only choose a CMQ Topic in the Guangzhou region (South China). If you want to trigger an SCF function via CMQ topic messages in a specific region, please create a function in the same region.

## Event Structure for CMQ Topic Trigger
When receiving a message, the specified CMQ Topic sends the following event data in JSON format to the bound SCF.

```
{
  "Records": [
    {
      "CMQ": {
        "type": "topic",
        "topicOwner":120xxxxx,
        "topicName": "testtopic",
        "subscriptionName":"xxxxxx",
        "publishTime": "1970-01-01T00:00:00.000Z",
        "msgId": "123345346",
        "requestId":"123345346",
        "msgBody": "Hello from CMQ!",
        "msgTag": ["tag1","tag2"]
      }
    }
  ]
}
```

The data structures are detailed as below:

| Parameter name| Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list |
| CMQ | This identifies the data structure source as a CMQ topic queue |
| type | Type of message source. It can be `topic` or `queue` |
| topicOwner | Topic owner's account ID |
| topicName | Topic name |
| subscriptionName | Name of the SCF function as a subscriber in the topic |
| publishTime | Publishing time of the message |
| msgId | Unique ID of the message |
| requestId | Request ID for message push |
| msgBody | Message content |
| msgTag | Message tag list |
