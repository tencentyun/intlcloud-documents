## Initialization
[V2TIMManager](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html) is a core class and also an entry class of the IM SDK. It implements features including IM SDK initialization and login, message sending and receiving, group creation, and group quitting. To complete initialization, call the [initSDK](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6) API.

<pre><code class="language-Objective-C"><span class="hljs-comment">// 1. Obtain the SDKAppID of the app from the IM console. For more information, see <a href="#SDKAppID">SDKAppID</a>.</span>
<span class="hljs-comment">// 2. Initialize the config object.</span>
V2TIMSDKConfig *config = [[V2TIMSDKConfig alloc] init];
<span class="hljs-comment">// 3. Specify the log output level. For more information, see [SDKConfig](#SDKAppID)。</span>
config.logLevel = V2TIM_LOG_INFO;
<span class="hljs-comment">// 4. Initialize the SDK and set the listening object of V2TIMSDKListener.</span>
<span class="hljs-comment">// After you call initSDK, the SDK automatically connects to the network. The network connection status can be monitored in the V2TIMSDKListener callback.</span>
[[V2TIMManager sharedInstance] initSDK:<span class="hljs-number">1400000123</span> config:config listener:<span class="hljs-keyword">self</span>];

<span class="hljs-comment">// 5. Monitor the V2TIMSDKListener callback.</span>
- (<span class="hljs-keyword">void</span>)onConnecting {
    <span class="hljs-comment">// The SDK is connecting to the Tencent CVM instance.</span>
}
- (<span class="hljs-keyword">void</span>)onConnectSuccess {
    <span class="hljs-comment">// The SDK has successfully connected to the Tencent CVM instance.</span>
}
- (<span class="hljs-keyword">void</span>)onConnectFailed:(<span class="hljs-keyword">int</span>)code err:(<span class="hljs-built_in">NSString</span>*)err {
    <span class="hljs-comment">// The SDK failed to connect to the Tencent CVM instance.</span>
}</code></pre>

The initialization API, initSDK (SDKAppID, SDKConfig, listener), contains three required parameters: `SDKAppID`, `Config`, and `listener`.

[](id:SDKAppID)
### SDKAppID
SDKAppID indicates the app ID. It is a unique ID that the IM service uses to identify a customer account. We recommend that you apply for a new SDKAppID for every independent app to automatically isolate messages between SDKAppIDs.
You can view all SDKAppIDs in the [IM console](https://console.cloud.tencent.com/im). Alternatively, you can create an SDKAppID by clicking **Add Application**.

[](id:SDKAppID)
### SDKConfig
The `V2TIMSDKConfig` parameter is used for initialization configuration of the SDK. It is often used to set the log level, that is, [logLevel](http://doc.qcloudtrtc.com/im/interfaceV2TIMSDKConfig.html). The following table describes possible log levels.

| Log Level | Log Output |
|---------|---------|
| V2TIM_LOG_NONE | No log is output. |
| V2TIM_LOG_DEBUG | Logs of the DEBUG, INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_INFO | Logs of the INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_WARN | Logs of the WARNING and ERROR levels are output. |
| V2TIM_LOG_ERROR | Logs of the ERROR level are output. |

- IM SDK logs are stored in the `/Library/Caches/` directory by default.
- Starting from V4.7.1, the xlog module of the WeChat team is used to output IM SDK logs. The xlogs are compressed by default and must be decompressed by using a Python script.
 - To obtain the decompression script, click [Decode Log 27](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python27.py) if you are using Python 2.7, or click [Decode Log 30](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python30.py) if you are using Python 3.0.
 - In the Windows or Mac console, you can run the following command to decompress the log files. The decompressed files are suffixed with "xlog.log" and can be directly opened in a text editor.
```
python decode_mars_nocrypt_log_file.py imsdk_yyyyMMdd.xlog
```

### Listener
[V2TIMSDKListener](http://doc.qcloudtrtc.com/im/protocolV2TIMSDKListener-p.html) is used to monitor the network status and user information changes.

| Event Callback | Event Description | Recommended Operation |
|---------|---------|---------|
| onConnecting | The SDK is connecting to the CVM instance. | Display the "Connecting" state on the UI. |
| onConnectSuccess | The SDK has successfully connected to the CVM instance. | - |
| onConnectFailed | The SDK failed to connect to the CVM instance. | Notify the user that the network connection is currently unavailable. |
| onKickedOffline | The current user was forced offline. | Display the message stating "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" on the UI. |
| onUserSigExpired | The UserSig has expired. | Use the new UserSig for login. |
| onSelfInfoUpdated | The information of the current user was updated. | Update your own profile photo and nickname on the UI. |

>! If the `onUserSigExpired` callback is received, in indicates that the UserSig used for login has expired. In this case, you need to update the UserSig and then log in again. If you continue to use the expired UserSig, the SDK falls into an endless login loop.

## Login
You can call the [login(userID, userSig)](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c) function of `V2TIMManager` to log in to the SDK. Features of the IM SDK are available to you only after you successfully log in to the SDK.

- UserID: we recommend that the UserID contains only uppercase or lowercase letters, digits, underscores, and hyphens with a length less than 32 bytes.
- UserSig: indicates the login ticket of the IM SDK. It is calculated by your business server to ensure security. For more information on the calculation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Login scenarios
You need to call the `login` function in the following scenarios:
- When you need to use features of the IM SDK for the first time after the app is started.
- When the IM SDK throws an `onUserSigExpired` callback. That is, when the UserSig expires, you need to use the new UserSig for login.
- When the IM SDK throws an `onKickOffline` callback. That is, when the current user is forced offline, the message stating "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" can be displayed on the UI. In this case, you can select "Yes" to log in again.

You do not need to call the `login` function in the following scenarios:
- When your network is disconnected and then reconnected, you do not need to call the `login` function as the SDK automatically goes online.
- When a login process is running, you do not need to log in to the SDK again.

### Multi-device login
You cannot use the same account to log in on two mobile phones of the same model. For example, you cannot use the same account for login on two Apple mobile phones. However, one Android mobile phone and one Apple mobile phone will be considered as two different devices, and you can use the same account to log in on these two devices. For more information on configurations related to multi-device login, see [Login Settings](https://intl.cloud.tencent.com/document/product/1047/34419).

## Logout
To log out of the SDK, call the [logout()](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f) function.




