

腾讯云物联网设备端 C SDK 依靠安全且性能强大的数据通道，为物联网领域开发人员提供设备端快速接入云端，并和云端进行双向通信的能力。

>?在版本v3.1.0之后，SDK 对编译环境，代码及目录结构进行了重构优化，提高了可用性和可移植性。 

## C SDK 适用范围
C SDK 采用模块化设计，分离核心协议服务与硬件抽象层，并提供灵活的配置选项和多种编译方式，适用于不同设备的开发平台和使用环境。

#### 具备网络通讯能力并使用 Linux/Windows 操作系统的设备

- 对于具备网络通讯能力并使用标准 Linux/Windows 系统的设备。例如 PC/服务器/网关设备，及较高级的嵌入式设备树莓派等，可直接在该设备上编译运行 SDK。
- 对于需要交叉编译的嵌入式 Linux 设备，如果开发环境的 toolchain 具备 glibc 或类似的库，可以提供包括 socket 通讯，select 同步 IO，动态内存分配，获取时间/休眠/随机数/打印函数，以及临界数据保护如 Mutex 机制（仅在需要多线程时）等系统调用，则只要做简单适配（例如，在 CMakeLists.txt 或 make.settings 里修改交叉编译器的设定）即可编译运行 SDK。

#### 具备网络通讯能力并采用 RTOS 系统的设备
- 对于具备网络通讯能力并采用 RTOS 的物联网设备，C SDK 需要针对不同的 RTOS 做移植适配工作，目前 C SDK 已经适配了包括 FreeRTOS/RT-Thread/TencentOS tiny 等多个面向物联网的 RTOS 平台。
- 在 RTOS 设备移植 SDK 时，如果平台提供了类似 newlib 的 C 运行库和类似 lwIP 的嵌入式 TCP/IP 协议栈，则移植适配工作也可轻松完成。

#### MCU+ 通讯模组的设备

- 对于不具备网络通讯能力的 MCU，一般采用 MCU+ 通讯模组的方式，通讯模组（包括 Wi-Fi/2G/4G/NB-IoT）一般提供了基于串口的 AT 指令协议供 MCU 进行网络通讯。针对这种场景，C SDK 封装了 AT-socket 网络层，网络层之上的核心协议和服务层无须移植。并提供了基于 FreeRTOS 和不带操作系统（nonOS）两种方式的 HAL 实现。
- 除此之外，腾讯云物联网还提供了专用的 AT 指令集，如果通讯模组实现了该指令集，则设备接入和通讯更为简单，所需代码量更少，针对这种场景，请参考面向腾讯云定制 AT 模组专用的 [MCU AT SDK](https://github.com/tencentyun/qcloud-iot-sdk-tencent-at-based.git)。

## SDK 目录结构简介

目录结构及顶层文件简介如下：

| 名称               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| CMakeLists.txt     | cmake 编译描述文件                                            |
| CMakeSettings.json | visual studio下的 cmake 配置文件                               |
| cmake_build.sh     | Linux 下使用 cmake 的编译脚本                                   |
| make.settings      | Linux 下使用 Makefile 直接编译的配置文件                        |
| Makefile           | Linux 下使用 Makefile 直接编译                                  |
| device_info.json   | 设备信息文件，当 DEBUG_DEV_INFO_USED=OFF 时，将从该文件解析出设备信息 |
| docs               | 文档目录，SDK 在不同平台下使用说明文档                      |
| external_libs      | 第三方软件包组件，例如 mbedtls                                  |
| samples            | 应用示例                                                     |
| include            | 提供给用户使用的外部头文件                                   |
| platform           | 平台相关的源码文件，目前提供了针对不同 OS（Linux/Windows/FreeRTOS/nonOS），TLS（mbedtls）以及 AT 模组下的实现 |
| sdk_src            | SDK 核心通信协议及服务代码                                    |
| tools              | SDK 配套的编译及代码生成脚本工具                              |

## SDK 编译方式说明

C SDK 支持三种编译方式：
- cmake 方式。
- Makefile 方式。
- 代码抽取方式。

编译方式以及编译配置选项的详细说明请参考 [编译配置说明](https://intl.cloud.tencent.com/document/product/1105/41850) 和 [编译环境说明](https://intl.cloud.tencent.com/document/product/1105/41851)。

## SDK 示例体验
C SDK 的 samples 目录有使用各个功能的示例，关于运行示例的详细说明，请参考 SDK 文档目录下所有文档。
物联网通信平台快速体验设备端 MQTT 接入和收发消息，请参考 [MQTT 快速入门
](https://intl.cloud.tencent.com/document/product/1105/41852)。

## 注意事项

#### OTA 升级 API 变化
从 SDK 版本3.0.3开始，OTA 升级支持了断点续传，当固件下载过程中如果因为网络异常或其他原因被打断，可以将已经下载的固件部分保存，在下次恢复下载时候可以不用从零开始下载，而是从未下载的部分开始。
在支持这一新特性之后，OTA 相关 API 的使用方法发生了变化，对于从3.0.2及以前的版本升级的用户，需要修改用户逻辑代码，否则固件下载会失败，请参考`samples/ota/ota_mqtt_sample.c`进行修改。

#### 代码命名变化
为了提高代码可读性，保证命名规范，SDK 3.1.0版本对部分变量、函数及宏命名进行了变更，对于从3.0.3及以前的版本升级的用户，可以在 Linux 环境下面执行 `tools/update_from_old_SDK.sh` 脚本，对自己的用户代码执行名字替换，替换完成就可以直接使用新版本的 SDK。

| 旧命名              | 新命名                                                         |
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
| product_key           | product_secret。 |
| DEBUG            | eLOG_DEBUG                                    |
| INFO              | eLOG_INFO                              |
| WARN            | eLOG_WARN                                                     |
| ERROR            | eLOG_ERROR                                   |
| DISABLE           | eLOG_DISABLE |
| Log_writter            | IOT_Log_Gen                                    |
| qcloud_iot_dyn_reg_dev              | IOT_DynReg_Device                              |
| IOT_SYSTEM_GET_TIME              | IOT_Get_SysTime                              |


