## Initializing the Communication Manager
Each operation in the IM SDK starts with `TIMManager`. Therefore, the first of all is to obtain a `TIMManager` singleton.

**Prototype:**
```
@interface TIMManager : NSObject
/**
 *  Obtain the manager instance
 *
 *  @return Manager instance
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
 *  @param config Configuration information that is globally valid
 *
 *  @return 0 Succeeded
 */
- (int)initSdk:(TIMSdkConfig*)globalConfig;

/**
 *  Initialize the current manager, and call it after initSdk: and before login:
 *
 *  @param config Configuration information that is valid for the current TIMManager
 *
 *  @return 0 Succeeded
 */
- (int)setUserConfig:(TIMUserConfig*)config;
 
@end

//Global configuration information
@interface TIMSdkConfig : NSObject

//App ID for identifying the user’s access to the SDK (required)
@property(nonatomic,assign) int sdkAppId;

//Forbid the console from printing logs
@property(nonatomic,assign) BOOL disableLogPrint;

//Local log writing level, which defaults to DEBUG
@property(nonatomic,assign) TIMLogLevel logLevel;

//Log file path. The default path is used when this parameter is not specified. The log path can be obtained through TIMManager > getLogPath.
@property(nonatomic,strong) NSString * logPath;

//Log level that is called back to the logFunc function, which defaults to DEBUG
@property(nonatomic,assign) TIMLogLevel logFuncLevel;

//Log listener function
@property(nonatomic,copy) TIMLogFunc logFunc;

//Message database path. The default path is used when this parameter is not specified.
@property(nonatomic,strong) NSString * dbPath;

//Network listener for monitoring whether the network connection succeeded or failed
@property(nonatomic,strong) id<TIMConnListener> connListener;

@end

//User configuration information
@interface TIMUserConfig : NSObject

//Disable local storage
@property(nonatomic,assign) BOOL disableStorage;

//Whether or not to enable multi-client unread synchronization notification. This option determines the unread notification logic in the case of multi-client login. YES: only when one client calls setReadMessage() to mark the message as read, the other client will not receive an unread notification. NO: once the message is received by one client, the other client will not receive an unread notification. Similarly, these unread messages will not be received after the app is uninstalled and installed again.
@property(nonatomic,assign) BOOL disableAutoReport;

//Whether or not to enable read receipts. YES: after the recipient reads the message (setReadMessage), the sender will receive the TIMMessageReceiptListener callback notification. NO: disable read receipts, which is the default.
@property(nonatomic,assign) BOOL enableReadReceipt;

//Sets group information to be pulled by default. To pull custom fields, configure "Custom Fields" and corresponding user operation permissions by navigating to IM Console > **Feature Configuration** > **Group Custom Fields**. The configuration will take effect in 5 minutes.
@property(nonatomic,strong) TIMGroupInfoOption * groupInfoOpt;

//Sets group member information to be pulled by default. To pull custom fields, configure "Custom Fields" and corresponding user operation permissions by navigating to IM Console > **Feature Configuration** > **Group Member Custom Fields**. The configuration will take effect in 5 minutes.
@property(nonatomic,strong) TIMGroupMemberInfoOption * groupMemberInfoOpt;

//Relationship chain parameter
@property(nonatomic,strong) TIMFriendProfileOption * friendProfileOpt;

//User login state listener that monitors forcible logout, network reconnection failure, and UserSig expiration notifications
@property(nonatomic,weak) id<TIMUserStatusListener> userStatusListener;

//Conversation refreshing listener that monitors the refreshment of conversations
@property(nonatomic,weak) id<TIMRefreshListener> refreshListener;

//Read receipt listener that monitors the read receipts of messages. The enableReadReceipt field must be set to YES.
@property(nonatomic,weak) id<TIMMessageReceiptListener> messageReceiptListener;

//Message update listener that monitors message state changes
@property(nonatomic,weak) id<TIMMessageUpdateListener> messageUpdateListener;

//Message recall listener that monitors message recall notifications in conversations
@property(nonatomic,weak) id<TIMMessageRevokeListener> messageRevokeListener;

//File upload progress listener that monitors the upload progress of audio, image, video, and file messages that are uploaded to the server before being sent
@property(nonatomic,weak) id<TIMUploadProgressListener> uploadProgressListener;

//Group event notification listener
@property(nonatomic,weak) id<TIMGroupEventListener> groupEventListener;

//Listener for locally cached relationship chain data
@property(nonatomic,weak) id<TIMFriendshipListener> friendshipListener;

@end
```

