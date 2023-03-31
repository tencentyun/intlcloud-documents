## Feature Description

You **must** initialize the IM SDK before using its features.
In most scenarios, you need to initialize the IM SDK only once during the application lifecycle.

## Initialization

You can initialize the SDK in the following steps:

1. Prepare an `SDKAppID`.
2. Set the `LogLevelEnum`.
3. Set the SDK event listener.
4. Call `initSDK` to initialize the SDK.

The detailed steps are as follows.

[](id:SDKAppID)

### Preparing an SDKAppID

To perform the initialization, you must have a correct `SDKAppID`.
The `SDKAppID` uniquely identifies a Tencent Cloud IM account. We recommend you apply for a new `SDKAppID` for each application. Messages are naturally isolated and cannot communicate between different `SDKAppID` values.
In the [IM console](https://console.cloud.tencent.com/im), you can view all your `SDKAppID` values, and you can click **Create Application** to create an `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/3a2d8ad3204410bccc0ee5c3f1907bd6.png)

[](id:SDKConfig)

### Setting the LogLevelEnum

Before initializing the SDK, you need to initialize the [`LogLevelEnum`](https://comm.qq.com/im/doc/RN/en/Enum/LogLevelEnum.html) object, which is used to set the SDK log level.

#### Setting the log level

The IM SDK supports the following log levels:

| Log Level                    | Log Output                                                   |
| ---------------------------- | ------------------------------------------------------------ |
| LogLevelEnum.V2TIM_LOG_NONE  | No log is output.                                            |
| LogLevelEnum.V2TIM_LOG_DEBUG | Logs at the DEBUG, INFO, WARNING, and ERROR levels are output (default log levels). |
| LogLevelEnum.V2TIM_LOG_INFO  | Logs at the INFO, WARNING, and ERROR levels are output.      |
| LogLevelEnum.V2TIM_LOG_WARN  | Logs at the WARNING and ERROR levels are output.             |
| LogLevelEnum.V2TIM_LOG_ERROR | Logs at the ERROR level are output.                          |

SDK log storage rules are as follows:

- Local IM SDK logs are retained for seven days by default, after which the logs will be automatically cleared during the SDK initialization.
- By default, IM SDK logs on Android are stored in the `/sdcard/tencent/imsdklogs/application package name` directory for versions earlier than v4.8.50 and in the `/sdcard/Android/data/package name/files/log/tencent/imsdk` directory for v4.8.50 or later.

Starting from v4.7.1, the xlog module is used to output IM SDK logs, which are compressed by default and must be decompressed by using the Python script.

- To obtain the script for decompression, click [Decode Log 27](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python27.py) (for Python 2.7) or [Decode Log 30](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python30.py) (for Python 3.0).
- In the Windows or macOS console, you can decompress log files by running the following command. After decompression, the file names end with "xlog.log", and you can use the text editor to open these files.

```
python decode_mars_nocrypt_log_file.py imsdk_yyyyMMdd.xlog
```

### Setting the SDK event listener

After the initialization, the SDK will report such events as connection status and login ticket expiration through `V2TimSDKListener`.
We recommend you pass in `V2TimSDKListener` ([Details](https://comm.qq.com/im/doc/RN/en/Interface/Listener/V2TimSDKListener.html)) when calling `initSDK` to add the SDK event listener and perform logic processing in the callback.

`V2TimSDKListener` callbacks are as follows:

| Event Callback    | Event Description                                      | Recommended Operation                                        |
| ----------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| onConnecting      | The SDK is connecting to the CVM instance.             | Display the "connecting" status on the UI.                   |
| onConnectSuccess  | The SDK is successfully connected to the CVM instance. | -                                                            |
| onConnectFailed   | The SDK failed to connect to the CVM instance.         | Notify the user that the network connection is currently unavailable. |
| onKickedOffline   | The current user is kicked offline.                    | Display the "You have already logged in to the current account on another device. Are you sure you want to log in again?" message on the UI. |
| onUserSigExpired  | The login ticket expired.                              | Log in with a new `UserSig`.                                 |
| onSelfInfoUpdated | The current user's profile is updated.                 | Update the profile photo and nickname on the UI.             |

> ! If you receive the `onUserSigExpired` callback, the `UserSig` that you use for login has expired. In this case, you need to use a new `UserSig` to log in again. If you continue to use the expired `UserSig`, the IM SDK will be in an infinite login loop.

### Calling the initialization API

After performing the above steps, you can call `initSDK` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMManager/initSDK.html)) to initialize the SDK.

Below is the sample code:

```javascript
import { TencentImSDKPlugin, LogLevelEnum } from 'react-native-tim-js';


// 1. Get the `SDKAppID` from the IM console.
const sdkAppID = 0;
// 2. Add the `V2TimSDKListener` event listener.
const sdkListener = {
      onConnectFailed: (code, error) {},
      onConnectSuccess: () {},
      onConnecting: () {},
      onKickedOffline: () {},
      onSelfInfoUpdated: (V2TimUserFullInfo info) {},
      onUserSigExpired: () {},
};

// 3. Perform the initialization and register the event.
TencentImSDKPlugin.v2TIMManager.initSDK(
      sdkAppID: sdkAppID,
      loglevel: LogLevelEnum.V2TIM_LOG_ALL,
      listener: sdkListener,
);

```

### Uninitialization

Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, you don't need to uninitialize the IM SDK before exiting the application.
However, you can uninitialize the IM SDK in special cases, for example, only after you enter a specific UI and no longer use it after exiting the UI.

You can perform the uninitialization by calling the uninitialization API `unInitSDK` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMManager/unInitSDK.html)).

Below is the sample code:

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

// Uninitialize the SDK
TencentImSDKPlugin.v2TIMManager.unInitSDK();
```

[](id:qa)

## FAQs

[](id:qa1)

### 1. What should I do if error code 6013 is returned along with the description "not initialized" when I call the login or another API?

You must initialize the IM SDK before using the login, message, group, conversation, relationship chain and profile, and signaling features.
