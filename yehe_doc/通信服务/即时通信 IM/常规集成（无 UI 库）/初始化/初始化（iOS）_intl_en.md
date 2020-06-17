## Initializing Communication Manager
Every operation in the IM SDK starts with `TIMManager`. Therefore, the first step is to get a `TIMManager` singleton.

**Prototype:**
```
@interface TIMManager : NSObject
/**
 *  Get manager instance
 *
 *  @return manager instance
 */
+(TIMManager*)sharedInstance;
@end
```

**Example:**
```
TIMManager * manager = [TIMManager sharedInstance];
```
Before using the SDK for further operations, you need to initialize the SDK.

**Prototype:**
```
@interface TIMManager : NSObject

/**
 *  Initialize the SDK
 *
 *  @param config      Configuration information, globally effective
 *
 *  @return 0 Success
 */
- (int)initSdk:(TIMSdkConfig*)globalConfig;

/**
 *  Initialize the current manager, call after initSdk: and before login:
 *
 *  @param config    Configuration information, valid for the current TIMManager
 *
 *  @return 0 Success
 */
- (int)setUserConfig:(TIMUserConfig*)config;
 
@end

//Global configuration information
@interface TIMSdkConfig : NSObject

//User identifier app ID for connecting to the SDK (required)
@property(nonatomic,assign) int sdkAppId;

//Forbid the console from printing logs
@property(nonatomic,assign) BOOL disableLogPrint;

//Local write log file level. The default level is DEBUG.
@property(nonatomic,assign) TIMLogLevel logLevel;

//Log file path. The default path is used when this parameter is not set. The log path can be obtained through TIMManager -> getLogPath.
@property(nonatomic,strong) NSString * logPath;

//Log level that is called back to the logFunc function. The default level is DEBUG.
@property(nonatomic,assign) TIMLogLevel logFuncLevel;

//Log listener function
@property(nonatomic,copy) TIMLogFunc logFunc;

//Message database path. The default path is used when this parameter is not set.
@property(nonatomic,strong) NSString * dbPath;

//Network listener that listens for the successful and failed status of network connections
@property(nonatomic,strong) id<TIMConnListener> connListener;

@end

//User configuration information
@interface TIMUserConfig : NSObject

//Disable local storage
@property(nonatomic,assign) BOOL disableStorage;

//Whether or not to enable multi-client unread synchronization notification. This option modifies the unread notification logic in the case of multi-client login. YES: only when one client calls setReadMessage() to mark the message as read, the other client will not receive an unread notification. NO: once the message is received by one client, the other client will not receive an unread notification. In the same way, these unread messages will not be received after the app is uninstalled and installed again.
@property(nonatomic,assign) BOOL disableAutoReport;

//Whether or not to enable read receipts. YES: after the recipient reads the message (setReadMessage), the sender will receive the TIMMessageReceiptListener callback notification. NO: do not enable read receipts. This is the default setting.
@property(nonatomic,assign) BOOL enableReadReceipt;

//Set the group profiles to be pulled by default. To pull custom fields, configure “Custom Fields” and corresponding user operation permissions in IM Console -> Feature Configuration -> Group Custom Fields. The configuration takes effect after 5 minutes.
@property(nonatomic,strong) TIMGroupInfoOption * groupInfoOpt;

//Set the group member profiles to be pulled by default. To pull custom fields, configure “Custom Fields” and corresponding user operation permissions in IM Console -> Feature Configuration -> Group Member Custom Fields. The configuration takes effect after 5 minutes.
@property(nonatomic,strong) TIMGroupMemberInfoOption * groupMemberInfoOpt;

//Relationship chain parameter
@property(nonatomic,strong) TIMFriendProfileOption * friendProfileOpt;

//User login status listener that listens for force offline, network reconnection failure, and UserSig expiration notifications
@property(nonatomic,weak) id<TIMUserStatusListener> userStatusListener;

//Conversation refresh listener that listens for the refresh of conversations
@property(nonatomic,weak) id<TIMRefreshListener> refreshListener;

//Read receipts listener that listens for the read receipts of messages. The enableReadReceipt field must be set to YES.
@property(nonatomic,weak) id<TIMMessageReceiptListener> messageReceiptListener;

//Message update listener that listens for message status changes
@property(nonatomic,weak) id<TIMMessageUpdateListener> messageUpdateListener;

//Message recall listener that listens for message recall notifications in conversations
@property(nonatomic,weak) id<TIMMessageRevokeListener> messageRevokeListener;

//File upload progress listener that listens for the upload progress of audio, image, video, and file messages which are uploaded to the server before being sent
@property(nonatomic,weak) id<TIMUploadProgressListener> uploadProgressListener;

//Group event notification listener
@property(nonatomic,weak) id<TIMGroupEventListener> groupEventListener;

//Listener for locally cached relationship chain data
@property(nonatomic,weak) id<TIMFriendshipListener> friendshipListener;

@end
```

