
## Retry Letter Topic

A retry letter topic is designed to ensure that messages are consumed normally. If no normal response is received after a message is consumed by the consumer for the first time, it will enter the retry letter topic, and after a specified number of failed retries, it will be delivered to the dead letter topic.

In actual scenarios, messages may not be processed promptly due to temporary issues such as network jitter and service restart, and the retry mechanism of the retry letter topic can be a good solution in this case.

## Dead Letter Topic

A dead letter topic is a special type of message topic used to centrally process messages that cannot be consumed normally. If a message cannot be consumed after a specified number of retries in the retry letter topic, TDMQ for Pulsar will determine that the message cannot be consumed under the current situation and deliver it to the dead letter topic.

In actual scenarios, messages may not be consumed due to service downtime or network disconnection. In this case, they will not be discarded immediately; instead, they will be persisted by the dead letter topic. After fixing the problem, you can create a consumer subscription to the dead letter topic to process such messages.
