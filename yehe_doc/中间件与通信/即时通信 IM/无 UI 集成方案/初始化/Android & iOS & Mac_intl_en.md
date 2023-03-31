## Feature Description
You **must** initialize the IM SDK before using its features.
In most scenarios, you need to initialize the IM SDK only once during the application lifecycle.

## Initialization
You can initialize the SDK in the following steps:
1. Prepare an `SDKAppID`.
2. Configure the `V2TIMSDKConfig` object.
3. Add an SDK event listener.
4. Call `initSDK` to initialize the SDK.

The detailed steps are as follows.

[](id:SDKAppID)
### Preparing an SDKAppID
`SDKAppID` uniquely identifies a Tencent Cloud IM account.
We recommend you apply for a new `SDKAppID` for each application. Messages are naturally isolated and cannot communicate between different `SDKAppID` values.
To perform the initialization, you must have a correct `SDKAppID`.
In the [IM console](https://console.cloud.tencent.com/im), you can view all your `SDKAppID` values, and you can click **Create Application** to create an `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/0f985a6fa6ac7f6a8c278ae021da7b12.png)


[](id:SDKConfig)
### Configuring the `V2TIMSDKConfig`

Before initializing the SDK, you need to initialize the `V2TIMSDKConfig` object ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKConfig.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMSDKConfig.html)), which is used to configure the SDK initially, such as setting the log level and log listening callback.

#### Setting the log level
The IM SDK supports the following log levels:

| Log Level       | Log Output                                                   |
| --------------- | ------------------------------------------------------------ |
| V2TIM_LOG_NONE  | No log is output.                                            |
| V2TIM_LOG_DEBUG | Logs at the DEBUG, INFO, WARNING, and ERROR levels are output (default log levels). |
| V2TIM_LOG_INFO  | Logs at the INFO, WARNING, and ERROR levels are output.      |
| V2TIM_LOG_WARN  | Logs at the WARNING and ERROR levels are output.             |
| V2TIM_LOG_ERROR | Logs at the ERROR level are output.                          |

SDK log storage rules are as follows:
- Local IM SDK logs are retained for seven days by default, after which the logs will be automatically cleared during the SDK initialization.
- By default, IM SDK logs on Android are stored in the `/sdcard/tencent/imsdklogs/application package name` directory for versions earlier than v4.8.50 and in the `/sdcard/Android/data/package name/files/log/tencent/imsdk` directory for v4.8.50 or later.
  

Starting from v4.7.1, the xlog module from WeChat is used to output IM SDK logs, which are compressed by default and must be decompressed by using the Python script.
 - To obtain the script for decompression, click [Decode Log 27](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python27.py) (for Python 2.7) or [Decode Log 30](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python30.py) (for Python 3.0).
 - In the Windows or macOS console, you can decompress log files by running the following command. After decompression, the file names end with "xlog.log", and you can use the text editor to open these files.
```
python decode_mars_nocrypt_log_file.py imsdk_yyyyMMdd.xlog
```

