For MCUs that have no network communication capabilities, the "MCU + communication module" combination is often used. Communication modules (including Wi-Fi/2G/4G/NB-IoT) generally provide serial port-based AT instruction protocols for MCUs to communicate over the network. For this scenario, the C-SDK encapsulates the AT-socket network layer, where the core protocol and service layer don't need to be ported. This document describes how to port C-SDK for connection to IoT Hub in the target environment of MCU (FreeRTOS) + universal TCP AT module.

## SDK Download
Download the latest version of the device [C-SDK](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c).

## SDK Feature Configuration
Use the general TCP module to compile and configure the options as follows:

| Name | Configuration | Description |
| :------------------------------- | ------------- | ------------------------------------------------------------ |
| BUILD_TYPE | debug/release | Set as needed |
| EXTRACT_SRC | ON | Enable code extraction |
| COMPILE_TOOLS | gcc/MSVC | Set as needed and ignore in case of IDE |
| PLATFORM | Linux/Windows | Set as needed and ignore in case of IDE |
| FEATURE_OTA_COMM_ENABLED | ON/OFF | Set as needed |
| FEATURE_AUTH_MODE | KEY | Key authentication is recommended for resource-constrained devices |
| FEATURE_AUTH_WITH_NOTLS | ON/OFF | Enable TLS as needed |
| FEATURE_EVENT_POST_ENABLED | ON/OFF | Enable event reporting as needed |
| FEATURE_AT_TCP_ENABLED | ON | Whether to enable TCP feature in AT module  |
| FEATURE_AT_UART_RECV_IRQ | ON | Whether to enable receipt interruption feature in AT module |
| FEATURE_AT_OS_USED | ON | Whether to enable multithreaded feature in AT module |
| FEATURE_AT_DEBUG | OFF | The AT module debugging feature is disabled by default, and it needs to be enabled during debugging |

## Code Extraction
1. Run the following command on Linux:
```
mkdir build
cd build
cmake ..
```
2. You can find the relevant code files in `output/qcloud_iot_c_sdk` with the following directory hierarchy:
```
 qcloud_iot_c_sdk
 ├── include
 │   ├── config.h
 │   ├── exports
 ├── platform
 └── sdk_src
     └── internal_inc
```
>?
> - `include` directory: contains the SDK APIs and variable parameters, where `config.h` is the compilation macros generated according to the compilation options.
> - `platform` directory: contains platform-related code, which can be modified and adapted according to the specific conditions of the device.
> - `sdk_src` directory: contains the SDK core logic and protocol-related code, which generally don't need to be modified, where `internal_inc` is the header file used internally by the SDK.
3. You can copy `qcloud_iot_c_sdk` to the compilation and development environment of your target platform and then modify the compilation options as needed.

## HAL Porting

Please refer to [Overview](https://intl.cloud.tencent.com/document/product/1105/41844) to port first.
For network HAL APIs, the `AT_Socket` framework provided by the SDK has been selected through the above compilation options. The SDK will call the `at_socket` API of `network_at_tcp.c`. You don't need to port the `at_socket` layer, but you need to implement the AT serial port driver and AT module driver. For the AT module driver, you only need to implement the driver API of the driver structure `at_device_op_t` in `at_device` of the AT framework. You can refer to the supported modules in the `at_device` directory.
Currently, the SDK provides underlying API implementation for the Wi-Fi module ESP8266, which is widely used in the IoT field, for reference when you port to other communication modules.

## Business Logic Development

You can refer to the routines in the SDK's `samples` directory for development.