## Message Notifications
In most cases, users need to be notified of new messages. To this end, register the new message notification callback `TIMMessageListener`. When the user logs in, offline messages will be pulled. To ensure that no message notification is missing, register new message notifications before login.

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
 *  @param msgs List of new messages as a TIMMessage array
 */
- (void)onNewMessage:(NSArray*) msgs;
@end
 
@interface TIMManager : NSObject
 
/**
 *  Add a message callback (repeated additions will be ignored)
 *
 *  @param listener Callback
 *
 *  @return Succeeded
 */
- (int)addMessageListener:(id<TIMMessageListener>)listener;
 
@end
```

The content of messages that are called back is transferred through the `TIMMessage` parameter. With `TIMMessage`, you can obtain details about messages and conversations, such as message text, audio data, and images. The following example sets message callback notifications and directly prints messages upon their arrival. For more information, see [Message Parsing](https://intl.cloud.tencent.com/document/product/1047/34321#.E6.B6.88.E6.81.AF.E8.A7.A3.E6.9E.90).

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
This setting is optional. To allow users to detect whether the IM SDK is connected to the server, set this callback. It notifies the user of connection and disconnection events between the caller and the communication backend. If the network connection is disconnected, the IM SDK will reconnect to the network after the network restores and automatically pull messages to notify the user. The user does not need to concern about the network state. This is for notification purposes only.

> **Note:**
> Here, network events do not reflect the user’s local network state, but whether the IM SDK is connected to the IM cloud server or not. As long as the user is logged in, **the IM SDK will reconnect internally without user intervention.**

**Prototype:**

```
/**
 *  Connection notification callback
 */
@protocol TIMConnListener <NSObject>
@optional
/**
 *  Network connection succeeded
 */
- (void)onConnSucc;
/**
 *  Network connection failed
 *
 *  @param code Error code
 *  @param err Error description
 */
- (void)onConnFailed:(int)code err:(NSString*)err;
/**
 *  The network is disconnected. Users are notified of the disconnection, but do not need to log in again. Users automatically go online once the network restores.
 *
 *  @param code Error code
 *  @param err Error description
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

The following example monitors network events and outputs logs.
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
  // code Error code: see the error code table for details
    NSLog(@"Connect Failed: code=%d, err=%@", code, err);
} 
- (void)onDisconnect:(int)code err:(NSString*)err {
  // code Error code: see the error code table for details
    NSLog(@"Disconnect: code=%d, err=%@", code, err);
} 
@end
TIMConnListenerImpl * connListenerImpl = [[TIMConnListenerImpl alloc] init];
TIMSdkConfig * cfg = [[TIMSdkConfig alloc] init];
cfg.connListener = connListenerImpl;
[[TIMManager sharedInstance] initSdk:cfg];
```

## Log Events
The IM SDK prints logs internally. If callers have their own unified log collection methods, they can set log event callbacks, which are called by the SDK to return logs to the callers. Callbacks can be implemented through **blocks** or the **`protocol` API**.
After callbacks are set, the IM SDK will still print logs internally. You can disable this by setting the console not to print logs, or by setting the log level.

**Prototype:**

```
@interface TIMSdkConfig : NSObject
/**
 *  Log listener function
 */
@property(nonatomic,copy) TIMLogFunc logFunc;
@end
```
 
The following example uses blocks to call back printed logs to the console.
**Example:**

```
TIMSdkConfig * cfg = [[TIMSdkConfig alloc] init];
cfg.logFunc = ^(NSString* content) {
		NSLog(@"%@", content);
}];
```

## User State Changes

The SDK sends notifications for user state changes. You can listen to notifications for various changes by setting listeners for user state change notifications, which can be done by setting the `userStatusListener` attribute in `TIMUserConfig`. Currently, there are three kinds of notifications. For more information, see [User Forcible Logout Notifications](#user-forcible-logout-notifications) and [User Ticket Expiration Notifications](#user-ticket-expiration-notifications). In this case, users need to log in again to normally use the message, group, and friend features.

**Prototype:**
```
/**
 *  User online state notification
 */
