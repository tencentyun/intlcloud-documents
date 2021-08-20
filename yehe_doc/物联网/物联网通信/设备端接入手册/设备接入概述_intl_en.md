
## Feature Overview

To facilitate the connection of your devices and ensure the security of connection, IoT Hub provides a complete device connection service. To connect a device to IoT Hub, you need to complete [device registration/creation](https://intl.cloud.tencent.com/document/product/1105/41476) first. The process of connection to IoT Hub be completed only after the device registration/creation succeeds.

### Device connection service

- The device connection service provides the feature of dynamic device registration, so device registration can be completed by devices themselves.
- The device connection service supports connection over diverse protocols, including MQTT, WebSocket, HTTP/HTTPS, and CoAP.
- The device connection service is capable of connection authentication, so devices need to be authenticated based on the connection protocol to ensure the connection security.
- The device connection service offers device SDKs, based on which devices can be connected easily.


### Device connection based on SDK

IoT Hub provides SDKs for [C](hhttps://intl.cloud.tencent.com/document/product/1105/41849), [Android](https://intl.cloud.tencent.com/document/product/1105/41857), and [Java](https://intl.cloud.tencent.com/document/product/1105/41860) for device connection. They are integrated with the features included in the device connection service, so you only need to set the device information (for key-authenticated devices: `ProductID`, `DeviceName`, and device key; for certificate-authenticated devices: `ProductID`, `DeviceName`, certificate file, key file, and CA Certificate) in them and integrate their corresponding features into your devices to complete device connection. In addition to the connection service features, the SDKs also include functional APIs for device shadow, OTA, and RRPC. For more information on the APIs, please see:
- [SDK for C Use Instructions](https://intl.cloud.tencent.com/document/product/1105/41849).
- [SDK for Android Use Instructions](https://intl.cloud.tencent.com/document/product/1105/41857).
- [SDK for Java Use Instructions](https://intl.cloud.tencent.com/document/product/1105/41860).

>?IoT Hub supports custom connection. You can connect devices to it in a custom way simply by following the protocols and authentication processes it provides.





