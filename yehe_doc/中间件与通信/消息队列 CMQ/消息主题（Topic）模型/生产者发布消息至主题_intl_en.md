A producer can push a message to a topic by specifying the following information:
- Topic name
- Topic resource ID
- Target topic, which can be customized
- Published content: it is the body of the message and can be customized. CMQ will not encode or modify it.
- Message filter tag: a tag, i.e., message tag or message type, is used to identify a message category under a topic in CMQ. A consumer can filter messages by tag so that it can consume only message types of interest to it. This feature is disabled by default. If it is disabled, all messages will be sent to all subscribers. If a tag is set by a subscriber, unmatched messages will not be received by the subscriber. A message filter tag describes the tag used for message filtering in the subscription (only messages with the same tag can be pushed). One tag can contain up to 16 characters, and up to 5 tags can be added to one message.
