<span id="Configuring Push"></span>
## Configuring Offline Push
To receive APNs offline message notifications, you need to submit a push certificate on the Tencent Cloud management platform so that every time you log in on your client, you can obtain and report the token through an API. The APNs push feature is only used for notifying users. If the app is running on the frontend, new messages obtained by the `onNewMessage` callback prevail, and messages obtained by `didReceiveRemoteNotification` can be ignored. For details on push principles, see [Apple Push Notification Service](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

### Applying for an APNs certificate
For details on how to apply for an APNs certificate, see [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).

### Uploading the certificate to the console
1. Log in to [IM Console](https://console.cloud.tencent.com/im).
2. Click the target app card to go to its basic configuration page.
3. Click **Add Certificate** to the right of **iOS Platform Push Settings**.
4. Select the certificate type, upload an iOS certificate (p.12), set the certificate password, and click **OK**.
 >
 >- We recommend that the name of the certificate to be uploaded is in all English letters (and it must not contain special characters such as brackets).
 >- You need to set a password for the uploaded certificate. Without a password, no push message can be received.
 >- Certificates to be published on App Store need to be set to the production environment. Otherwise, no pushed content can be received.
 >- The uploaded p12 certificate must be an authentic and valid certificate that you have personally applied for.
 >
5. After the push certificate information is generated, record the certificate ID.

### Implementing APNs push on the client

To enable a client to receive APNs push messages, complete the following steps. 

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
 * The callback of AppDelegate returns deviceToken, which needs to be reported to the Tencent Cloud backend after login.
/**
-(void)application:(UIApplication *)app didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    //Record the deviceToken returned by Apple.
    _deviceToken = deviceToken;
}
```

#### Uploading Token to Tencent Cloud after logging in to the IM SDK

> busiId must be consistent with the certificate ID assigned by the console.

```
  __weak typeof(self) ws = self;
 //If TUIKit is used here, set Token in the TUKit login callback. If it is not used, set Token in the login callback of TIMManager.
 [[TUIKit sharedInstance] loginKit:identifier userSig:userSig succ:^{
    TIMTokenParam *param = [[TIMTokenParam alloc] init];
/* Users themselves need to register a developer certificate with Apple, then download and generate the certificate (p12 file) under the developer account, and send the generated p12 file to Tencent’s certificate management console. Then, the console automatically generates a certificate ID and sends it to the busiId parameter.*/
#if kAppStoreVersion
// App Store version
#if DEBUG
    param.busiId = 2383;
#else
    param.busiId = 2382;
#endif
#else
    //Business certificate ID
    param.busiId = 2516;
#endif    
    [param setToken:ws.deviceToken];    
    [[TIMManager sharedInstance] setToken:param succ:^{       
        NSLog(@"-----> Uploaded the token successfully");
    } fail:^(int code, NSString *msg) {
        NSLog(@"-----> Failed to upload the token");
    }];
 } fail:^(int code, NSString *msg) {
        NSLog(@"Login failed!");
    }];
  }
