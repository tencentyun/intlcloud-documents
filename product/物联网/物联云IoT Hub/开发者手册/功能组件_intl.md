[//]: # (chinagitpath:XXXXX)

### 1. SDK

For details, see the [SDK document](https://cloud.tencent.com/document/product/634/11928). Currently, IoT Hub supports SDKs for operating systems such as Linux, Android and Windows.

### 2. Device Access

Devices access the IoT Hub platform via SDK:

- The application layer is based on MQTT and CoAP protocols.
- The transfer layer is based on TCP and UDP protocols. Secure network transfer protocols (TLS and DTLS) are also introduced to realize two-way authentication and encrypted data transfer between client and server.
- SDK supports RTOS portability, porting cross platforms, and framework detachment from the hardware abstraction layer, enabling fast and easy access to IoT Hub from different platforms.

Device SDK supports TLS (for MQTT) and DTLS (for CoAP) asymmetric and symmetric encryption to protect device communication security:

- Asymmetric encryption
  Based on certificate and asymmetric encryption algorithm, asymmetric encryption is highly secured and good for devices that have high hardware specifications and are insensitive to power consumption. It needs information such as device certificates, private keys and root certificates and those related information will be returned after device creation in the IoT Hub.
- Symmetric encryption
  Based on key and symmetric encryption algorithm, symmetric encryption is generally safe and is good for devices that are  resource-constrained, and sensitive to power consumption. It relies on the device psKey, and relevant information will be returned when the device is created by IoT Hub.

In addition to access through the device-side SDK, IoT Hub provides:

- MQTT over WebSocket access, which is suitable for establishing connection and communication between browser-based applications and IoT Hub.
- HTTP access, which has a low threshold for access and is suitable for low-power, short-connection data reporting scenarios.

### 3. Device Management

![img](https://mc.qcloudimg.com/static/img/a853b52c3dd9f2bbedef3023e81f3fa2/3-2.png)

Up to 2,000 products can be created under one Tencent Cloud account; up to 200,000 devices can be created under one product. A device belongs to one product only. The product name and device name must be unique under the same Tencent Cloud account.

### 4. Permission Management

Topics that devices can publish and subscribe to are rigorously managed in the IoT Hub. All devices under the same product have the same topic restrictions, which by default include the following:

| Topic | Description |
| ---------------------------------------- | ------------------ |
| ${productId}/${deviceName}/event | Publishing permission for device data reporting |
| ${productId}/${deviceName}/control | Subscribing permission for devices to obtain backend data |

For a specific device, the productId and deviceName marked with the $ symbol above should be mapped to the specific product ID and device name. For example, if a product named "pro" (assuming the product Id is "pro_id") has 2 devices (assuming the device names are "dev_1" and "dev_2" respectively), then the topics that dev_1 can publish include pro_id/dev_1/event but not pro_id/dev_2/event, and the topics that it can subscribe to include pro_id/dev_1/control but not pro_id/dev_2/control.

You can edit and modify the topic permissions in the console and add or remove devices' topic permissions.

To enable device SDK’s bulk topic subscription, wildcard can be used when device subscribes to or unsubscribes from topics to indicate multiple matching topics:

| Wildcard | Description |
| ------- | ----- |
| #	 | This wildcard can only appear at the end of the topic, representing the topics at the current level and all sub-levels, for example, if the wildcard topic is pro_id/dev_1/#, it can represent not only pro_id/dev_1/event but also pro_id/dev_1/event/subeventA |
| +	 | This wildcard can only appear after deviceName, representing all the topics at the current level. For example, if the wildcard topic is pro_id/dev_1/event/+, it can represent pro_id/dev_1/event/subeventA and pro_id/dev_1/event/subeventB but not pro_id/dev_1/event/subeventA/close. This wildcard can appear multiple times, such as pro_id/dev_1/event/+/subeventA/+ |

A wildcard must be used as a complete level. For example, both ${productId}/${deviceName}/e# and ${productId}/${deviceName}/e+ are invalid.
The system topics defined by IoT Hub ($shadow, $ota and $sys) do not support wildcards.

The performance of the wildcard when subscribing to topics: all the topics with subscribing permission under the product matching the wildcard topic are subscribed to, and a success will be returned even if the matched topic list is empty.
The performance of the wildcard when unsubscribing from topics: all the subscribed topics matching the wildcard topic are unsubscribed from, and a success will be returned even if the matched topic list is empty. Use ${productId}/${deviceName}/# to unsubscribe from all user topics.

### 5. Message Management

![img](https://mc.qcloudimg.com/static/img/24e01a9e0f2c534dcacec016c4bf2b13/3-3.png)

Based on MQTT protocols, IoT Hub supports QoS=0 or 1 but not QoS=2 for MQTT data transfer. Device messages can be saved offline.

- If QoS=0, message can be sent to device no more than once.
  Choose this QoS for publishing and subscription when you need average reliable data transfer. 
- If QoS=1, at least one message will be sent to the device.
  Choose this QoS for publishing and subscription when you need highly reliable data transfer. 

Other parameters:

| Parameter | Description |
| ------------------------- | --------- |
| Topic name length | Up to 128 bytes |
| MQTT protocol packet size | Up to 256 KB |
| QoS=1 message storage period (when receiver is offline or fails to send online) | 24 hours |
| Number of QoS=1 messages not confirmed by the device | Up to 50 |

### 6. Device Shadow

Device shadow is essentially a copy of device data in JSON format cached on the server and is mainly used to save:

- Current device configurations; and
- Current device status.

As a medium, device shadow can effectively achieve bilateral data synchronization between device and user application:
 
- For device configuration, the user application does not need to directly modify the device; instead, it can modify the device shadow on the server which will sync modifications to the device. If a device is offline at the time of modification, it will be synced with the latest configuration from the shadow once it is back online.
- Device reports its status to the device shadow. When users initiate queries, they can simply query the shadow. It effectively reduces the network interactions between device and server, especially for low power consumption devices.

The following shows how device shadow operate in Quick Start:

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

IoT Hub supports OTA firmware upgrades, making it possible to perform OTA upgrades on IoT servers in case of device firmware’ security risks or functional vulnerabilities.

### 12. Collaboration Management

IoT Hub supports secure access, use and management of cloud account resources through [CAM](https://cloud.tencent.com/product/cam). Isolation and collaboration of IoT cloud resources are realized through identity and policy management of sub-accounts and collaborators.
