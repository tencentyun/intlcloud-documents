### What features and services does IoT Hub provide?
IoT Hub provides features such as device management, device shadow, messaging, firmware update, and connection with Tencent Cloud services. As a message channel, it can be flexibly accessed by devices. Plus, it connects a wide variety of Tencent Cloud components to create full-stack services for message acquisition, storage, and computation.

### What are the use limits of IoT Hub?
For more information on the use limits of IoT Hub, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1105/41464).

### What are the differences between the message queue and rule engine forwarding in IoT Hub?
Both message queue and rule engine forwarding can forward messages to the specified Tencent Cloud components, but they differ in the dimensions of forwarding, message filtering, and message format requirements.

- Message queue: it forwards messages in the product dimension. As long as a message queue is configured for a product, the messages of all devices under the product will be forwarded to the message queue unconditionally. There are no message filters or requirements for the message format.
- Rule engine forwarding: currently, messages should be forwarded by topic, and filters can be configured based on topic to specify which topic's messages can be forwarded. You can also set filters for message fields to specify that only the messages containing fields that meet certain conditions can be forwarded. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/1105/41484).


### Does IoT Hub provide mobile application development?
No. Currently, IoT Hub focuses on feature components at the IoT platform layer but does not provide application capabilities. You need to build an application server by yourself and develop the corresponding mobile application or directly use [IoT Explorer](hhttps://intl.cloud.tencent.com/product/iothub), which provides the application development capabilities.


