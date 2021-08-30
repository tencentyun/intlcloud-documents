
### Product
A product is a collection of devices of a certain type, which usually have the same features. IoT Hub assigns a globally unique `ProductID` to each product. Through products, you can manage devices, topic permissions, and product-level data processing operations.

### ProductID
`ProductID` is a unique product identifier assigned by the platform for easier product search. It is also used for identity authentication when a device connects to the platform. It can be viewed in the basic information of a product.
![](https://main.qcloudimg.com/raw/06db3fdbeb4cb57e4878ed7ef169eb24.png)

### DeviceName
`DeviceName` is the name of a device under a product. It is used for identity authentication when the device connects to the platform.

### Node Type
According to the types of devices actually connected to the IoT Hub platform, nodes can be divided into device type and gateway type.

### Gateway Node
Devices of a gateway node can be directly connected to the platform. Devices under a device product can be added as subdevices, and after their topic permissions are added, the gateway node can publish and subscribe to data on behalf of the subdevices.

### Device Node
Devices of a device node can be connected to the platform directly or through gateway devices. If the added devices cannot be connected to the platform directly, this node type can be selected, so that the devices will be connected to the platform through gateway devices.

### Product Type
According to different application scenarios, the IoT Hub platform defines the categories of various hardware products in different application fields, which can be selected based on the communication methods of the devices actually connected to the platform. For NB and LoRa products, the platform performs targeted processing on the data transfer link.

### Authentication Method
Device connection authentication supports certificate authentication (based on TLS asymmetric encryption and suitable for scenarios with high security requirements) and key authentication (based on symmetric encryption and suitable for resource-constrained devices). Authentication is performed at the device granularity to ensure the cloud-to-device and device-to-cloud message confidentiality. At the same time, the platform has designed a dynamic registration feature for scenarios where it is impossible to burn different firmware for each device. This feature supports getting a device key (or certificate + private key) through product-level key registration and then performing connection authentication, which enhances the connection flexibility.

### Certificate Authentication
In certificate authentication mode, a device needs to carry the `ProductID`, `DeviceName`, certificate file, key file, and CA certificate to prove its validity before connection to the platform. After the device is connected, a certificate file and a key file will be generated, which can be viewed in the device information.
![](https://main.qcloudimg.com/raw/da4add21f0b939456cfe3da6077753e6.png)

### CA Certificate
CA certificate is one of the identity authentication conditions for devices authenticated with certificate, which can be viewed in the basic information of the product.
![](https://main.qcloudimg.com/raw/bcc4bb167c7677021d490fae0c8b1a4b.png)

### Key Authentication
In key authentication mode, a device needs to carry the `ProductID`, `DeviceName`, and device key to prove its validity before connection to the platform. The key can be viewed in the device information.
![](https://main.qcloudimg.com/raw/4ce73f14d695055aec4b8f72e3c2101f.png)
![](https://main.qcloudimg.com/raw/ece7e8466c67e2abaf2c2d8f0639dddb.png)

### ProductSecret
`ProductSecret` is a key at the product level. It is used to calculate the device-side signature when a device is dynamically registered, in exchange for the device-level key or certificate + private key.

### Dynamic Registration
A device carries a unified `ProductId`, `ProductSecret`, and custom `DeviceName` to complete the first authentication with the platform. After the authentication is successful, the platform will issue a device-level key or certificate + private key, which, together with `ProductId+DeviceName`, will be carried by the device to complete the eventual authentication with the platform.

### Topic
A topic is a UTF-8 string as the medium for message publishing/subscribing. You can publish messages to a topic or subscribe to messages in a topic.

### Publishing
This is a type of permission (Pub) that manipulates a topic, i.e., publishing messages to the topic.

### Subscribing
This is a type of permission (Sub) that manipulates a topic, i.e., subscribing to messages in the topic.


