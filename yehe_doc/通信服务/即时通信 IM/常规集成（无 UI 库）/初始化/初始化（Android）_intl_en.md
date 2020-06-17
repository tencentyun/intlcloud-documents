## Getting Communication Manager
Every operation in the IM SDK starts with `TIMManager`. Therefore the first step is to get a `TIMManager` singleton. The prototype of `getInstance` retrieval of a communication manager instance is as follows.

**Prototype:**

```
public static TIMManager getInstance()
```

**Example:**

```
TIMManager.getInstance();
```
## Configuring IM SDK for Initialization
Before initializing the IM SDK, you need to make some IM SDK configurations, including SDKAppID and log control. The corresponding configuration class is `TIMSdkConfig`.

### Log event

The IM SDK prints logs internally. If callers have their own unified log collection methods, they can utilize the `setLogListener` API in` TIMSdkConfig` to set a log event callback which returns logs to the callers. However, the IM SDK will still print logs internally in this case. You can disable printing by setting the console not to print logs, or setting the log level.

**Prototype:**

```
/**
 * Setting current log callback listener, which must be performed before IM SDK initialization.
 * @param logListener Log callback listener
 */
public TIMSdkConfig setLogListener(TIMLogListener logListener) 
```

**Example:**

```
//Set log callback. This API returns a copy of logs output by the IM SDK.
//[NOTE]: level is defined in TIMManager, for example, TIMManager.ERROR. It is not equivalent to the definition in Android systems.
mTIMSdkConfig.setLogListener(new TIMLogListener() {
    @Override
    public void log(int level, String tag, String msg) {
        //You can output the SDK logs to your own logging system through this callback.
    }
});
```

### Setting log level

When permissions allow, the IM SDK writes logs to log files by default. You can control the file log output of the IM SDK by modifying the internal write log level of the IM SDK through `setLogLevel` in `TIMSdkConfig`.

>
>- The API for setting write log level **must be called before IM SDK initialization** for the setting to take effect.
>- You can disable the file log output of IM SDK by setting the log level to TIMLogLevel.OFF. We recommend that you leave it enabled to facilitate troubleshooting.

**Prototype:**

```
/**
 * Setting write log level. Must be called before IM SDK initialization for the setting to take effect.
 * @param logLevel Log level
 */
public TIMSdkConfig setLogLevel(@NonNull TIMLogLevel logLevel) 
```


### Disabling console log printing

By default, the IM SDK prints logs to the console. If this produces too much disruption, you can disable console logs through `enableLogPrint` in `TIMSdkConfig` (file logs will still be printed, but you can disable this by setting the log level).

> The API for log settings **must be called before IM SDK initialization** for the settings to take effect.


**Prototype:**

```
/**
 * Enabling or disabling printing logs to the console. This must be set before IM SDK initialization.
 * @param logPrintEnabled true - Logs will be output to the console
 */
public TIMSdkConfig enableLogPrint(boolean logPrintEnabled) 
```

### Modifying the log path

For the unified management of logs, you can modify the default log storage path. Use `setLogPath` in `TIMSdkConfig` to set the storage path for logs.

>
> * The API for setting the log path **must be called before IM SDK initialization** for the settings to take effect.
> * The default IM SDK log storage path is: `/tencent/imsdklogs/(your app package name)/` on the SD card.

**Prototype:**

```
/**
 * Setting the log path. Must be called before IM SDK initialization for the settings to take effect.
 * @param logPath Log path
 */
public TIMSdkConfig setLogPath(@NonNull String logPath)
```

## Initializing the IM SDK

Before using the IM SDK for further operations, you need to initialize the IM SDK.

> When there are **multiple processes**, initialize the IM SDK in only one process. Call `SessionWrapper.isMainProcess(Context context)` to determine the correct process.

**Prototype:**

```
/**
 * Initializing the IM SDK
 * @param context application context
 * @param config IM SDK global configuration
 * @return true - initialization successful, false - initialization failed
 */
public boolean init(@NonNull Context context, @NonNull TIMSdkConfig config)
```

**Example:**

```
//Initialize the IM SDK basic configuration
//Determine whether this is the main thread
if (SessionWrapper.isMainProcess(getApplicationContext())) {
	TIMSdkConfig config = new TIMSdkConfig(sdkAppId)
			.enableCrashReport(false)  //API has been deprecated
			.enableLogPrint(true)
			.setLogLevel(TIMLogLevel.DEBUG)
			.setLogPath(Environment.getExternalStorageDirectory().getPath() + "/justfortest/");

	//Initialize the SDK
	TIMManager.getInstance().init(getApplicationContext(), config);
}
```
## User Configuration

After the IM SDK has been initialized and before logging in to the IM SDK, configure a user through TIMUserConfig. After configuration and **before login**, bind the user configuration to the current communication manager through `setUserConfig` of `TIMManager`.

**Prototype:**
```
/**
 * Setting the user configuration for the current user before login
 * @param userConfig User configuration
 */
public void setUserConfig(TIMUserConfig userConfig) 
```

