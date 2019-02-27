[//]: # (chinagitpath:XXXXX)

### Product
This is a collection of devices of a certain type, usually referring to a group of devices with the same features. IoT Hub issues a globally unique ProductID to each product, and multiple devices can be created under each product.

### Product ID
This is the unique identifier assigned by the platform to the product, which makes it easy to search for the product and is used for identity authentication when the device establishes a connection with the platform.

### Product Type
According to the selected communication method of the actual device connected to IoT Hub, the platform will handle the data transfer link in a targeted manner for NB-IoT and LoRa products. For details, see NB-IoT Product Quick Start and LoRa Product Quick Start.


### Device
A device belongs to a product. The device name must be unique under the same product. The platform assigns a private key or private key + certificate to each device according to the authentication method of the product to which the device belongs.

### Authentication Method
Device connection authentication supports certificate authentication (based on TLS asymmetric encryption, suitable for scenarios with high security requirements) and key authentication (symmetric encryption, suitable for resource-constrained devices). Authentication at the device level ensures the confidentiality of cloud-to-device and device-to-cloud messages.

### Device Certificate
This is a unique certificate file the platform issues to a certificate-authenticated device when the device is created. When the device establishes a connection with IoT Hub, IoT Hub will verify the device certificate file to ensure the validity of the device identity.

### Device Key
This is a unique key the platform issues to a key-authenticated device when the device is created, which is used to sign and calculate the connect password. When the device establishes a connection with IoT Hub, IoT Hub will verify the device key to ensure the validity of the device identity.

### Topic
This is a message communication topic, acting as the communication medium of the messages in the Pub/Sub pattern. A topic is required when publishing and subscribing to messages, and the communication is based on the specific topic of each device.

### Publishing
This is a type of permission (Pub) that operates a topic, i.e., publishing messages to the topic.

### Subscribing
This is a type of permission (Sub) that operates a topic, i.e., subscribing to messages from the topic.


### Rule Engine
IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered and extracted through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, message queue and Tencent Big Data Suite (TBDS) for seamless access or used for machine-to-machine (M2M) messaging.

### Device Shadow
Essentially a copy of device data in JSON format cached on the server, a device shadow is mainly used to save the current status of the device and the desired configuration of the device.

### Message Queue
IoT Hub can write specified device messages to Tencent Cloud CMQ or CKafka queues. From there, third-party services can obtain the device messages through Cloud API, enabling async message communication and implementing backend storage, analysis and device management logics.

### AppEui
This is a globally unique device application identifier in a LoRA network, which is assigned by the cloud or registered by the client when the product is created. It is used to identify the application group to which the device belongs and can only contain 16 lowercase letters (a-f) and numbers (0-9).

### DevEui
This is a globally unique identifier of a LoRA device and used to mark the hardware address of the LoRA device. It can be found from the provider or on the device or be a locally unique identifier assigned by the cloud. It can only contain 16 lowercase letters (a-f) and numbers (0-9).

