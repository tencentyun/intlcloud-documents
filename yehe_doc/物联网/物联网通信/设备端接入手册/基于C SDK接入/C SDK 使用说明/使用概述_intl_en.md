

IoT Hub device SDK for C relies on a secure and powerful data channel to enable IoT developers to quickly connect devices to the cloud for two-way communication.

>?After v3.1.0, the SDK refactored and optimized the compilation environment, code, and directory structure, increasing the availability and portability. 

## Scope of Application of SDK for C
Featuring a modular design, the SDK for C separates the core protocol service from the hardware abstraction layer and provides flexible configuration options and multiple compilation methods, making it suitable for development platforms and use environments of different devices.

#### Network communication-capable devices on Linux/Windows

- For devices that have network communication capabilities and run on standard Linux/Windows, such as PCs, servers, and gateway devices, as well as advanced embedded devices such as Raspberry Pi, you can directly compile and run the SDK on them.
- For embedded Linux devices that require cross compilation, if the toolchain of the development environment has `glibc` or similar libraries which can provide system calls, including socket communication, SELECT sync IO, dynamic memory allocation, functions for getting time/sleeping/generating random number/printing, as well as critical data protection such as the mutex mechanism (only when multiple threads are required), only simple adaptation (e.g., changing the cross compiler settings in `CMakeLists.txt` or `make.settings`) is required before the SDK can be compiled and run.

#### Network communication-capable devices on RTOS
- For IoT devices that have network communication capabilities and run on RTOS, the SDK for C needs to be adapted to different RTOS systems for porting. Currently, it has been adapted to multiple IoT-oriented RTOS platforms, including FreeRTOS, RT-Thread, and TencentOS tiny.
- When porting the SDK to an RTOS device, if the platform provides C runtime libraries like `Newlib` and embedded TCP/IP protocol stacks like lwIP, adaptation for porting can be done easily.

#### Devices with MCU + communication module

- For MCUs that have no network communication capabilities, the "MCU + communication module" combination is often used. Communication modules (including Wi-Fi/2G/4G/NB-IoT) generally provide serial port-based AT instruction protocols for MCUs to communicate over the network. For this scenario, the SDK for C encapsulates the AT-socket network layer, where the core protocol and service layer don't need to be ported. In addition, it provides FreeRTOS-based and nonOS HAL implementation methods.
- In addition, IoT Hub provides a dedicated AT instruction set. If the communication module implements this instruction set, it will be easier for devices to connect and communicate, and less code will be required. For this scenario, please refer to the [SDK for MCU AT](https://github.com/tencentyun/qcloud-iot-sdk-tencent-at-based.git) dedicated to the Tencent Cloud customized AT module.

## SDK Directory Structure Overview

The directory structure and top-level documents are described as follows:

| Name               | Description                                                         |
| ------------------ | ------------------------------------------------------------ |
| CMakeLists.txt     | CMake compilation and description file                                            |
| CMakeSettings.json | CMake configuration file on Visual Studio                               |
| cmake_build.sh     | Compilation script with CMake on Linux                                   |
| make.settings      | Configuration file compiled directly by Makefile on Linux                        |
| Makefile           | Direct compilation with Makefile on Linux                                  |
| device_info.json   | Device information file. If `DEBUG_DEV_INFO_USED` = `OFF`, the device information will be parsed from this file |
| docs               | Documentation directory, i.e., the use instructions of the SDKs for different platforms                      |
| external_libs      | Third-party package components, such as Mbed TLS                                  |
| samples            | Application demos                                                     |
| include            | External header files provided to users                                   |
| platform           | Platform source code files. Currently, implementations are provided for different OS (Linux/Windows/FreeRTOS/nonOS), TLS (Mbed TLS), and AT module |
| sdk_src            | Core communication protocols and service code of the SDK                                    |
| tools              | Compilation and code generation script tools supporting the SDK                              |

## SDK Compilation Method Description

The SDK for C supports three compilation methods:
- CMake
- Makefile
- Code extraction

For more information on the compilation methods and compilation configuration options, please see [Compilation Configuration Description](https://intl.cloud.tencent.com/document/product/1105/41850) and [Compilation Environment (Linux and Windows)](https://intl.cloud.tencent.com/document/product/1105/41851).

## SDK Demos
The `samples` directory of the SDK for C contains demos showing how to use the features. For more information on how to run the demos, please see the corresponding documents in the SDK documentation directory.
For more information on device connection to and message sending/receiving in IoT Hub over MQTT, please see [Getting Started with MQTT](https://intl.cloud.tencent.com/document/product/1105/41852).


## Notes

#### API changes for OTA update
Starting from SDK v3.0.3, OTA update supports checkpoint restart. When the firmware download process is interrupted due to network exceptions or other issues, the downloaded part of the firmware can be saved, so that the download can start from where interrupted instead of from the beginning when it is resumed.
After this new feature was supported, the methods of using relevant OTA APIs changed. If you have upgraded from v3.0.2 or below, you should modify your logic code; otherwise, firmware download will fail. For more information on how to modify it, please see `samples/ota/ota_mqtt_sample.c`.

#### Code name changes
To improve the code readability and comply with the naming conventions, SDK v3.1.0 incorporated changes to certain variables, functions, and macro names. If you have upgraded from v3.0.3 or below, you can run the `tools/update_from_old_SDK.sh` script on Linux to replace the names in your own code, and then you can use the new version of the SDK directly.

| Old Name              | New Name                                                         |
| ------------------ | ------------------------------------------------------------ |
| QCLOUD_ERR_SUCCESS     | QCLOUD_RET_SUCCESS                                            |
| QCLOUD_ERR_MQTT_RECONNECTED | QCLOUD_RET_MQTT_RECONNECTED                               |
| QCLOUD_ERR_MQTT_MANUALLY_DISCONNECTED     | QCLOUD_RET_MQTT_MANUALLY_DISCONNECTED                                   |
| QCLOUD_ERR_MQTT_CONNACK_CONNECTION_ACCEPTED      | QCLOUD_RET_MQTT_CONNACK_CONNECTION_ACCEPTED                        |
| QCLOUD_ERR_MQTT_ALREADY_CONNECTED           | QCLOUD_RET_MQTT_ALREADY_CONNECTED                                  |
| MAX_SIZE_OF_DEVICE_SERC   | MAX_SIZE_OF_DEVICE_SECRET |
| devCertFileName               | dev_cert_file_name                      |
| devPrivateKeyFileName      | dev_key_file_name                                  |
| devSerc            | device_secret                                                     |
| MAX_SIZE_OF_PRODUCT_KEY            | MAX_SIZE_OF_PRODUCT_SECRET                                   |
| product_key           | product_secret |
| DEBUG            | eLOG_DEBUG                                    |
| INFO              | eLOG_INFO                              |
| WARN            | eLOG_WARN                                                     |
| ERROR            | eLOG_ERROR                                   |
| DISABLE           | eLOG_DISABLE |
| Log_writter            | IOT_Log_Gen                                    |
| qcloud_iot_dyn_reg_dev              | IOT_DynReg_Device                              |
| IOT_SYSTEM_GET_TIME              | IOT_Get_SysTime                              |


