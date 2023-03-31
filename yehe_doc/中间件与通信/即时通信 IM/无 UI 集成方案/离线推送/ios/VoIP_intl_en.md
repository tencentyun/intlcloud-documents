- ## Overview

  Voice over IP (VoIP) Push is a notification mechanism powered by Apple to respond to VoIP calls. Combined with `PushKit.framework` and `CallKit.framework` provided by Apple, it can implement the system-level call effect. Currently, the VoIP Push service provided by IM only supports offline push notifications.

  <table style="text-align:center;vertical-align:middle;width:1000px">
    <tr>
      <th style="text-align:center;" width="200px">VoIP calls<br></th>
      <th style="text-align:center;" width="200px">Recent calls<br></th>
    </tr>
    <tr>
      <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/1.jpeg?1"  />    </td>
      <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/2.jpeg?1"  />     </td>
  	 </tr>
  </table>
  
  
  
  > ? 
  >
  > - As required by Apple, for iOS 13.0 and later, VoIP Push must be used together with `CallKit.framework`; otherwise, a crash will occur after app running.
  > - VoIP Push cannot directly use the push certificate for APNs. You need to separately [Generate a VoIP Push  certificate](#apply_ceritificate) on Apple Developer.
  > - VoIP Push cannot directly use the push token for APNs. You need to separately [Get the VoIP token](#apply_token) from the client code and [Report the token](#upload_token).
  
  
  
  [](id:configuration)
  
  ## Setting up VoIP Push
  
  Follow the steps below to receive VoIP push notifications:
  
  1. Generate a VoIP Push certificate;
  2. Upload the certificate to the IM console;
  3. Get the VoIP token from Apple after each successful login of the app.
  4. Call the `setVOIP` API to report the token to the backend of IM.
  
  
  
  [](id:apply_ceritificate)
  
  ### Step 1. Generate a VoIP Push certificate
  
  Before generating a VoIP Push certificate, log in to [Apple Developer](https://developer.apple.com/account/) to activate the remote push service for your app as instructed [here](https://www.tencentcloud.com/document/product/1047/39157).
  
  After the Push Notifications capability is enabled for your app (AppID), generate a VoIP Push certificate and set it up as instructed below:
  
  1. Log in to [Apple Developer](https://developer.apple.com/account/) and click **Certificates, Identifiers & Profiles** in the right pane or **Certificates, IDs & Profiles** in the left sidebar to enter the **Certificates, IDs & Profiles** page;
  
     <img src="https://qcloudimg.tencent-cloud.cn/raw/5888bba294f17848ab8343d507ee427d.jpg" alt="img" style="zoom:40%;" />
  
  2. Click + on the right of **Certificates**;
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/3.png" style="zoom:40%;" />
  
  3. Select **VoIP Services Certificate** in the **Create a New Certificate** pane and click **Continue**;
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/4.png" style="zoom:50%;" />
  
  4. Select the **BundleID** of your app in the **Select an App ID for your VoIP Service Certificate** pane, and click **Continue**;
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/5.png" style="zoom:35%;" />
  
  5. The system will prompt you that a Certificate Signing Request (CSR) is required;
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/6.png" style="zoom:35%;" />
  
  6. Create a CSR file: Launch **Keychain Access** on Mac, and select **Keychain Access** > **Certificate Assistant** > **Request a Certificate from a Certificate Authority**;
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/12.png" />
  
  7. In the **User Email Address** and **Common Name** fields, enter your email address and your name or company name; Select **Saved to disk** and click **Continue**. Then the system will generate a `*.certSigningRequest` file.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/13.png" />
  
  8. Go back to the Apple Developer page shown in [step 5]() and click **Choose File** to upload the `*.certSigningRequest` file.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/6.png" style="zoom:35%;" />
  
  9. Click **Continue** to generate the certificate, and click **Download** to save the certificate locally.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/7.png" style="zoom:35%;" />
  
  10. Double click the `voip_services.cer` file downloaded. The system will import it to Keychain Access.
  
  11. Launch Keychain Access, select **Login** > **My Certificates**, and right click to export the `.p12` file generated for the created `VoIP Services`.
  
      > ? Set the password when saving the `.p12` file.
  
    ![](https://im.sdk.cloud.tencent.cn/tools/resource/voip/9.png)
  
  
  
  
  [](id:upload_ceritificate)
  
  ## Step 2. Upload the certificate to the IM console
  
  Log in to the [IM console](https://console.cloud.tencent.com/im/detail), select your IM app and upload the certificate as instructed below:
  
  1. Select your IM app, and click **Add Certificate** in the **Offline Push Certificate Configuration** pane;
  
     <img src="https://qcloudimg.tencent-cloud.cn/raw/bf16c9502fb348eef784c781038bcd02.png" style="zoom:35%;" />
  
  2. In the **Add iOS Certificate** window, upload the VoIP certificate for production or development environment;
  
     > ? 
     >
     > - The VoIP Push certificate is not distinguished for the production environment and development environment. The certificate IDs required for the production environment and development environment will be automatically generated after you upload the certificate.
     > - We recommend naming the uploaded certificate in English (special characters such as brackets are not allowed).
     > - You need to set a password for the uploaded certificate. Without a password, push notifications cannot be received.
     > - For an app published on App Store, the environment of the certificate must be the production environment. Otherwise, push notifications cannot be received.
     > - The uploaded .p12 certificate must be your own authentic and valid certificate.
  
     ![](https://qcloudimg.tencent-cloud.cn/raw/c2586fb817abf5aa7edddfe2c1f45b91.png)
  
  3. Record the certificate IDs for environments after upload.
  
     > ? The certificate ID for the development environment and that for the production environment must be strictly distinguished, and entered in [Step 4. Report the token](#upload_token) accordingly.
  
     ![](https://qcloudimg.tencent-cloud.cn/raw/975eb45a0fe6fcee783a2bde693b5d2b.png)
  
     
  
  [](id:apply_token)
  
  ### Step 3. Get the token from Apple
  
  Add the following code in your app to get the VoIP Push token from Apple:
  
  > ? For the purpose of compliance, we recommend getting the VoIP Push token from Apple after the user agrees to the privacy policy.
  
  ``` objective-c
  // Register VoIP Push with Apple
  - (void)registerForVOIPPush
  {
      _voipRegistry = [[PKPushRegistry alloc] initWithQueue:nil];
      _voipRegistry.delegate = self;
      _voipRegistry.desiredPushTypes = [NSSet setWithObject:PKPushTypeVoIP];
  }
  
  // The VoIP token will be returned to you in the delegate method and needs to be reported to the Tencent Cloud backend.
  - (void)pushRegistry:(PKPushRegistry *)registry didUpdatePushCredentials:(PKPushCredentials *)pushCredentials forType:(PKPushType)type
  {
      NSData *token = pushCredentials.token;
      [self reportVOIPToken:token];
  }
  ```
  
  
  
  [](id:upload_token)
  
  ### Step 4. Log in to the IM SDK and report the token
  
  After login to the IM SDK, call the [setVOIP]() API to upload the VoIP Push token stated in [Step 3](#apply_token) to the Tencent Cloud backend as shown below (example code). For more details, see [TUIOfflinePush]().
  
  ```objective-c
  - (void)reportVOIPToken:(NSData *)token
  {
      // Note: `config.certificateID` is the certificate ID generated after the certificate is uploaded to the IM console, and it is different for the development environment and for the production environment.
      NSLog(@"[TUIOfflinePushManager] %s", __func__);
      if (token) {
          V2TIMVOIPConfig *config = [[V2TIMVOIPConfig alloc] init];
          config.token = token;
          config.certificateID = self.voipCertificateID;
          [[V2TIMManager sharedInstance] setVOIP:config succ:^{
              NSLog(@"%s, succ, id:%zd", __func__, config.certificateID);
          } fail:^(int code, NSString *desc) {
              NSLog(@"%s, fail, %d, %@", __func__, code, desc);
          }];
      }
  }
  ```
  
  
  
  ## Initiating VoIP Push
  
  You can mark the message push type as VoIP Push by setting the `iOSPushType` field of the [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) object to `V2TIM_IOS_OFFLINE_PUSH_TYPE_VOIP` when calling the [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) API to send the message.
  
  ```
  NSDictionary *ext = @{
              @"entity": @{
                      @"action": @1,
                      @"content": @"this is voip push",
                      @"sender": @"senderid",
                      @"nickname": @"nickName",
                      @"faceUrl": @"",
                      @"chatType": @(V2TIM_C2C)
              }
          };
  NSData *data = [NSJSONSerialization dataWithJSONObject:ext options:NSJSONWritingPrettyPrinted error:nil];
  
  V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
  pushInfo.ext = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
  pushInfo.iOSPushType = V2TIM_IOS_OFFLINE_PUSH_TYPE_VOIP;// Marked as VoIP Push
  
  [V2TIMManager.sharedInstance sendMessage:message
                                  receiver:# your userID #
                                   groupID:# your groupID #
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:pushInfo
                                  progress:nil
                                      succ:nil
                                      fail:nil
  }];
  ```
  
  
  
  ## FAQs
  
  ### What should I do if no VoIP Push token is obtained or the token request failure is prompted?
  
  Check whether the Push Notifications capability is added to Capability of your project.
  
  <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/10.png" style="zoom:50%;" />
  
  
  
  ### Why cannot VoIP push notifications be received even though the certificate is uploaded and the token reported successfully?
  
  1. First, check whether the certificate type and certificate ID match the running environment of the app. If not, push notifications cannot be received.
  
  2. Check the status of your account: Press the Home key to switch the app to the backend, or log in and kill the process. Currently, VoIP Push supports offline push notifications only.
  
  3. Check whether the Voice over IP option is checked in `Background Modes` of `Capability ` of your project.
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/11.png" style="zoom:50%;" />
  
  
  
  [](id:feedback)
