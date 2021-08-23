
This document describes the compilation methods and compilation configuration options of the SDK for C, as well as the compilation environment setup and compilation samples in the Linux and Windows development environments.

## SDK for C Compilation Method Description
The SDK for C supports the following compilation methods.

#### CMake
- We recommend you use CMake, a cross-platform compilation tool, for compilation in the Linux and Windows development environments.
- Compilation with CMake uses `CMakeLists.txt` as the input file for compilation configuration options.

#### Makefile
- For environments that don't support CMake, Makefile can be used for compilation.
- As for SDK v3.0.3 or below, compilation with Makefile uses `make.settings` as the input file for compilation configuration options, and you only need to run `make` after the modification.

#### Code extraction
- This method allows you to select features based on your needs and extract the relevant code into a separate folder. The code hierarchy in the folder is concise, making it easy for you to copy and integrate it into your own development environment.
- This method relies on CMake. Configure relevant features in `CMakeLists.txt`, set `EXTRACT_SRC` to `ON`, and run the following command on Linux:
```
mkdir build
cd build
cmake ..
```
 - You can find the relevant code files in `output/qcloud_iot_c_sdk` with the following directory hierarchy:
```
 qcloud_iot_c_sdk
 ├── include
 │   ├── config.h
 │   ├── exports
 ├── platform
 └── sdk_src
     └── internal_inc
```
 - The `include` directory contains the SDK APIs and variable parameters, where `config.h` is the compilation macros generated according to the compilation options.
 - The `platform` directory contains platform-related code, which can be modified and adapted according to the specific conditions of the device.
 - The `sdk_src` directory contains the SDK core logic and protocol-related code, which generally don't need to be modified, where `internal_inc` is the header file used internally by the SDK.

>?You can copy `qcloud_iot_c_sdk` to the compilation and development environment of your target platform and then modify the compilation options as needed.

## SDK for C Compilation Option Description

#### Compilation configuration options
Most of the following configuration options apply to CMake and `make.setting`. The `ON` value in CMake corresponds to `y` in `make.setting`, and `OFF` to `n`.

| Name                             | CMake Value            | Description                                                         |
| :------------------------------- | ------------- | ------------------------------------------------------------ |
| BUILD_TYPE                       | release/debug | release: disable the `IOT_DEBUG` information (the compilation is output to the `release` directory).<br />debug: enable the `IOT_DEBUG` information (the compilation is output to the `debug` directory). |
| EXTRACT_SRC                      | ON/OFF        | Whether to enable code extraction, which takes effect only for CMake.                                             |
| COMPILE_TOOLS                    | gcc           | GCC and MSVC are supported. It can also be a cross compiler, such as `arm-none-linux-gnueabi-gcc`. |
| PLATFORM                         | Linux         | Includes Linux/Windows/FreeRTOS/nonOS.                             |
| FEATURE_MQTT_COMM_ENABLED        | ON/OFF        | Whether to enable MQTT channel.                                               |
| FEATURE_MQTT_DEVICE_SHADOW       | ON/OFF        | Whether to enable device shadow.                                               |
| FEATURE_COAP_COMM_ENABLED        | ON/OFF        | Whether to enable CoAP channel.                                               |
| FEATURE_GATEWAY_ENABLED          | ON/OFF        | Whether to enable gateway feature.                                               |
| FEATURE_OTA_COMM_ENABLED         | ON/OFF        | Whether to enable OTA firmware update.                                            |
| FEATURE_OTA_SIGNAL_CHANNEL       | MQTT/CoAP     | OTA signaling channel type.                                              |
| FEATURE_AUTH_MODE                | KEY/CERT      | Connection authentication method.                                                 |
| FEATURE_AUTH_WITH_NOTLS          | ON/OFF        | OFF: TLS enabled; ON: TLS disabled.    |                                
| FEATURE_DEV_DYN_REG_ENABLED      | ON/OFF        | Whether to enable dynamic device registration.                                             |
| FEATURE_LOG_UPLOAD_ENABLED       | ON/OFF        | Whether to enable log reporting.                                                 |
| FEATURE_EVENT_POST_ENABLED       | ON/OFF        | Whether to enable event reporting.                                                 |
| FEATURE_DEBUG_DEV_INFO_USED      | ON/OFF        | Whether to enable device information source acquisition.                                         |
| FEATURE_SYSTEM_COMM_ENABLED      | ON/OFF        | Whether to enable backend time acquisition.                                             |
| FEATURE_AT_TCP_ENABLED           | ON/OFF        | Whether to enable TCP feature in AT module.                                            |
| FEATURE_AT_UART_RECV_IRQ         | ON/OFF        | Whether to enable receipt interruption feature in AT module.                                       |
| FEATURE_AT_OS_USED               | ON/OFF        | Whether to enable multithreaded feature in AT module.                                         |
| FEATURE_AT_DEBUG                 | ON/OFF        | Whether to enable debugging feature in AT module.                                           |
| FEATURE_MULTITHREAD_TEST_ENABLED | ON/OFF        | Whether to compile the Linux multithreaded test routine.                                  |

There is a dependency relationship between the configuration options. A configuration option is valid only when the value of its dependent option is valid as shown below:

| Name                             | Dependent Option                                                | Valid Value       |
| :------------------------------- | ------------------------------------------------------- | ------------ |
| FEATURE_MQTT_DEVICE_SHADOW       | FEATURE_MQTT_COMM_ENABLED                               | ON           |
| FEATURE_GATEWAY_ENABLED          | FEATURE_MQTT_COMM_ENABLED                               | ON             |
| FEATURE_OTA_SIGNAL_CHANNEL(MQTT) | FEATURE_OTA_COMM_ENABLED<br />FEATURE_MQTT_COMM_ENABLED | ON<br />ON   |
| FEATURE_OTA_SIGNAL_CHANNEL(COAP) | FEATURE_OTA_COMM_ENABLED<br />FEATURE_COAP_COMM_ENABLED | ON<br />ON   |
| FEATURE_AUTH_WITH_NOTLS          | FEATURE_AUTH_MODE                                       | KEY          |
| FEATURE_AT_UART_RECV_IRQ         | FEATURE_AT_TCP_ENABLED                                  | ON           |
| FEATURE_AT_OS_USED               | FEATURE_AT_TCP_ENABLED                                  | ON           |
| FEATURE_AT_DEBUG                 | FEATURE_AT_TCP_ENABLED                                  | ON           |


#### Device information options
After a device is created in the IoT Hub console, you need to configure its information (`ProductID/DeviceName/DeviceSecret/Cert/Key` file) in the SDK first before it can run properly. In the development phase, the SDK provides two methods of storing the device information:
- If the device information is stored in the code (compilation option `DEBUG_DEV_INFO_USED` = `ON`), you should modify the device information in `platform/os/xxx/HAL_Device_xxx.c`. This method can be used on platforms without a file system.
- If the device information is stored in the configuration file (compilation option `DEBUG_DEV_INFO_USED` = `OFF`), you should modify the device information in the `device_info.json` file with no need to recompile the SDK. This method is recommended for development on Linux and Windows.

