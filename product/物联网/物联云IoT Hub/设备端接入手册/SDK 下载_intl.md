[//]: # (chinagitpath:XXXXX)

## C Language SDK
### Code Hosting
- The device-side SDK code is hosted on GitHub since v1.0.0
  [https://github.com/tencentyun/qcloud-iot-sdk-embedded-c](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c)
- Download the latest version 
  [https://github.com/tencentyun/qcloud-iot-sdk-embedded-c/releases](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c/releases)
  
### v2.2.0  
- Release date: July 20, 2018
- Development language: C
- Development environment: Linux, GNU Make
- Content:
	1. Added the NB-IoT device access capability
	2. Adapted to the topic wildcards "#" and "+"
	3. Organized the directory structure of third-party libraries
	4. Fixed several bugs
  
### v2.1.0
- Release date: May 2, 2018
- Development language: C
- Development environment: Linux, GNU Make
- Content:
	1. Added new firmware upgrade (OTA-CoAP channel) capability
	2. Added the HMAC-SHA1 authentication access capability for low-end resource-constrained devices
	3. Added the ability to get backend time

### v2.0.0
- Release date: March 12, 2018
- Development language: C
- Development environment: Linux, GNU Make
- Content:
	1. Added firmware upgrade (OTA-MQTT channel) capability
    2. Fixed the issue that the device shadow heartbeat interval was invalid	
	3. Fixed the issue that the data received by MQTT caused buffer overflow when the data length was at the threshold
  
### v1.2.2
- Release date: February 7, 2018
- Development language: C
- Development environment: Linux, GNU Make
- Content:
	1. Added the support for MQTT/CoAP symmetric encryption connection
	2. Optimized the Linux C compilation

### v1.2.1
- Release date: February 2, 2018
- Development language: C
- Development environment: Linux, GNU Make
- Content:
	1. Fixed the logic error of the Publish message timeout callback

### v1.2.0
- Release date: January 17, 2018
- Development language: C
- Development environment: Linux, GNU Make
- Content:
  1. Modified the message publishing/subscribing ACK for receipt through the callback without blocking the sending thread
  2. Added the capabilities of the device and the backend for connection and logging
  3. Added a new UDP-based CoAP channel which uses DTLS asymmetric encryption and consumes less energy in pure data reporting scenarios

### v1.0.0
- Release date: November 15, 2017
- Development language: C
- Development environment: Linux, GNU Make
- Content:
  1. Added the support for MQTT protocol: The device can quickly and easily connect to the cloud server of IoT Hub. For more information, see [MQTT Protocol Details](https://github.com/mcxiaoke/mqtt)
  2. Added the support for device shadow function: For more information, see [Device Shadow Details](https://cloud.tencent.com/document/product/634/11918)
  3. Added the support for symmetric and asymmetric encryption

## Android SDK

### Code Hosting
- The Android device-side SDK code is hosted on GitHub since v1.0.0
  [https://github.com/tencentyun/qcloud-iot-sdk-android](https://github.com/tencentyun/qcloud-iot-sdk-android)
  
### v2.0.0
- Release date: March 12, 2018
- Content:
	1. Added firmware upgrade (OTA-MQTT channel) capability

### v1.2.0
- Release date: January 17, 2018
- Content:
  1. Added the support for MQTT protocol: The device can quickly and easily connect to the cloud server of IoT Hub. For more information, see [MQTT Protocol Details](https://github.com/mcxiaoke/mqtt)
  2. Added the support for device shadow function: For more information, see [Device Shadow Details](https://cloud.tencent.com/document/product/634/11918)
  3. Added the capability of cross-process API call for MQTT and device shadow
  4. Added the support for asymmetric encryption
