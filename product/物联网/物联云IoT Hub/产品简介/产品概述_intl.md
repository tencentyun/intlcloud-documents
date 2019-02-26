[//]: # (chinagitpath:XXXXX)

## What is IoT Hub?
Tencent Cloud IoT Hub service is a secure, stable and efficient platform. It helps developers achieve quick, low-priced, concurrent and omnidirectional data communication among devices, user applications and cloud services. IoT Hub enables interactions between devices, device data reporting and configuration delivery.  Based on the rule engine, it can also access Tencent Cloud products, making the storage, computation and analysis of massive data quick and easy. To sum up, developers can use IoT Hub to make connections among devices, data, applications and cloud service at a low cost and quickly build an IoT application platform.

## Product Architecture
![](https://main.qcloudimg.com/raw/3ada4b9604d3218dfe92d75b4382728e.png)

- Access the IoT Hub:
  Devices can access the IoT Hub via SDK. The underlying data transmission is based on MQTT or CoAP protocols, effectively reducing bandwidth. HTTP and WebSocket accesses are also availiable. Secure network transfer protocols (TLS and DTLS) are used to prevent unauthorized access, data theft and tampering. Subject to different devices and uses, IoT Hub adopts asymmetric encryption (authentication based on device certificates for high security requirements scenarios) or symmetric encryption (authentication based on keys for resource-constrained devices).

- Device message publishing and subscription based on SDK:
  To segregate device data for security purposes, IoT Hub currently only allows device to publish and subscribe to its own topic, but device can communicate with other entities using configuration rule engine.

- Rule engines can be configured in the console to enable devices to access messages of other entities:
  At present, rule engines support operations in SQL-like syntax, which allow message communication between devices through "repub" (republishing messages). Devices can also forward the messages to third-party services through "forward" (forwarding messages to servers). We are working on connecting device message communication with other Tencent Cloud products, including storage, function computation and big data analysis suites.

- Connecting device message communication with third-party services:
  As the only accessor of the devices and with the message queue feature enabled, IoT Hub can quickly write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can obtain and consume the data through the SDK of CMQ or CKafka queues, achieving asynchronous message communication between the devices and third-party services.

- Users can realize bilateral synchronization of configuration and status data between devices and applications based on device shadows:
  On the one hand, users can set configuration parameters to device shadows via Cloud API, so that configuration parameters can be obtained from shadows when the devices are online or just get online. On the other hand, the devices can report the latest status to the device shadows. When the status of a device is queried, it is sufficient to query its shadow without having to perform direct network communication with the device.

- Devices can be managed through Cloud API:
  IoT Hub provides convenient SDK tools to enhance IoT device management capabilities. These tools enable quick and bulk creating, querying and operation in the backend, improving efficiency.Now it supports Python, PHP and JAVA toolkits.

