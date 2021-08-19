### APPEUI
`APPEUI` is a globally unique device application identifier in a LoRA network, which is assigned by the cloud or registered by the client when the product is created. It is used to identify the application group to which the device belongs and can only contain 16 lowercase letters (a–f) and digits (0–9).


### Product
A product is a collection of devices of a certain type, which usually have the same features. IoT Hub assigns a globally unique `ProductID` to each product, under which multiple devices can be created.


### Product ID
`ProductID` (product ID) is a unique product identifier assigned by the platform for easier product search. It is also used for identity authentication when a device is connected to the platform.


### Product Type
According to the communication methods of the devices actually connected to the IoT Hub platform, the platform performs targeted processing on the data transfer linkage for NB and LoRa products. For more information, please see Getting Started with NB-IoT Product and Getting Started with LoRa Product.


### DevEUI
`DevEUI` is a globally unique identifier of a LoRA device and used to identify its hardware address. It can be found from the vendor or on the device or be a locally unique identifier assigned by the cloud. It can only contain 16 lowercase letters (a–f) and digits (0–9).


### Node Type
According to the types of devices actually connected to the IoT Hub platform, nodes can be divided into device type and gateway type.



### Devices
A device belongs to a product. The device name must be unique under the same product. The platform assigns a key or private key + certificate to each device according to the authentication method of the product to which it belongs.


### Authentication Method
Device connection authentication supports certificate authentication (based on TLS asymmetric encryption and suitable for scenarios with high security requirements) and key authentication (based on symmetric encryption and suitable for resource-constrained devices). Authentication is performed at the device granularity to ensure the cloud-to-device and device-to-cloud message confidentiality. At the same time, the platform has designed a dynamic registration feature for scenarios where it is impossible to burn different firmware for each device. This feature supports getting a device key (or certificate + private key) through product-level key registration and then performing connection authentication, which enhances the connection flexibility.

### ProductSecret
`ProductSecret` is a key at the product level. It is used to calculate the device-side signature when a device is dynamically registered, in exchange for the device-level key or certificate + private key.

### Device Certificate
A device certificate is a unique certificate file the IoT Hub platform issues to a certificate-authenticated device when it is created. When the device establishes a connection with the platform, the platform will verify the device certificate file to ensure the validity of the device identity.

### Device Key
A device key is a unique key the IoT Hub platform issues to a key-authenticated device when it is created, which is used to sign and calculate the `connect password`. When the device establishes a connection with the platform, the platform will verify the device key to ensure the validity of the device identity.


### Device Shadow
Device shadow is essentially a copy of device data in JSON document format cached on the server and is mainly used to save the current status and desired configuration of the device.


### Topic
A topic is a message communication topic, acting as the communication intermediary of the messages in the Pub/Sub pattern. It is required when publishing and subscribing to messages, and the communication is made based on the specific topic of each device.

### Publishing
This is a type of permission (Pub) that manipulates a topic, i.e., publishing messages to the topic.


### Subscribing
This is a type of permission (Sub) that manipulates a topic, i.e., subscribing to messages in the topic.


### Rule Engine
IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, and extracted through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, message queue, and TBDS for seamless data connection or to implement M2M.




### Message Queue
IoT Hub can write specified device messages to Tencent Cloud message queue services CMQ and CKafka. From there, third-party services can get the device messages through TencentCloud APIs to enable async communication. Based on this, storage, analysis, and device control logic can be implemented on the backend.

