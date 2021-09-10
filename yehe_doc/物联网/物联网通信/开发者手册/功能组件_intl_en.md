### 1. SDK
For more information, please see the [SDK documentation](https://intl.cloud.tencent.com/document/product/1105/41840). Currently, IoT Hub supports device SDKs for Linux and Android and supports porting to different hardware platforms.


### 2. Device Connection
Devices can be connected to the IoT Hub platform through the SDK:
- The application layer is based on MQTT and CoAP protocols.
- The transport layer is based on TCP and UDP protocols, and on this basis, secure network transfer protocols TLS and DTLS are introduced for two-way authentication and encrypted data transfer between clients and servers.
- The SDK supports RTOS portability for cross-platform porting and detachment of framework from hardware abstraction layer, enabling quick and easy connection to IoT Hub from different platforms.

The device SDK supports TLS (for MQTT) and DTLS (for CoAP) for asymmetric and symmetric encryption to protect device communication security:
- Asymmetric encryption
This is based on the certificate and asymmetric encryption algorithm for a high security level and suitable for devices with high hardware specifications and low sensitivity to power consumption. It relies on device certificates, private keys, and root certificates, and relevant information will be returned when a device is created in IoT Hub.
- Symmetric encryption
This is based on the key and symmetric encryption algorithm for a general security level and suitable for resource-constrained devices sensitive to power consumption. It relies on the device `psKey`, and relevant information will be returned when a device is created in IoT Hub.

In addition to connection through the device SDK, IoT Hub also supports HTTP connection, which has low requirements for connection and is suitable for low-power data reporting scenarios over non-persistent connections.


### 3. Device Management
![img](https://main.qcloudimg.com/raw/28c720726f112be7abe6ed415f0a09c8.png)

- Up to 2,000 products can be created under one Tencent Cloud account, and up to 1 million devices can be created for one product. A device can only belong to one product. Product names and device names must be unique under the same Tencent Cloud account.
- Devices can be enabled/disabled. After a device is disabled, it cannot be connected to the IoT Hub platform, and device-related operations cannot be performed, but the information associated with it will be retained, so device information can still be queried.

<span id="Permission-Management"></span>
### 4. Permission Management

In IoT Hub, the topics that devices can publish and subscribe to are strictly managed. All devices under the same product have the same topic class permissions, including the following by default:

| Topic | Description |
| ---------------------------------------- | ------------------ |
| ${productId}/${deviceName}/event | Publishing permission for the device to report data |
| ${productId}/${deviceName}/control | Subscribing permission for the device to get the data sent by the backend |

For a specific device, the `productId` and `deviceName` marked with the `$` symbol above should be mapped to the specific product ID and device name. For example, if a product named `pro` (with the product ID `pro_id`) has 2 devices (named `dev_1` and `dev_2` respectively), then the topics that `dev_1` can publish include `pro_id/dev_1/event` but not `pro_id/dev_2/event`, and the topics that it can subscribe to include `pro_id/dev_1/control` but not `pro_id/dev_2/control`.

You can edit and modify the topic permissions in the console and add or remove the topic class permissions of products.

To facilitate batch subscription to topics by the device SDK, wildcards can be used to indicate multiple matching topics when a device subscribes to or unsubscribes from topics:

| Wildcard | Description |
| ------- | ----- |
| #	 | This wildcard can only appear at the end of the topic, representing the topics at the current level and all sub-levels; for example, if the wildcard topic is `pro_id/dev_1/#`, it can represent not only `pro_id/dev_1/event` but also `pro_id/dev_1/event/subeventA` |
| +	 | This wildcard can only appear after `deviceName`, representing all the topics at the current level; for example, if the wildcard topic is `pro_id/dev_1/event/+`, it can represent `pro_id/dev_1/event/subeventA` and `pro_id/dev_1/event/subeventB` but not `pro_id/dev_1/event/subeventA/close`. This wildcard can appear multiple times, such as `pro_id/dev_1/event/+/subeventA/+` |

A wildcard must be used as a complete level; for example, both `${productId}/${deviceName}/e#` and `${productId}/${deviceName}/e+` are invalid.
The system topics defined by IoT Hub (`$shadow`, `$ota`, and `$sys`) don't support wildcards.

- Effect of the wildcard when subscribing to topics: all the topics with the subscribing permission under the product matching the wildcard topic are subscribed to, and a success message will be returned even if the matched topic list is empty.
- Effect of the wildcard when unsubscribing from topics: all the subscribed topics matching the wildcard topic are unsubscribed from, and a success message will be returned even if the matched topic list is empty. `${productId}/${deviceName}/#` can be used to unsubscribe from all topics.

### 5. Message Management

![img](https://main.qcloudimg.com/raw/5bf4fbb13814c391e3b2572a043fdc18.png)

For MQTT data transfer, IoT Hub supports QoS 0 or 1 but not QoS 2. Device messages can be stored offline.

- If QoS is 0, the message will be sent to the device at most once
  For scenarios where the requirement for data transfer reliability is not high, please select this QoS level for publishing and subscribing.
- If QoS is 1, the device should receive the message at least once
  For scenarios where the requirement for data transfer reliability is high, please select this QoS level for publishing and subscribing.

Other parameters are as follows:

| Parameter | Description |
| ------------------------- | --------- |
| Topic name length | Up to 64 bytes |
| MQTT protocol packet size | Up to 16 KB |
| QoS 1 message storage period (if the recipient is offline or online sending fails) | 24 hours |
| Number of QoS 1 messages not confirmed by the device | Up to 150 |

### 6. Device Shadow

Device shadow is essentially a copy of device data in JSON format cached on the server and is mainly used to save:

- Current device configurations
- Current device status

As an intermediary, device shadow can effectively implement two-way data sync between device and user application:

- For device configuration, the user application does not need to directly modify the device; instead, it can modify the device shadow on the server, which will sync modifications to the device. In this way, if the device is offline at the time of modification, it will receive the latest configuration from the shadow once coming back online.
- For device status, the device reports the status to the device shadow, and when users initiate queries, they can simply query the shadow. This can effectively reduce the network interactions between the device and the server, especially for low-power devices.

The figure below is a sample use case of the device shadow in "Getting Started":

![img](https://main.qcloudimg.com/raw/9f582908d0e9276646597b53eecdac26.png)
![img](https://main.qcloudimg.com/raw/50ef5d9ad4ce5b85b3bc573b4ffdbb74.png)


>!Device shadow and device message have different applicable scenarios. In terms of implementation mechanism, the server-side device shadow always saves the last copy of data, and multiple messages that successively arrive do not overwrite one another.

- For scenarios where the device reports data, the device shadow is more suitable for reporting the device's own information (such as energy consumption), while the device message is more suitable for reporting the data collected by the device (such as the measured temperature).
- For scenarios where the device receives data, the device shadow is more suitable for notifying the device of updated configuration (such as changing the target temperature), while the device message is more suitable for real-time control of the device (such as turning the device to the left by 45 degrees).

For more information, please see [Device Shadow Details](https://intl.cloud.tencent.com/document/product/1105/41834).

### 7. Rule Engine

Based on the rule engine, you can configure rules to do the following:

- **Syntax rules**
  IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, extracted, and reintegrated through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, function, and TBDS for seamless data connection.
- **Device-to-Device connection**
  In order to isolate device data, devices can only publish and subscribe to messages in their own topics (for more information, please see [Permission Management](#Permission-Management)). To implement message connection, the repub feature of the rule engine is needed.
- **Device-to-Server connection**
  The rule engine provides a simple forwarding feature that can copy messages to your server through HTTP requests. This can implement fast connection between device messages and your services.
- **Device-to-Cloud connection**
  Tencent Cloud offers corresponding services (such as TencentDB and TBDS) for scenarios where users require further processing of device data (such as persistent storage and big data analysis).
For more information, please see [Rule Engine Details](https://intl.cloud.tencent.com/document/product/1105/41484).

### 8. Message Queue

As devices are connected only to IoT Hub, IoT Hub can write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can get the device messages through the SDK APIs of CMQ or CKafka, enabling async message communication between devices and third-party services. Based on this, data storage, computational analysis, and device control logic can be implemented on the backend.

### 9. Console
The [IoT Hub console](https://console.cloud.tencent.com/iotcloud) provides visual management UIs where you can manage products, devices, and permissions, configure the rule engine, and perform other operations. You can try it out easily.


### 10. TencentCloud API
For the device management flow in IoT scenarios, IoT Hub provides various APIs in Python, PHP, Java, Go, Node.js, and .NET for fast and batch operations on the backend. Currently, it offers APIs related to product, device, task, message, rule engine, and device shadow. For more information, please see TencentCloud API Overview.

### 11. Firmware Update

When firmware has security risks or functional problems, IoT Hub servers can perform OTA updates to eliminate dangers and reduce security risks.

### 12. Collaboration Management

IoT Hub supports secure access, use, and management of cloud account resources through [CAM](https://intl.cloud.tencent.com/product/cam). Isolation and collaboration of IoT Hub resources are implemented through identity and policy management of sub-accounts and collaborators.

