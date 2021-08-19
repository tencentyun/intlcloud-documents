## Device Connection
### Connection through SDK
IoT Hub currently supports SDKs for various platforms such as Linux and Android. For SDK download addresses, please see [SDK for C Download](https://intl.cloud.tencent.com/document/product/1105/41840).

### Transfer protocol
- TCP- and TLS-based MQTT (encrypted connection) is a mainstream IoT communication protocol and is appropriate for communication between devices or receiving reverse control signals and configurations.
- UDP- and DTLS-based CoAP (encrypted connection) has less consumption and requirements for resources, which is applicable for pure data reporting.

### Security protocol
IoT Hub performs two-way authentication and encrypted data transfer between client and server based on security protocols such as TLS and DTLS, so as to prevent risks including unauthorized access, data theft, and tampering. Taking into account the diversity of devices and use cases, it supports both asymmetric encryption (authentication based on device certificates for scenarios with high security requirements) and symmetric encryption (authentication based on keys for resource-constrained devices). Authentication at the device granularity ensures the confidentiality of cloud-to-device and device-to-cloud messages.

### RTOS portability
IoT Hub's SDK supports cross-platform porting and detachment of framework from hardware abstraction layer, enabling quick and easy connection to IoT Hub from different platforms.

### Device firmware update
When firmware has security risks or functional problems, IoT Hub servers can perform OTA updates to eliminate dangers and reduce security risks.

### Gateway product connection

IoT Hub supports the creation of gateway and subdevice products. You can bind a gateway device and the corresponding subdevice, and then the gateway device can connect, disconnect, and send/receive messages on behalf of the subdevice over the MQTT protocol.

## Device Management
### Lifecycle management
Devices can be registered, added, deleted, or terminated in the console. This can also be done through the SDK toolkits for Python, PHP, and Java, which is faster and more efficient.

### Device status
Device status can be monitored throughout the entire process, with instant notifications for any status changes.

### Group management
IoT Hub supports group management for devices under different products to meet the multi-level management needs of different types of devices in different business scenarios.

### Log collection
IoT Hub can collect and report the upstream and downstream communication logs, message content logs, and SDK debugging logs of devices to meet the query requirements in multiple business scenarios.

## Device Communication
The topics that devices can publish and subscribe to are managed by permission control, and all devices under the same product have the same topic class permissions. For data transfer over MQTT, QoS=0 and QoS=1 message features are supported. Plus, messages can be stored offline, and the rule engine can swiftly implement message communication between devices.

## Device Shadow
Device shadow is essentially a copy of device data in JSON format cached on the server and is mainly used to save:
- Current device configurations
- Current device status

As a medium, device shadow can effectively implement two-way data sync between device and user application:
- For device configuration, the user application does not need to directly modify the device; instead, it can modify the device shadow on the server, which will sync modifications to the device. In this way, if the device is offline at the time of modification, it will receive the latest configuration from the shadow once going back online.
- For device status, the device reports the status to the device shadow, and when users initiate queries, they can simply query the shadow. This can effectively reduce the network interactions between the device and the server, especially for low-power devices.

## Rule Engine
### Syntax rules
IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, extracted, and reintegrated through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, function, and TBDS for seamless data connection.

### Connection between devices
In order to isolate device data, devices can only publish and subscribe to messages in their own topics. Message connection between devices can be achieved through the repub feature of the rule engine.

### Device message forwarding to third-party
The rule engine can configure directly forwarding device messages to third-party services, thereby quickly enabling communication between the device and the connecting party's backend services.

### Device-Cloud connection
Tencent Cloud offers corresponding services (such as TencentDB, SCF, message queue, and TBDS) for scenarios where users require further processing of device data (such as persistent storage, function computing, and big data analysis). In addition, the direct connection between IoT Hub and these Tencent Cloud services will be available soon.

## Message Queue
As devices are connected only to IoT Hub, IoT Hub can write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can get the device messages through the SDK APIs of CMQ or CKafka, enabling async message communication between devices and third-party services. Based on this, data storage, computational analysis, and device control logic can be implemented on the backend.

## Collaboration Management
IoT Hub supports secure access, use, and management of cloud account resources through CAM. Isolation and collaboration of IoT Hub resources are implemented through identity and policy management of sub-accounts and collaborators.

## Data Processing
### Real-Time computing
In the field of IoT, massive amounts of data is reported in real time, and core businesses have high requirements for the timeliness of data monitoring, making stream computing and real-time computing significant for such use cases. The rule engine forwards device data to CKafka in real time, which is connected to Storm/SparkStreaming for stream computing. This helps you implement real-time computation of device data.

### Intelligent processing
IoT Hub enables data connection with TBDS. TBDS' extraordinary capabilities in data discovery, analysis, and mining enable users to quickly process data from billions of IoT devices, tap into the value of data, increase efficiency, and seize market opportunities.

### Visualization
IoT Hub can access Tencent Cloud RayData, a service for big data visualization. Powered by the real-time data rendering technology, you can visualize, contextualize, and interact with massive amounts of data reported from devices, achieving personalized data management and usage.

