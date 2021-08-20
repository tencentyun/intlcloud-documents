

For MCUs that have no network communication capabilities, the "MCU + communication module" combination is often used. Communication modules (including Wi-Fi/2G/4G/NB-IoT) generally provide serial port-based AT instruction protocols for MCUs to communicate over the network. For this scenario, the C-SDK encapsulates the AT-socket network layer, where the core protocol and service layer don't need to be ported. This document describes how to port C-SDK for connection to IoT Hub in the target environment of MCU (nonOS) + universal TCP AT module.
Compared with the RTOS scenario, the network data received by `at_socket` is processed differently. The application layer needs to periodically call **`IOT_MQTT_Yield`** to receive the server's downstream data. If the receipt window is missed, there will be data loss. Therefore, in scenarios with complex business logic, we recommended you use RTOS and select the nonOS mode by configuring `FEATURE_AT_OS_USED = OFF`.

## SDK Download
Download the latest version of the device [C-SDK](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c).

## SDK Feature Configuration
Use the general TCP module to compile and configure the options for nonOS as follows:

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
| FEATURE_AT_TCP_ENABLED | ON | Enable `at_socket` component |
| FEATURE_AT_UART_RECV_IRQ | ON | Enable AT serial port receipt interruption |
| FEATURE_AT_OS_USED               | OFF        | Use `at_socket` component in environment without RTOS                         |
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
 - `include` directory: contains the SDK APIs and variable parameters, where `config.h` is the compilation macros generated according to the compilation options.
 - `platform` directory: contains platform-related code, which can be modified and adapted according to the specific conditions of the device.
 - `sdk_src` directory: contains the SDK core logic and protocol-related code, which generally don't need to be modified, where `internal_inc` is the header file used internally by the SDK.

3. You can copy `qcloud_iot_c_sdk` to the compilation and development environment of your target platform and then modify the compilation options as needed.

## HAL Porting

Please refer to [Overview](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c/blob/master/docs/C-SDK_Porting%E8%B7%A8%E5%B9%B3%E5%8F%B0%E7%A7%BB%E6%A4%8D%E6%A6%82%E8%BF%B0.md) first.

For network HAL APIs, the `AT_Socket` framework provided by the SDK has been selected through the above compilation options. The SDK will call the `at_socket` API of `network_at_tcp.c`. You don't need to port the `at_socket` layer, but you need to implement the AT serial port driver and AT module driver. For the AT module driver, you only need to implement the driver API of the driver structure `at_device_op_t` in `at_device` of the AT framework. You can refer to the supported modules in the `at_device` directory. For the AT serial port driver, you need to implement serial port receipt interruption and then call the callback function `at_client_uart_rx_isr_cb` in the interruption service program. You can refer to `HAL_OS_nonos.c` to port for the target platform.

## Business Logic Development
You can refer to the routines in the SDK's `samples` directory for development.


