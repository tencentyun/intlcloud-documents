You can write an SCF function to handle a message received in a CMQ topic. The CMQ topic can deliver the message to the function and invoke it by using the message content and related information as parameters.

Characteristics of CMQ topic triggers:

- **Push model**: the CMQ topic will push the message to all subscribers of the topic after receiving the message. If it is configured to trigger a function, the function will also receive the push from the queue as a subscriber. In the push model, the CMQ topic stores the event source mapping with SCF.
- **Async invocation**: a CMQ topic trigger always invokes a function asynchronously, and the result is not returned to the invoker. For more information on invocation types, please see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).

## CMQ Topic Trigger Attributes
**CMQ topic (required)**: configure a CMQ topic. It can only be a CMQ queue in the same region.

## CMQ Topic Trigger Binding Limit
 
One CMQ topic supports up to 100 subscribers. If this limit is reached, function trigger binding may fail. You can bind multiple functions to one single topic within the limit.

In addition, CMQ topic triggers can only trigger functions in the same region; for example, for an SCF function created in the Guangzhou region, you can only select a CMQ topic in the Guangzhou region (South China) when configuring a CMQ topic trigger. If you want to trigger a function through CMQ topic messages in a specific region, please create a function in that region.

## Event Structure for CMQ Topic Trigger
When receiving a message, the specified CMQ topic will send the following event data in JSON format to the bound function.

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
        "msgTag": "tag1,tag2"
      }
    }
  ]
}
```

The data structures are detailed as below:

| Structure Name| Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list |
| CMQ | This identifies the data structure source as CMQ |
| type | Type of message source. It can be `topic` or `queue` |
| topicOwner | Topic owner's account ID |
| topicName | Topic name |
| subscriptionName | Name of the function as a subscriber in the topic |
| publishTime | Message publishing time |
| msgId | Unique message ID |
| requestId | Message push request ID |
| msgBody | Message content |
| msgTag | Message tag list recorded through strings |
