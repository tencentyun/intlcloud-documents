### What is the rule engine and what does it do?
The rule engine is a backend module that can process the messages reported by devices and forward them to other Tencent Cloud components. It can filter messages by topic or message content and extract the specified fields into new messages for forwarding to Tencent Cloud components responsible for tasks such as message storage and computation.

### What are the requirements for the formats of the messages to be forwarded?
Currently, messages forwarded by the rule engine can be in JSON or binary format. JSON messages can be filtered, while binary messages can only be passed through for forwarding.

### What are the formats of messages forwarded by the rule engine to other Tencent Cloud services in the console?
After a device reports a payload message, it will be encapsulated in JSON format in the console before being forwarded to other Tencent Cloud services by the rule engine. The `Payload` field in the encapsulated message indicates the original payload message reported by the device, and the console will use different methods to process it based on the forwarding scenario:
- If the message is forwarded to CMQ or CKafka, the encapsulated `Payload` field will be Base64-encoded and needs to be Base64-decoded  when the correct data is extracted.
- If the message is forwarded to a third-party service (HTTP forward), the original payload message reported by the device will be checked. If it is in JSON format, it will be passed through; if it is in binary format, it will be Base64-encoded.

### The rule engine was configured in the console to forward messages to other Tencent Cloud services, but the forwarding did not work. What should I do?
You can check the cloud logs of message forwarding in the IoT Hub console to confirm the forwarding situation.
Common causes of message forwarding failures include:
- The format of the message body does not match the data format defined during product creation.
- The topic of the message is written incorrectly and does not match the topic configured in the rule.
- The forwarding information entered in the rule is incorrect and causes the rule engine to fail to forward.


