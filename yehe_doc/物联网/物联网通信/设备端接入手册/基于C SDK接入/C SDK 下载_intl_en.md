
### Code Hosting
- The code of the device SDK has been hosted on GitHub since v1.0.0
  [https://github.com/tencentyun/qcloud-iot-sdk-embedded-c](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c)
- Download the latest version 
  [https://github.com/tencentyun/qcloud-iot-sdk-embedded-c/releases](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c/releases)
	
### v3.2.1

- Release date: August 4, 2020
- Programming language: C
- Development environments: Linux/Windows
- Content:
  1. Added the RRPC sync communication feature and samples.
  2. Added the broadcasting feature and samples.
  3. Added the subdevice binding/unbinding APIs for gateway devices.
  4. Updated the documentation.

### v3.2.0

- Release date: April 30, 2020
- Programming language: C
- Development environments: Linux/Windows
- Content:
  1. Merged the MTMC branch code, supported multi-device connection, and optimized multithreaded APIs.
  2. Fixed some potential memory leak and out-of-bounds issues as well as cross-platform compilation and running issues.
  3. Used clang-format to format the code and introduced the code checkers clang-tidy and cpplint.

### v3.1.3

- Release date: March 6, 2020
- Programming language: C
- Development environments: Linux/Windows
- Content:
  1. Optimized `ota_mqtt_sample` to decouple and separate the OTA process and the places where file operations were required, and added the checkpoint restart capability for the sample in case of MQTT reconnection.
  2. Optimized `gateway_sample` and added the sample code for proxying more than one subdevice.
  3. Added the API for querying whether the MQTT topic was subscribed to successfully.
  4. Optimized and updated the documentation.
  5. Fixed some compilation warnings and bugs.
  6. Unified the code indentation style.

### v3.1.2

- Release date: November 11, 2019
- Programming language: C
- Development environments: Linux/Windows
- Content:
  1. Removed the relevant code and documentation for IoT Explorer to support IoT Hub only, and optimized the document descriptions.
  2. Fixed memory leaks in the OTA module, `device_info.json` file parsing issues, and Windows time format issues.
  3. Renamed `ca.c/h` to `qcloud_iot_ca.c/h` and `device.c/h` to `qcloud_iot_device.c/h` to avoid filename conflicts.

### v3.1.0

- Release date: September 19, 2019
- Programming language: C
- Development environments: Linux/Windows
- Content:
  Refactored C-SDK:
  1. Optimized the code structure and directory hierarchy, used English comments, improved the documentation, and improved the usability and portability.
  2. Added the CMake compilation method and code extraction method on the basis of original Makefile compilation to adapt to multiple compilation environments.
  3. Added support for Windows to support development in Microsoft Visual Studio.
  4. Added the `AT_socket` network layer to support the development and porting of MCU+TCP AT module devices.
  5. Added the porting adaptation for FreeRTOS + lwIP platforms.

### v3.0.3

- Release date: August 26, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Supported OTA checkpoint restart: added local firmware version information management (version, checkpoint, and MD5) in `ota_mqtt_sample.c`, and supported the `range` parameter when an HTTPS connection is established during firmware download.
  2. Updated the SDK version number to v3.0.3.

### v3.0.2

- Release date: July 18, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Supported escape character processing for the string type in data templates.
  2. Removed device version management from device shadow.
  3. Optimized relevant examples of data templates.

### v3.0.1

- Release date: June 11, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Optimized the log reporting feature, introduced dynamic buffer memory allocation, and supported multipart log reporting for large logs in various scenarios.
  2. Added the event handler callback of `subscribe` for MQTT to notify the status change of the subscribed topic timely.
  3. Fixed some code issues, such as improper judgment on the return values of MQTT APIs.

### v3.0.0

- Release date: May 17, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Added the data template feature based on shadow.
  2. Added the event reporting feature.
  3. Added the data template code generation script tool.
  4. Fixed several bugs in JSON processing.
  5. Added data template samples, event samples, and smart light scenario samples in the data template.
  6. Adjusted the documentation structure and added the document directory `docs` and platform SDK use instructions.
  7. Supported both IoT Hub and IoT Explorer starting from v3.0.0.

### v2.3.5

- Release date: May 15, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Added the dynamic device registration feature.
  2. Added dynamic device registration samples.
  3. Added device information read/write HAL APIs.
  4. Added AES encryption and decryption APIs.
  5. Changed the device information acquisition method of all samples to implementation by APIs at the HAL layer.

### v2.3.3

- Release date: May 6, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Optimized the MQTT keepalive connection mechanism and ping request packet sending policy.
  2. Stored the topic names of MQTT subscription/unsubscription in the dynamic memory to make them easier to be called.
  3. Changed the maximum length of topic name to 128 for consistency with the cloud backend.
  4. Fixed the bugs with the acquisition of `sys` and `log` messages by HTTPC and MQTT.
  5. Optimized the error code types.

### v2.3.2

- Release date: April 12, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Fixed user experience issues: added the gateway compilation option (disabled by default) in `make.settings` and modified the firmware update print level.
  2. Fixed the problem where the MQTT receiving buffer was prone to loss during shadow message downstreaming: added an error message when the receiving buffer was insufficient, and changed the default size of the MQTT sending/receiving buffer to 2,048 bytes.
  3. Changed the maximum number of successfully subscribed topics to 10.

### v2.3.1

- Release date: March 12, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
1. Added the device log reporting feature in the SDK, making it easier for users to remotely monitor and diagnose the network status of devices in the console (only supported for the MQTT mode).
2. Streamlined the printout content of SDK logs, fixed several bugs, and optimized the code design.
3. Changed the maximum length of device name to 48 characters for consistency with the IoT Hub console.





### v2.3.0

- Release date: February 25, 2019
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
 1. Added the gateway feature to allow gateway devices to connect/disconnect and send/receive messages on behalf of subdevices based on the MQTT protocol.
 2. Optimized the thread safety design for multithreaded applications and added multithreaded routines and precautions in the samples.
 3. Optimized the MQTT reconnection mechanism and heartbeat packet timer refresh policy.
 4. Fixed several bugs and added validity checks for some memory operations.
 5. Removed the bit field operation mode from some structures to reduce cross-platform errors.


​	
​	

### v2.2.0  
- Release date: July 20, 2018
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
	1. Added the NB-IoT device connection capability.
	2. Adapted to the topic wildcards `#` and `+`.
	3. Organized the directory structure of third-party libraries.
	4. Fixed several bugs.
  
	
### v2.1.0
- Release date: May 2, 2018
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
	1. Added the new firmware update capability (over the OTA-CoAP channel).
	2. Added the HMAC-SHA1 connection authentication capability for low-end resource-constrained devices.
	3. Added the capability to get backend time.


### v2.0.0
- Release date: March 12, 2018
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
	1. Added the new firmware update capability (over the OTA-MQTT channel).
	2. Fixed the issue where the device shadow heartbeat interval was invalid.
	3. Fixed the issue where the data received by MQTT caused buffer overflow when the data length was at the threshold.
  
### v1.2.2
- Release date: February 7, 2018
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
	1. Added support for MQTT/CoAP symmetric encryption connection.
	2. Optimized the Linux C compilation.

### v1.2.1
- Release date: February 2, 2018
- Programming language: C
- Development environments: Linux/GNU Make
- Content: fixed the incorrect logic of message publishing timeout callback.


### v1.2.0
- Release date: January 17, 2018
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Modified the message publishing/subscribing ACKs for receipt through the callback without blocking the sending thread.
  2. Added the capabilities of devices and the backend for connection and logging.
  3. Added the new UDP-based CoAP channel which used DTLS asymmetric encryption and consumed less power in pure data reporting scenarios.

### v1.0.0
- Release date: November 15, 2017
- Programming language: C
- Development environments: Linux/GNU Make
- Content:
  1. Added support for the MQTT protocol: devices could quickly and easily connect to the cloud server of IoT Hub. For more information, please see [MQTT Protocol Details](https://github.com/mcxiaoke/mqtt).
  2. Added support for device shadow: for more information, please see [Device Shadow Details](https://intl.cloud.tencent.com/document/product/1105/41834).
  3. Added support for symmetric and asymmetric encryption.

