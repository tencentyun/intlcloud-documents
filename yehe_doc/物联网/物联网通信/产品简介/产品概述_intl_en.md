

Tencent Cloud Internet of Things Hub (IoT Hub) provides a secure, stable, and efficient connection platform that helps developers quickly achieve reliable and high-concurrency data communications among devices, user applications and cloud services at low costs. In other words, IoT Hub can realize cross-device interaction, device data reporting and configuration distribution. In addition, by opening up the link between device data and Tencent Cloud products using the rule engine, it allows for the quick and easy storage, real-time computation and intelligent processing and analytics of massive amounts of data.


## Service Architecture

![](https://main.qcloudimg.com/raw/98032ab77586fb80fc9b6b6eac8a3626.png)



### Devices can be connected to IoT Hub
User devices can be connected to IoT Hub through SDKs. The underlying data transfer is based on MQTT or CoAP protocols, which effectively lowers the consumption of network bandwidth. In terms of security, IoT Hub introduces secure network transfer protocols (TLS and DTLS) to prevent risks such as unauthorized access, data theft, and tampering. Taking into account the diversity of devices and use cases, it supports both asymmetric encryption (authentication based on device certificates for scenarios with high security requirements) and symmetric encryption (authentication based on keys for resource-constrained devices).

### Messages can be published and subscribed to by devices through SDKs
In order to isolate device data for security purposes, IoT Hub currently limits that devices can only publish and subscribe to messages in their own topics, but they can access messages of other entities by configuring the rule engine.

### The rule engine can be configured in the console to enable devices to access messages of other entities
At present, the rule engine supports operations in SQL-like syntax, which implement message communication between devices through "repub" (republishing messages) and device message forwards to third-party services through "forward" (forwarding messages to servers). Meanwhile, device messages can be forwarded to Tencent Cloud services such as TencentDB, CTSDB, and message queue. Forwarding messages to SCF, TBDS, RayData, and BI will be supported soon.

### Device messages can be interconnected with third-party services
As devices are connected only to IoT Hub, IoT Hub can quickly write specified device messages to Tencent Cloud CMQ or CKafka queues, with the message queue feature enabled. From there, third-party services can get and consume the data through the SDK of CMQ or CKafka queues, achieving async message communication between devices and third-party services.

### Device shadows can effectively achieve two-way sync of configuration and status data between devices and applications
On the one hand, configuration parameters can be set for device shadows through TencentCloud API, so that when devices are connected or online, they can get the configuration parameters from the shadows. When the status of a device is queried, it is sufficient to query its shadow without having to perform direct network communication with the device.


### Devices can be managed through TencentCloud API
IoT Hub provides convenient SDK tools to enhance IoT device management capabilities. These tools enable quick and batch creating, querying, and operation on the backend, greatly improving the efficiency. Currently, Python, PHP, and Java toolkits are supported.

