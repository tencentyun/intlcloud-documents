The model where a topic delivers a message to a subscriber is as shown below:
![](https://main.qcloudimg.com/raw/6df92543e8958a1a252ad8d7e962bab4.jpg)

The topic follows the rules below when delivering the message to the subscriber:
- The topic will try its best to deliver the message published by the producer to the subscriber.
- If the delivery fails after multiple retries, the message will be retained in the topic and wait for the next delivery. If the next delivery still fails, the message will be discarded after the maximum lifecycle (1 day).

If the topic fails to deliver the message to the subscriber, you can troubleshoot as follows:
- The `SecretId` and `SecretKey` need to be provided for message delivery (persistent key is required). You can get them in [API Key Management](https://console.cloud.tencent.com/cam/capi).
- You need to use a root account rather than sub-account to create a subscription.
- If the queue name does not exist, please check whether the queue exists in the [CMQ Console](https://console.cloud.tencent.com/mq/index).
