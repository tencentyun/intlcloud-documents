## Obtaining the Communication Manager
Each operation in the IM SDK starts with `TIMManager`. Therefore, the first step is to obtain a `TIMManager` singleton. The `getInstance` prototype of a communication manager instance is as follows.

**Prototype:**

```
public static TIMManager getInstance()
```

**Example:**

```
TIMManager.getInstance();
```
## Configuring IM SDK for Initialization
Before initializing the IM SDK, you need to complete some IM SDK configurations, including configuring SDKAppID and log control. The corresponding configuration class is `TIMSdkConfig`.

### Log events

The IM SDK prints logs internally. If callers have their own unified log collection methods, they can use the `setLogListener` API in` TIMSdkConfig` to set a log event callback that returns logs to the callers. However, the IM SDK will still print logs internally in this case. You can disable printing by setting the console not to print logs, or by setting the log level.

**Prototype:**

```
/**
 * Set the current log callback listener, which must be done before IM SDK initialization
 * @param logListener Log callback listener
 */
public TIMSdkConfig setLogListener(TIMLogListener logListener) 
```

**Example:**

```
//Sets log callback. This API returns a copy of output logs from the IM SDK.
//[NOTE]: the level is defined in TIMManager, such as TIMManager.ERROR. It is different from the definition in the Android system.
mTIMSdkConfig.setLogListener(new TIMLogListener() {
    @Override
    public void log(int level, String tag, String msg) {
        //You can output SDK logs to your own logging system through this callback.
    }
});
```

### Setting the log level

When permissions allow, the IM SDK writes logs to log files by default. You can control the log output of the IM SDK by modifying the internal log writing level of the IM SDK through `setLogLevel` in `TIMSdkConfig`.

>
>- The API for setting the log writing level **must be called before IM SDK initialization** for the setting to take effect.
>- You can disable the log output of the IM SDK by setting the log level to TIMLogLevel.OFF. We recommend that you leave it enabled to facilitate troubleshooting.

**Prototype:**

```
/**
 * Set the log writing level, which must be called before IM SDK initialization for the setting to take effect
 * @param logLevel Log level
 */
public TIMSdkConfig setLogLevel(@NonNull TIMLogLevel logLevel) 
```


### Disabling console log printing

By default, the IM SDK prints logs to the console. If this produces too much disruption, you can disable console logs through `enableLogPrint` in `TIMSdkConfig` (file logs will still be printed, but you can disable this by setting the log level.)

> The API for configuring log settings **must be called before IM SDK initialization** for the settings to take effect.


**Prototype:**

```
/**
 * Enable or disable printing logs to the console, which must be set before IM SDK initialization
 * @param logPrintEnabled true - Output logs to the console
 */
public TIMSdkConfig enableLogPrint(boolean logPrintEnabled) 
```

### Modifying the log path

To manage logs centrally, you can modify the default log storage path. To do this, use `setLogPath` in `TIMSdkConfig` to set the storage path of logs.

>
> * The API for setting the log path **must be called before IM SDK initialization** for the setting to take effect.
> * The default IM SDK log storage path is: `/tencent/imsdklogs/(Your app package name)/` on the SD card.

**Prototype:**

```
/**
 * Set the log path, which must be called before IM SDK initialization for the setting to take effect.
 * @param logPath Log path
 */
public TIMSdkConfig setLogPath(@NonNull String logPath)
```

## Initializing the IM SDK

To use the IM SDK for further operations, you must initialize the IM SDK.

> When **multiple processes** exist, initialize the IM SDK in one process. Call `SessionWrapper.isMainProcess(Context context)` to determine the correct process.

**Prototype:**

```
/**
 * Initialize the IM SDK
 * @param context application context
 * @param config IM SDK global configuration
 * @return true - initialization succeeded, false - initialization failed
 */
public boolean init(@NonNull Context context, @NonNull TIMSdkConfig config)
```

**Example:**

```
//Initialize the IM SDK basic configuration
//Determine whether the current process is the main process
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

After initializing the IM SDK and before logging in to the IM SDK, configure a user through TIMUserConfig. After configuration and **before login**, bind the user configuration to the current communication manager through `setUserConfig` in `TIMManager`.

**Prototype:**
```
/**
 * Set the user configuration for the current user before login
 * @param userConfig User configuration
 */
