[](id: configuring push)
## Configuring Offline Push
To receive APNs offline message notifications, you need to submit a Push certificate in the Tencent Cloud console. Then, during each login, the client obtains and reports the Token through an API. The APNs push feature is only used to notify users. If the app runs in the foreground, the new message obtained by the `onNewMessage` callback takes precedence, and the message obtained by `didReceiveRemoteNotification` can be ignored. For more information on how the push service works, see [Apple Push Notification Service](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

### Applying for an APNs certificate
For more information on how to apply for an APNs certificate, see [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).

### Uploading a certificate to the console
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
2. Click the target app card to go to its basic configuration page.
3. Click **Add Certificate** on the right side of **iOS Platform Push Settings**.
4. Choose the certificate type, upload an iOS certificate (p.12), set the certificate password, and click **OK**.
 >!
 >- We recommend that the name of the certificate to be uploaded should be in all English letters (it must not contain special characters such as brackets).
 >- You need to set a password for the uploaded certificate. Without a password, push messages cannot be received.
 >- Certificates to be published on App Store need to be set to the Release environment. Otherwise, push cannot be received.
 >- The uploaded p12 certificate must be an authentic valid certificate that you have personally applied for.
 >
5. After the push certificate information is generated, record the certificate ID.

### Implementing APNs push on clients

To implement APNs push on clients, perform the following steps:

#### Requesting DeviceToken from the Apple backend

```
- (void)registNotification
{
    if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0)
    {
        [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:nil]];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    }
    else
    {
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
    }
}
/**
 *  The callback of AppDelegate returns deviceToken, which needs to be reported to the Tencent Cloud backend after login.
/**
-(void)application:(UIApplication *)app didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    // Note the deviceToken returned by Apple.
    _deviceToken = deviceToken;
}
```

#### Uploading Token to Tencent Cloud after IM SDK login

>! busiID must be consistent with the certificate ID assigned by the console.

```
  __weak typeof(self) ws = self;
 // If the TUIKit is used here, set the Token in the TUIKit login callback. If it is not used, set the Token in the TIMManager login callback.
 [[TUIKit sharedInstance] loginKit:identifier userSig:userSig succ:^{
    TIMTokenParam *param = [[TIMTokenParam alloc] init];
/* Users need to register a developer certificate with Apple, download and generate the certificate (p12 file) in their developer accounts, and upload the generated p12 file to the Tencent certificate console. The console will automatically generate a certificate ID and pass it to the busiID parameter.*/
#if kAppStoreVersion
// App Store version
#if DEBUG
    param.busiId = 2383;
#else
    param.busiId = 2382;
#endif
#else
    // Enterprise certificate ID
    param.busiId = 2516;
#endif    
    [param setToken:ws.deviceToken];    
    [[TIMManager sharedInstance] setToken:param succ:^{       
        NSLog(@"-----> Uploading token succeeded ");
    } fail:^(int code, NSString *msg) {
        NSLog(@"-----> Uploading token failed ");
    }];
 } fail:^(int code, NSString *msg) {
        NSLog(@"Login failed!");
    }];
  }
```

#### Reporting a background switch event when the app goes to the background

```
- (void)applicationDidEnterBackground:(UIApplication *)application
{
    __block UIBackgroundTaskIdentifier bgTaskID;
    bgTaskID = [application beginBackgroundTaskWithExpirationHandler:^ {
        // End the background_task regardless of whether it has been completed
        [application endBackgroundTask: bgTaskID];
        bgTaskID = UIBackgroundTaskInvalid;
    }];
     // Obtain the unread count
    int unReadCount = 0;
    NSArray *convs = [[TIMManager sharedInstance] getConversationList];
    for (TIMConversation *conv in convs) {
        if([conv getType] == TIM_SYSTEM){
            continue;
        }
        unReadCount += [conv getUnReadMessageNum];
    }
    [UIApplication sharedApplication].applicationIconBadgeNumber = unReadCount;
    
    //doBackground
    TIMBackgroundParam  *param = [[TIMBackgroundParam alloc] init];
    [param setC2cUnread:unReadCount];
    [[TIMManager sharedInstance] doBackground:param succ:^() {
        NSLog(@"doBackgroud Succ");
    } fail:^(int code, NSString * err) {
        NSLog(@"Fail: %d->%@", code, err);
    }];
}
```

#### Reporting a foreground switch event when the app goes to the foreground

```
- (void)applicationDidBecomeActive:(UIApplication *)application {
    [[TIMManager sharedInstance] doForeground:^() {
        NSLog(@"doForegroud Succ");
    } fail:^(int code, NSString * err) {
        NSLog(@"Fail: %d->%@", code, err);
    }];
}
```

## Push Format 
An example of the push format is as shown below.
<img src="//main.qcloudimg.com/raw/d23be65b4c481beb71db993045b4fec9.png" width=480 />


### General push rules
For one-to-one messages, the APNs push rules are as follows. Note that the nickname is the sender’s nickname. If the nickname is not set, only the content is displayed.

```
Nickname: content
```

For group messages, the APNs push rules are as follows. The name is either the group name card or the sender’s nickname. The priority is: `group name card` > `nickname`.

```
Name (group name): content
```

### Push rules for different types of messages
The APNs push content consists of the content of each `Elem` in the message body. The display of different `Elem` in offline messages is shown in the following table.

| Parameter | Description |
| --- | --- |
| Text Elem | Directly display the content |
| Voice Elem | Display `[voice]` |
| File Elem | Display `[file]` |
| Image Elem | Display `[image]` |
| Custom Elem | Display the content of the `desc` field. If it is empty, the message will not be pushed offline. |


### Communication among multiple apps

If you set `SDKAppID` to the same value for multiple apps, these apps communicate with each other. Different apps need to use different push certificates, and you need to [apply for an APNs certificate](https://intl.cloud.tencent.com/document/product/1047/34346) for each app and complete [offline push configuration](#configuring push).


## Push Alert Sound
### Setting custom push alert sounds

IM SDK provides an API for setting user sounds. You can use the API to customize the alert sound for one-to-one messages and the alert sound for group messages. You can also set the specific users to receive push messages.

```
/**
 *  APNs configuration
 */
@interface TIMAPNSConfig : NSObject
/**
 *  Whether push is enabled. 0: not set. 1: enabled. 2: disabled.
 */
@property(nonatomic,assign) uint32_t openPush;
/**
 *  C2C message sound. If you do not want to set it, pass nil
 */
@property(nonatomic,retain) NSString * c2cSound;
/**
 *  Group message sound. If you do not want to set it, pass nil
 */
@property(nonatomic,retain) NSString * groupSound;
@end
@interface TIMManager : NSObject
/**
 *  Setting APNs configuration
 *
 *  @param config APNs configuration
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Success
 */
-(int) setAPNS:(TIMAPNSConfig*)config succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameters**

| Parameter | Description |
| --- | --- |
| config | openPush: whether push is enabled. 0: not set. 1: enabled. 2: disabled. <br>c2cSound: alert sound for one-to-one messages, which needs to be set to a file name (including the suffix) <br>groupSound: alert sound for group messages, which needs to be set to a file name (including the suffix) |
| succ | Success callback |
| fail | Failure callback |

**Directions**
1. Integrate the audio file into your project.
 <img src="//main.qcloudimg.com/raw/c0aca90f7de2f67d815ddfcf13f9fcfc.png" width=480 />
2. After successful login, call the `setToken` API to set token and busiID information.
3. Call the `setAPNS` API to set the audio file information.
 >? You only need to set the **file name (including the suffix)** of the audio file.
 >
<img src="//main.qcloudimg.com/raw/76005ecd34b9cabf23536d77828f2de7.png" width=480 />

### Obtaining the push message alert sound

You can use the `getAPNSConfig` API to obtain the push message alert sound. This API synchronizes data from the server for each request and does not cache data locally.

```
@interface TIMManager : NSObject
/**
 *  Obtaining the APNs configuration
 *
 *  @param succ Success callback, which returns the configuration information
 *  @param fail Failure callback
 *
 *  @return 0 Success
 */
-(int) getAPNSConfig:(TIMAPNSConfigSucc)succ fail:(TIMFail)fail;
@end
```

Parameter descriptions:

| Parameter | Description |
| --- | --- |
| succ | Success callback, which returns the TIMAPNSConfig structure |
| fail | Failure callback |

## Customizing Offline Message Attributes

You can set `TIMOfflinePushInfo` in each message to determine the displayed text, extension field, alert sound, and whether to enable push. During message push, the original default attributes will be replaced by the custom attributes that you have set. For example, if you enter `kIOSOfflinePushNoSound` in the `sound` attribute, the push received by the recipient will be forcibly muted.

```
/**
 Entering `kIOSOfflinePushNoSound` in the `sound` field indicates that no sound will be played when the push message is received.
 */
extern NSString * const kIOSOfflinePushNoSound;
@interface TIMAndroidOfflinePushConfig : NSObject
/**
 *  Offline push display tag
 */
@property(nonatomic,retain) NSString * title;
/**
 *  Sound field information during offline push on Android
 */
@property(nonatomic,retain) NSString * sound;
/**
 *  Notification mode for offline push
 */
@property(nonatomic,assign) TIMAndroidOfflinePushNotifyMode notifyMode;
@end
@interface TIMIOSOfflinePushConfig : NSObject
/**
 *  Sound field information during offline push
 */
@property(nonatomic,retain) NSString * sound;
/**
 *  Ignore badge count
 */
@property(nonatomic,assign) BOOL ignoreBadge;
@end
@interface TIMOfflinePushInfo : NSObject
/**
 *  Custom message description information to be displayed in text during offline push
 */
@property(nonatomic,retain) NSString * desc;
/**
 *  Extension field information during offline push
 */
@property(nonatomic,retain) NSString * ext;
/**
 *  Push rule flag
 */
@property(nonatomic,assign) TIMOfflinePushFlag pushFlag;
/**
 *  iOS offline push configuration
 */
@property(nonatomic,retain) TIMIOSOfflinePushConfig * iosConfig;
/**
 *  Android offline push configuration
 */
@property(nonatomic,retain) TIMAndroidOfflinePushConfig * androidConfig;
@end
```
