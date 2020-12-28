
## TIMInit

This API is used to initialize the IM SDK.

**Prototype**

```c
TIM_DECL int TIMInit(uint64_t sdk_app_id, const char* json_sdk_config);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| sdk_app_id | Uint64_t | SDKAppID applied for from the Tencent Cloud official website. |
| json_sdk_config | Const char\* | JSON string of the IM SDK configuration option. For more information, see [SdkConfig](https://intl.cloud.tencent.com/document/product/1047/34551#sdkconfig). |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>?
- Initialize the IM SDK before using the IM SDK for further operations.
- `json_sdk_config` can be set to a `NULL` string pointer or a "" null string, in which case the default SdkConfig value is used.
- Every JSON key in `json_sdk_config` is optional. For more information, see [SdkConfig](https://intl.cloud.tencent.com/document/product/1047/34551#sdkconfig).


**Example**

```c
Json::Value json_value_init;
json_value_init[kTIMSdkConfigLogFilePath] = "D:\\";
json_value_init[kTIMSdkConfigConfigFilePath] = "D:\\";

uint64_t sdk_app_id = 1234567890;
if (TIM_SUCC != TIMInit(sdk_app_id, json_value_init.toStyledString().c_str())) {
    // Failed to call the TIMInit API. IM SDK initialization fails.   
}

// The json_sdk_config JSON string obtained by json_value_init.toStyledString() is as follows:
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

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>?Call this API to uninstall the IM SDK and clear IM SDK resources before you uninstall the DLL or exit a process.


**Example**

```c
if (TIM_SUCC != TIMUninit()) {
    // Failed to uninstall the IM SDK.  
}
```


## TIMGetSDKVersion

This API is used to obtain the IM SDK version number.

**Prototype**

```c
TIM_DECL const char* const TIMGetSDKVersion(void);
```

**Return values**

| Type | Description |
|-----|-----|
| Const char\* | Version number of the IM SDK |

## TIMSetConfig

This API is used to set extra user configurations.

**Prototype**

```c
TIM_DECL int TIMSetConfig(const char* json_config, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_config | Const char\* | Configuration option. |
| cb | TIMCommCallback | Callback for returning all set configurations. The callback cb can be null, which indicates that all configurations are not obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>? `json_config` can be set to a `NULL` string pointer or a "" null string. If the callback cb is not null, call the callback cb to return all the configurations. Currently, the following items can be configured: IP address and port of the HTTP proxy, IP address and port of the SOCKS5 proxy, output log level, default option for obtaining the group or group member information, and whether to accept the message read receipt event. We recommend that you configure the IP addresses and ports of the HTTP proxy and SOCKS5 proxy before calling [TIMInit](#timinit). These items can be configured either separately or together. For more information, see [SetConfig](https://intl.cloud.tencent.com/document/product/1047/34551#setconfig).


**Example 1**

```c
Json::Value json_user_config;
json_user_config[kTIMUserConfigIsReadReceipt] = true;  // Enable the read receipt.
Json::Value json_config;
json_config[kTIMSetConfigUserConfig] = json_user_config;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API.
} 

// The json_config JSON string obtained by json_config.toStyledString().c_str() is as follows:
{
   "set_config_user_config" : {
      "user_config_is_read_receipt" : true
   }
}
```


**Example 2: Enabling the HTTP proxy**

```c
Json::Value json_http_proxy;
json_http_proxy[kTIMHttpProxyInfoIp] = "http://http-proxy.xxxxx.com ";
json_http_proxy[kTIMHttpProxyInfoPort] = 8888;
Json::Value json_config;
json_config[kTIMSetConfigHttpProxyInfo] = json_http_proxy;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API.
}
```


**Example 3: Disabling the HTTP proxy**

```c
Json::Value json_http_proxy;
json_http_proxy[kTIMHttpProxyInfoIp] = "";
json_http_proxy[kTIMHttpProxyInfoPort] = 0;
Json::Value json_config;
json_config[kTIMSetConfigHttpProxyInfo] = json_http_proxy;

if (TIM_SUCC != TIMSetConfig(json_config.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    // Internal content of the callback
}, this)) {
    // Failed to call the TIMSetConfig API.
}
```


**Example 4: Enabling the SOCKS5 proxy**

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
    // Failed to call the TIMSetConfig API.
}
```


**Example 5: Disabling the SOCKS5 proxy**

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
    // Failed to call the TIMSetConfig API.
}
```

