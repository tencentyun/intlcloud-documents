TDMQ for CMQ routing key match is similar to exchange queue in RabbitMQ and can be used to filter messages so as to enable subscribers to get different messages by condition. When creating a topic, you can enable **Routing Matching Key**.

## Use Instructions

The binding key and routing key are used together and function in a way similar to the message filtering capability of RabbitMQ. The routing key carried when a message is sent is added by the client, and the binding key carried when a subscription relationship is created is the binding relationship between the topic and the subscriber.

## Use Limits

- There can be up to 5 binding keys, and each of them can contain up to 64 bytes to indicate the route for message delivery, which can include up to 15 dots (namely up to 16 segments).
- All routing keys are contained in a string, and each of them can contain up to 64 bytes to indicate the route for message delivery, which can include up to 15 dots (namely up to 16 segments).

## Wildcard Description

- * (asterisk) represents a word (a letter string) and cannot be empty.
- # (hashtag) matches zero or multiple characters.


**Example:**

- If the subscriber is **1.*.0**, and the message is **1.any character.0**, then it can be received by the subscriber.
- If the subscriber is **1.#.0**, and the messages are **1.2.3.4.4.2.2.0** and **1.0**, then both of them can be received by the subscriber (the elements in the middle of the messages can be arbitrary).
- If the subscriber is **#**, then the subscriber can receive all messages.


![](https://mc.qcloudimg.com/static/img/d12ffc8e91322fead97b7633cea47f9a/image.png)

