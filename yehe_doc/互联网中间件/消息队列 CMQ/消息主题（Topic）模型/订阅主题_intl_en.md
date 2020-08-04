You can subscribe to a topic by specifying the following attributes:
- Topic name.
- Topic resource ID.
- Subscription name, which cannot be modified once entered.
- Subscription terminal protocol, which can be a queue message service or URL address.
- Subscription address, which can be a URL or queue name. Currently, a topic can send messages to a queue under the same account.
- Retry policy: it is the `NotifyStrategy` attribute of the subscription, i.e., the retry policy used when an error occurs during message push to recipients. This policy is enabled by default, and you need to select one of the following two options:
 - Backoff retry: an attempt will be retried three times at random intervals between 10 and 20 seconds. After three retries, the message will be discarded for the subscriber and will not be retried again.
 - Exponential decay retry (checked by default): an attempt will be retried 176 times at exponentially increasing intervals: 2^0 seconds, 2^1 seconds, ..., 512 seconds, 512 seconds, ..., 512 seconds. The total retry duration is 1 day.
- Retry verification: if the HTTP return code is 200, it is successful.
- Subscriber tag: when adding a subscriber, you can add filter tags (`FilterTag`), so that the subscriber can receive only messages with the specified tags. One tag can contain up to 16 characters, and up to 5 tags can be added for one subscriber. As long as a tag matches a topic filter tag, the subscriber can receive messages delivered by the topic. If a message does not have any tag, the subscriber cannot receive it.
- Maximum number of subscribers to topic: one topic can be associated with up to 500 subscribers.
- Total number of messages associated with subscriber: it is an approximate value and indicates the number of messages that are waiting for or being retried for delivery to the subscriber in a topic.