@protocol TIMUserStatusListener <NSObject>
@optional
/**
 *  Forcible logout notification
 */
- (void)onForceOffline;
/**
 *  Reconnection failed
 */
- (void)onReConnFailed:(int)code err:(NSString*)err;
/**
 *  UserSig expired (in this case, the user needs to obtain a new UserSig before logging in)
 */
- (void)onUserSigExpired;
@end
@interface TIMUserConfig : NSObject
/**
 *  User login state listener
 */
@property(nonatomic,retain) id<TIMUserStatusListener> userStatusListener;
@end
```
 
The following example prints logs after receiving a forcible logout event callback. **Example:**
 
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

### Forcible logout notifications
The user will be forced logout when calling login to log in on another device. When this happens, the SDK sends a forcible logout notification. If you have set a user state change notification listener (see [User State Changes](#user-state-changes)), this situation will be handled in the listener’s callback method `onForceOffline`. The common practice is to prompt the user to log out or force the other party logout by calling login again.

> **Note:**
> If the user is logged out when offline, the subsequent login by calling login will fail with a strong alert and a strong alert (login error code `ERR_IMSDK_KICKED_BY_OTHERS: 6208`) is displayed to the user. Developers can also choose to ignore this error and allow the user to log in again.

The following diagram illustrates the **forcible logout process in online scenarios**. The user logs in on device 1 by calling login, stays online, and then logs in on device 2 by calling login. At this point, the user is forced logout on device 1 and receives the `onForceOffline` callback. After receiving the callback on device 1, the user is prompted to call `login` to go back online and force device 2 logout.

![](https://main.qcloudimg.com/raw/40551f5696d97d39d7a905d5c88f6261.png)

The following diagram illustrates the **forcible logout process in offline scenarios**. The user logs in on device 1 by calling login and the process exits without calling `logout`. The user then logs in on device 2 by calling login, but device 1 is unaware of this event because the user is not online. To explicitly alert the user and avoid imperceptible forcible logout, `ERR_IMSDK_KICKED_BY_OTHERS: 6208` is returned when the user tries to log in on device 1 again, notifying the user of the forcible logout event and asking whether to force the other party logout. To force the other party logout, the user calls `login` again to force a login, and the logged-in instance on device 2 receives the `onForceOffline` callback.

![](https://main.qcloudimg.com/raw/44ffa44fad6cc2c2de8a791e610da480.png)

### User ticket expiration notifications
When the user logs in (see [Login](https://intl.cloud.tencent.com/document/product/1047/34317)), a user ticket needs to be provided, which will expire after a certain period of time. If the user ticket expires, the interaction between the SDK and the server fails and the SDK sends the user ticket expiration notification. If you have set a user state change notification listener (see [User State Changes](#user-state-changes)), the corresponding processing can be done in the listener's callback method `onUserSigExpired`. To continue to interact with the server, the user must refresh the ticket and log in again.

## Setting the Log Level
You can modify the internal log level of the IM SDK by configuring `TIMSdkConfig`. You can disable IM SDK log output by setting the log level to TIMLogLevel.OFF. We recommend that you leave it enabled to facilitate troubleshooting.

**Prototype:**

```
@interface TIMSdkConfig : NSObject
/**
 *  Local log writing level, which defaults to DEBUG.
 */
@property(nonatomic,assign) TIMLogLevel logLevel;
@end
```

## Forbidding Console Log Printing or Modifying the Log Path
By default, the IM SDK prints logs to the console. If this produces too much disruption during testing and debugging, you can disable console logs (file logs will still be printed, but you can disable this by setting the log level.) If you do not modify the log path but only the level, use `getLogPath` to obtain the default path and pass it into `initLogSettings`. The default log path is `Library/Caches/imsdk_YYYYMMDD.log` in the app.

**Prototype:**

```
@interface TIMSdkConfig : NSObject
/**
 *  Log file path. The default path is used if this is not specified.
 */
@property(nonatomic,retain) NSString * logPath;
/**
 *  Forbid the console from printing logs
 */
@property(nonatomic,assign) BOOL disableLogPrint;
@end
```
