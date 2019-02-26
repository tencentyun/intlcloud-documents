[//]: # (chinagitpath:XXXXX)

## 1. Device Access
### SDK Access
IoT Hub SDK can be downloaded [here](https://cloud.tencent.com/document/product/634/11928). Currently, SDKs for Linux, Android and Windows are available.

### Transfer Protocols
- TCP- and TLS-based MQTT (encrypted access) is a mainstream IoT communication protocol and is appropriate for communication between devices or receiving reverse control signals and configurations.
- UDP- and DTLS-based CoAP (encrypted access) has less consumption and requirements for resources, which is applicable for pure data reporting.
- WebSocket-based MQTT is suitable for establishing connection and communication between browser-based applications and IoT Hub.
- HTTP has a low threshold for access and is suitable for low-power, short-connection data reporting.

### Security Protocols
IoT Hub performs two-way authentication and encrypted data transfer between client and server based on security protocols such as TLS and DTLS to prevent risks like unauthorized access, data theft and tampering. Taking into account the diversity of devices and usage scenarios, IoT Hub supports both asymmetric encryption (authentication based on device certificates for scenarios with high security requirements) and symmetric encryption (authentication based on device certificates for high security requirements). Authentication at the device level ensures the confidentiality of cloud-to-device and device-to-cloud messages.

### RTOS Portability
SDK supports porting across platforms and detachment of framework from hardware abstraction layer, enabling quick and easy access to IoT Hub from different platforms.

### Device Firmware Upgrade
IoT Hub supports OTA firmware upgrades. When firmware has security risks or functional problems, IoT servers can perform OTA upgrades to eliminate danger and reduce security risks.

## 2. Device Management
### Life Cycle Management
Devices can be registered, added, deleted or terminated within the console. SDK toolkit enables better operation and efficiency. Now it supports Python, PHP and JAVA toolkit.

### Device Status
Device status can be monitored throughout the entire process, with instant notifications for any status changes.

## 3. Device Communication
Topics devices can publish and subscribe to are managed by permission controls, and all devices under the same product have the same topic class permissions. For MQTT transfer, message features such as QoS=0 and QoS=1 are supported. Offline message storage is also supported. The rule engine enables fast information communication between devices.

## 4. Device Shadow
Essentially a copy of device data in JSON format cached on the server, a device shadow is mainly used to save:
- the current configuration of the device; and
- the current status of the device.

As a medium, the device shadow can effectively achieve bilateral data synchronization between device and user application:
- For device configuration, the user application does not need to directly modify the device; instead, it can modify the device shadow on the server which will sync modifications to the device. If the device is offline at the time of modification, it will be synced to the latest configuration from the shadow once back online.
- For device status, the device reports the status to the device shadow, and when the user initiates queries, they can simply query the shadow. This can effectively reduce the network interactions between the device and the server, especially for low-power devices.

## 5. Rule Engine
### Syntax Rules
IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, extracted and re-integrated through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, function computing and Tencent Big Data Suite (TBDS) for seamless access.

### Connection Between Devices
In order to isolate device data, a device can only publish and subscribe to its own topic. Connection between devices can be achieved through the repub function which is based on the rule engine.

### Forwarding Device Messages to the Third-party
The rule engine supports configurations forwarding device messages to the third-party, therefore enables communication between the device and the accessor's backend services.

### Device-to-cloud Interconnection
Tencent Cloud offers products such as TencentDB and Big Data Analytics Suite to users who need further device data processing. Scenarios include persistent storage, function computation, big data analytics, etc. Additionally, Tencent Cloud will supports the direct connection between the IoT Hub and these cloud products. 

## 6. Message Queue
As the only interface of the devices, the IoT Hub can record specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can obtain the device messages through the SDK API of CMQ or CKafka, enabling asynchromous message communication between devices and third-party services. The backend data storage, computational analysis or device control logic will be completed on this basis.

## 7. Collaborative Management
IoT Hub supports secure access, use and management of cloud account resources through CAM. Isolation and collaboration of IoT cloud resources are realized by managing sub-accounts and collaborators' identities and stategies.

## 8. Data Processing
### Real-time Computation
Massive amounts of data need to be reported in real time in IoT. At the same time, data monitoring is time-sensitive to core businesses. Therefore, stream computing and real-time computing are crucial in these scenarios. The rule engine forwards device data to CKafka in real time, then connects to Storm/SparkStreaming stream computing, enabling real-time device data computation.

### Smart Processing 
IoT Hub can be connected to Tencent Big Data Suite (TBDS). TBDS' extrordinary capacity in data discovery, analytics and mining enables user to quickly process data from billions of IoT devices, find data values, increase efficiency and seize market opportunities.

### Visualization
IoT Hub is capable of accessing Tencent Cloud RayData, a big data visualization service. This feature enables you to visualize, contextualize and interact with high volumes of data reported by the devices with the aid of real-time data rendering technology, facilitating personalized management and usage of data.


