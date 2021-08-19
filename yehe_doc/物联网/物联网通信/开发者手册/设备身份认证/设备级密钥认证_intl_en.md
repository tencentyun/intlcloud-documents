
## Overview
The IoT Hub platform supports device-level key authentication. In this mode, you need to burn different configuration firmware for each device. The platform will perform certificate authentication or key authentication according to your selection. After successful authentication, devices can establish a connection with the platform for data communication.


## Flowchart
Device-level key authentication requires you to burn different firmware for each device. It incurs certain implementation costs in production applications, but it has higher security and is thus recommended.
![](https://main.qcloudimg.com/raw/20bbcc26439b20cd41fc64d72a2f3af2.png)


## Directions
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and create a product and a device as instructed in [Device Connection Preparations](https://intl.cloud.tencent.com/document/product/1105/41476).
2. Get the product information on the product details page and get the device name and device certificate/key on the device details page.
 - Product information
![](https://main.qcloudimg.com/raw/aca400b6f81833f551e2dd9b428cc210.png)
 - Device information
![](https://main.qcloudimg.com/raw/64862bbc5a5aface8f45a6de0d4c2dd7.png)
3. Burn the device firmware in the following steps:
 1. Download the [device SDK](https://intl.cloud.tencent.com/document/product/1105/41840).
 2. Implement the HAL layer functions in the SDK for reading and writing product and device information, including `ProductID`, `Devicename`, and device certificate or key. For more information, please see [SDK for C Connection Description](https://intl.cloud.tencent.com/document/product/1105/41842).
 3. Develop the device firmware based on the SDK according to your actual business needs so as to implement various features such as unique device ID reading, dynamic device registration, connection authentication, communication, and OTA.
 4. In the production process, batch burn the developed and tested device firmware into the device.
4. The device uses the burned device-level certificate/key to establish a connection with the platform. After successful authentication, it will be activated and connected. At this time, it can exchange data with the cloud to implement business requirements.



