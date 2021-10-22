### APPEUI
This is a unique device application identifier in a LoRA network, which is assigned by the cloud or registered by the client when the product is created. It is used to identify the application group to which the device belongs and must be a hexadecimal string formed by 16 characters from the digits 0–9 and letters a–f.

### DevEUI
`DevEUI` is a globally unique identifier of a LoRA device and used to identify its hardware address. It can be found from the vendor or on the device or be a locally unique identifier assigned by the cloud. It can only contain 16 lowercase letters (a–f) and digits (0–9).

### Subscribe
This is a type of permission (Sub) that manipulates a topic, i.e., subscribing to messages in the topic.

### Rules Engine
IoT Hub supports SQL-like syntax and basic semantic operations. The contents of device messages can be parsed, filtered, and extracted through simple syntax, with the results forwarded to Tencent Cloud's backend services such as storage, message queue, and TBDS for seamless data connection or to implement M2M.

### Node Type
According to the types of devices actually connected to the IoT Hub platform, nodes can be divided into device type and gateway type.

### Device Shadow
Device shadow is essentially a copy of device data in JSON document format cached on the server and is mainly used to save the current status and desired configuration of the device.

### Device Certificate
A device certificate is a unique certificate file the IoT Hub platform issues to a certificate-authenticated device when it is created. When the device establishes a connection with the platform, the platform will verify the device certificate file to ensure the validity of the device identity.

### IoT Hub
Tencent Cloud Internet of Things Hub (IoT Hub) provides a secure, stable, and efficient connection platform that helps developers quickly achieve reliable and high-concurrency data communications among devices, user applications and cloud services at low costs. In other words, IoT Hub can realize cross-device interaction, device data reporting and configuration distribution. In addition, by opening up the link between device data and Tencent Cloud products using the rule engine, it allows for the quick and easy storage, real-time computation and intelligent processing and analytics of massive amounts of data.

