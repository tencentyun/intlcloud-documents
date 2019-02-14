[//]: # (chinagitpath:XXXXX)

## What Is IoT Hub?
Tencent Cloud IoT Hub service aims to provide a secure, stable and efficient connection platform that helps developers quickly achieve stable, high-concurrency, omnidirectional data communication among devices, user applications and cloud services at low cost. IoT Hub can realize cross-device interaction, device data reporting and configuration sending. Furthermore, by opening up the link between device data and Tencent Cloud products based on the rule engine, it allows for the storage, real-time computation and intelligent processing and analytics of massive amounts of data with speed and ease. In general, by taking advantage of IoT Hub, connections among devices, data, applications and cloud services can be created at low cost to quickly build an IoT application platform.

## Product Architecture
![](https://main.qcloudimg.com/raw/3ada4b9604d3218dfe92d75b4382728e.png)

- Access to IoT Hub
  IoT Hub can be accessed by devices through the SDK. The underlying data transfer is based on MQTT or CoAP protocols, which effectively lowers the requirement for network bandwidth. Meanwhile, it also supports access via HTTP and WebSocket. In the security field, it introduces secure network transfer protocols (TLS and DTLS) to prevent risks such as unauthorized access, data theft and tampering. Taking into account the diversity of devices and usage scenarios, IoT Hub supports both asymmetric encryption (authentication based on device certificates for scenarios with high security requirements) and symmetric encryption (authentication based on keys for resource-constrained devices).

- Messages can be published and subscribed to by devices based on the SDK
  In order to isolate device data for security purposes, IoT Hub currently limits that the devices can only publish and subscribe to messages in their own topics, but they can access messages of other entities by configuring rule engines.

- Rule engines can be configured in the console to enable devices to access messages of other entities
  At present, rule engines support operations in SQL-like syntax, which allow message communication between devices through "repub" (republishing messages). Devices can also forward the messages to third-party services through "forward" (forwarding messages to servers). The capability of device message communication with other Tencent Cloud products (such as storage, function computation and big data analysis suites) is also under construction.

- Message communication is enabled between devices and third-party services
  As the only accessor of the devices and with the message queue feature enabled, IoT Hub can quickly write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can obtain and consume the data through the SDK of CMQ or CKafka queues, achieving async message communication between the devices and third-party services.

- Device shadows can effectively achieve bilateral synchronization of configuration and status data between devices and applications
   On one hand, configuration parameters can be set for the device shadows through Cloud API, so that when the devices are online or coming online, they can obtain the configuration parameters from the shadows. On the other hand, the devices can report their latest status to the device shadows. When the status of a device is queried, it is sufficient to query its shadow without having to perform direct network communication with the device.

- Devices can be managed through Cloud API
  In terms of the device management capabilities in IoT scenarios, IoT Hub provides convenient SDK tools for quickly creating, querying and operating devices in batches in the backend to improve efficiency. Currently, it supports Python, PHP and JAVA toolkits.

