[//]: # (chinagitpath:XXXXX)

### Rule Engine Explained
A rule engine is a backend module that forwards device messages to Tencent Cloud components. It can filter messages by topic and message content, extract specified fields into new messages and forward them to Tencent Cloud components. Messages are stored and computed by the Tencent Cloud components.

### What are the requirements for the forwarded message format?
Currently, messages that can be forwarded using rule engine must be in JSON format. Forwarding binary messages will be supported in the future.

### A rule engine is configured in the console to forward messages to other Tencent Cloud products, but the forwarding does not work. What should I do?
You can check the log of message forwarding under Cloud Log in the IoT Hub console to confirm the forwarding situation.

Common reasons for message forwarding failures include:
1. The message body is not in JSON format.
2. The topic of the message is written incorrectly and does not match the topic configured in the rule.
3. The forwarding information entered in the rule is incorrect and causes the rule engine to fail to forward.

