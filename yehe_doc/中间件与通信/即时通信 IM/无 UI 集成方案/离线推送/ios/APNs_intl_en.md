- ## Overview

  IM terminal users need to obtain the latest messages at any time. However, considering the limited performance and battery SOC of mobile devices, IM recommends you use the system-grade push channels (APNs) provided by Apple for message notifications when the app is running in the background to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push channels, APNs provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

  
  >!
  >- If you want users to receive IM message notifications when, without proactive logout, the app is switched to the background, the mobile phone screen is locked, or the app process is killed by a user, you can enable the IM offline push.
  >- If the `logout` API is called to log out proactively or you are forced to log out due to multi-device login, you cannot receive offline push messages even though IM offline push is enabled.
  
  
  
   [](id:Configuring Offline Push)
  
  ## Configuring Offline Push
  
  If you want to receive APNs offline message notifications, follow these steps:
  
  1. [Apply for APNs certificates](#ApplyForCertificate).
  2. [Upload the certificates to the IM console](#UploadCertificate).
  3. The app requests [deviceToken](#DeviceToken) from Apple every time it logs in.
  4. Call [setAPNS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) to report the token to the IM backend.
  
  
  
  [](id:ApplyForCertificate)
  
  ### Step 1: Apply for APNs certificates
  
  #### Activate the remote push service for your app
  
  1. Log in to the [Apple Developer](https://developer.apple.com/account/) website and click **Certificates, Identifiers & Profiles** in the right pane or **Certificates, IDs & Profiles** in the left sidebar to access the **Certificates, IDs & Profiles** page.
     <img src="https://main.qcloudimg.com/raw/71c3b2db72e1bdcb55c0a68bae15e546.jpg" style="zoom:50%;" />
  
  2. Click **+** on the right of Identifiers.
     <img src="https://main.qcloudimg.com/raw/185cbd57e0a1a206d1e97e9f59c9cec5.jpg" style="zoom:50%;" />
  
  3. You can register an AppID by following the steps below or add the `Push Notification` service to your existing AppID.
  
     > ? Please note that your `Bundle ID` cannot contain the wildcard `*`. Otherwise, you will be unable to use the remote push service.
  
  4. Check **App IDs** and click **Continue**.
     <img src="https://main.qcloudimg.com/raw/1e047d154a30d4dc95e3d9fa52779a37.jpg" style="zoom:50%;" />
  
  5. Select **App** and click **Continue**.
     <img src="https://main.qcloudimg.com/raw/584b1b697c21832d864a75c541da7fde.jpg" style="zoom:50%;" />
  
  6. Configure `Bundle ID` and other information. Click **Continue**.
     <img src="https://qcloudimg.tencent-cloud.cn/raw/bc8105688bc097e5028585f4a1a57088.png" style="zoom:50%;" />
  
  7. Select **Push Notifications** to activate the remote push service.
     <img src="https://main.qcloudimg.com/raw/4720490316ac5180de0742ca1ed50c8f.jpg" style="zoom:50%;" />
  
  #### Generating certificates
  
  1. Select your AppID and click **Configure**.
     <img src="https://main.qcloudimg.com/raw/ef9be51df8bb1c5d56febd10d8deb2a2.jpg" style="zoom:50%;" />
  
  2. In the **Apple Push Notification service SSL Certificates**, you will see two SSL certificates: **Development SSL Certificate** and **Production SSL Certificate**.
     <img src="https://main.qcloudimg.com/raw/bd55cffb96e80b505e70db33c73e27dd.jpg" style="zoom:50%;" />
  
  3. <span id="step3"></span>Click **Create Certificate** under **Development SSL Certificate** to create a certificate. You will be prompted that `Certificate Signing Request (CSR)` is required.
     <img src="https://main.qcloudimg.com/raw/637ce37ec54ca5a4bf3006b527572da5.jpg" style="zoom:50%;" />
  
  4. Open **Keychain Access** on Mac. Select **Keychain Access** > **Certificate Assistant** > **Request a Certificate From a Certificate Authority**.
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/offlinepush/ios/en/cert_assistant_en.png" style="zoom:80%;" />
  
  5. Fill in your email for **User Email Address** and your name or company name for **Common Name**. Select **Saved to disk** and click **Continue**. Then the system will generate a `*.certSigningRequest` file.
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/offlinepush/ios/en/root_cert_apply_en.png" style="zoom:80%;" />
  
  6. Return the `Apple Developer` page shown in [step 3](#step3) and click **Choose File** to upload the `*.certSigningRequest` file.
     <img src="https://main.qcloudimg.com/raw/59dfdb08864d6469199684c50c53b7e6.jpg" style="zoom:50%;" />
  
  7. Click **Continue** to generate the push certificate.
     <img src="https://main.qcloudimg.com/raw/c337d5282ac10f6bec7c5ef5864b94cb.jpg" style="zoom:50%;" />
  
  8. Click **Download** to save the `Development SSL Certificate` locally.
     ![](https://main.qcloudimg.com/raw/9dece7f318c93e97732fe7ea7806f961.jpg)
  
  9. Repeat steps 1-8 to generate and download the production SSL certificate locally.
  
     >? Actually, this certificate is a `Sandbox` and `Production` merged certificate that applies to both the development and production environments.
  
     []()
  
     <img src="https://main.qcloudimg.com/raw/eaa08da45f36435155a4a37938ddc84e.jpg" style="zoom:50%;" />
  
     <img src="https://main.qcloudimg.com/raw/bf80c3a06f74080bf81fd857f15a2b86.jpg" style="zoom:50%;" />
  
     
  
  10. Double-click and open the development SSL certificate and production SSL certificate that have been downloaded to import them to Keychain Access.
  
  11. Open Keychain Access, choose **Login** > **My Certificates**, and right-click to export the P12 files generated for the development environment (`Apple Development IOS Push Service`) and production environment (`Apple Push Services`).
      <img src="https://im.sdk.cloud.tencent.cn/tools/resource/offlinepush/ios/en/push_cert_dev_en.png" style="zoom:80%;" />
  
      > ! Remember to set the password when saving the P12 files.
  
  
  
  [](id:UploadCertificate)
  
  ### Step 2: Upload the certificates to the console
  
  1. Log in to the [IM console](https://console.cloud.tencent.com/im).
  
  2. Click the target app card to go to its basic configuration page.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/offlinepush/ios/en/console_en.png" style="zoom:50%;" />
  
  3. Click **Add Certificate** on the right side of **iOS Native Offline Push**.
  
  4. Choose the certificate type, upload an iOS certificate (p.12), set the certificate password, and click **OK**.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/offlinepush/ios/en/console_upload_en.png" style="zoom:50%;" />
  
     []()
  
  >!
  >- We recommend that the names of the uploaded certificates be in English (special characters such as brackets are not allowed).
  >- You need to set passwords for the uploaded certificates. Without a password, push messages cannot be received.
  >- The environments of the certificates published on App Store must be the production environment. Otherwise, push messages cannot be received.
  >- The uploaded P12 certificates must be authentic valid certificates applied for by yourself.
  >[](id:businessid)
  
  5. After the push certificate information is generated, record the certificate IDs.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/offlinepush/ios/en/console_cert_en.png" style="zoom:50%;" />
  
  [](id:DeviceToken)
  
  ### Step 3: The app requests deviceToken from the Apple backend
  
  To request deviceToken from Apple's backend server, add the following code to your app.
  
  > ? For compliance considerations, we recommend that you request deviceToken from the Apple backend after the user agrees to the Privacy Policy.
  
  ```
  // Request deviceToken from the Apple backend
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
  
  // The callback of AppDelegate returns deviceToken, which needs to be reported to the Tencent Cloud backend after login.
  -(void)application:(UIApplication *)app didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
  {
      // Note the deviceToken returned by Apple.
      _deviceToken = deviceToken;
  }
  ```
  
  [](id:uploadDeviceToken)
  
  #### Step 4: Log in to IM SDK and upload deviceToken to Tencent Cloud
  
  After logging in to the IM SDK, call the [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e) API to upload the deviceToken obtained in [step 3](#DeviceToken) to the Tencent Cloud backend. The following is the sample code. For more information, see [TUIKitDemo](https://github.com/TencentCloud/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+Push.m).
  
  ```
  - (void)push_registerIfLogined:(NSString *)userID
  {
      NSLog(@"[PUSH] %s, %@", __func__, userID);
      BOOL supportTPNS = NO;
      if ([self respondsToSelector:@selector(supportTPNS:)]) {
          supportTPNS = [self supportTPNS:userID];
      }
      
      if (self.deviceToken) {
          V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
          /* Users need to register a developer certificate with Apple, download and generate the certificate (P12 file) in their developer accounts, and upload the generated P12 file to the Tencent certificate console. The console will automatically generate a certificate ID and pass it to the `businessID` parameter.*/
          // Push certificate ID
          confg.businessID = sdkBusiId;
          confg.token = self.deviceToken;
          [[V2TIMManager sharedInstance] setAPNS:confg succ:^{
               NSLog(@"%s, succ, %@", __func__, supportTPNS ? @"TPNS": @"APNS");
          } fail:^(int code, NSString *msg) {
               NSLog(@"%s, fail, %d, %@", __func__, code, msg);
          }];
      }
      // ...
  }
  ```
  
  >! `businessID` must be consistent with the [certificate ID](#businessid) assigned by the console.
  
  ## Push Format 
  
  An example of the push format is as shown below.
  <img src="https://im.sdk.cloud.tencent.cn/tools/resource/tuicalling/ios/offline_push_tuicalling_ios.png" width=480 />
  
  ### General push rules
  
  For one-to-one messages, the APNs push format is as follows. `Nickname` indicates the sender's nickname. If no nickname is specified, only content is displayed.
  ```
  Nickname: Content
  ```
  For group messages, the APNs push format is as follows. The display priority for `Name` is: sender's `Group name card` > `Group nickname`. If neither is available, no name is displayed.
  ```
  Name (group name): Content
  ```
  
  ### Push rules for different types of messages
  
  The APNs push content consists of the content of each `Elem` in the message body. The display of different `Elem` in offline messages is shown in the following table.
  
  | Parameter   | Description                                                  |
  | ----------- | ------------------------------------------------------------ |
  | Text Elem   | Directly display the content                                 |
  | Audio Elem  | Display `[audio]`                                            |
  | File Elem   | Display `[file]`                                             |
  | Image Elem  | Display `[image]`                                            |
  | Custom Elem | Display the [desc](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html#aca3d09a4807ffc6486d556c055605c41) field set when message is sent. If `desc` is not set, it will not be pushed. |
  
  > ? If the default push rules do not meet your requirements, you can customize your own push rule. For more information, see [Setting Custom Display for Offline Push](#customdisplay).
  
  ### Communication among multiple apps
  
  If you want multiple apps to receive push message from each other, you can set `SDKAppID` to the same value for the apps.
  
  > ? Different apps need to use different push certificates, and you need to [apply for APNs certificates](#ApplyForCertificate) for each app and [configure offline push](#Configuring Offline Push).
  
  ## Customizing the Badge Number
  - By default, when an app goes to the background, the IM SDK sets the current total unread message count of IM as the badge number.
  - If you want to customize the badge number, follow the steps below:
   1. Use the app to call the [- (void)setAPNSListener:(id<V2TIMAPNSListener>)apnsListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683) API to configure listening.
   2. Use the app to implement the [- (uint32_t)onSetAPPUnreadCount](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAPNSListener-p.html#a164265ae900e0ddeb6d6393786a548ba) API and return the badge number to be customized internally.
  - If offline push is enabled in the app, and a new offline push message is received, the badge number of the app will be increased by one based on the benchmark badge number (which is the total unread message count of IM by default and is the custom badge number if there is any).
  
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
  
  ## Customizing Push Alert Sounds
  
  ### iOS push alert sound
  
  When calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages, set the `iOSSound` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) to the name of the audio file.
  
  > ? 
  >
  > - Offline push sound setting is valid only for iOS. When `iOSSound` is `kIOSOfflinePushNoSound`, no sound is played when a push message is received. 
  > - When `iOSSound` is `kIOSOfflinePushDefaultSound`, the system alert sound is played when a push message is received. 
  > - To customize `iOSSound`, link the audio file to the Xcode project and set `iOSSound` to the audio filename (with the extension name).
  
  ```
  V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
  pushInfo.title = @"push title";
  pushInfo.iOSSound = @"phone_ringing.mp3"; // Name of your audio file
  [[V2TIMManager sharedInstance] sendMessage:msg receiver:receiver groupID:groupID priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:NO offlinePushInfo:pushInfo progress:nil succ:^{
  
  } fail:^(int code, NSString *msg) {
  
  }];
  ```
  
  ### Android push alert sound
  
  When calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages, set the `AndroidSound` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) to the name of the audio file.
  
  > ? 
  >
  > * For offline push sound setting (valid only for Android and supported by IM SDK 6.1 or later), only Huawei and Google mobile phones support ringtone setting.
  > * To customize `AndroidSound`, you need to place the audio file to the `raw` directory of the Android project and set the audio file name (without the file extension) as the value of `AndroidSound`.
  
  ```
  V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
  pushInfo.title = @"push title";
  pushInfo.AndroidSound = @"phone_ringing"; // your voice file's name
  [[V2TIMManager sharedInstance] sendMessage:msg receiver:receiver groupID:groupID priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:NO offlinePushInfo:pushInfo progress:nil succ:^{
  
  } fail:^(int code, NSString *msg) {
  
  }];
  ```
  
  
  
  
  
  [](id:customdisplay)
  
  ## Customizing the Display for Offline Push
  
  Set the `title` and `desc` fields of [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) when calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages. Once set, the `title` content will be added to the default push content and `desc` will be displayed as the push content.
  
  ```
  V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
  info.title = @"Harvy";                        // Offline push display title
  info.desc = @"You have a call invitation.";   // Offline push display content
  
  // `receiver` and `groupID` cannot empty at the same time, and only one of them can be set.
  [[V2TIMManager sharedInstance] sendMessage:msg receiver:receiver groupID:groupID priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:NO offlinePushInfo:pushInfo progress:nil succ:^{
  
  } fail:^(int code, NSString *msg) {
  
  }];
  ```
  
  <img src="https://qcloudimg.tencent-cloud.cn/raw/ba596982ee5ebaafc575ef1469ff4ff7.png" style="zoom:50%;" />
  
  []()
  
  > ? You can also use the `multable-content` field of APNs and `NSNotification Service Extension` to customize the display content. If you have any questions or feedback, feel free to [contact us](https://intl.cloud.tencent.com/contact-us).
  
  
  
  ## Customizing Click-to-Redirect Logic
  
  When calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages, set the `ext` field in [https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html). When the user receives an offline push message and starts the app, the `ext` field can be obtained from the `AppDelegate -> didReceiveRemoteNotification` system callback, and the user is redirected to the UI as specified by `ext`. For more information, see [TUIKitDemo](https://github.com/TencentCloud/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate%2BPush.m).
  
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
  
  First, verify that the app runtime environment is the same as the certificate environment. Otherwise, offline push messages will not be received.
  Then, verify that the app and the certificate run in the development environment. If that is the case, requesting `deviceToken` from Apple might fail. Please switch to the production environment to solve the problem.
  
  ### Why doesn't offline push work for custom messages?
  
  The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the `desc` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56), and the `desc` information will be displayed by default during push.
  
  ### How do I disable the receiving of offline push messages?
  
  To disable the receiving of offline push messages, set the `config` parameter of the [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) API to `nil`. This feature is supported from v5.6.1200.
  
  ### What should I do if push messages cannot be received and the backend reports the "bad devicetoken" error?
  
  For Apple devices, `deviceToken` is related to the current compilation environment. If the certificate ID used to [upload deviceToken to Tencent Cloud after logging in to IM SDK](#uploadDeviceToken) is inconsistent with the environment token, the error will be reported.
  
  - If the compilation environment is `Release`, `- application:didRegisterForRemoteNotificationsWithDeviceToken:` calls back the release environment token, `businessID` must be set to the [certificate ID](#businessid) of the production environment.
  - If the compilation environment is `Debug`, `- application:didRegisterForRemoteNotificationsWithDeviceToken:` calls back the development environment token, `businessID` must be set to the [certificate ID](#businessid) of the development environment.
  
  ```
  V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
  /* Users need to register a developer certificate with Apple, download and generate the certificate (P12 file) in their developer accounts, and upload the generated P12 file to the Tencent certificate console. The console will automatically generate a certificate ID and pass it to the `businessID` parameter.*/
  // Push certificate ID
  confg.businessID = sdkBusiId;
  confg.token = self.deviceToken;
  [[V2TIMManager sharedInstance] setAPNS:confg succ:^{
       NSLog(@"%s, succ, %@", __func__, supportTPNS ? @"TPNS": @"APNS");
  } fail:^(int code, NSString *msg) {
       NSLog(@"%s, fail, %d, %@", __func__, code, msg);
  }];
  ```
  
  ### What should I do if `deviceToken` is not returned for registration occasionally or APNs' request for token fails in the iOS development environment?
  
  This problem is caused by instability of APNs. You can fix it in the following ways:
  
  1. Insert a SIM card into the phone and use the 4G network.
  2. Uninstall and reinstall the application, restart the application, or shut down and restart the phone.
  3. Use a package for the production environment.
  4. Use another iPhone.
  
  
  
  ## Exchange and feedback
  
  Join a Tencent Cloud IM group for:
  
  * Reliable technical support
  * Product details
  * Constant exchange of ideas
  
  Telegram group: [join](https://t.me/tencent_imsdk)
