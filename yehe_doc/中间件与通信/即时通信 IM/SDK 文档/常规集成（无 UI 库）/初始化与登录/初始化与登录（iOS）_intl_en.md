## Initialization
[V2TIMManager](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html) is a core class and also an entry class of the IM SDK. It implements features such as IM SDK initialization and login, message sending/receiving, group creation, and group leaving. To complete initialization, call the [initSDK](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6) API.

<pre><code class="language-Objective-C"><span class="hljs-comment">// 1. Obtain the SDKAppID of the application from the IM console. For more information, see <a href="#SDKAppID">SDKAppID</a>.</span>
<span class="hljs-comment">// 2. Initialize the `config` object.</span>
V2TIMSDKConfig *config = [[V2TIMSDKConfig alloc] init];
<span class="hljs-comment">// 3. Specify the log output level. For more information, see [SDKConfig](#SDKAppID).</span>
config.logLevel = V2TIM_LOG_INFO;
<span class="hljs-comment">// 4. Initialize the SDK and set the listening object of `V2TIMSDKListener`.</span>
<span class="hljs-comment">// After you call `initSDK`, the SDK automatically connects to the network. The network connection status can be listened to in the `V2TIMSDKListener` callback.</span>
[[V2TIMManager sharedInstance] initSDK:<span class="hljs-number">1400000123</span> config:config listener:<span class="hljs-keyword">self</span>];

<span class="hljs-comment">// 5. Listen to the `V2TIMSDKListener` callback.</span>
- (<span class="hljs-keyword">void</span>)onConnecting {
    <span class="hljs-comment">// The SDK is connecting to the Tencent CVM instance.</span>
}
- (<span class="hljs-keyword">void</span>)onConnectSuccess {
    <span class="hljs-comment">// The SDK is successfully connected to the Tencent CVM instance.</span>
}
- (<span class="hljs-keyword">void</span>)onConnectFailed:(<span class="hljs-keyword">int</span>)code err:(<span class="hljs-built_in">NSString</span>*)err {
    <span class="hljs-comment">// The SDK fails to connect to the Tencent CVM instance.</span>
}</code></pre>

The initialization API `initSDK` contains three required parameters, including `SDKAppID`, `Config`, and `listener`.

[](id:SDKAppID)
### SDKAppID
`SDKAppID` is a unique ID that the IM service uses to identify a customer account. We recommend that you apply for a new `SDKAppID` for every independent app to automatically isolate messages between `SDKAppIDs`.
You can view all `SDKAppIDs` in the [IM console](https://console.cloud.tencent.com/im) or click **Add Application** to create an `SDKAppID`.
![](https://main.qcloudimg.com/raw/06d521fdb60cd86e40a82080ff90be3f.png)

[](id:SDKAppID)
### SDKConfig
The `V2TIMSDKConfig` parameter is used for initialization configuration of the SDK. It is often used to set the log level, that is, the [logLevel](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMSDKConfig.html) parameter. The following table lists the log levels.

| Log Level | Log Output |
|---------|---------|
| V2TIM_LOG_NONE | No log is output. |
| V2TIM_LOG_DEBUG | Logs of the DEBUG, INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_INFO | Logs of the INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_WARN | Logs of the WARNING and ERROR levels are output. |
| V2TIM_LOG_ERROR | Logs of the ERROR level are output. |

- Logs of the IM SDK are stored in the `/Library/Caches/` directory by default.
- Starting from V4.7.1, the xlog module of the WeChat team is used to output IM SDK logs. The xlogs are decompressed by default and must be decompressed using the Python script.
 - To obtain the script for decompression, click [Decode Log 27](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python27.py) if you are using Python 2.7, or click [Decode Log 30](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python30.py) if you are using Python 3.0.
 - In the Windows or Mac console, you can run the following command to decompress the log files. After decompression, the file names end with "xlog.log", and you can use the text editor to open these files.
```
python decode_mars_nocrypt_log_file.py imsdk_yyyyMMdd.xlog
```

### Listener
[V2TIMSDKListener](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html) is used to listen to the network status and changes to the user information.

| Event Callback | Event Description | Recommended Operation |
|---------|---------|---------|
| onConnecting | The SDK is connecting to the CVM instance. | The "Connecting" status can be displayed on the UI. |
| onConnectSuccess | The SDK is successfully connected to the CVM instance. | - |
| onConnectFailed | The SDK fails to connect to the CVM instance. | The user can be notified that the network connection is currently unavailable. |
| onKickedOffline | The current user is kicked offline. | The "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. |
| onUserSigExpired | The UserSig expires. | Use the new UserSig for login. |
| onSelfInfoUpdated | The information of the current user is updated. | Update your own profile photo and nickname on the UI. |

>!If you receive the `onUserSigExpired` callback, the UserSig that you use for login has expired. In this case, you need to update the UserSig and then log in again. If you continue to use the expired UserSig, the SDK falls into an endless login loop.

## Login
You can call the [login(userID, userSig)](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c) function of `V2TIMManager` to log in to the SDK. Features of the IM SDK are available to you only after you successfully log in to the SDK.

- UserID: we recommend that UserID contain only uppercase or lowercase letters, digits, underscores, and hyphens. Its length cannot exceed 32 bytes.
- UserSig: login ticket of the IM SDK. It is calculated by your business server to ensure security. For more information on the calculation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
>!After you log in successfully by calling `IM SDK Login`, DAU will be calculated. Please use `IM SDK Login` appropriately according to the business scenario to avoid an excessively high DAU.
### Login scenarios
You need to call the `login` function in the following scenarios:
- When you need to use features of the IM SDK for the first time after the app is started.
- When the IM SDK triggers an `onUserSigExpired` callback. That is, when the UserSig expires, you need to use the new UserSig for login.
- When the IM SDK triggers an `onKickOffline` callback. That is, when the current user is kicked offline, the "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. In this case, you can select "Yes" to log in again.

You do not need to call the `login` function in the following scenarios:
- When your network is disconnected and then reconnected, you do not need to call the `login` function as the SDK automatically goes online.
- When a login process is running, you do not need to log in to the SDK again.

### Multi-device login
You cannot use the same account to log in on two mobile phones of the same model. For example, you cannot use the same account for login on two Apple mobile phones. However, one Android mobile phone and one Apple mobile phone will be considered as two different devices, and you can use the same account to log in on these two devices. For more information on configurations related to multi-device login, see the **Login settings** section in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

## Logout
To log out of the SDK, call the [logout()](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f) function.




