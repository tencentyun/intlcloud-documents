## Compilation

Please first download the latest version of the device-side C language SDK [here](https://github.com/tencentyun/qcloud-iot-sdk-embedded-c/releases).

After decompression, open the compilation configuration file ```make.settings``` and edit the configuration items as needed.

```
BUILD_TYPE                    = release	#release/debug

PLATFORM_CC                   = gcc
PLATFORM_AR                   = ar
PLATFORM_OS                   = linux
PLATFORM_SSL                  = mbedtls

#
# Uncomment below and specify PATH to your toolchain when cross-compile SDK
#
# PLATFORM_CC                 = /home/shock/openwrt/packages/toolchain/mipsel-linux-gcc
# PLATFORM_AR                 = /home/shock/openwrt/packages/toolchain/mipsel-linux-ar
# PLATFORM_CC                 = armcc
# PLATFORM_AR                 = armar

FEATURE_MQTT_COMM_ENABLED     = y    # Whether to turn on the master switch of the MQTT channel
FEATURE_MQTT_DEVICE_SHADOW    = y    # Whether to turn on the master switch of the device shadow
FEATURE_COAP_COMM_ENABLED     = y    # Whether to turn on the master switch of the CoAP channel
FEATURE_NBIOT_COMM_ENABLED    = y    # Whether to turn on the message assembly of the NB-IoT channel

FEATURE_OTA_COMM_ENABLED      = y    # Whether to turn on the master switch of the OTA firmware upgrade
FEATURE_OTA_SIGNAL_CHANNEL    = MQTT # OTA signaling channel type: MQTT/CoAP

FEATURE_AUTH_MODE             = CERT # MQTT/CoAP access authentication method; CERT: authentication with certificate; KEY: authentication with key
FEATURE_AUTH_WITH_NOTLS       = n    # Whether not to use TLS for access authentication; TLS is required for authentication with certificate, but it is optional for authentication with key

FEATURE_SYSTEM_COMM_ENABLED   = y    # Whether to enable the function to get the IoT backend time
```
The specific meanings are listed in the table below:

| Configuration item                       | Meaning                                                                                    |
| ----------------------------- | --------------------------------------------------------------------------------------- |
| BUILD_TYPE | Compilation mode; if it is debug, the code tracking function is enabled, and the call stack of the functions will be tracked and printed when the program runs |
| PLATFORM_CC | C source compiler; when using cross-compilation, please make sure that gcc and ar are in the same directory |
| PLATFORM_AR | Static library compressor; when using cross-compilation, please make sure that gcc and ar are in the same directory |
| PLATFORM_OS | Specify the operating system of the target platform; a Linux version example is included in the SDK |
| FEATURE_MQTT_COMM_ENABLED | Whether to enable the device MQTT function; enabled by default |
| FEATURE_MQTT_DEVICE_SHADOW | Whether to enable the device shadow function; enabled by default |
| FEATURE_COAP_COMM_ENABLED | Whether to enable the device CoAP function; enabled by default |
| FEATURE_OTA_COMM_ENABLED | Whether to enable the device OTA function; enabled by default |
| FEATURE_OTA_SIGNAL_CHANNEL | OTA channel selection: MQTT or CoAP; MQTT channel by default |
| FEATURE_AUTH_MODE | MQTT/CoAP access authentication method; CERT: authentication with certificate; KEY: authentication with key; CERT by default |
| FEATURE_AUTH_WITH_NOTLS | Whether not to use TLS for access authentication; TLS is required for authentication with certificate, but it is optional for authentication with key; TLS not used by default |
| FEATURE_SYSTEM_COMM_ENABLED | Whether to enable the function to get the IoT backend time; enabled by default |

## Run
See [Quick Start](https://cloud.tencent.com/document/product/634/11912).

## Descriptions of the APIs Provided by C-SDK
The following are the features and corresponding APIs provided by C-SDK v2.1.0 for reference when writing business logic. For more detailed instructions, see the comments in src/sdk-impl/qcloud_iot_export.h and src/sdk-impl/exports/*.h.

### 1. Log API

| No. | Function name | Description |
| ---- | -------------------------- | --------------------------------------------- |
| 1 | IOT_Log_Set_Level | Set the log level for printing |
| 2 | IOT_Log_Get_Level | Return the level of log output |
| 3 | IOT_Log_Set_MessageHandler | Set the log callback function to take over the SDK log for other output methods |


### 2. MQTT API

| No. | Function name | Description |
| ---- | -------------------- | ----------------------------------------------- |
| 1 | IOT_MQTT_Construct | Construct MQTTClient and complete the MQTT connection |
| 2 | IOT_MQTT_Destroy | Close the MQTT connection and terminate MQTTClient |
| 3 | IOT_MQTT_Yield | Yield a certain amount of CPU execution time for the underlying MQTT client in the current thread |
| 4 | IOT_MQTT_Publish | Publish an MQTT message |
| 5 | IOT_MQTT_Subscribe | Subscribe to an MQTT topic |
| 6 | IOT_MQTT_Unsubscribe | Unsubscribe from the subscribed MQTT topic |
| 7 | IOT_MQTT_IsConnected | Check whether the firmware is downloading |


### 3. Device Shadow API

| No. | Function name | Description |
| ---- | -------------------------------------------------- | ---------------------------------------------- |
| 1 | IOT_Shadow_Construct | Construct the ShadowClient |
| 2 | IOT_Shadow_Publish | Publish an MQTT message |
| 3 | IOT_Shadow_Subscribe | Subscribe to an MQTT message |
| 4 | IOT_Shadow_Unsubscribe | Unsubscribe from an MQTT message |
| 5 | IOT_Shadow_IsConnected | Whether the Shadow client is currently connected |
| 6 | IOT_Shadow_Destroy | Close the Shadow connection and terminate the ShadowClient |
| 7 | IOT_Shadow_Yield | Yield a certain amount of CPU execution time for the underlying Shadow client in the current thread |
| 8 | IOT_Shadow_Update | Update the device shadow document asynchronously |
| 9 | IOT_Shadow_Update_Sync | Update the device shadow document synchronously |
| 10 | IOT_Shadow_Get | Get the device shadow document asynchronously |
| 11 | IOT_Shadow_Get_Sync | Get the device shadow document synchronously |
| 12 | IOT_Shadow_Register_Property | Register device attributes of the current device |
| 13 | IOT_Shadow_UnRegister_Property | Delete the registered device attributes |
| 14 | IOT_Shadow_JSON_ConstructReport | Add a reported field to the JSON document for update in a non-overwriting manner |
| 15 | IOT_Shadow_JSON_Construct_OverwriteReport | Add a reported field to the JSON document for update in an overwriting manner |
| 16 | IOT_Shadow_JSON_ConstructReportAndDesireAllNull | Add a reported field to the JSON document and empty the desired field |
| 17 | IOT_Shadow_JSON_ConstructDesireAllNull | Add a "desired": null field to the JSON document |


### 4. CoAP API

| No. | Function name | Description |
| ---- | ---------------------------- | ------------------------------------------------- |
| 1 | IOT_COAP_Construct | Construct the CoAPClient and complete the CoAP connection |
| 2 | IOT_COAP_Destroy | Close the CoAP connection and terminate the CoAPClient |
| 3 | IOT_COAP_Yield | Yield a certain amount of CPU execution time for the underlying CoAP client in the current thread |
| 4 | IOT_COAP_SendMessage | Publish a CoAP message |
| 5 | IOT_COAP_GetMessageId | Get the msgId of the CoAP Response message |
| 6 | IOT_COAP_GetMessagePayload | Get the content of the CoAP Response message |
| 7 | IOT_COAP_GetMessageCode | Get the error code of the CoAP Response message |


### 5. OTA API

| No. | Function name | Description |
| ---- | ---------------------------- | ------------------------------------------------- |
| 1 | IOT_OTA_Init | Initialize the OTA module; the client must be initialized before calling this API |
| 2 | IOT_OTA_Destroy | Release the resources related to OTA module |
| 3 | IOT_OTA_ReportVersion | Report firmware version information to the OTA server |
| 4 | IOT_OTA_ReportUpgradeBegin | Before upgrading, the status of the upgrade start needs to be reported to the OTA server |
| 5 | IOT_OTA_ReportUpgradeSuccess | After the upgrade is successful, the status of the upgrade success needs to be reported to the OTA server |
| 6 | IOT_OTA_ReportUpgradeFail | After the upgrade fails, the status of the upgrade failure needs to be reported to the OTA server |
| 7 | IOT_OTA_IsFetching | Check whether the firmware is being downloaded |
| 8 | IOT_OTA_IsFetchFinish | Check whether the firmware has been downloaded |
| 9 | IOT_OTA_FetchYield | Get the firmware from a remote server with a specific timeout value |
| 10 | IOT_OTA_Ioctl | Get the specified OTA information |
| 11 | IOT_OTA_GetLastError | Get the last error code |


### 6. SYSTEM API

| No. | Function name | Description |
| ---- | ---------------------------- | ------------------------------------------------- |
| 1 | IOT_SYSTEM_GET_TIME | Get IoT Hub's backend time; currently, the time syncing function is supported only for the MQTT channel |

### 7. NB-IoT API

| No. | Function name | Description |
| ---- | ---------------------------- | ------------------------------------------------- |
| 1 | IOT_NB_setMessage | API for NB-IoT platform uplink message encoding API |
| 2 | IOT_NB_getMessage | API for NB-IoT platform downlink message decoding |
