[//]: # (chinagitpath:XXXXX)

### 1. SDK

For details, see the [SDK document](https://cloud.tencent.com/document/product/634/11928). Currently, IoT Hub supports SDKs for operating systems such as Linux, Android and Windows.

### 2. Device Access

The device accesses the IoT Hub platform through the SDK:

- The application layer is based on MQTT and CoAP protocols.
- The transfer layer is based on TCP and UDP protocols, and on this basis, the secure network transfer protocols (TLS and DTLS) are introduced for two-way authentication and encrypted data transfer between client and server.
- The SDK supports RTOS portability for cross-platform porting with the hardware abstraction layer detached from the framework, making access to IoT Hub from different platforms fast and easy.

The device-side SDK supports TLS (for MQTT) and DTLS (for CoAP) for asymmetric and symmetric encryption to protect device communication security:

- Asymmetric encryption
  This is based on certificate and asymmetric encryption algorithm for a high security level and suitable for devices with high hardware specifications and low sensitivity to power consumption. It relies on device certificates, private keys and root certificates, and relevant information will be returned when the device is created by IoT Hub.
- Symmetric encryption
  This is based on key and symmetric encryption algorithm for a general security level and suitable for resource-constrained, power consumption-sensitive devices. It relies on the device psKey, and relevant information will be returned when the device is created by IoT Hub.

In addition to access through the device-side SDK, IoT Hub provides:

- MQTT over WebSocket access, which is suitable for establishing connection and communication between browser-based applications and IoT Hub.
- HTTP access, which has a low threshold for access and is suitable for low-power, short-connection data reporting scenarios.

### 3. Device Management

![img](https://mc.qcloudimg.com/static/img/a853b52c3dd9f2bbedef3023e81f3fa2/3-2.png)

Up to 2,000 products can be created under one Tencent Cloud account and up to 200,000 devices can be created for one product. One device can only belong to one product. The product name and device name must be unique under the same Tencent Cloud account.

### 4. Permission Management

In IoT Hub, the topics that devices can publish and subscribe to are strictly managed. All devices under the same product have the same topic class permissions, including the following by default:

| Topic | Description |
| ---------------------------------------- | ------------------ |
| ${productId}/${deviceName}/event | Publishing permission for the device to report data |
| ${productId}/${deviceName}/control | Subscribing permission for the device to obtain the data sent by the backend |

For a specific device, the productId and deviceName marked with the $ symbol above should be mapped to the specific product ID and device name. For example, if a product named "pro" (assuming the product Id is "pro_id") has 2 devices (assuming the device names are "dev_1" and "dev_2" respectively), then the topics that dev_1 can publish include pro_id/dev_1/event but not pro_id/dev_2/event, and the topics that it can subscribe to include pro_id/dev_1/control but not pro_id/dev_2/control.

You can edit and modify the topic permissions in the console and add or remove the topic class permissions of the product.

In order to facilitate the batch subscription to topics by the device-side SDK, wildcards can be used to indicate multiple matching topics when the device subscribes to and unsubscribes from topics:

| Wildcard | Description |
| ------- | ----- |
| #	 | This wildcard can only appear at the end of the topic, representing the topics at the current level and all sub-levels, for example, if the wildcard topic is pro_id/dev_1/#, it can represent not only pro_id/dev_1/event but also pro_id/dev_1/event/subeventA |
| +	 | This wildcard can only appear after deviceName, representing all the topics at the current level, for example, if the wildcard topic is pro_id/dev_1/event/+, it can represent pro_id/dev_1/event/subeventA and pro_id/dev_1/event/subeventB but not pro_id/dev_1/event/subeventA/close. This wildcard can appear multiple times, such as pro_id/dev_1/event/+/subeventA/+ |

A wildcard must be used as a complete level, for example, both ${productId}/${deviceName}/e# and ${productId}/${deviceName}/e+ are invalid.
The system topics defined by IoT Hub ($shadow, $ota and $sys) do not support wildcards.

The performance of the wildcard when subscribing to topics: all the topics with subscribing permission under the product matching the wildcard topic are subscribed to, and a success will be returned even if the matched topic list is empty.
The performance of the wildcard when unsubscribing from topics: all the subscribed topics matching the wildcard topic are unsubscribed from, and a success will be returned even if the matched topic list is empty. ${productId}/${deviceName}/# clears subscriptions to all user topics.

### 5. Message Management

![img](https://mc.qcloudimg.com/static/img/24e01a9e0f2c534dcacec016c4bf2b13/3-3.png)

For MQTT data transfer, IoT Hub supports QoS=0 or 1 but not QoS=2. Device messages can be stored offline.

- If QoS=0, the message is sent to the device at most once
  For scenarios where the requirement for data transfer reliability is not high, please select this QoS for publishing and subscribing.
- If QoS=1, the device should receive the message at least once
  For scenarios where the requirement for data transfer reliability is high, please select this QoS for publishing and subscribing.

Other parameters are as follows:

| Parameter | Description |
| ------------------------- | --------- |
| topic name length | Up to 128 bytes |
| MQTT protocol packet size | Up to 256 KB |
| QoS=1 message storage period (if the receiver is offline or online sending fails) | 24 hours |
| Number of QoS=1 messages not confirmed by the device | Up to 50 |

### 6. Device Shadow

Essentially a copy of device data in JSON format cached on the server, a device shadow is mainly used to save:

- the current configuration of the device; and
- the current status of the device.

As an intermediary, the device shadow can effectively achieve bilateral data synchronization between device and user application:
 
- For device configuration, the user application does not need to directly modify the device; instead, it can modify the device shadow on the server which will sync modifications to the device. If the device is offline at the time of modification, it will be synced with the latest configuration from the shadow once coming back online.
- For device status, the device reports the status to the device shadow, and when the user initiates queries, they can simply query the shadow. This can effectively reduce the network interactions between the device and the server, especially for low-power devices.

The figure below is an application example of the device shadow in Quick Start:

![img](https://mc.qcloudimg.com/static/img/7bf7a659ce098b28a700037ff09e123d/3-4.png)![img](https://mc.qcloudimg.com/static/img/d895eaad6f25bf78c8ac2bb2ae8d81d7/3-5.png)

> **Note:**
> Device shadows and device messages have different application scenarios. In terms of implementation mechanism, the server-side device shadow always saves the last copy of data, and multiple messages that successively arrive do not overwrite one another.
 
- For the scenario where the device reports data, the device shadow is more suitable for reporting the device's own information (such as energy consumption), while the device message is more suitable for reporting the data collected by the device (such as the measured temperature).
- For scenarios where the device receives data, the device shadow is more suitable for notifying the device of updated configuration (such as changing the target operating temperature), while the device message is more suitable for real-time control of the device (such as turning the device to the left by 45 degrees)

For more information, see [Device Shadow Details](https://cloud.tencent.com/document/product/634/11918).

### 7. Rule Engine

Based on rule engine, you can configure rules to do the following:

- **Syntax rules**
  IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, extracted and re-integrated through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, function computing and Tencent Big Data Suite (TBDS) for seamless access.
- **Device-to-device interconnection**
  In order to isolate device data, the device can only publish and subscribe to messages in its own topics (for details, see [Feature Components - Permission Management](https://cloud.tencent.com/document/product/634/11915)). Interconnection can be achieved through the repub function based on the rule engine.
- **Device-to-server interconnection**
  The rule provides a simple forwarding function that can copy messages to your server via HTTP requests. This can achieve fast interconnection between device messages and your services.
- **Device-to-cloud interconnection**
  Tencent Cloud offers corresponding products (such as TencentDB and Big Data Analytics Suite) for scenarios where users require further processing of device data (such as persistent storage and big data analytics). In addition, the direct connection between IoT Hub and these cloud products will be made available soon.

For more information, see [Rule Engine Details](https://cloud.tencent.com/document/product/634/11917).

### 8. Message Queue

As the only interface of the devices, IoT Hub can write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can obtain the device messages through the SDK API of CMQ or CKafka, enabling async message communication between the devices and third-party services. The backend data storage, computational analysis or device control logic is completed on this basis.

### 9. Console

The console provides visual management interfaces where you can manage products, devices and permissions and configure rule engines.
For more information, go to the [Console](https://console.cloud.tencent.com/iotcloud) or see [Console User Manual](https://cloud.tencent.com/document/product/634/11916).

### 10. Cloud API

For the device management flow in IoT scenarios, IoT Hub provides various APIs for fast and batch operations in the backend. Currently, it supports Python, PHP and JAVA toolkits. At present, IoT Hub provides the following cloud APIs:

| Category | List |
| ------ | ---------------------------------------- |
| Product-related | [CreateProduct](https://cloud.tencent.com/document/product/634/12051), [ListProducts](https://cloud.tencent.com/document/product/634/12054), [DeleteProduct](https://cloud.tencent.com/document/product/634/14068)     |
| Device-related   | [CreateDevice](https://cloud.tencent.com/document/product/634/12050), [ListDevices](https://cloud.tencent.com/document/product/634/12053), [CreateMultiDevice](https://cloud.tencent.com/document/product/634/12276), [DeleteDevice](https://cloud.tencent.com/document/product/634/12277), [GetCreateMultiDevTask](https://cloud.tencent.com/document/product/634/14069), [GetMultiDevices](https://cloud.tencent.com/document/product/634/14070)    |
| Device shadow-related | [UpdateDeviceShadow](https://cloud.tencent.com/document/product/634/12055), [GetDeviceShadow](https://cloud.tencent.com/document/product/634/12052)|
| Message publishing-related | [Publish](https://cloud.tencent.com/document/product/634/12278)|

For an example of a Python-based cloud API, see [here](https://mc.qcloudimg.com/static/archive/c6b492abe009de1c47b91b8bfd93c7d2/iotcloud_RestAPI_python.zip).

### 11. Firmware Upgrade

IoT Hub supports OTA firmware upgrades, making it possible to perform OTA upgrades on IoT servers in case of security risks or functional vulnerabilities with device firmware.

### 12. Collaboration Management

IoT Hub supports secure access, use and management of cloud account resources through [CAM](https://cloud.tencent.com/product/cam). Isolation and collaboration of IoT cloud resources are realized through identity and policy management of sub-accounts and collaborators.
