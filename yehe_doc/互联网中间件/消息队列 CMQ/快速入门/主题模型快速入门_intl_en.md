A topic can publish messages only if it is subscribed to by at least one subscriber. If there are no subscribers, messages in the topic will not be delivered, and message publishing will be meaningless.

## 1. Create a Topic
```
	endpoint='' // CMQ domain name
	secretId ='' // User ID and key
	secretKey = ''
	account = Account(endpoint,secretId,secretKey)
	topicName = 'TopicTest8B'
	my_topic = account.get_topic(topicName)
	topic_meta = TopicMeta()
	my_topic.create(topic_meta)
```
You can view the created topic in the console. Here, QPS is 5000, indicating that the default highest frequency for calling the same API is 5,000 calls per second. To increase the upper limit, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.


## 2. Publish a Message
You can publish a message through the SDK or in the console.
### Through SDK
```
	message = Message()
	message.msgBody = "this is a test message"
	my_topic.publish_message(message)
```
### In Console
Topics support message filtering. A tag, i.e., message tag or message type, is used to identify a message category under a topic in CMQ. A consumer can filter messages by tag so that it can consume only message types of interest to it. This feature is disabled by default. If it is disabled, all messages will be sent to all subscribers. If a tag is added, subscribers can receive only messages with the set tag. A message filter tag describes the tag used for message filtering in the subscription (only messages with the same tag can be pushed). One tag can contain up to 16 characters, and up to 5 tags can be added to one message.
Topics currently support filtering by tag and `routingKey`.

**Publish messages in batches:**

```
	vmsg = []
	for i in range(6):
	message = Message()
	message.msgBody = "this is a test message"
	vmsg.append(message)

	my_topic.batch_publish_message(vmsg)
```


## 3. Process the Message
After a message is published by a topic, it will automatically be pushed to the subscription. If the push fails, there are two retry policies:
- **Backoff retry**: an attempt will be retried three times at random intervals between 10 and 20 seconds. After three retries, the message will be discarded for the subscriber and will not be retried again.
- **Exponential decay retry**: an attempt will be retried 176 times at exponentially increasing intervals: 2^0 seconds, 2^1 seconds, ..., 512 seconds, 512 seconds, ..., 512 seconds. The total retry duration is 1 day. This is the default retry policy.


### Using queue to process messages
A subscriber can enter a queue so as to use it to receive published messages.
```
	subscription_name = "subsc-test"
	my_sub = my_account.get_subscription(topic_name, subscription_name)
	subscription_meta = SubscriptionMeta()
	# Enter the subscription name, which is a queue name here
	subscription_meta.Endpoint = "queue name  "
	subscription_meta.Protocal = "queue"
	my_sub.create(subscription_meta)
```

### Using other means to process messages
Subscribers can process messages on their own without using queues. For more information, please see [Delivering Messages](https://cloud.tencent.com/document/product/406/7420).


## 4. Use Routing Matching
The binding key and routing key are used together and are compatible with the topic match mode of RabbitMQ. The routing key carried when a message is sent is added by the client and must be a string without a wildcard, and the binding key carried when a subscription relationship is created is the binding relationship between the topic and the subscriber.

**Use limits:**
- There can be up to 5 binding keys, and each of them can contain up to 64 bytes to represent the route for message sending, which can have up to 15 `.`, i.e., up to 16 phrases.
- All routing keys are contained in a string, and each of them can contain up to 64 bytes to represent the route for message sending, which can have up to 15 `.`, i.e., up to 16 phrases.

**Wildcard description:**
- \* (asterisk): represents a word (a letter string).
- # (hashtag) matches one or multiple characters.
- Special rule of RabbitMQ: when `routing_key` is an empty string, it cannot match \* but can match #.

**Example:**
- If the subscriber is **1.*.0**, and the message is **1.any character.0**, then it can be received by the subscriber.
- If the subscriber is **1.#.0**, and the message is **1.2.3.4.4.2.2.0**, then it can be received by the subscriber (the elements in the middle of the message can be arbitrary).

### Using routing matching feature
```
    endpoint='' // CMQ domain name
    secretId ='' // User ID and key
    secretKey = ''
    account = Account(endpoint,secretId,secretKey)
    topicName = 'TopicTest'
    my_topic = account.get_topic(topicName)
    topic_meta = TopicMeta()
    topic_meta.filterType = =2 // It indicates that routing matching will be used when messages are delivered to subscriptions
    // If `filterType` is 1, tags are used for filtering
    my_topic.create(topic_meta)

    subscription_name = "subsc-test"
    my_sub = my_account.get_subscription(topic_name, subscription_name)
    subscription_meta = SubscriptionMeta()
    // Enter the subscription name, which is a queue name here
    subscription_meta.Endpoint = "queue name  "
    subscription_meta.Protocal = "queue"
    subscription_meta.bindingKey=[1.*.0]  // If the message tag is `[1.any characters.0]`, all subscribers will
    // receive messages carrying this tag
    my_sub.create(subscription_meta)
```


### Publishing message
```
    message = Message()
    message.msgBody = "this is a test message"
    routingKey = '1.test.0' // This message will be delivered to the address subscribed to by `my_sub`
    my_topic.publish_message(message)
```

   
