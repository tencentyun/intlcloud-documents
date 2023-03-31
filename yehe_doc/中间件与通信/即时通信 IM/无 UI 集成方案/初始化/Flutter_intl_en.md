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
`SDKAppID` is the unique ID that the IM service uses to identify a customer account. We recommend you apply for a new `SDKAppID` for every independent app to automatically isolate messages between `SDKAppIDs`.
You can view all `SDKAppIDs` in the [IM console](https://console.cloud.tencent.com/im) or click **Create Application** to create an `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/0f985a6fa6ac7f6a8c278ae021da7b12.png)


[](id:SDKConfig)
### Setting the LogLevelEnum

Before initializing the SDK, you need to initialize the `LogLevelEnum` ([Dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Enum/LogLevelEnum.html)) object, which is used to set the SDK log level.

#### Setting the log level
The IM SDK supports the following log levels:

| Log Level                    | Log Output                                                   |
| ---------------------------- | ------------------------------------------------------------ |
| LogLevelEnum.V2TIM_LOG_NONE  | No log is output.                                            |
| LogLevelEnum.V2TIM_LOG_DEBUG | Logs of the DEBUG, INFO, WARNING, and ERROR levels (default log levels) are output. |
| LogLevelEnum.V2TIM_LOG_INFO  | Logs at the INFO, WARNING, and ERROR levels are output.      |
| LogLevelEnum.V2TIM_LOG_WARN  | Logs at the WARNING and ERROR levels are output.             |
| LogLevelEnum.V2TIM_LOG_ERROR | Logs at the ERROR level are output.                          |

SDK log storage rules are as follows:
- Local IM SDK logs are stored for seven days by default, and logs generated earlier than seven days ago will be automatically cleared during SDK initialization.
- For Android, IM SDK logs are stored in the `/sdcard/tencenet/imsdklogs/<App package name>` directory by default for versions earlier than 4.8.50 and in the `/sdcard/Android/data/<Package name>/files/log/tencent/imsdk` directory for version 4.8.50 or later.
  

Starting from v4.7.1, the xlog module from WeChat is used to output IM SDK logs, which are compressed by default and must be decompressed by using the Python script.
 - To obtain the script for decompression, click [Decode Log 27](https://imsdk-1252463788.cos.ap-guangenou.myqcloud.com/tools/xlog_decoder_python27.py) if you are using Python 2.7, or click [Decode Log 30](https://imsdk-1252463788.cos.ap-guangenou.myqcloud.com/tools/xlog_decoder_python30.py) if you are using Python 3.0.
 - In the Windows or Mac console, you can decompress log files by running the following command. After decompression, the file names end with "xlog.log", and you can use the text editor to open these files.
```
python decode_mars_nocrypt_log_file.py imsdk_yyyyMMdd.xlog
```


### Setting the SDK event listener
After the initialization, the SDK will report such events as connection status and login ticket expiration through `V2TimSDKListener`.
We recommend you pass in `V2TimSDKListener` ([Dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimSDKListener.html)) when calling `initSDK` to add the SDK event listener and perform logic processing in the callback.

`V2TimSDKListener` callbacks are as follows:

| Event Callback    | Event Description                                      | Recommended Operation                                        |
| ----------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| onConnecting      | The SDK is connecting to the CVM instance.             | Display the "connecting" status on the UI.                   |
| onConnectSuccess  | The SDK is successfully connected to the CVM instance. | -                                                            |
| onConnectFailed   | The SDK failed to connect to the CVM instance.         | Notify the user that the network connection is currently unavailable. |
| onKickedOffline   | The current user is kicked offline.                    | Display the "You are already logged in on another device. Are you sure you want to log in again?" message on the UI. |
| onUserSigExpired  | The login ticket expired.                              | Log in with a new `UserSig`.                                 |
| onSelfInfoUpdated | The current user's profile is updated.                 | Update the profile photo and nickname on the UI.             |

>! If you receive the `onUserSigExpired` callback, the UserSig that you use for login has expired. In this case, you need to use the newly issued `UserSig` to log in again. If you continue to use the expired `UserSig`, the IM SDK will enter an infinite login loop.




### Calling the initialization API
After performing the above steps, you can call `initSDK` ([Dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/initSDK.html)) to initialize the SDK.

Sample code:

```dart
    // 1. Get the `SDKAppID` from the IM console.
    int sdkAppID = 0;
    // 2. Add the `V2TimSDKListener` event listener. `sdkListener` is the implementation class of `V2TimSDKListener`.
    V2TimSDKListener sdkListener = V2TimSDKListener(
      onConnectFailed: (int code, String error) {
        // Connection failure callback function
        // `code`: Error code
        // `error`: Error message
      },
      onConnectSuccess: () {
        // The SDK is successfully connected to the CVM instance
      },
      onConnecting: () {
        // The SDK is connecting to the CVM instance
      },
      onKickedOffline: () {
        // The current user is kicked offline: the SDK notifies the user on the UI, and the user can choose to call the login() function of V2TIMManager to log in again.
      },
      onSelfInfoUpdated: (V2TimUserFullInfo info) {
        // The profile of the current user was updated
        // `info`: information of the login user
      },
      onUserSigExpired: () {
        // The ticket expires when the user is online: the user needs to generate a new userSig and call the login() function of V2TIMManager to log in again.
      },
      onUserStatusChanged: (List<V2TimUserStatus> userStatusList) {
        // User status change notification
        // `userStatusList`: list of users whose status changes
        // Notification receiving: This callback will be triggered if a subscribed user status (including online status and custom status) changes.
        // This callback will be triggered when a friend's status changes after notifications of friends' statuses are enabled in the IM console, even if the status has not been subscribed to.
        // This callback will be sent to all the devices when an account is logged in on them and the custom status is changed on one of them.
      },
    );
    // 3. Initialize the SDK
    V2TimValueCallback<bool> initSDKRes =
        await TencentImSDKPlugin.v2TIMManager.initSDK(
      sdkAppID: sdkAppID, // SDKAppID
      loglevel: LogLevelEnum.V2TIM_LOG_ALL, // Log registration level
      listener: sdkListener, // Event listener
    );
    if (initSDKRes.code == 0) {
      // Initialized successfully
    }

```
// Uninitialization
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, you don't need to uninitialize the IM SDK before exiting the application.
However, you can uninitialize the IM SDK in special cases, for example, only after you enter a specific UI and no longer use it after exiting the UI.

You can perform the uninitialization by calling the uninitialization API `unInitSDK` ([Dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/unInitSDK.html)).

Sample code:

```dart
// Uninitialize the SDK
TencentImSDKPlugin.v2TIMManager.unInitSDK();
```
[](id:qa)

## FAQs

[](id:qa1)

### 1. What should I do if error code 6013 is returned along with the description "not initialized" when I call the login or another API?
You must initialize the IM SDK before using the login, message, group, conversation, relationship chain and profile, and signaling features.
