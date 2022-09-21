## Initialization and Login
[V2TIMManager](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_manager/V2TIMManager-class.html) is a core class and also an entry class of the IM SDK. It implements features such as IM SDK initialization and login, message sending and receiving, group creation, and group leaving. You can call [initSDK](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/initSDK.html) to complete initialization:

```
import 'package:tencent_im_sdk_plugin/enum/V2TimSDKListener.dart';
import 'package:tencent_im_sdk_plugin/enum/log_level_enum.dart';
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';


    TencentImSDKPlugin.v2TIMManager.initSDK(
      sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
      loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
      listener: V2TimSDKListener(),
    );
```


The initialization API `initSDK` has three required parameters: `SDKAppID`, `LogLevelEnum`, and `listener`.

### SDKAppID
`SDKAppID` is the unique ID that the IM service uses to identify a customer account. We recommend you apply for a new `SDKAppID` for every independent app to automatically isolate messages between `SDKAppIDs`.
You can view all `SDKAppIDs` in the [IM console](https://console.cloud.tencent.com/im) or click **Create Application** to create an `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/7e268b79ee43c10816bf3de0b5853542.png)

### LogLevelEnum
[LogLevelEnum](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/enum_log_level_enum/LogLevelEnum.html) is used to set the log output level, which is described as below:

| Log Level       | Log Output                                                     |
| --------------- | -------------------------------------------------------------- |
| V2TIM_LOG_NONE  | No log is output.                                              |
| V2TIM_LOG_DEBUG | Logs of the DEBUG, INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_INFO  | Logs of the INFO, WARNING, and ERROR levels are output.        |
| V2TIM_LOG_WARN  | Logs of the WARNING and ERROR levels are output.               |
| V2TIM_LOG_ERROR | Logs of the ERROR level are output.                            |


### Listener
[V2TimSDKListener](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimSDKListener/V2TimSDKListener-class.html) is used to listen for network status and user information changes.

| Event Callback    | Event Description                                      | Recommended Operation                                                                                                                                               |
| ----------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| onConnecting      | The SDK is connecting to the CVM instance.             | The "Connecting" status can be displayed on the UI.                                                                                                                 |
| onConnectSuccess  | The SDK is successfully connected to the CVM instance. | -                                                                                                                                                                   |
| onConnectFailed   | The SDK fails to connect to the CVM instance.          | The user can be notified that the network connection is currently unavailable.                                                                                      |
| onKickedOffline   | The current user is kicked offline.                    | The "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. |
| onUserSigExpired  | The `UserSig` expired.                                 | Use a new `UserSig` for login.                                                                                                                                      |
| onSelfInfoUpdated | The information of the current user is updated.        | Update your profile photo and nickname on the UI.                                                                                                                   |

>! If you receive the `onUserSigExpired` callback, the `UserSig` that you use for login has expired. In this case, you need to update the `UserSig` and then log in again. If you continue to use the expired `UserSig`, the SDK will be in an infinite login loop.

## Login
You can call the [login (userID, userSig)](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/login.html) function of `v2TIMManager` to log in to the SDK. The features of the IM SDK are available to you only after you successfully log in to it.

```
    V2TimCallback res = await TencentImSDKPlugin.v2TIMManager.login (
      userID: userID,
      userSig: userSig, 
    );
```

- UserID: We recommend that `UserID` contain only letters, digits, underscores, and hyphens. Its length cannot exceed 32 bytes.
- UserSig: login ticket of the IM SDK. It is calculated by your business server to ensure security. For more information on the calculation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
>! After you log in successfully by calling `IM SDK Login`, DAU will be calculated. Use `IM SDK Login` appropriately according to the business scenarios to avoid an excessively high DAU.

### Login scenarios
You need to call the `login` function in the following scenarios:
- When you use features of the IM SDK for the first time after the app is started.
- When the IM SDK triggers an `onUserSigExpired` callback. That is, when the `UserSig` expires, you need to use a new `UserSig` for login.
- When the IM SDK triggers an `onKickedOffline` callback. That is, when the current user is kicked offline, the "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. In this case, you can select "Yes" to log in again.

You do not need to call the `login` function in the following scenarios:
- When your network is disconnected and then reconnected, you do not need to call the `login` function as the SDK automatically goes online.
- When a login process is running, you do not need to log in to the SDK again.

### Multi-client login
You cannot use the same account to log in on two mobile phones of the same model. For example, you cannot use the same account for login on two iPhones. However, one Android phone and one iPhone are considered as two different devices, and you can use the same account to log in on these two devices. For more information on configurations related to multi-client login, see the **Login settings** section in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

## Logout
| To log out, call the [logout()](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/logout.html) function. |