**Example:**
```
//Basic user configuration
TIMUserConfig userConfig = new TIMUserConfig()
		//Set listener for user status change events
		.setUserStatusListener(new TIMUserStatusListener() {
			@Override
			public void onForceOffline() {
				//Kicked offline by another client
				Log.i(tag, "onForceOffline");
			}

			@Override
			public void onUserSigExpired() {
				//User signature expired, you must refresh userSig and log in to the IM SDK again
				Log.i(tag, "onUserSigExpired");
			}
		})
		//Set listener for connection status events
		.setConnectionListener(new TIMConnListener() {
			@Override
			public void onConnected() {
				Log.i(tag, "onConnected");
			}

			@Override
			public void onDisconnected(int code, String desc) {
				Log.i(tag, "onDisconnected");
			}

			@Override
			public void onWifiNeedAuth(String name) {
				Log.i(tag, "onWifiNeedAuth");
			}
		})
		//Set listener for group events
		.setGroupEventListener(new TIMGroupEventListener() {
			@Override
			public void onGroupTipsEvent(TIMGroupTipsElem elem) {
				Log.i(tag, "onGroupTipsEvent, type: " + elem.getTipsType());
			}
		})
		//Set listener for conversation refresh
		.setRefreshListener(new TIMRefreshListener() {
			@Override
			public void onRefresh() {
				Log.i(tag, "onRefresh");
			}

			@Override
			public void onRefreshConversation(List<TIMConversation> conversations) {
				Log.i(tag, "onRefreshConversation, conversation size: " + conversations.size());
			}
		});

//Disable all local storage
userConfig.disableStorage();
//Enable read receipt
userConfig.enableReadReceipt(true);
		
//Bind user configuration to communication manager
TIMManager.getInstance().setUserConfig(userConfig);
```

### Network event notifications

This is an optional setting. To allow users to detect whether the IM SDK is connected to the server, set this callback through `TIMUserConfig`. It notifies the user whether the link between the invoker and communication backend is connected or disconnected. Additionally, if the network disconnected, the IM SDK will reconnect to the network after the network recovers and automatically pull messages to notify the user. The user does not need to worry about the network status. This is for notification purposes only.

>Here, network events do not indicate the user’s local network status, but the connection status between the IM SDK and IM Cloud Server. As long as the user is logged in, the **IM SDK will reconnect internally, and no intervention by the user is required**.

**Prototype:**

```
/**
 * Setting connection listener
 * @param listener Connection listener
 */
public TIMUserConfig setConnectionListener(TIMConnListener listener) 
```

**Example:**