```

#### Reporting the background switching event when the app enters the background

```
- (void)applicationDidEnterBackground:(UIApplication *)application
{
    __block UIBackgroundTaskIdentifier bgTaskID;
    bgTaskID = [application beginBackgroundTaskWithExpirationHandler:^ {
        //End the background_task task, regardless of whether it has been completed or not
        [application endBackgroundTask: bgTaskID];
        bgTaskID = UIBackgroundTaskInvalid;
    }];
     //Obtain the unread message count
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

#### Reporting the foreground switching event when the app enters the foreground

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
An example of the push format is shown in the figure below.
![](https://main.qcloudimg.com/raw/0602abcefdd6062d8492c720f6886b82.png)


### General push rules
For one-to-one chat messages, APNs push rules are as follows. Note that the nickname is the sender’s nickname. If the nickname is not specified, only the content is displayed.

```
Nickname: content
```

For group messages, APNs push rules are as follows. Note that the name refers to the group name card or the sender’s nickname. The priority of the `group name card` is higher than the `group name`.

```
Name (group name): content
```

### Push rules for different types of messages
APNs push content consists of the content of each `Elem` in the message body. The display of different `Elem` in offline messages is described in the following table.

| Parameter | Description |
| --- | --- |
| Text Elem | Directly display the content |
| Audio Elem | Display `[audio]` |
| File Elem | Display `[file]` |
| Image Elem | Display `[image]` |
| Custom Elem | Display the content of the `desc` field. If the custom message `desc` is empty, the message is not pushed offline. |


### Communication among multiple apps

If you set `SDKAppID` to the same value for multiple apps, these apps can communicate with each other. Different apps need to use different push certificates, and you need to [apply for an APNs certificate](https://intl.cloud.tencent.com/document/product/1047/34346) for each app and complete [offline push configuration](#configuring push) accordingly.


## Push Notification Sounds
### Setting custom push notification sounds

The IM SDK provides APIs for setting user sounds. You can customize the notification sound for one-to-one chat messages and that for group messages based on your needs. You can also set whether to receive push messages in user levels.

```
/**
 *  APNs configuration
 */
@interface TIMAPNSConfig : NSObject
/**
 *  Whether to enable push. 0: do not set. 1: enable. 2: disable.
 */
@property(nonatomic,assign) uint32_t openPush;
/**
 *  C2C message sound. If it has not been specified, ‘nil’ is passed in.
 */
@property(nonatomic,retain) NSString * c2cSound;
/**
 *  Group message sound. If it is not specified, ‘nil’ is passed in.
 */
@property(nonatomic,retain) NSString * groupSound;
@end
@interface TIMManager : NSObject
/**
 *  Configure APNs settings
 *
 *  @param config APNs configuration
 *  @param succ   Success callback
 *  @param fail   Failure callback
 *
 *  @return 0 Success
 */
-(int) setAPNS:(TIMAPNSConfig*)config succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description**

| Parameter | Description |
| --- | --- |
| config | openPush: whether to enable push. 0: do not set. 1: enable. 2: disable. <br>c2cSound: notification sound for one-to-one chat messages, which needs to be set to a file name (including the suffix) <br>groupSound: notification sound for group messages, which needs to be set to a file name (including the suffix) |
| succ | Success callback |
| fail | Failure callback |

**Directions**
1. Integrate an audio file into the project.
 <img src="//main.qcloudimg.com/raw/c0aca90f7de2f67d815ddfcf13f9fcfc.png" width=480 />
2. After successful login, call the `setToken` API to set the token and busiId information.
3. Call the `setAPNS` API to set audio file information.
 > You only need to set the **file name (including the suffix)** of the audio file.
 >

### Obtaining the notification sound for push messages

If you need to obtain the notification sound for push messages, you can do so through `getAPNSConfig`. This API always synchronizes data from the server and does not cache data locally.

```
@interface TIMManager : NSObject
/**
 *  Obtain APNs configuration
 *
 *  @param succ Success callback, in which case configuration information is returned
 @param fail Failure callback
 *
 *  @return 0 Success
 */
-(int) getAPNSConfig:(TIMAPNSConfigSucc)succ fail:(TIMFail)fail;
@end
```

The parameters are described in the following table:

| Parameter | Description |
| --- | --- |
| succ | Success callback, in which case the TIMAPNSConfig structure is returned |
| fail | Failure callback |

## Customizing Offline Message Attributes

To customize the display content, extension field, notification sound, and push attributes for each message, you can set `TIMOfflinePushInfo` in the message. When the message is sent, original default attributes are replaced, achieving customized push for each message. For example, entering `kIOSOfflinePushNoSound` in the `sound` attribute forcibly mutes the sound on the receiving end.

```
/**
 If the sound field is specified, it indicates that sounds are not played when messages are received.
 */
extern NSString * const kIOSOfflinePushNoSound;
@interface TIMAndroidOfflinePushConfig : NSObject
/**
 *  Offline push display tag
 */
@property(nonatomic,retain) NSString * title;
/**
 *  Sound field information for Android offline push
 */
@property(nonatomic,retain) NSString * sound;
/**
 *  Offline push notification mode
 */
@property(nonatomic,assign) TIMAndroidOfflinePushNotifyMode notifyMode;
@end
@interface TIMIOSOfflinePushConfig : NSObject
/**
 *  Sound field information for offline push
 */
@property(nonatomic,retain) NSString * sound;
/**
 *  Ignore the badge count
 */
@property(nonatomic,assign) BOOL ignoreBadge;
@end
@interface TIMOfflinePushInfo : NSObject
/**
 *  Custom message descriptive information, which is displayed as text during offline push
 */
@property(nonatomic,retain) NSString * desc;
/**
 *  Extension field information for offline push
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
