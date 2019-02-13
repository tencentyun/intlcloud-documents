[//]: # (chinagitpath:XXXXX)

### What features and services are provided by IoT Hub?
IoT Hub provides features such as device management, device shadow, message communication and Tencent Cloud product accessing. As a message channel, it can be flexibly accessed by devices. Plus, it connects a rich variety of Tencent Cloud components to create full-stack services for message acquisition, storage and computation.

### What are the restrictions in IoT Hub?
For restrictions on the use of IoT Hub, see the [product restrictions document](https://cloud.tencent.com/document/product/634/15241).

### What are the differences between the message queue and rule engine forwarding provided by IoT Hub?
Both message queue and rule engine forwarding can forward messages to the specified Tencent Cloud components, but they differs in the dimensions of forwarding, message filtering and message format requirements.

Message queue forwards messages at the product dimension. As long as a message queue is configured for a product, the messages of all devices under the product will be forwarded to the message queue unconditionally. There are no message filters or requirements for message format.

Currently, rule engine forwarding requires messages to be in JSON format. The forwarding is at the topic dimension and filters can be configured based on the topic to specify which topic's messages can be forwarded. You can also set filters for message fields to specify that only the messages containing fields that satisfy certain criteria can be forwarded. For more information, see the [rule engine document](https://cloud.tencent.com/document/product/634/14447).

### Does IoT Hub provide mobile app development?
No. Currently, IoT Hub focuses on the basic platforms. If you need integrated IoT solutions, please contact Tencent Cloud's sales team.
