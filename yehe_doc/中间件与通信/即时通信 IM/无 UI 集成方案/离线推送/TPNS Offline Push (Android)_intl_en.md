- 3. The offline push feature of IM is provided by [Tencent Push Notification Service (TPNS)](https://intl.cloud.tencent.com/document/product/1024/32592). This document introduces how to integrate TPNS and run through the offline push feature.

     >!
     >
     >- Before integrating TPNS, you need to upgrade your IM SDK to [v6.0.1975 or later](https://intl.cloud.tencent.com/document/product/1047/33996).
     
     ## Integrating TPNS and Run Through the Offline Push Feature
     
     [](id:step1)
     ### Step 1. Register your app with vendor push platforms
     
     The offline push feature depends on vendors' original channels. You need to register your app with each vendor's push platform to obtain parameters such as AppID and AppKey. Currently, mobile phone vendors supported inside the Chinese mainland are [Mi](https://dev.mi.com/console/doc/detail?pId=68), [Huawei](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/service-introduction-0000001050040060), [OPPO](https://open.oppomobile.com/wiki/doc#id=10195), [vivo](https://dev.vivo.com.cn/documentCenter/doc/281), and [Meizu](http://open-wiki.flyme.cn/doc-wiki/index#id?129), and the mobile phone vendor supported outside the Chinese mainland is [Google FCM](https://console.firebase.google.com/u/0/?hl=zh-cn).
     
     [](id:step2)
     ### Step 2. TPNS console configuration 
     If you haven't configured offline push information in the IM console, log in to the [TPNS console](https://console.cloud.tencent.com/tpns/product) and configure offline push information as follows:
     1. Create a product: go to the TPNS console, choose **Product Management**, click **Create Product**, and enter product information such as the product name and description.
     ![](https://qcloudimg.tencent-cloud.cn/raw/555f2583fc28cc7b6b304f41494f48bc.png)
     2. In the **Basic Configuration** area, select the added product and enter the package name of the app configured.
     ![](https://qcloudimg.tencent-cloud.cn/raw/d1f1e800449e766c94583cba05c355d8.png)
     3. After the product is successfully created, you can obtain the product's TPNS parameters such as AccessID and AccessKey.
     ![](https://qcloudimg.tencent-cloud.cn/raw/3848bbe752e5c18be4a7f4c950169959.png)
     4. Set vendor push parameters: go to the TPNS console, select a product, choose **Basic Config**, and select and enable a vendor channel. Then set the product information according to the product information obtained in step 1, including the AppID, AppKey, and AppSecret.
     ![](https://qcloudimg.tencent-cloud.cn/raw/4f6bbfa988b5e7bcb4dff4e5282a736b.png)
     5. Third-party service authorization: go to the **Third-Party Service Authorization** page to authorize the offline push feature of the IM app to TPNS.
         1. Select **Cloud IM App Authorization** and click **Add Authorization**.
         ![](https://qcloudimg.tencent-cloud.cn/raw/ca16238809104e98c512457b8de00fd5.png)
         2. Select the IM app for authorization, select the newly created TPNS product app, and submit the authorization.
         ![](https://qcloudimg.tencent-cloud.cn/raw/dbd9bea878d12e4fc1db8d4909e1dc5b.png)
     
     >? If you have already configured offline push information in the IM console, the system will automatically migrate the information to the [TPNS console](https://console.cloud.tencent.com/tpns/product), and you can log in to the [TPNS console](https://console.cloud.tencent.com/tpns/product) to modify the information. IM will continue to use the configured information to perform offline push.
     
     [](id:step3)
     
     ### Step 3. TPNS project configuration
     On the **Configuration Management** page, click **Quick Integration**.
     1. As instructed in step 1 in **Quick Integration**, download the `tpns-configs.json` file and add it to your Android Studio project.
     ![](https://qcloudimg.tencent-cloud.cn/raw/234299da1705138b1fa2c4548eeff350.png)
     2. As instructed in step 2 in **Quick Integration**, add the project configuration and modify the project-level and app-level `build.gradle` configuration.
     ![](https://qcloudimg.tencent-cloud.cn/raw/938bfc1286f7b0e8f40eb7486c60b06b.png)
     
     [](id:step4)
     ### Step 4. Set offline push redirection parameters
     If a message pushed offline is received, the message will be displayed in the notification bar as shown in the figure below, and you can click the notification bar to open the app and go to the redirected-to page configured. Follow the steps below to configure the activities to be redirected to upon notification message clicking.
     1. Log in to the TPNS console and set redirection parameters in the format of `protocol://hostname/path/`.
      ![](https://qcloudimg.tencent-cloud.cn/raw/8c76f34388cb4024a7c61200158fb32a.png)
     2. In [AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/AndroidManifest.xml), set offline push redirection parameters.
     >! These redirection parameters must be consistent with those in the TPNS console.
     >
     ```
     <activity
         android:name="Complete class name of the page to which your app is to be redirected"
         android:launchMode="singleTask"
         android:screenOrientation="portrait"
         android:windowSoftInputMode="adjustResize|stateHidden">
     
             <intent-filter>
                 <action android:name="android.intent.action.VIEW" />
                     <category android:name="android.intent.category.DEFAULT" />
                     <!-- The scheme protocol can be customized by developers. Format: protocol://hostname/path/-->
                     <data
                         android:host="Your hostname"
                         android:path="Your path"
                         android:scheme="Your protocol, i.e., the scheme that you defined" />
             </intent-filter>
     
     </activity>
     ```
     
     
     [](id:step5)
     ### Step 5. Configure TPNS push rules
     
     In [AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/AndroidManifest.xml), set TPNS push rules, such as the TPNS service access point and TPNS push class.
     
     ```
     <!-- Step 1: configure the TPNS service access point, which is the service access point selected during product creation in the TPNS console (step 2). To access Google FCM to support customers outside the Chinese mainland, select Singapore or Hong Kong (China) as the service access point; to support customers inside the Chinese mainland only, use the default service access point Guangzhou:
     
             Shanghai: tpns.sh.tencent.com
             Singapore: tpns.sgp.tencent.com
             Hong Kong (China): tpns.hk.tencent.com
     
     <!-- Configuration format -->
     <meta-data
            android:name="XG_SERVER_SUFFIX"
            android:value="Domain names of other service access points" />
     
     <!-- Step 2: configure the TPNS receiver, which is used in offline push to receive messages and result feedback, such as in-app messages and registration token callback -->
     <receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.TPNSPush.TPNSMessageReceiver">
         <intent-filter>
             <!-- Receive in-app messages -->
             <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
             <!-- Listen for results of registration, unregistration, tag setting/deletion, and notification clicks -->
             <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
         </intent-filter>
     </receiver>
     
     <!-- Step 3: To enable TPNS to be compatible with Android P, you need to add and use the Apache HTTP client library. To do this, add the following configuration to the `application` node in the `AndroidManifest` file.-->
     <uses-library android:name="org.apache.http.legacy" android:required="false"/>
     ```
     
     [](id:step6)
     ### Step 6. Integrate the TPNS SDK
     Follow the steps below to integrate the TPNS SDK. For sample code, see the code of the init() method in [TPNSPushSetting](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/TPNSPush/TPNSPushSetting.java).
     
     1. In the [gradle](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/build.gradle) file, add the push SDKs of various vendors and the AccessID and AccessKey obtained after successful product creation in step 2.
     ```
     android {
         ......
         defaultConfig {
             ......
     
             manifestPlaceholders = [
                 // Enter the AccessID and AccessKey obtained in step 2.
                 XG_ACCESS_ID : "accessid of the registered app",
                 XG_ACCESS_KEY : "accesskey of the registered app",
             ]
             ......
         }
         ......
     }
     
     dependencies {
         ......
         // Main package
         implementation 'com.tencent.tpns:tpns:1.3.1.1-release'
         // Mi
         implementation "com.tencent.tpns:xiaomi:1.3.1.1-release"
         // Meizu
         implementation "com.tencent.tpns:meizu:1.3.1.1-release"
         // OPPO
         implementation "com.tencent.tpns:oppo:1.3.1.1-release"
         // vivo
         implementation "com.tencent.tpns:vivo:1.3.1.1-release"
         // Huawei
         implementation 'com.tencent.tpns:huawei:1.3.1.1-release'
         implementation 'com.huawei.hms:push:5.0.2.300'
     }
     ```
     2. After the app starts, register the TPNS service and record the token obtained after successful registration.
     ```
     final Context context = DemoApplication.instance();
     
     XGPushConfig.enableDebug(context, true);
     // Use OPPO as an example
     XGPushConfig.setOppoPushAppId(context, PrivateConstants.OPPO_PUSH_APPKEY);
     XGPushConfig.setOppoPushAppKey(context, PrivateConstants.OPPO_PUSH_APPSECRET);
     // Important: enable vendor channel registration
     XGPushConfig.enableOtherPush(context, true);
     // Register the TPNS push service
     XGPushManager.registerPush(context, new XGIOperateCallback() {
             @Override
             public void onSuccess(Object o, int i) {
                 DemoLog.w(TAG, "tpush register success token: " + o);
                 // This token needs to be recorded for subsequent operations.
                 String token = (String) o;
             }
     
             @Override
             public void onFail(Object o, int i, String s) {
                 DemoLog.w(TAG, "tpush register failed errCode: " + i + ", errMsg: " + s);
             }
     });
     ```
     - After successful IM login, call the [setOfflinePushConfig](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) API of the IM SDK to report the TPNS token.
     >! To build the V2TIMOfflinePushConfig class, you need to set `businessID` to `0` and `isTPNSToken` to `true`, and report the token obtained after successful TPNS registration.
     >
     ```
     V2TIMOfflinePushConfig v2TIMOfflinePushConfig = null;
     // Set `businessID` to `0` and `isTPNSToken` to `true`, and report the token obtained after successful TPNS registration in step 2.  
     v2TIMOfflinePushConfig = new V2TIMOfflinePushConfig(0, token, true);
     V2TIMManager.getOfflinePushManager().setOfflinePushConfig(v2TIMOfflinePushConfig, new V2TIMCallback() {
             @Override
             public void onError(int code, String desc) {
                 DemoLog.d(TAG, "setOfflinePushToken err code = " + code);
             }
     
             @Override
             public void onSuccess() {
                 DemoLog.d(TAG, "setOfflinePushToken success");
             }
     });
     ```
     3. In the TPNS push class [TPNSMessageReceiver](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/TPNSPush/TPNSMessageReceiver.java), if a TPNS token change is detected, you need to report the TPNS token again.
     
     ```
     /**
      *  Registration callback
      * @param context
      * @param errorCode //0 indicates success, while other values are error codes
      */
     @Override
     public void onRegisterResult(Context context, int errorCode, XGPushRegisterResult message) {
       if (context == null || message == null) {
         return;
       }
       String text = "";
       if (errorCode == XGPushBaseReceiver.SUCCESS) {
         String token = message.getToken();
         text = "Registration succeeded. Token:" + token;
         // Call the `setOfflinePushConfig` API of the IM SDK to report the TPNS token.
         ...
       } else {
         text = message + "Registration failed. Error code:" + errorCode;
       }
     }
     
     ```
     - After successfully reporting the TPNS token, bind the IM login account and TPNS to start receiving messages pushed offline.
     ``` 
     public void bindUserID(String userId) {
         // Important: When you log in to IM, you can call the TPNS account binding API to bind your IM account with the device token so that you can use the account to receive messages pushed offline by TPNS.
         XGPushManager.AccountInfo accountInfo = new XGPushManager.AccountInfo(
                 XGPushManager.AccountType.UNKNOWN.getValue(), userId);
         XGPushManager.upsertAccounts(DemoApplication.instance(), Arrays.asList(accountInfo), new XGIOperateCallback() {
             @Override
             public void onSuccess(Object o, int i) {
                 DemoLog.w(TAG, "upsertAccounts success");
             }
     
             @Override
             public void onFail(Object o, int i, String s) {
                 DemoLog.w(TAG, "upsertAccounts failed");
             }
         });
     }
     ```
     - Before you log out of IM, you need to unbind your account from TPNS to stop receiving messages pushed offline.
     ```
     public void unBindUserID(String userId) {
             // Unbind the TPNS token from your account
             XGIOperateCallback xgiOperateCallback = new XGIOperateCallback() {
                 @Override
                 public void onSuccess(Object data, int flag) {
                     DemoLog.i(TAG, "onSuccess, data:" + data + ", flag:" + flag);
                 }
                 @Override
                 public void onFail(Object data, int errCode, String msg) {
                     DemoLog.w(TAG, "onFail, data:" + data + ", code:" + errCode + ", msg:" + msg);
                 }
             };
     
             //XGPushManager.delAccount(context, UserInfo.getInstance().getUserId(), xgiOperateCallback);
             Set<Integer> accountTypeSet = new HashSet<>();
             accountTypeSet.add(XGPushManager.AccountType.CUSTOM.getValue());
             accountTypeSet.add(XGPushManager.AccountType.IMEI.getValue());
             XGPushManager.delAccounts(DemoApplication.instance(), accountTypeSet, xgiOperateCallback);
     } 
     ```
     - If your app is switched to the background, a message newly received needs to be displayed in the phone's notification bar, and you need to call the [doBackground()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a2b191294ac4d68a2d69e482eae1b638f) API of the IM SDK to sync the app status to the IM background. If you app is switched back to the foreground, you need to call the [doForeground()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a4c2ff4eea609da1d0950648905fbf6aa) API of the IM SDK to sync the app status to the IM background. For the scheme for listening on the switching between the app foreground and background, you are advised to refer to the logic related to the StatisticActivityLifecycleCallback class in [DemoApplication](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/DemoApplication.java).
     ```
     // When the app is switched to the background
     V2TIMManager.getOfflinePushManager().doBackground(totalCount, new V2TIMCallback() {
         @Override
         public void onError(int code, String desc) {
             DemoLog.e(TAG, "doBackground err = " + code + ", desc = " + desc);
         }
     
         @Override
         public void onSuccess() {
             DemoLog.i(TAG, "doBackground success");
         }
     });
     // When the app is switched to the foreground
     V2TIMManager.getOfflinePushManager().doForeground(new V2TIMCallback() {
         @Override
         public void onError(int code, String desc) {
             DemoLog.e(TAG, "doForeground err = " + code + ", desc = " + desc);
         }
     
         @Override
         public void onSuccess() {
             DemoLog.i(TAG, "doForeground success");
         }
     });
     ```
     - After the preceding configuration is completed, you can go to the [Task List](https://console.cloud.tencent.com/tpns/push) page in the TPNS console to test offline message push to verify the integration.
     ![](https://qcloudimg.tencent-cloud.cn/raw/13cda362b6ce2f41a3e3c0629b5c5d53.png)
     
     [](id:step7)
     ### Step 7. Set offline push parameters when sending messages
     
     When you call [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) to send messages, you can use V2TIMOfflinePushInfo to set offline push parameters. For more information, see the sendMessage() method in [ChatProvider](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/model/ChatProvider.java):
     
     ```
     OfflineMessageContainerBean containerBean = new OfflineMessageContainerBean();
     OfflineMessageBean entity = new OfflineMessageBean();
     entity.content = message.getExtra().toString();
     entity.sender = message.getFromUser();
     entity.nickname = chatInfo.getChatName();
     entity.faceUrl = TUIChatConfigs.getConfigs().getGeneralConfig().getUserFaceUrl();
     containerBean.entity = entity;
             
     V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
     v2TIMOfflinePushInfo.setExt(new Gson().toJson(containerBean).getBytes());
     // For OPPO, you must set the `ChannelID` to receive push messages. The `ChannelID` must be consistent with that in the console.
     v2TIMOfflinePushInfo.setAndroidOPPOChannelID("tuikit");
     
     final V2TIMMessage v2TIMMessage = message.getTimMessage();
     String msgID = V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, isGroup ? null : userID, isGroup ? groupID : null,
         V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
             @Override
             public void onProgress(int progress) {
     
             }
     
             @Override
             public void onError(int code, String desc) {
                 TUIChatUtils.callbackOnError(callBack, TAG, code, desc);
             }
     
             @Override
             public void onSuccess(V2TIMMessage v2TIMMessage) {
                 TUIChatLog.v(TAG, "sendMessage onSuccess:" + v2TIMMessage.getMsgID());
                 message.setMsgTime(v2TIMMessage.getTimestamp());
                 TUIChatUtils.callbackOnSuccess(callBack, message);
             }
         });
     ```
     
     [](id:step8)
     ### Step 8. Parse offline push messages
     
     When your phone receives a message pushed offline, the message will be displayed in the system notification bar. When you click the message in the notification bar, the system automatically redirects to the page configured in step 4. On the page, you can call `getIntent().getData()` to get the offline push parameters configured in [step 7](#step7). For sample code, see the code of the [handleOfflinePush()](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/main/MainActivity.java) method of the TUIKit demo.
     
     
     ```
     private void handleOfflinePush() {
         // Determine whether to log in to IM again based on the login status.
         // 1. If the login state is V2TIMManager.V2TIM_STATUS_LOGOUT, redirect to the login page and log in to IM again.
         if (V2TIMManager.getInstance().getLoginStatus() == V2TIMManager.V2TIM_STATUS_LOGOUT) {
             Intent intent = new Intent(MainActivity.this, SplashActivity.class);
             if (getIntent() != null) {
                 intent.setData(getIntent().getData());
             }
             startActivity(intent);
             finish();
             return;
         }
      
         // 2. If the login state is not V2TIMManager.V2TIM_STATUS_LOGOUT, the app runs in the background, and the offline push parameters can be parsed directly.
         final OfflineMessageBean bean = OfflineMessageDispatcher.parseOfflineMessage(getIntent());
         if (bean != null) {
             setIntent(null);
             NotificationManager manager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
             if (manager != null) {
                 manager.cancelAll();
             }
     
             if (bean.action == OfflineMessageBean.REDIRECT_ACTION_CHAT) {
                 if (TextUtils.isEmpty(bean.sender)) {
                     return;
                 }
                 TUIKit.startChat(bean.sender, bean.nickname, bean.chatType);
             } else if (bean.action == OfflineMessageBean.REDIRECT_ACTION_CALL) {
                 IBaseLiveListener baseCallListener = TUIKitLiveListenerManager.getInstance().getBaseCallListener();
                 if (baseCallListener != null) {
                     baseCallListener.handleOfflinePushCall(bean);
                 }
             }
         }
     }
         
     ```
     
     
     ## FAQs
     ### How to set a custom sound for push notifications on Android phones?
     Currently, most vendors do not support setting a custom sound for push notifications, therefore it is not supported by the IM SDK.
     
     ### Why do OPPO mobile phones fail to receive offline push messages?
     This generally occurs for the following reasons:
     
     - According to requirements on the official website of OPPO Push, ChannelID must be configured on OPPO mobile phones that run Android 8.0 or later versions. Otherwise, push messages cannot be displayed. For the configuration method, see [OPPO Push configuration](https://intl.cloud.tencent.com/document/product/1047/39156#oppo-.E6.8E.A8.E9.80.81).
     - The [custom content in the message for pass-through offline push](https://intl.cloud.tencent.com/document/product/1047/39156#.E9.80.8F.E4.BC.A0.E8.87.AA.E5.AE.9A.E4.B9.89.E5.86.85.E5.AE.B93) is not in the JSON format. As a result, OPPO mobile phones do not receive the push message.
     
     ### Why doesn't offline push work for custom messages?
     
     The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the [desc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe), and the `desc` information will be displayed by default during push.
     
     ### Why can't I receive offline push messages?
     After you complete the process according to the instructions in this document, the offline push feature should work properly. Otherwise, troubleshoot as follows:
     - Test whether messages can be pushed offline properly by using the [offline test tool](https://console.cloud.tencent.com/im-detail/tool-push-check) in the IM console or creating a push test on the [Task List](https://console.cloud.tencent.com/tpns/push) page in the TPNS console.
     If offline push does not work properly, and the device status is exceptional, check the parameters in the IM console and then check the code initialization and registration logic, including the vendor push service registration and IM offline push configuration.
     If offline push does not work properly but the device status is normal, check whether the channel ID is entered correctly or whether the backend service is working properly.
     
     - Offline push depends on the capabilities of vendors. Some simple characters may be filtered by vendors and cannot be passed through for push. In addition, some vendors classify notifications and apply different push strategies to different notification types, which may lead to delayed or no push. In that case, you need to apply for the rights and interests of the notification types desired for your app on the vendor's official website to achieve effective and real-time push.
     
     ### Why did page redirection fail?
     Page redirection is implemented as follows: The backend delivers the redirection modes and page parameters that you configure for various vendors in the console to vendor servers based on vendor API rules. When you click the notification bar of offline push messages, the system opens and redirects to the corresponding page. Opening of the corresponding page also depends on the manifest file. Only when the configuration in the manifest file is consistent with that in the console, the corresponding page can be opened and redirected properly.
     
     Therefore, if page redirection fails, you need to check whether the configuration in the console and that in the manifest file are correct and consistent with each other. For more information, see the configuration of the TUIKit demo. Note that some vendors provide different API modes.