## New Message Notifications
In most cases, users need to be notified of new messages. Therefore, register the new message notification callback `TIMMessageListener`. When the user logs in, offline messages will be pulled. So that users do not miss message notifications, register new message notifications before login.

**Prototype:**

```
/**
 *  Callback for receiving new messages
 */
@protocol TIMMessageListener <NSObject>
@optional
/**
 *  New message callback notification
 *
 *  @param msgs List of new messages, an array of TIMMessage types
 */
- (void)onNewMessage:(NSArray*) msgs;
@end
 
@interface TIMManager : NSObject
 
/**
 *  Add message callback (ignores repeated adding)
 *
 *  @param listener Callback
 *
 *  @return Successful
 */
- (int)addMessageListener:(id<TIMMessageListener>)listener;
 
@end
```

Callback message content is passed through `TIMMessage`. With `TIMMessage`, you can get detailed information about messages and the corresponding conversations, such as text, audio data, and images. The following example sets a message callback notification and prints new messages directly. For more information, see [Parsing messages](https://intl.cloud.tencent.com/document/product/1047/34321).

**Example:**

```
@interface TIMMessageListenerImpl : NSObject
- (void)onNewMessage:(TIMMessage*) msg;
@end
@implementation TIMMessageListenerImpl
- (void)onNewMessage:(NSArray*) msgs {
    NSLog(@"NewMessages: %@", msgs);
}
@end
TIMMessageListenerImpl * impl = [[TIMMessageListenerImpl alloc] init];
[[TIMManager sharedInstance] addMessageListener:impl];
```

## Network Event Notifications
This setting is optional. To allow users to detect whether the IM SDK is connected to the server, set this callback function. It notifies the user of the connection and disconnection events between the caller and the communication backend. If the network connection is interrupted, the IM SDK will reconnect to the network after the network recovers and automatically pull messages to notify the user. The user does not need to worry about the network status. This is for notification purposes only.

> **Note:**
> Here, network events do not indicate the user’s local network status, but whether the IM SDK is connected to the IM cloud server. As long as the user is logged in, **IM SDK will reconnect internally, and no intervention by the user required.**

**Prototype:**

```
/**
 *  Connection notification callback
 */
@protocol TIMConnListener <NSObject>
@optional
/**
 *  Network connection successful
 */
- (void)onConnSucc;
/**
 *  Network connection failed
 *
 *  @param code Error code
 *  @param err  Error description
 */
- (void)onConnFailed:(int)code err:(NSString*)err;
/**
 *  Network disconnected. Users are notified of the disconnection but do not need to log in again. Users return to the online status automatically once the network is reconnected.
 *
 *  @param code Error code
 *  @param err  Error description
 */
- (void)onDisconnect:(int)code err:(NSString*)err;
/**
 *  Connecting
 */
- (void)onConnecting;
@end
@interface TIMSdkConfig : NSObject
/**
 *  Network listener
 */
@property(nonatomic,retain) id<TIMConnListener> connListener;
@end
```

The following example listens for network events and outputs logs.
**Example:**

```
@interface TIMConnListenerImpl : NSObject
- (void)onConnSucc;
- (void)onConnFailed:(int)code err:(NSString*)err;
- (void)onDisconnect:(int)code err:(NSString*)err;
@end
@implementation TIMConnListenerImpl
 
- (void)onConnSucc {
    NSLog(@"Connect Succ");
} 
- (void)onConnFailed:(int)code err:(NSString*)err {
  // code Error code: see the Error Code Table for more information
    NSLog(@"Connect Failed: code=%d, err=%@", code, err);
} 
- (void)onDisconnect:(int)code err:(NSString*)err {
  // code Error code: see the Error Code Table for more information
    NSLog(@"Disconnect: code=%d, err=%@", code, err);
} 
@end
TIMConnListenerImpl * connListenerImpl = [[TIMConnListenerImpl alloc] init];
TIMSdkConfig * cfg = [[TIMSdkConfig alloc] init];
cfg.connListener = connListenerImpl;
[[TIMManager sharedInstance] initSdk:cfg];
```

## Log Events
The IM SDK prints logs internally. If callers have their own unified log collection methods, they can set log event callbacks, which are called by the SDK to return logs to the callers. Callbacks can be called through **blocks** or the **`protocol` API**.
After callbacks are set, the IM SDK will still print logs internally. You can disable this by setting the console to not print logs, or setting the log level.

**Prototype:**

```
@interface TIMSdkConfig : NSObject
/**
 *  log listener function
 */
@property(nonatomic,copy) TIMLogFunc logFunc;
@end
```

The following example uses block to call back printing logs to the console.
**Example:**

```
TIMSdkConfig * cfg = [[TIMSdkConfig alloc] init];
cfg.logFunc = ^(NSString* content) {
		NSLog(@"%@", content);
}];
```

## User Status Changes

The SDK sends notifications for user status changes. You can listen to notifications for various changes by setting listeners for user status change notifications using the `userStatusListener` property in `TIMUserConfig`. Currently, there are three kinds of notifications. For more information, see [User force offline notifications](#.E7.94.A8.E6.88.B7.E8.A2.AB.E8.B8.A2.E4.B8.8B.E7.BA.BF.E9.80.9A.E7.9F.A5) and [User ticket expiration notifications](#.E7.94.A8.E6.88.B7.E7.A5.A8.E6.8D.AE.E8.BF.87.E6.9C.9F.E9.80.9A.E7.9F.A5). In this case, users need to log in again to use messages, groups, and friends features normally.

**Prototype:**
```
/**
 *  User online status notification
 */
@protocol TIMUserStatusListener <NSObject>
@optional
/**
 *  Force offline notification
 */
- (void)onForceOffline;
/**
 *  Reconnection failed
 */
- (void)onReConnFailed:(int)code err:(NSString*)err;
/**
 *  The userSig expired (Obtain a new userSig to log in)
 */
- (void)onUserSigExpired;
@end
@interface TIMUserConfig : NSObject
/**
 *  User login status listener
 */
@property(nonatomic,retain) id<TIMUserStatusListener> userStatusListener;
@end
```

The following example prints logs after receiving a force offline event callback. **Example:**

```
@interface TIMUserStatusListenerImpl : NSObject{
}
- (void)onForceOffline;
- (void)onUserSigExpired;
@end
@implementation TIMUserStatusListenerImpl 
- (void)onForceOffline {
    NSLog(@"force offline");
}
- (void)onUserSigExpired {
    NSLog(@"userSig expired");
}
@end
TIMUserStatusListenerImpl * impl = [[TIMUserStatusListenerImpl alloc] init];
TIMUserConfig * cfg = [[TIMUserConfig alloc] init];
cfg.userStatusListener = impl;
```

### Force offline notifications
The user will be forced to log out when calling login to log in on another device. When this happens, the SDK sends a force offline notification. If a user status change notification listener has been set (see [User Status Changes](#user-state-changes)), the situation will be handled in the listener’s callback method `onForceOffline`. Common practice is to prompt the user to log out or force the other party to log out by calling login again.

> **Note:**
> If the user is logged out when offline, the subsequent login by calling login will fail with a strong alert and a strong alert (login error code `ERR_IMSDK_KICKED_BY_OTHERS: 6208`) is displayed to the user. Developers can also choose to ignore this error and let the user log in again.

The following diagram illustrates the **force offline process in online scenarios**. The user logs in on device 1 by calling login, stays online, and then logs in on device 2 by calling login. At this point, the user is logged out on device 1 and receives the `onForceOffline` callback. After receiving the callback on device 1, the user is prompted to call `login` to go back online and force device 2 to log out.

![](https://main.qcloudimg.com/raw/40551f5696d97d39d7a905d5c88f6261.png)

The following diagram illustrates the **force offline process in offline scenarios**. The user logs in on device 1 by calling login and the process exits without calling `logout`. The user then logs in on device 2 by calling login, but device 1 is unaware of this event because the user is not online. To explicitly alert the user and avoid imperceptible force offline, `ERR_IMSDK_KICKED_BY_OTHERS: 6208` is returned when the user tries to log in on device 1 again, notifying the user of the force offline event and asking whether to kick the other party offline. To kick the other party offline, the user calls `login` again to force a login and the logged-in instance on device 2 receives the `onForceOffline` callback.

![](https://main.qcloudimg.com/raw/44ffa44fad6cc2c2de8a791e610da480.png)

### User ticket expiration notifications
When the user logs in (see [Login](https://intl.cloud.tencent.com/document/product/1047/34317)), a user ticket needs to be provided, which will expire after a certain period of time. If the user ticket has expired, the interaction between the SDK and the server fails and the SDK gives the user ticket expiration notification. If a user status change notification listener is set (see [User Status Changes](#user-state-changes)), corresponding processing can be carried out in the listener's callback method `onUserSigExpired`. To continue interacting with the server, the user must change the ticket and log in again.

## Setting Log Level
You can modify the IM SDK internal log level by configuring `TIMSdkConfig`. You can disable IM SDK log output by setting the log level to TIMLogLevel.OFF. We recommend that you leave it enabled to facilitate troubleshooting.

**Prototype:**

```
@interface TIMSdkConfig : NSObject
/**
 *  Local write log file level. The default level is DEBUG.
 */
@property(nonatomic,assign) TIMLogLevel logLevel;
@end
```

## Disabling Console Log Printing or Modifying the Log Path
By default, the IM SDK prints logs to the console. If this produces too much disruption during testing and debugging, you can disable console logs (file logs will still be printed, but you can disable this by setting the log level). If you do not modify the log path but only the level, use `getLogPath` to get the default path to pass to `initLogSettings`. The default log path is `Library/Caches/imsdk_YYYYMMDD.log` under the app directory.

**Prototype:**

```
@interface TIMSdkConfig : NSObject
/**
 *  Log file path. The default path is used if it is not set.
 */
@property(nonatomic,retain) NSString * logPath;
/**
 *  Forbid the console from printing logs
 */
@property(nonatomic,assign) BOOL disableLogPrint;
@end
```