public void setUserConfig(TIMUserConfig userConfig) 
```

**Example:**
```
//Basic user configuration
TIMUserConfig userConfig = new TIMUserConfig()
		//Set the listener for user state change events
		.setUserStatusListener(new TIMUserStatusListener() {
			@Override
			public void onForceOffline() {
				//Forced offline by another client
				Log.i(tag, "onForceOffline");
			}

			@Override
			public void onUserSigExpired() {
				//User signature expired, and therefore you must refresh userSig and log in to the IM SDK again
				Log.i(tag, "onUserSigExpired");
			}
		})
		//Set the listener for connection state events
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
		////Set the listener for group events
		.setGroupEventListener(new TIMGroupEventListener() {
			@Override
			public void onGroupTipsEvent(TIMGroupTipsElem elem) {
				Log.i(tag, "onGroupTipsEvent, type: " + elem.getTipsType());
			}
		})
		//Set the listener for conversation refreshing
		.setRefreshListener(new TIMRefreshListener() {
			@Override
			public void refresh() {
				Log.i(tag, "onRefresh");
			}

			@Override
			public void onRefreshConversation(List<TIMConversation> conversations) {
				Log.i(tag, "onRefreshConversation, conversation size: " + conversations.size());
			}
		});

//Disable all local storage
userConfig.disableStorage();
//Enable message read receipts
userConfig.enableReadReceipt(true);
		
//Bind the user configuration to the communication manager
TIMManager.getInstance().setUserConfig(userConfig);
```

### Network event notifications

This setting is optional. To allow users to detect whether the IM SDK is connected to the server, set this callback through `TIMUserConfig`. It notifies the user whether the link between the caller and the communication backend is connected or disconnected. Additionally, if the network is disconnected, the IM SDK will reconnect to the network after the network restores and automatically pull messages to notify the user. During the process, the user does not need to concern about the network condition. This is for notification purposes only.

>Here, network events do not reflect the user’s local network condition, but the connection status between the IM SDK and IM Cloud Server. As long as the user is logged-in, **the IM SDK will reconnect internally without user intervention**.

**Prototype:**

```
/**
 * Set the connection listener
 * @param listener Connection listener
 */
public TIMUserConfig setConnectionListener(TIMConnListener listener) 
```

**Example:**

See the example in [User Configuration](#User Configuration).

### User state changes

The IM SDK sends notifications for user state changes. You can monitor notifications for various changes by setting a listener for user state change notifications through `TIMUserConfig`. Currently, there are two types of notifications. For more information, see [Forcible User Offline Notifications](#.E7.94.A8.E6.88.B7.E8.A2.AB.E8.B8.A2.E4.B8.8B.E7.BA.BF.E9.80.9A.E7.9F.A5) and [User Ticket Expiration Notifications](#.E7.94.A8.E6.88.B7.E7.A5.A8.E6.8D.AE.E8.BF.87.E6.9C.9F.E9.80.9A.E7.9F.A5).

**Prototype:**

```
/**
 * Set the user state notification callback
 * @param userStatusListener User state notification callback
 */
public TIMUserConfig setUserStatusListener(TIMUserStatusListener userStatusListener)
```

**The listener for user state change notifications `TIMUserStatusListener` is defined as follows:**

```
/**
 * Listener for user state change notifications
 */
public interface TIMUserStatusListener {

    /**
     * Forcible offline callback
     */
    public void onForceOffline();

    /**
     * Ticket expiration callback
     */
    public void onUserSigExpired();
}
```


**Example:**

See the example in [User Configuration](#user-configuration).


### Forcible offline notifications

The user will be forced to log out when logging in on another device. When this happens, the IM SDK sends a forcible offline notification. If a listener for user state change notifications has been set (see [User State Changes](#user-state-changes)), this will be handled in the listener’s callback method `onForceOffline`. The common practice to this situation is to prompt the user to log out or force the other party to log out.


>If the user is logged out when offline, the following login attempt fails and a critical alert (login error code ERR_IMSDK_KICKED_BY_OTHERS: 6208) is displayed to the user. Developers can also choose to ignore this error and allow the user to log in again.

The following diagram illustrates the mutual forcible offline process in online scenarios. The user logs in on device 1, stays online, and then logs in on device 2. At this point, the user is forced offline by device 1 and the `onForceOffline` callback is triggered. After receiving the callback result on device 1, the user is prompted to call `login` to go back online and force device 2 offline.

![](https://main.qcloudimg.com/raw/40551f5696d97d39d7a905d5c88f6261.png)

The following diagram illustrates the mutual forcible offline process in offline scenarios. The user logs in on device 1 and kills the app process without calling `logout`. Then, the user logs in on device 2, but device 1 is unaware of this event because the app process has been killed. To explicitly alert the user and avoid imperceptible forcible offline, error code `ERR_IMSDK_KICKED_BY_OTHERS: 6208` is returned when the user tries to log in on device 1 again. This notifies the user of the forcible offline event and asks whether to force the other party offline. To force the other party offline, the user calls `login` again to forcibly go online, and the logged-in instance on device 2 receives the `onForceOffline` callback.
![](https://main.qcloudimg.com/raw/44ffa44fad6cc2c2de8a791e610da480.png)

### User ticket expiration notifications

When the user logs in (see [Login](https://intl.cloud.tencent.com/document/product/1047/34316#.E7.99.BB.E5.BD.951)), a user ticket needs to be provided, which expires after a certain period of time. If the user ticket expires, the interaction between the SDK and the server fails and the SDK sends the user ticket expiration notification. If the listener for user state change notifications has been set (see [User State Changes](#user-state-changes)), corresponding processing is performed in the listener's callback method `onUserSigExpired`. To continue to interact with the server, the user must refresh the ticket and log in again.


### Disabling storage
By default, the IM SDK stores messages, profiles, conversations, and other information. If you do not need to store these information, disable storage through `TIMUserConfig` to improve processing performance.

> Local storage disablement **must be called before login**.

**Prototype:**
```
/**
 * Disable local storage
 */
