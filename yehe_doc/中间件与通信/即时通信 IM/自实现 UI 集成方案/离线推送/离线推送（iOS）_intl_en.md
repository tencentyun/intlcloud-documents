[](id: configuring push)

## Configuring Offline Push

To integrate the TPNS push feature, see [TPNS Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/45554). To receive APNs offline message notifications, you need to follow the directions:

1. [Apply for an APNs certificate](#step-1.3A-apply-for-an-apns-certificate).
2. [Upload the certificate to the IM console](#UploadCertificate).
3. The app requests [deviceToken](#DeviceToken) from Apple every time it logs in.
4. Call [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) to report the token to the IM backend.

When the app configured with APNs switches to the background or is killed by the user, the Tencent Cloud backend pushes offline messages to the device through Apple’s APNs. For more information, see [Apple Push Notification Service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).
>!Users who have logged out normally or have been forced offline will not receive any message notifications.

[](id:ApplyForCertificate)

### Step 1: Apply for an APNs certificate

For more information on how to apply for an APNs certificate, see [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).

[](id:UploadCertificate)

### Step 2: Upload the certificate to the console

1. Log in to the [IM console](https://console.cloud.tencent.com/im).
2. Click the target app card to go to its basic configuration page.
3. Click **Add Certificate** on the right side of **iOS Platform Push Settings**.
4. Choose the certificate type, upload an iOS certificate (p.12), set the certificate password, and click **OK**.
>!
>- We recommend that the name of the certificate to be uploaded should be in all English letters (it cannot contain special characters such as brackets).
>- You need to set a password for the uploaded certificate. Without a password, push messages cannot be received.
>- Certificates to be published on App Store need to be set to the Release environment. Otherwise, push cannot be received.
>- The uploaded p12 certificate must be an authentic valid certificate that you have personally applied for.
5. After the push certificate information is generated, record the certificate ID.

[](id:DeviceToken)

### Step 3: The app requests DeviceToken from Apple’s backend

To request DeviceToken from Apple's backend server, add the following code to your app.

```
// Request DeviceToken from the Apple backend
- (void)registNotification
{
    if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0)
    {
        [[UIApplication sharedApplication] registerUserNotificationSettings:
                [UIUserNotificationSettings settingsForTypes:
                (UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge)
                categories:nil]];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    }
    else
    {
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
                (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
    }
}
//The callback of AppDelegate returns deviceToken, which needs to be reported to the Tencent Cloud backend after login.
-(void)application:(UIApplication *)app didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    // Note the deviceToken returned by Apple.
    _deviceToken = deviceToken;
}
```

[](id:uploadDeviceToken)

#### Step 4: Upload the token to Tencent Cloud after IM SDK login

After logging in to the IM SDK, call [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) to upload the DeviceToken obtained in [step 3](#DeviceToken) to the Tencent Cloud backend:

```
V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
// Push certificate ID, generated after the push certificate (p.12) is uploaded to the IM console backend
confg.businessID = businessID;
// The deviceToken requested by Apple’s backend
confg.token = deviceToken;
[[V2TIMManager sharedInstance] setAPNS:confg succ:^{
     NSLog(@"-----> APNS set successfully");;
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> Failed to set APNS");
}];
```

>! `businessID` must be consistent with the certificate ID assigned by the console.

## Push Format 

An example of the push format is as shown below.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ddae975fa432d18e27dd11c8cf23047d.png" width=480 />


### General push rules

For one-to-one messages, the APNs push rules are as follows. Note that the nickname is the sender's nickname. If the nickname is not set, only the content is displayed.
```
Nickname: content
```
For group messages, the APNs push rules are as follows. The priority order for displaying the name is: message sender's `group name card` > `group nickname`. If neither is available, no name is displayed.
```
Name (group name): content
```

### Push rules for different types of messages

The APNs push content consists of the content of each `Elem` in the message body. The display of different `Elem` in offline messages is shown in the following table.

| Parameter | Description |
| ----------- | ------------------------------------------------------------ |
| Text Elem | Directly display the content |
| Audio Elem | Display `[audio]` |
| File Elem | Display `[file]` |
| Image Elem | Display `[image]` |
| Custom Elem | Display the [desc](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html#aca3d09a4807ffc6486d556c055605c41) field set when message is sent. If `desc` is not set, it will not be pushed. |


### Communication among multiple apps

If you set `SDKAppID` to the same value for multiple apps, these apps can communicate with each other. Different apps need to use different push certificates, and you need to [apply for an APNs certificate](https://intl.cloud.tencent.com/document/product/1047/34346) for each app and complete [offline push configuration](#configuring push).

### Customizing the badge number
- By default, when an app goes to the background, the IM SDK sets the current total unread message count of IM as the badge number.
- If you want to customize the badge, follow the steps below:
 1. Use the app to call the `- (void)setAPNSListener:(id<V2TIMAPNSListener>)apnsListener` API to configure listening.
 2. Use the app to implement the `- (uint32_t)onSetAPPUnreadCount` API and return the badge to be customized internally.
- If offline push is enabled in the app, and a new offline push message is received, the badge number of the app will be increased by one based on the benchmark badge number (the total unread message count of the IM by default; if a badge number is customized, the custom badge number prevails).
```
// 1. Configure listening
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Listen for push messages
    [V2TIMManager.sharedInstance setAPNSListener:self];
    // Listen for the unread message counts of conversations
    [[V2TIMManager sharedInstance] setConversationListener:self];
    return YES;
}

// 2. When the unread message count changes, save the new unread message count
- (void)onTotalUnreadMessageCountChanged:(UInt64)totalUnreadCount {
    self.unreadNumber = totalUnreadCount;
}


// 3. The app goes to the background and reports the custom unread message count
/** After the app goes to the background, customize the unread message count of the app. If you do not customize the unread message count, the sum of the unread message counts of all conversations is used as the unread message count of the app.
 *  <pre>
 *
 *   - (uint32_t)onSetAPPUnreadCount {
 *       return 100;  // Custom unread message count
 *   }
 *
 *  </pre>
 */
- (uint32_t)onSetAPPUnreadCount {
    // 1. Get the custom badge number
    uint32_t customBadgeNumber = ...
    
    // 2. Add the unread message count of IM
    customBadgeNumber += self.unreadNumber;
    
    // 3. Use the IM SDK to report to the IM server
    return customBadgeNumber;
}
```

## Setting Custom iOS Push Alert Sound

Set the `iOSSound` field of [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages. `iOSSound` passes the name (with the extension) of the audio file which must be linked to the Xcode project.

## Setting Custom Display for Offline Push

Set the `title` and `desc` fields of [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages. Once set, the `title` content will be added to the default push content and `desc` will be displayed as the push content.

## Setting Custom Click-to-Redirect Logic

Set the `ext` field of [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages. When the user receives offline push and starts the app, the `ext` field can be obtained from the `AppDelegate -> didReceiveRemoteNotification` system callback, and the user is redirected to the UI as specified by `ext`.

The following example assumes that Denny sends a message to Vinson.
- Sender: Denny needs to set `ext` before sending a message.
```
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"Text message"];
V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
info.ext = @"jump to denny";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"vinson" groupID:nil priority:V2TIM_PRIORITY_DEFAULT
onlineUserOnly:NO offlinePushInfo:info progress:^(uint32_t progress) {
} succ:^{
} fail:^(int code, NSString *msg) {
}];
```
- Recipient: Although Vinson's app is not online, it can still receive an APNs offline message notification. When Vinson clicks this notification, the app is started.
```
// Vinson receives the following callback when the app is started.
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo 
fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler {
    // Resolve the extension field `desc`.
    if ([userInfo[@"ext"] isEqualToString:@"jump to denny"]) {
        // Go to the chat window with Denny.
    }
}
```

## FAQs

### Why doesn't offline push work for common messages?

First, verify that the app and the certificate have the same runtime environment. Otherwise, offline pushes will not be received.
Then, verify that the app and the certificate run in the development environment. If that is the case, requesting `deviceToken` from Apple might fail. Please switch to the production environment to solve the problem.

### Why doesn't offline push work for custom messages?

The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the `desc` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56), and the `desc` information will be displayed by default during push.

### How to disable the receiving of offline push messages?

To disable the receiving of offline push messages, set the `config` parameter of the [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) API to `nil`. This feature is supported from v5.6.1200.

