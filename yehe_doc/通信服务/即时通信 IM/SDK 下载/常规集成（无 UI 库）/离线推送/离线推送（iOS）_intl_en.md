<span id="configuring offline push"></span>

## Configuring Offline Push

To receive APNs offline message notifications, complete the following steps:

1. [Apply for an APNs certificate](#ApplyForCertificate).
2. [Upload the certificate to the console](#UploadCertificate).
3. Use the app to request a [deviceToken](#DeviceToken) from Apple upon each login.
4. Call [setAPNS](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) to report the token to the IM backend.

When the app configured with APNs switches to the background or is killed by the user, the Tencent Cloud backend pushes offline messages to the device through Apple’s APNs. For more information, see [Apple Push Notification Service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

>!Users who have logged out normally or forcibly will not receive any message notifications.

<span id ="ApplyForCertificate"></span>

### Step 1: Apply for an APNs certificate

For details on how to apply for an APNs certificate, see [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).

<span id ="UploadCertificate"></span>

### Step 2: Upload the certificate to the console

1. Log in to the [IM console](https://console.cloud.tencent.com/im).
2. Click the target application card to go to the basic configuration page of the app.
3. Click **Add Certificate** to the right of **iOS Platform Push Settings**.
4. Select the certificate type, upload an iOS certificate (p.12), set the certificate password, and click **OK**.
 >
 >- We recommend that the name of the certificate to be uploaded is completely in English letters (and must not contain special characters such as brackets).
 >- You need to set a password for the uploaded certificate. Without a password, push messages cannot be received.
 >- Certificates to be published in App Store need to be set to the Release environment. Otherwise, push notifications cannot be received.
 >- The uploaded p12 certificate must be an authentic and valid certificate that you have personally applied for.
5. After the push certificate information is generated, take note of the certificate ID.

<span id ="DeviceToken"></span>

### Step 3: Use the app to request a deviceToken from Apple’s backend

To request a deviceToken from Apple’s backend server, add the following code to your app.

```
// Request a deviceToken from Apple’s backend.
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
//The callback of AppDelegate returns a deviceToken, which needs to be reported to the Tencent Cloud backend after login.
-(void)application:(UIApplication *)app didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    //Take note of the deviceToken returned by Apple.
    _deviceToken = deviceToken;
}
```

<span id ="uploadDeviceToken"></span>

### Step 4: Upload the token to Tencent Cloud after IM SDK login

After logging in to the IM SDK, call [setAPNS](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) to uploaded the deviceToken obtained in [step 3](#DeviceToken) to the Tencent Cloud backend:

```
V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
// Business certificate ID, which is generated after the certificate is uploaded to the IM console
confg.businessID = businessID;
// Requested deviceToken from Apple’s backend
confg.token = deviceToken;
[[V2TIMManager sharedInstance] setAPNS:confg succ:^{
     NSLog(@"-----> Set APNs successfully");;
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> Failed to set APNs");
}];
```

> The businessID must be consistent with the certificate ID assigned by the console.

## Push Format 

The following gives an example of the push format.
<img src="https://main.qcloudimg.com/raw/0602abcefdd6062d8492c720f6886b82.png" width=480 />


### General push rules

For one-to-one chat messages, the APNs push rules are as follows. Note that the nickname is the sender’s nickname. If the nickname is not specified, only the content is displayed.

```
Nickname: content
```

For group chat messages, the APNs push rules are as follows. The priority of displayed names is: the message sender’s `group name card` > `group nickname`. If neither of these two items is available, no name is displayed.

```
Name (group name): content
```

### Push rules for different types of messages

APNs push content consists of the content of each `Elem` in the message body. The display of different `Elem` items in offline messages is described in the following table.

| Parameter | Description |
| ----------- | ------------------------------------------------------------ |
| Text Elem | Directly display the content |
| Audio Elem | Display `[audio]` |
| File Elem | Display `[file]` |
| Image Elem | Display `[image]` |
| Custom Elem | Display the [desc](http://doc.qcloudtrtc.com/im/interfaceV2TIMOfflinePushInfo.html#aca3d09a4807ffc6486d556c055605c41) field set when the message was sent. If `desc` was not specified, the message will not be pushed. |


### Communication among multiple apps

If you set `SDKAppID` to the same value for multiple apps, these apps can communicate with each other. Different apps need to use different push certificates, and you need to [apply for an APNs certificate](https://intl.cloud.tencent.com/document/product/1047/34346) for each app and complete [offline push configuration](#configuring push).


## Setting Custom iOS Push Alert Sounds

Set the `iOSSound` field of [offlinePushInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send messages. `iOSSound` passes the name (with the extension) of the audio file that must be linked to the Xcode project.

## Setting Custom Display for Offline Push

Set the `title` and `desc` fields of [offlinePushInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send messages. Once set, the `title` content will be added to the default push content, and `desc` will be displayed as the push content.

## Setting Custom Click-to-Redirect Logic

Set the `ext` field of [offlinePushInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) to send messages. When the user receives an offline push notification and starts the app, the `ext` field can be obtained from the `AppDelegate -> didReceiveRemoteNotification` system callback, and the user is redirected to the UI as specified by `ext`.

The following example assumes that Denny sends a message to Vinson.

- Sender: Denny needs to set `ext` before sending a message.

```
// Denny sets `offlinePushInfo` and specifies `ext` before sending a message.
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"Text message"];
V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
info.ext = @"jump to denny";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"vinson" groupID:nil priority:V2TIM_PRIORITY_DEFAULT
onlineUserOnly:NO offlinePushInfo:info progress:^(uint32_t progress) {
} succ:^{
} fail:^(int code, NSString *msg) {
}];
```

Recipient: although Vinson's app is not online, it can still receive an APNs offline message notification. When Vinson clicks this notification, the app is started.

```
// Vinson receives the following callback when the app is started.
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo 
fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler {
    // Parse the desc extension field.
    if ([userInfo[@"ext"] isEqualToString:@"jump to denny"]) {
        // Jump to the chat window with Denny.
    }
}
```

## FAQs

### Why does not offline push work for ordinary messages?

First, verify that the app runtime environment is consistent with that of the certificate. Otherwise, offline push notifications cannot be received.
Then, verify that the app and the certificate are in the development environment. If this is the case, the request for `deviceToken` from Apple might fail. To solve this problem, switch to the production environment.

### Why does not offline push work for custom messages?

The offline push feature for custom messages is different from ordinary messages. Since we are not able to resolve the content of custom messages and determine what to push, we simply do not push custom messages by default. If you do need to enable offline push for custom messages, set the `desc` field of [offlinePushInfo](http://doc.qcloudtrtc.com/im/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21). Then, the content of `desc` will be used for display during offline push.