public TIMUserConfig disableStorage() 
```

### Conversation refreshing listener

By default, C2C offline messages and recent contacts will be obtained asynchronously, and profile data will be synchronized after login (If IM SDK storage has been enabled, see [Relationship Chain Profile Storage](https://intl.cloud.tencent.com/document/product/1047/34332#7.-.E5.85.B3.E7.B3.BB.E9.93.BE.E8.B5.84.E6.96.99.E5.AD.98.E5.82.A8) and [Group Profile Storage](https://intl.cloud.tencent.com/document/product/1047/34328#8.-.E7.BE.A4.E8.B5.84.E6.96.99.E5.AD.98.E5.82.A837)). When the synchronization is completed, the `onRefresh` callback in the conversation refreshing listener `TIMRefreshListener` sends an interface refresh notification. After receiving the notification, the user can refresh the interface (for example, refresh unread messages in the conversation list).

>If offline messages are not required, you can [send online messages](https://intl.cloud.tencent.com/document/product/1047/34320#.E5.9C.A8.E7.BA.BF.E6.B6.88.E6.81.AF) only.

In the event of multi-client login, the IM SDK updates the unread count locally and then notifies the user to update conversations. The notification will initiate a callback through `onRefreshConversation` in `TIMRefreshListener`. Users who require multi-client synchronization can perform relevant synchronous processing through this API. Therefore, we recommend that you use `setRefreshListener` in `TIMUserConfig` to configure a conversation refreshing listener.

**Prototype:**

```
/**
 * Set the listener for data refresh notifications
 * @param listener Listener for data refresh notifications
 */
public TIMUserConfig setRefreshListener(TIMRefreshListener listener)
```

### Listener for message recall notifications

The message recalling feature is available in IM SDK 3.1.0 and later. You can set the message recall listener through `setMessageRevokedListener` of `TIMUserConfig`.

**Prototype:**
```
/**
 * Set the listener for message recall notifications
 * @param listener Listener for message recall notifications
 * @since 3.1.0
 */
public TIMUserConfig setMessageRevokedListener(@NonNull TIMMessageRevokedListener listener)
```

## New Message Notifications

In most cases, users need to be notified of new messages. By registering the new message notification callback `TIMMessageListener`, when the user logs in, C2C offline messages and recent contacts will be pulled. In this way, users do not miss any message notifications. We recommend that you register new message notifications before login.

> The IM SDK calls back all messages that are not stored locally to the app through registered message notifications.

The following shows a message listener prototype. By default, all message listeners will be called back according to the order in which they were added until the `onNewMessages` callback returns true. If this is the case, no further message listeners will be called back.

**Prototype:**

```
/**
 * Add a message listener
 * @param listener Message listener
 * By default, all message listeners will be called back according to the order in which they were added.
 * However, if the `onNewMessages` callback returns true, no further message listeners will be called back.
 */
public void addMessageListener(TIMMessageListener listener) 
```

**The following shows a new message receipt callback:**

```
/**
* New messages receipt callback
* @param msgs Newly received messages
* @return Normally, if multiple listeners are registered, the IM SDK calls back all listeners in sequence. When the callback of a listener returns true, no further listeners will be called back.
*/
public boolean onNewMessages(List<TIMMessage> msgs)
```

A deleted listener will not be called. **The following shows the prototype for message listener deletion:**

```
public void removeMessageListener(TIMMessageListener listener)
```

The content of messages that are called back is transferred through the parameter `TIMMessage`. With `TIMMessage`, you can obtain detailed information about messages and conversations, such as message text, audio data, and images. For more information, see [Message Parsing](https://intl.cloud.tencent.com/document/product/1047/34320#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90).

**Example:**

```
//Sets the message listener. When a new message arrives, the callback is triggered through this listener.
TIMManager.getInstance().addMessageListener(new TIMMessageListener() {//Message listener
    @Override
    public boolean onNewMessages(List<TIMMessage> msgs) {//Newly received messages
		//For the parsing of message content, see the message parsing description in Receiving and Sending Messages.
		return true; //When true is returned, the callback chain stops and no further new message listeners will be called.
    }
});
```