#### Setting a log listener
If you need to listen on IM SDK logs in real time, you can call `setLogListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKConfig.html#a5e8f7fa8dc56123e353a416d8742835b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMSDKConfig.html#aef1bb8224f845539ecb15cccfd07f82b)) to set a log listener.
After it is set, the SDK will throw log information through this callback in real time.

> ! The callback is in the main thread. Log callbacks can be quite frequent, so be careful not to synchronize too many time-consuming tasks in the callback, which may block the main thread.


The sample code of configuring `V2TIMSDKConfig` is as follows:

<dx-tabs>
::: Android
```java
// Initialize the `config` object
V2TIMSDKConfig config = new V2TIMSDKConfig();
// Specify the log output level
config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_INFO);
// Specify the log listener
config.setLogListener(new V2TIMLogListener() {
    @Override
    public void onLog(int logLevel, String logContent) {
        // `logContent` is the SDK log content
    }
});
```
:::
::: iOS and macOS
```objectivec
// Initialize the `config` object
V2TIMSDKConfig *config = [[V2TIMSDKConfig alloc] init];
// Specify the log output level
config.logLevel = V2TIM_LOG_INFO;
// Set the log listener
config.logListener = ^(V2TIMLogLevel logLevel, NSString *logContent) {
    // `logContent` is the SDK log content
};
```
:::
</dx-tabs>


### Adding an SDK event listener
After the initialization, the SDK will report such events as connection status and login ticket expiration through `V2TIMSDKListener`.
We recommend you call the `addIMSDKListener` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2f0297e96d365013e7923275ce2a5d4e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac569656a58908afba491710a8cb3c8d9)) to add an SDK event listener and perform logic processing in the corresponding callback.

`V2TIMSDKListener` callbacks are as follows:

| Event Callback    | Description                                            | Recommended Operation                                        |
| ----------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| onConnecting      | The SDK is connecting to the CVM instance.             | Display the "connecting" status on the UI.                   |
| onConnectSuccess  | The SDK is successfully connected to the CVM instance. | -                                                            |
| onConnectFailed   | The SDK failed to connect to the CVM instance.         | Notify the user that the network connection is currently unavailable. |
| onKickedOffline   | The current user is kicked offline.                    | Display the "You are already logged in on another device. Are you sure you want to log in again?" message on the UI. |
| onUserSigExpired  | The login ticket expired.                              | Log in with a new `UserSig`.                                 |
| onSelfInfoUpdated | The current user's profile is updated.                 | Update the profile photo and nickname on the UI.             |

>! If you receive the `onUserSigExpired` callback, the `UserSig` that you use for login has expired. In this case, you need to use a new `UserSig` to log in again. If you continue to use the expired `UserSig`, the IM SDK will be in an infinite login loop.

Sample code:
<dx-tabs>
::: Android
```java
// The `sdkListener` type is `V2TIMSDKListener`.
V2TIMManager.getInstance().addIMSDKListener(sdkListener);
```
:::

::: iOS and macOS
```objectivec
// The `self` type is id<V2TIMSDKListener>.
[[V2TIMManager sharedInstance] addIMSDKListener:self];
```
:::
</dx-tabs>


### Calling the initialization API
After performing the above steps, you can call `initSDK` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#aaad4f7139ba213f7e36da3e337c2f890) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2b417a8af0e974233baf1593ffa6c0f0)) to initialize the SDK.

Sample code:
<dx-tabs>
::: Android
```java
// 1. Get the `SDKAppID` from the IM console.
// 2. Initialize the `config` object.
V2TIMSDKConfig config = new V2TIMSDKConfig();
// 3. Specify the log output level.
config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_INFO);
// 4. Add the `V2TIMSDKListener` event listener. `sdkListener` is the implementation class of `V2TIMSDKListener`. If you don't need to listen to IM SDK events, skip this step.
V2TIMManager.getInstance().addIMSDKListener(sdkListener);
// 5. Initialize the IM SDK. You can call the login API as soon as you call this API.
V2TIMManager.getInstance().initSDK(context, sdkAppID, config);
```
:::

::: iOS and macOS
```objectivec
// 1. Get the `SDKAppID` from the IM console.
// 2. Initialize the `config` object.
V2TIMSDKConfig *config = [[V2TIMSDKConfig alloc] init];
// 3. Specify the log output level.
config.logLevel = V2TIM_LOG_INFO;
// 4. Add the `V2TIMSDKListener` event listener. `self` is the implementation class of id<V2TIMSDKListener>. If you don't need to listen to IM SDK events, skip this step.
[[V2TIMManager sharedInstance] addIMSDKListener:self];
// 5. Initialize the IM SDK. You can call the login API as soon as you call this API.
[[V2TIMManager sharedInstance] initSDK:sdkAppID config:config];
```
:::
</dx-tabs>

### Uninitialization
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, you don't need to uninitialize the IM SDK before exiting the application.
However, you can uninitialize the IM SDK in special cases, for example, only after you enter a specific UI and no longer use it after exiting the UI.

Uninitialization requires two steps:
1. If you have called `addIMSDKListener` to add the SDK listener, call `removeIMSDKListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9b98e6b9ac0f883f055ef82563467b43) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2e2a7e64bf51888c98636e5974a8aca7)) to remove it.
2. Call the `unInitSDK` uninitialization API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8ac73b4f71f9d9a1ca01551c919d3cdd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544)).

Sample code:
<dx-tabs>
::: Android
```java
// Remove the `V2TIMSDKListener` event listener. `sdkListener` is the implementation class of `V2TIMSDKListener`.
V2TIMManager.getInstance().removeIMSDKListener(sdkListener);
// Uninitialize the SDK
V2TIMManager.getInstance().unInitSDK();
```
:::

::: iOS and macOS
```objectivec
// `self` is the implementation class of id<V2TIMSDKListener>.
[[V2TIMManager sharedInstance] removeIMSDKListener:self];
// Uninitialize the SDK
[[V2TIMManager sharedInstance] unInitSDK];
```
:::
</dx-tabs>


[](id:qa)
## FAQs

[](id:qa1)
### 1. What should I do if error code 6013 is returned along with the description "not initialized" when I call the login or another API?
You must initialize the IM SDK before using the login, message, group, conversation, relationship chain and profile, and signaling features.
