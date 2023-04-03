## TIMInit

This API is used to initialize the IM SDK.

**Prototype**

```c
TIM_DECL int TIMInit(uint64_t sdk_app_id, const char* json_sdk_config);
```

**Parameters**

| Parameter       | Type         | Description                                                  |
| --------------- | ------------ | ------------------------------------------------------------ |
| sdk_app_id      | uint64_t     | `SDKAppID` applied for from the Tencent Cloud official website. |
| json_sdk_config | const char\* | JSON string of the IM SDK configuration option. For more information, see [SdkConfig](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- Initialize the IM SDK before using the IM SDK for further operations.
- In `json_sdk_config`, the two JSON keys `kTIMSdkConfigLogFilePath` and `kTIMSdkConfigConfigFilePath` are required. For more information, see [SdkConfig](https://intl.cloud.tencent.com/document/product/1047/34551).

**Example**

```c
Json::Value json_value_init;
json_value_init[kTIMSdkConfigLogFilePath] = "D:\\";
json_value_init[kTIMSdkConfigConfigFilePath] = "D:\\";

uint64_t sdk_app_id = 1234567890;
if (TIM_SUCC != TIMInit(sdk_app_id, json_value_init.toStyledString().c_str())) {
    // TIMInit API call error. IM SDK initialization failed.   
}

// The `json_sdk_config` JSON string obtained by `json_value_init.toStyledString()` is as follows:
{
   "sdk_config_config_file_path" : "D:\\",
   "sdk_config_log_file_path" : "D:\\"
}
```


## TIMUninit

This API is used to uninstall the IM SDK.

**Prototype**

```c
TIM_DECL int TIMUninit(void);
```

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Call this API to uninstall the IM SDK and clear IM SDK resources before you uninstall the DLL or exit a process.


**Example**

```c
if (TIM_SUCC != TIMUninit()) {
    // Failed to uninstall the IM SDK  
}
```


## TIMGetSDKVersion

This API is used to obtain the IM SDK version number.

**Prototype**

```c
TIM_DECL const char* TIMGetSDKVersion(void);
```

**Return values**

| Type         | Description                   |
| ------------ | ----------------------------- |
| const char\* | Version number of the IM SDK. |

## TIMSetConfig

This API is used to set extra user configurations.

**Prototype**

```c
TIM_DECL int TIMSetConfig(const char* json_config, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter   | Type            | Description                                                  |
| ----------- | --------------- | ------------------------------------------------------------ |
| json_config | const char\*    | Configuration option.                                        |
| cb          | TIMCommCallback | Callback function for returning all set configurations. The callback function `cb` can be null, which indicates that all configurations are not obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data   | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?`json_config` can be set to a `NULL` string pointer or a "" null string. If the callback `cb` is not null, call the callback `cb` to return all the configurations. Currently, the following items can be configured: IP address and port of the HTTP proxy, IP address and port of the SOCKS5 proxy, output log level, default option for obtaining the group or group member information, and whether to accept the message read receipt event. We recommend that you configure the IP addresses and ports of the HTTP proxy and SOCKS5 proxy before calling [TIMInit](#timinit). These items can be configured either separately or together. For more information, see [SetConfig](https://intl.cloud.tencent.com/document/product/1047/34551).


**Example 1**

```c
Json::Value json_user_config;
json_user_config[kTIMUserConfigIsReadReceipt] = true;  // Enable the read receipt
Json::Value json_config;
json_config[kTIMSetConfigUserConfig] = json_user_config;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API
} 

// The `json_config` JSON string obtained by `json_config.toStyledString().c_str()` is as follows:
{
   "set_config_user_config" : {
      "user_config_is_read_receipt" : true
   }
}
```


**Example 2: enabling the HTTP proxy**

```c
Json::Value json_http_proxy;
json_http_proxy[kTIMHttpProxyInfoIp] = "http://http-proxy.xxxxx.com ";
json_http_proxy[kTIMHttpProxyInfoPort] = 8888;
Json::Value json_config;
json_config[kTIMSetConfigHttpProxyInfo] = json_http_proxy;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API
}
```


**Example 3: disabling the HTTP proxy**

```c
Json::Value json_http_proxy;
json_http_proxy[kTIMHttpProxyInfoIp] = "";
json_http_proxy[kTIMHttpProxyInfoPort] = 0;
Json::Value json_config;
json_config[kTIMSetConfigHttpProxyInfo] = json_http_proxy;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API
}
```


**Example 4: enabling the SOCKS5 proxy**

```c
Json::Value json_socks5_value;
json_socks5_value[kTIMSocks5ProxyInfoIp] = "111.222.333.444";
json_socks5_value[kTIMSocks5ProxyInfoPort] = 8888;
json_socks5_value[kTIMSocks5ProxyInfoUserName] = "";
json_socks5_value[kTIMSocks5ProxyInfoPassword] = "";
Json::Value json_config;
json_config[kTIMSetConfigSocks5ProxyInfo] = json_socks5_value;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API
}
```


**Example 5: disabling the SOCKS5 proxy**

```c
Json::Value json_socks5_value;
json_socks5_value[kTIMSocks5ProxyInfoIp] = "";
json_socks5_value[kTIMSocks5ProxyInfoPort] = 0;
json_socks5_value[kTIMSocks5ProxyInfoUserName] = "";
json_socks5_value[kTIMSocks5ProxyInfoPassword] = "";
Json::Value json_config;
json_config[kTIMSetConfigSocks5ProxyInfo] = json_socks5_value;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API
}
```

## TIMGetServerTime

This API is used to get the current server time.

**Prototype**

```c
TIM_DECL uint64_t TIMGetServerTime();
```

**Return values**

| Type     | Description              |
| -------- | ------------------------ |
| uint64_t | Server time, in seconds. |

>?Can be used to determine whether a timeout occurs in offline signaling push scenarios.
