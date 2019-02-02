[//]: # (chinagitpath:XXXXX)

## 1. Device Access
### SDK Access
IoT Hub SDK can be downloaded [here](https://cloud.tencent.com/document/product/634/11928). Currently, SDKs for Linux, Android and Windows are available.

### Transfer Protocols
- TCP- and TLS-based MQTT (encrypted access) is a mainstream IoT communication protocol and suitable for message communication between devices or scenarios where it is needed to receive reverse control signals and configurations.
- UDP- and DTLS-based CoAP (encrypted access) has lower resource consumption and requirements, making it suitable for scenarios where the device only reports data.
- WebSocket-based MQTT is suitable for establishing connection and communication between browser-based applications and IoT Hub.
- HTTP has a low threshold for access and is suitable for low-power, short-connection data reporting scenarios.

### Security Protocols
IoT Hub performs two-way authentication and encrypted data transfer between client and server based on security protocols such as TLS and DTLS to prevent risks like unauthorized access, data theft and tampering. Taking into account the diversity of devices and usage scenarios, IoT Hub supports both asymmetric encryption (authentication based on device certificates for scenarios with high security requirements) and symmetric encryption (authentication based on keys for resource-constrained devices). Authentication at the device level ensures the confidentiality of cloud-to-device and device-to-cloud messages.

### RTOS Portability
IoT Hub's SDK supports cross-platform porting with the hardware abstraction layer detached from the framework, making access to IoT Hub from different platforms fast and easy.

### Device Firmware Upgrade
IoT Hub supports OTA firmware upgrades, making it possible to perform OTA upgrades on IoT servers in case of security risks or functional vulnerabilities with device firmware.

## 2. Device Management
### Lifecycle Management
Devices can be registered, added, deleted or terminated within the console. This can also be done using the SDK toolkit for improved efficiency. Currently, it supports Python, PHP and JAVA toolkits.

### Device Status
Device status can be monitored throughout the entire process, with instant notifications for any status changes.

## 3. Device Communication
The topics that devices can publish and subscribe to are managed by permission controls, and all devices under the same product have the same topic class permissions. For MQTT transfer, message features such as QoS=0 and QoS=1 are supported. Offline message storage is also supported. Fast message communication between devices is enabled based on the rule engine.

## 4. Device Shadow
Essentially a copy of device data in JSON format cached on the server, a device shadow is mainly used to save:
- the current configuration of the device; and
- the current status of the device.

As an intermediary, the device shadow can effectively achieve bilateral data synchronization between device and user application:
- For device configuration, the user application does not need to directly modify the device; instead, it can modify the device shadow on the server which will sync modifications to the device. If the device is offline at the time of modification, it will be synced with the latest configuration from the shadow once coming back online.
- For device status, the device reports the status to the device shadow, and when the user initiates queries, they can simply query the shadow. This can effectively reduce the network interactions between the device and the server, especially for low-power devices.

## 5. Rule Engine
### Syntax Rules
IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, extracted and re-integrated through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, function computing and Tencent Big Data Suite (TBDS) for seamless access.

### Device-to-device Interconnection
In order to isolate device data, the device can only publish and subscribe to messages in its own topics. Interconnection can be achieved through the repub feature based on the rule engine.

### Forwarding Device Messages to Third-party Services
The rule engine supports the configuration of direct forwarding of device messages to third-party services, thereby quickly making available the communication between the device and the accessor's backend services.

### Device-to-cloud Interconnection
Tencent Cloud offers corresponding products (such as TencentDB and Big Data Analytics Suite) for scenarios where users require further processing of device data (such as persistent storage, function computation and big data analytics). In addition, the direct connection between IoT Hub and these cloud products will be made available soon.

## 6. Message Queue
As the only interface of the devices, IoT Hub can write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can obtain the device messages through the SDK API of CMQ or CKafka, enabling async message communication between the devices and third-party services. The backend data storage, computational analysis or device control logic is completed on this basis.

## 7. Collaborative Management
IoT Hub supports secure access, use and management of cloud account resources through CAM. Isolation and collaboration of IoT cloud resources are realized through identity and policy management of sub-accounts and collaborators.

## 8. Data Processing
### Real-time Computation
In the field of IoT, massive amounts of data must be reported in real time, and core businesses have high requirements for the timeliness of data monitoring, making stream computing and real-time computing significant for such application scenarios. The rule engine forwards device data to CKafka in real time which is connected to Storm/SparkStreaming stream computing, helping enable real-time computation of device data.

### Intelligent Processing
IoT Hub is capable of connecting to Tencent Big Data Suite (TBDS). Leveraging TBDS' powerful data discovery, analytics and mining capabilities, data from billions of IoT devices can be quickly and intelligently processed to tap into the value of data, improve efficiency and seize market opportunities.

### Visualization
IoT Hub is capable of accessing Tencent Cloud RayData, a big data visualization service. This feature enables you to visualize, contextualize and interact with high volumes of data reported by the devices with the aid of real-time data rendering technology, facilitating personalized management and usage of data.