See the example in [User Configuration](#.E7.94.A8.E6.88.B7.E9.85.8D.E7.BD.AE).

### User status changes

The IM SDK sends notifications for user status changes. You can listen to notifications for various changes by setting a listener for user status change notifications through `TIMUserConfig`. Currently, there are two kinds of notifications. For more information, please see [User force offline notifications](#.E7.94.A8.E6.88.B7.E8.A2.AB.E8.B8.A2.E4.B8.8B.E7.BA.BF.E9.80.9A.E7.9F.A5) and [User ticket expiration notifications](#.E7.94.A8.E6.88.B7.E7.A5.A8.E6.8D.AE.E8.BF.87.E6.9C.9F.E9.80.9A.E7.9F.A5).

**Prototype:**

```
/**
 * Set the user status notification callback
 * @param userStatusListener User status notification callback
 */
public TIMUserConfig setUserStatusListener(TIMUserStatusListener userStatusListener)
```

**The listener for user status change notifications, `TIMUserStatusListener`, is defined as follows:**

```
/**
 * User status change notification listener
 */
public interface TIMUserStatusListener {

    /**
     * Force offline callback
     */
    public void onForceOffline();

    /**
     * Expired ticket callback
     */
    public void onUserSigExpired();
}
```


**Example:**

See the example in [User Configuration](#.E7.94.A8.E6.88.B7.E9.85.8D.E7.BD.AE).


### Force offline notifications

The user will be forced to log out when logging in on another device. When this happens, the IM SDK sends a force offline notification. If a user status change notification listener has been set (see [User status changes](#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B.B4)), the situation will be handled in the listener’s callback method `onForceOffline`. Common practice is to prompt the user to log out or force the other party to log out.


>If the user is logged out when offline, the subsequent login will fail and a strong alert (login error code ERR_IMSDK_KICKED_BY_OTHERS: 6208) is displayed to the user. Developers can also choose to ignore this error and let the user log in again.

The following diagram illustrates the force offline process in online scenarios. The user logs in on device 1, stays online, and then logs in on device 2. At this point, the user is logged out on device 1 and the `onForceOffline` callback is triggered. After receiving the callback on device 1, the user is prompted to call `login` to go back online and force device 2 to log out.

![](https://main.qcloudimg.com/raw/40551f5696d97d39d7a905d5c88f6261.png)

The following diagram illustrates the force offline process in offline scenarios. The user logs in on device 1 and kills the app process without calling `logout`. The user then logs in on device 2, but device 1 is unaware of this event because the app process has been killed. To explicitly alert the user and avoid imperceptible force offline, `ERR_IMSDK_KICKED_BY_OTHERS: 6208` is returned when the user tries to log in on device 1 again. This notifies the user of the force offline event and asks whether to kick the other party offline. To kick the other party offline, the user calls `login` again to force a login and the logged-in instance on device 2 receives the `onForceOffline` callback.
![](https://main.qcloudimg.com/raw/44ffa44fad6cc2c2de8a791e610da480.png)

### User ticket expiration notifications

When the user logs in (see [Login](https://intl.cloud.tencent.com/document/product/1047/34316)), a user ticket needs to be provided, which will expire after a certain period of time. If the user ticket has expired, the interaction between the SDK and the server fails and the SDK gives the user ticket expiration notification. If a user status change notification listener is set (see [User status changes](#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B .B4)), corresponding processing can be carried out in the listener's callback method `onUserSigExpired`. To continue interacting with the server, the user must change the ticket and log in again.


### Disabling storage
By default, the IM SDK stores messages, profiles, conversations, and other information. If you do not need to store this information, disable storage through `TIMUserConfig` to improve processing performance.

> The API for disabling local storage **must be called before login**.

**Prototype:**
```
/**
 * Disabling local storage
 */
public TIMUserConfig disableStorage() 
```

### Conversation refresh listener

By default, C2C offline messages and recent contacts will be obtained asynchronously and profile data will be synced after login (if IM SDK storage is enabled, see [Relationship chain profile storage](https://intl.cloud.tencent.com/document/product/1047/34332#7.-.E5.85.B3.E7.B3.BB.E9.93.BE.E8.B5.84.E6.96.99.E5.AD.98.E5.82.A8) and [Group profile storage](https://intl.cloud.tencent.com/document/product/1047/34328#8.-.E7.BE.A4.E8.B5.84.E6.96.99.E5.AD.98.E5.82.A837)). Once synchronization is complete, the `onRefresh` callback in the conversation refresh listener `TIMRefreshListener` sends an interface refresh notification. Upon receiving this message, the user can refresh the interface (for example, refresh unread messages in the conversation list).

>If offline messages are not required, you can [send online messages](https://intl.cloud.tencent.com/document/product/1047/34320#.E5.9C.A8.E7.BA.BF.E6.B6.88.E6.81.AF).

In the event of multi-device login, the IM SDK updates the unread count locally and then notifies the user to update conversations. The notification will initiate a callback through `onRefreshConversation` in `TIMRefreshListener`. Users who require multi-device synchronization can perform relevant synchronous processing in this API. Therefore, we recommend using `setRefreshListener` in `TIMUserConfig` to configure a conversation refresh listener.

**Prototype:**

```
/**
 * Setting data refresh notification listener
 * @param listener Data refresh notification listener
 */
public TIMUserConfig setRefreshListener(TIMRefreshListener listener)
```

### Listener for message recall notifications

A message recall feature is available in IM SDK 3.1.0 and later versions. A message recall listener can be set through `setMessageRevokedListener` of `TIMUserConfig`.

**Prototype:**
```
/**
 * Setting message recall notification listener
 * @param listener Message recall notification listener
 * @since 3.1.0
 */
public TIMUserConfig setMessageRevokedListener(@NonNull TIMMessageRevokedListener listener)
```

## New Message Notifications

In most cases, users need to be notified of new messages. Therefore, register the new message notification callback `TIMMessageListener`. When the user logs in, C2C offline messages and recent contacts will be pulled. So that users do not miss message notifications, we recommend registering new message notifications before login.

> The IM SDK calls back all messages that are not stored locally to the app through registered message notifications.

The following is a message listener prototype. By default, all message listeners will be called back according to the order in which they were added until the `onNewMessages` callback returns true. Then, the next message listener is not called back.

**Prototype:**

```
/**
 * Adding a message listener
 * @param listener Message listener
 * By default, all message listeners will be called back according to the order in which they were added.
 * However, if the `onNewMessages` callback returns true, the next message listener will not be called back.
 */
public void addMessageListener(TIMMessageListener listener) 
```

**The following is a new message receipt callback:**

```
/**
* New messages receipt callback
* @param msgs New messages received
* @return Normally, if multiple listeners are registered, the IM SDK calls back all listeners in sequence. When the callback of a listener returns true, the subsequent listeners will not be called back.
*/
public boolean onNewMessages(List<TIMMessage> msgs)
```

A deleted listener will not be called. **The following is the prototype for message listener deletion:**

```
public void removeMessageListener(TIMMessageListener listener)
```

Callback message content is passed through the `TIMMessage` parameter. With `TIMMessage`, you can get detailed information about messages and the corresponding conversations, such as text, audio data, and images. For more information, see [Parsing messages](https://intl.cloud.tencent.com/document/product/1047/34320#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90).

**Example:**

```
//Set message listener. When new messages arrive, callback is initiated through this listener.
TIMManager.getInstance().addMessageListener(new TIMMessageListener() {//Message listener
    @Override
    public boolean onNewMessages(List<TIMMessage> msgs) {//New message received
		//For the parsing of message content, please see the message parsing description in the Receiving and Sending Messages documentation.
		return true; //When true is returned, the callback chain stops and the next new message listener will not be called.
    }
});
```
