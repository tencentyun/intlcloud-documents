## Overview
The IoT Hub platform supports product-level key authentication. In this mode, you only need to enable dynamic device registration and then burn the same configuration firmware (ProductID + ProductSecret) for all devices under the same product. In this way, the devices can get device certificates or keys through registration requests and then communicate with the platform.

## Flowchart
>!If you want to use the dynamic registration feature, you need to manually enable dynamic registration for the product on the product details page in the console.

![](https://main.qcloudimg.com/raw/4ded886d8d6bf7da39fe28441eca8c99.png)

## Directions  
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and create a product as instructed in [Device Connection Preparations](https://intl.cloud.tencent.com/document/product/1105/41476).
2. Enable **Dynamic Registration** on the product details page, select whether to automatically create devices, and set the maximum number of automatically created devices.
>?To prevent too many devices from being created in unpredictable situations (such as device firmware bugs and product key theft), if you select automatic device creation, we recommend you set an appropriate device quantity upper limit.

![](https://main.qcloudimg.com/raw/cbeaa7b27399d363c6cafa1b7ee5eb1c.png)
3. Create a device under the product (optional).
 - You can add devices to the device list in the console or create devices through TencentCloud API.
 - If you don't enable automatic device creation, IoT Hub will verify whether each requested device name has been created in the cloud during device registration. We recommend you use a unique identifier that can be read by the device as the `Devicename`, such as IMEI, SN, or MAC address, which facilitates the smooth completion of the entire process.
![](https://main.qcloudimg.com/raw/fcfd1333204b327ce8d62428b030ac99.png)
4. Burn the device firmware in the following steps:
 1. Download the [device SDK](https://intl.cloud.tencent.com/document/product/1105/41840).
 2. Implement the HAL layer functions in the SDK for reading and writing product and device information, including `ProductID`, `ProductSecret`, and `Devicename`, and enable the dynamic registration feature in the SDK. For more information, please see [SDK for C Connection Description](https://intl.cloud.tencent.com/document/product/1105/41842).
 3. Develop the device firmware based on the SDK according to your actual business needs so as to implement various features such as unique device ID reading, dynamic device registration, connection authentication, communication, and OTA.
 4. In the production process, batch burn the developed and tested device firmware into the device.
5. After successful device registration, power-on, and connection, initiate a registration request to get the device certificate or key.
6. The device uses the obtained device-level certificate/key to establish a connection with the platform. After successful authentication, it will be activated and connected. At this time, it can exchange data with the cloud to implement business requirements.


