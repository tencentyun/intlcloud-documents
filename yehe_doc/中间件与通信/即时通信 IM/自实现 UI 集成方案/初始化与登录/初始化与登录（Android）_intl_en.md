
## Initialization
[V2TIMManager](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html) is a core class and also an entry class of the IM SDK. It implements features such as IM SDK initialization and login, message sending and receiving, and group creation and leaving. To initialize IM SDK, call the [initSDK](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ac905c315726b517ba62421471bbecf56) API.

<pre><code><span class="hljs-comment">// 1. Obtain the SDKAppID of the app from the IM console. For more information, see <a href="#SDKAppID">SDKAppID</a>.</span>
<span class="hljs-comment">// 2. Initialize the `config` object.</span>
V2TIMSDKConfig config = <span class="hljs-keyword">new</span> V2TIMSDKConfig();
<span class="hljs-comment">// 3. Specify the log output level. For more information, see <a href="#SDKConfig">SDKConfig</a>.</span>
config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_INFO);
<span class="hljs-comment">// 4. Initialize the SDK and set the listening object of `V2TIMSDKListener`.</span>
<span class="hljs-comment">// After you call `initSDK`, the SDK automatically connects to the network. The network connection status can be listened for in the `V2TIMSDKListener` callback.</span>
V2TIMManager.getInstance().initSDK(context, sdkAppID, config, <span class="hljs-keyword">new</span> V2TIMSDKListener() {
    <span class="hljs-comment">// 5. Listen for the `V2TIMSDKListener` callback.</span>
    <span class="hljs-meta">@Override</span>
    <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">onConnecting</span><span class="hljs-params">()</span> </span>{
        <span class="hljs-comment">// The SDK is connecting to the Tencent CVM instance.</span>
    }
    <span class="hljs-meta">@Override</span>
    <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">onConnectSuccess</span><span class="hljs-params">()</span> </span>{
        <span class="hljs-comment">// The SDK is successfully connected to the Tencent CVM instance.</span>
    }
    <span class="hljs-meta">@Override</span>
    <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">onConnectFailed</span><span class="hljs-params">(<span class="hljs-keyword">int</span> code, String error)</span> </span>{
        <span class="hljs-comment">// The SDK fails to connect to the Tencent CVM instance.</span>
    }
});</code></pre>

The initialization API `initSDK(SDKAppID, SDKConfig, listener)` has three required parameters, `SDKAppID`, `SDKConfig`, and `listener`.

[](id:SDKAppID)
### SDKAppID
`SDKAppID` is the unique ID that the IM service uses to identify a customer account. We recommend you apply for a new `SDKAppID` for every independent app to automatically isolate messages between `SDKAppIDs`.
You can view all `SDKAppIDs` in the [IM console](https://console.cloud.tencent.com/im) or click **Create Application** to create an `SDKAppID`.
![](https://main.qcloudimg.com/raw/06d521fdb60cd86e40a82080ff90be3f.png)

[](id:SDKConfig)
### SDKConfig
The `V2TIMSDKConfig` parameter is used for SDK initialization configuration. It is often used to set the log level, that is, the [setLogLevel](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKConfig.html#a033c4e90397236427f3dd65038df8033) API. The following table lists the log levels:

| Log Level | Log Output |
|---------|---------|
| V2TIM_LOG_NONE | No log is output. |
| V2TIM_LOG_DEBUG | Logs of the DEBUG, INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_INFO | Logs of the INFO, WARNING, and ERROR levels are output. |
| V2TIM_LOG_WARN | Logs of the WARNING and ERROR levels are output. |
| V2TIM_LOG_ERROR | Logs of the ERROR level are output. |

- By default, IM SDK logs are stored in the `/sdcard/tencenet/imsdklogs/<App package name>` directory for versions earlier than 4.8.50 and in the `/sdcard/Android/data/<Package name>/files/log/tencent/imsdk` directory for version 4.8.50 or later.
- Local IM logs are stored for seven days by default, and logs generated earlier than seven days ago will be automatically cleared during SDK initialization.
- Starting from v4.7.1, the IM SDK uses the xlog module to output logs. Logs in the xlog module are compressed by default and must be decompressed using a Python script.
 - To obtain the script for decompression, click [Decode Log 27](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python27.py) if you are using Python 2.7, or click [Decode Log 30](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/tools/xlog_decoder_python30.py) if you are using Python 3.0.
 - In the Windows or Mac console, you can decompress log files by running the following command. After decompression, the file names end with "xlog.log", and you can use the text editor to open these files.
```
python decode_mars_nocrypt_log_file.py imsdk_yyyyMMdd.xlog
```

### Listener
[V2TIMSDKListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html) is used to listen for network status and user information changes.

| Event Callback | Event Description | Recommended Operation |
|---------|---------|---------|
| onConnecting | The SDK is connecting to the CVM instance. | The "Connecting" status can be displayed on the UI. |
| onConnectSuccess | The SDK is successfully connected to the CVM instance. | - |
| onConnectFailed | The SDK fails to connect to the CVM instance. | The user can be notified that the network connection is currently unavailable. |
| onKickedOffline | The current user is kicked offline. | The "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. |
| onUserSigExpired | The UserSig expired. | Use a new UserSig for login. |
| onSelfInfoUpdated | The information of the current user is updated. | Update your profile photo and nickname on the UI. |

>! If you receive the `onUserSigExpired` callback, the UserSig that you use for login has expired. In this case, you need to update the `UserSig` and then log in again. If you continue to use the expired `UserSig`, the SDK will be in an infinite login loop.

## Login

You can call the [login(userID, userSig)](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/v2tmp/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a73fc0e14c5f2f5fc06a80081479fb416) function of `V2TIMManager` to log in to the IM SDK. Only after the login is successful, you can use the features of the IM SDK.

- `userID`: You are advised to enter only letters (a-z and A-Z), digits (0-9), underscores (_), and hyphens (-). The value cannot exceed 32 bytes.
- `userSig`: Login ticket of the IM SDK. It is calculated by your business server to ensure security. For more information on the calculation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
>! After you log in successfully by calling the `login` function of the IM SDK, DAU will be calculated. Use the `login` function appropriately according to business scenarios to avoid an excessively high DAU.
### Login scenarios
You need to call the `login` function in the following scenarios:
- When you use features of the IM SDK for the first time after the app is started.
- When the IM SDK triggers an `onUserSigExpired` callback. That is, when the `UserSig` expires, you need to use a new `UserSig` for login.
- When the IM SDK triggers an `onKickedOffline` callback. That is, when the current user is kicked offline, the "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. In this case, you can select **Yes** to log in again.

You do not need to call the `login` function in the following scenarios:
- When your network is disconnected and then reconnected. In this case, the SDK automatically goes online.
- When a login process is already running. In this case, repeated login is unnecessary.

### Multi-device login
You cannot use the same account to log in on two mobile phones of the same model. For example, you cannot use the same account to log in on two Apple mobile phones. However, one Android mobile phone and one Apple mobile phone will be considered as two different devices, and you can use the same account to log in on these two devices. For more information on configurations related to multi-device login, see the **Login Settings** section in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

### Logout
To log out of the SDK, call the [logout](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48) function.
