## Overview

IM terminal users need to obtain the latest messages at any time. However, considering the limited performance and battery SOC of mobile devices, IM recommends you use the system-grade push channels provided by vendors for message notifications when the app is running in the background to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push channels, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

>!
>- If you want users to receive IM message notifications when, without proactive logout, the app is switched to the background, the mobile phone screen is locked, or the app process is killed by a user, you can enable the IM offline push.
>- If the `logout` API is called to log out proactively or you are forced to log out due to multi-device login, you cannot receive offline push messages even though IM offline push is enabled.

## Running the demo for offline push

The TUIKit demo has integrated the offline push feature as described below. You may see the code links in the documentation.

### Step 1. Register your app with vendor push platforms

The offline push feature depends on vendors' original channels. You need to register your app with each vendor's push platform to obtain parameters such as `AppID` and `AppKey`. Currently, mobile phone vendors supported are [Google FCM](https://firebase.google.com/), [Mi](https://dev.mi.com/console/doc/detail?pId=68), [Huawei](https://developer.huawei.com/consumer/en/hms/huawei-pushkit), [OPPO](https://developers.oppomobile.com/newservice/capability?pagename=push), [vivo](https://dev.vivo.com.cn/documentCenter/doc/281), and Meizu.


### Step 2. Create resources in the IM console

You need to log in to the [IM console](https://console.qcloud.com/avc) to add the push certificates of required vendors, and configure parameters obtained in Step 1 such as `AppId`, `AppKey`, and `AppSecret` to the push certificates in the console. Take Google as an example.

<table> 
   <tr> 
     <th nowrap="nowrap">Vendor Push Platform</th> 
     <th>Configuring in the IM console</th> 
   </tr> 
   <tr> 
     <td><img src="https://qcloudimg.tencent-cloud.cn/raw/c59eb48da0064f27f32052e340276a47.png" style="zoom:150%;" /></td> 
     <td><img src="https://qcloudimg.tencent-cloud.cn/raw/bf75f9007c783bdf855cc4db8daa3295.png" style="zoom:300%;" />
</td> 
   </tr> 
</table>


### Step 3. Configure the redirected-to page for offline push

An offline push message received will be displayed in the notification bar as shown in the figure below. You can click the notification bar to open the app and go to the redirected-to page configured. Follow the steps below to configure the activities to be redirected to upon notification message clicking.

- **Configuring in the console**
The redirected-to page configuration varies by vendor as follows:
<table> 
   <tr> 
     <th nowrap="nowrap">Vendor</th> 
     <th nowrap="nowrap">Action after Click</th> 
     <th>Specified In-app Page</th> 
   </tr> 
   <tr> 
     <td>Mi</td> 
     <td>Open the specified in-app page</td> 
     <td>intent://`your hostname`/`your path`#Intent;scheme=`your protocol, that is, the scheme you defined`;launchFlags=0x4000000;component=`complete class name of the page to which your app is to be redirected`;end<br><br>TUIKit demo configuration: intent://com.tencent.qcloud/detail#Intent;scheme=pushscheme;launchFlags=0x4000000;component=com.tencent.qcloud.tim.tuikit/com.tencent.qcloud.tim.demo.main.MainActivity;end
</td> 
   </tr> 
   <tr> 
     <td>Huawei</td> 
     <td>Open the specified in-app page</td>  <td>intent://`your hostname`/`your path`#Intent;scheme=`your protocol, that is, the scheme you defined`;launchFlags=0x4000000;component=`complete class name of the page to which your app is to be redirected`;end<br><br>TUIKit demo configuration: intent://com.tencent.qcloud/detail#Intent;scheme=pushscheme;launchFlags=0x4000000;component=com.tencent.qcloud.tim.tuikit/com.tencent.qcloud.tim.demo.main.MainActivity;end
</td> 
   </tr> 
   <tr> 
     <td>Meizu</td> 
     <td>Open the specified in-app page</td> 
     <td>Complete class name of the page to which your app is to be redirected<br><br>TUIKit demo configuration: com.tencent.qcloud.tim.demo.main.MainActivity
</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap">OPPO</td> 
     <td>Open the specified in-app page</td> 
     <td>Complete class name of the page to which your app is to be redirected<br><br>TUIKit demo configuration: activity: com.tencent.qcloud.tim.demo.main.MainActivity
</td> 
   </tr>  
   <tr> 
     <td nowrap="nowrap">vivo</td> 
     <td nowrap="nowrap">Open the specified in-app page</td>  <td>intent://`your hostname`/`your path`#Intent;scheme=`your protocol, that is, the scheme you defined`;launchFlags=0x4000000;component=`complete class name of the page to which your app is to be redirected`;end<br><br>TUIKit demo configuration: intent://com.tencent.qcloud/detail#Intent;scheme=pushscheme;launchFlags=0x4000000;component=com.tencent.qcloud.tim.tuikit/com.tencent.qcloud.tim.demo.main.MainActivity;end
</td> 
   </tr>
	 </tr>  
   <tr> 
     <td nowrap="nowrap">Google FCM</td> 
     <td nowrap="nowrap">No need to configure</td>   <td>Redirect to the Launcher page of the app by default
</td> 
   </tr>
</table>

-  **Manifest file configuration**
In [AndroidManifest.xml](https://github.com/TencentCloud/TIMSDK/blob/master/Android/Demo/app/src/main/AndroidManifest.xml), configure the redirected-to page parameters. Please note that this configuration must be consistent with the Action after Click configured in the corresponding certificate in the IM console.
```
<!-- The redirected-to page configured in the TUIKit demo is `MainActivity`, so you need to fill in `com.tencent.qcloud.tim.demo.main.MainActivity` here. After integration with your app, you need to replace the class name with the complete class name of the page to which your app is to be redirected.-->
    <activity
        android:name="complete class name of the page to which your app is to be redirected"
        android:launchMode="singleTask"
        android:screenOrientation="portrait"
        android:windowSoftInputMode="adjustResize|stateHidden">

        <!-- Open the in-app page for offline push -->
        <intent-filter>
            <action android:name="android.intent.a, and configuration for Google FCM: pushscheme://com.tencent.qcloud/detail -->
                <data
                    android:host="your hostname"
                    android:path="your path"
                    android:scheme="your protocol, that is, the scheme you defined" />
        </intent-filter>

    </activity>
```

### Step 4. Set vendor push rules
-  **Applying the offline parameter configuration**
After you successfully add a push certificate as instructed in Step 2, the IM console will assign a certificate ID that needs to be filled in as a configuration parameter in [PrivateConstants](https://github.com/TencentCloud/TIMSDK/blob/master/Android/TUIKit/TUIOfflinePush/tuiofflinepush/src/main/java/com/tencent/qcloud/tim/tuiofflinepush/PrivateConstants.java). This ID will be needed for registering the push service and reporting the token. Take Google as an example.
**Push certificate ID:**
![](https://qcloudimg.tencent-cloud.cn/raw/66a2692812e69bd3b8bae892febc4f43.png)
**Parameters to be filled in:**
```
   public class PrivateConstants {
  // Certificate ID generated after uploading a third-party push certificate in the IM console
    public static final long GOOGLE_FCM_PUSH_BUZID = 15518;
   }
```

-  **Set vendor push rules in the manifest file**
You need to add vendor push rules in the manifest file. See configurations in the [manifest file](https://github.com/TencentCloud/TIMSDK/blob/master/Android/Demo/app/src/main/AndroidManifest.xml) of TUIKit demo for details. Take Google as an example.
```
<!-- Note: The `applicationId` of the TUIKit demo is `com.tencent.qcloud.tim.tuikit`. You need to replace xxxx here with the `applicationId` of your app. -->

<!-- ********Google cloud messaging starts******** -->
<service
    android:name="xxxx.GoogleFCMMsgService"
    android:exported="false">
    <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
</service>
<!-- ********Google cloud messaging ends******** -->
```

-  **Google FCM adaption**
For Huawei and Google FCM, you need to integrate the corresponding plugin and json configuration files by the vendor's methods.

 1. Download the configuration file and place it under the root directory of the project.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cca92fa6817e1941462489691ab76610.png" style="zoom:80%;" />

 2. Add the following configuration under "buildscript -> dependencies" of the project-level `build.gradle` file.
```    
dependencies {
    ...
    classpath 'com.google.gms:google-services:4.2.0'
}
```

 3. Add the following configuration in the app-level `build.gradle` file.
```
apply plugin: 'com.google.gms.google-services'
```
 4. Click **Sync Now** of the project.

### Step 5. Integrate the vendor push SDK

- **Integrating SDK**
In the [gradle](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/build.gradle) file, add the vendor push SDK.
 ```
 dependencies {
    ......
    // Main package
    implementation 'com.tencent.tpns:tpns:1.3.1.1-release'
    // Google FCM
    implementation "com.tencent.tpns:fcm:1.3.1.1-release"
    // Google cloud messaging
    implementation ('com.google.firebase:firebase-messaging:19.0.1')
    // Mi
    implementation "com.tencent.tpns:xiaomi:1.3.1.1-release"
    // Meizu
    implementation "com.tencent.tpns:meizu:1.3.1.1-release"
    // OPPO
    implementation "com.tencent.tpns:oppo:1.3.1.1-release"
    // vivo
    implementation "com.tencent.tpns:vivo:1.3.2.0-release"
    // Huawei
    implementation 'com.tencent.tpns:huawei:1.3.1.1-release'
    implementation 'com.huawei.hms:push:5.0.2.300'
}
 ```

-  **Adding push classes**
Include the vendor push classes. The methods are specific to vendors. See and copy the following files in [TUIOfflinePush code links](https://github.com/TencentCloud/TIMSDK/tree/master/Android/TUIKit/TUIOfflinePush/tuiofflinepush/src/main/java/com/tencent/qcloud/tim/tuiofflinepush/OEMPush):
![](https://qcloudimg.tencent-cloud.cn/raw/e25a0e1de5649df68eed39545b4390af.png)

-  **Registering push services**
To meet compliance requirements, you need to initialize and register the vendor push service after the user agrees to the privacy policy and logs in successfully, store the token (obtained after successful registration) in the registration result callback, and call the [setOfflinePushConfig](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) API to report the push token to the backend. For some vendors, the token can also be returned via API calls after registration. See the following code for details.
```
public void init() {
    ...
        
    if (BrandUtil.isBrandXiaoMi()) {
        // Mi offline push
        MiPushClient.registerPush(this, PrivateConstants.XM_PUSH_APPID, PrivateConstants.XM_PUSH_APPKEY);
    } else if (BrandUtil.isBrandHuawei()) {
        // For Huawei offline push, set whether to receive the call example of the push notification bar message
        HmsMessaging.getInstance(this).turnOnPush().addOnCompleteListener(new com.huawei.hmf.tasks.OnCompleteListener<Void>() {
            @Override
            public void onComplete(com.huawei.hmf.tasks.Task<Void> task) {
                if (task.isSuccessful()) {
                    DemoLog.i(TAG, "huawei turnOnPush Complete");
                } else {
                    DemoLog.e(TAG, "huawei turnOnPush failed: ret=" + task.getException().getMessage());
                }
            }
        });
						
        new Thread(){
            @Override
            public void run() {
                try{
                    // read from agconnect-services.json
                    String appId = AGConnectServicesConfig.fromContext(MainActivity.this).getString("client/app_id");
                    String token = HmsInstanceId.getInstance(MainActivity.this).getToken(appId, "HCM");
                    DemoLog.i(TAG, "huawei get token:" + token);
                    if(!TextUtils.isEmpty(token)) {
                        // Call the `setOfflinePushConfig` API of the IM SDK to report this token
                        String token = (String) o;
                    }
                } catch (ApiException e) {
                    DemoLog.e(TAG, "huawei get token failed, " + e);
                }
            }
        }.start();
    } else if (MzSystemUtils.isBrandMeizu(this)) {
        // Meizu offline push
        PushManager.register(this, PrivateConstants.MZ_PUSH_APPID, PrivateConstants.MZ_PUSH_APPKEY);
    } else if (BrandUtil.isBrandVivo()) {
        // vivo offline push
        PushClient.getInstance(getApplicationContext()).initialize();
						
        DemoLog.i(TAG, "vivo support push: " + PushClient.getInstance(getApplicationContext()).isSupport());
        PushClient.getInstance(getApplicationContext()).turnOnPush(new IPushActionListener() {
            @Override
            public void onStateChanged(int state) {
                if (state == 0) {
                    String regId = PushClient.getInstance(getApplicationContext()).getRegId();
                    DemoLog.i(TAG, "vivopush open vivo push success regId = " + regId);
                       
					// // Call the `setOfflinePushConfig` API of the IM SDK to report this token
					String token = (String) o;
                } else {
                    // According to the vivo documentation, state = 101 means this particular vivo device or system version does not support vivo Push. See https://dev.vivo.com.cn/documentCenter/doc/156 for details.
                    DemoLog.i(TAG, "vivopush open vivo push fail state = " + state);
                }
            }
        });
    } else if (HeytapPushManager.isSupportPush()) {
        // OPPO offline push
        OPPOPushImpl oppo = new OPPOPushImpl();
        oppo.createNotificationChannel(this);
        // According to the OPPO documentation, the app must call the init(...) API before proceeding to subsequent operations.
        HeytapPushManager.init(this, false);
        HeytapPushManager.register(this, PrivateConstants.OPPO_PUSH_APPKEY, PrivateConstants.OPPO_PUSH_APPSECRET, oppo);
    } else if (BrandUtil.isGoogleServiceSupport()) {
        FirebaseInstanceId.getInstance().getInstanceId()
                .addOnCompleteListener(new com.google.android.gms.tasks.OnCompleteListener<InstanceIdResult>() {
                    @Override
                    public void onComplete(Task<InstanceIdResult> task) {
                        if (!task.isSuccessful()) {
                            DemoLog.w(TAG, "getInstanceId failed exception = " + task.getException());
                            return;
                        }

                        // Get new Instance ID token
                        String token = task.getResult().getToken();
                        DemoLog.i(TAG, "google fcm getToken = " + token);
                        
                        // Call the `setOfflinePushConfig` API of the IM SDK to report this token
                        String token = (String) o;
                    }
                });
    }
}
```
Take Google FCM as an example. Store the token (obtained after successful registration) in the registration result callback, and call the [setOfflinePushConfig](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) API to report the token to the backend.
```
public class GoogleFCMMsgService extends FirebaseMessagingService {

    ...

    @Override
    public void onNewToken(String token) {
        DemoLog.i(TAG, "onNewToken token=" + token);
        
        // Call the `setOfflinePushConfig` API of the IM SDK to report this token
        String pushToken = token;
    }

    ...
}
```

- **Reporting the push certificate and token to the backend**
Call the [setOfflinePushConfig](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) API to report the push token. Construct the V2TIMOfflinePushConfig class, where you need to set `businessID` as the certificate ID of the vendor and `isTPNSToken` as `false` and report the token obtained after successful registration of the vendor push service. Note: If you use the offline push service of TPNS, set `isTPNSToken` as `true` and report the token obtained after successful registration of the TPNS push service. Then, TPNS will provide the push service.
```
V2TIMOfflinePushConfig v2TIMOfflinePushConfig = null;
// Set `businessID` as the certificate ID of the vendor and `isTPNSToken` as `false`, and report the token obtained after registration of the vendor push service.  
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

### Step 6. Sync foreground and background status [](id:step6)

 If a message newly received needs to be displayed in the phone's notification bar when your app is switched to the background, call the [doBackground()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a2b191294ac4d68a2d69e482eae1b638f) API of the IM SDK to sync the app status to the IM backend. When your app is switched back to the foreground, call the [doForeground()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a4c2ff4eea609da1d0950648905fbf6aa) API of the IM SDK to sync the app status to the IM backend. For the scheme for listening for the app switching between foreground and background, see relevant logic in the initActivityLifecycle() class of [TUIOfflinePushService](https://github.com/TencentCloud/TIMSDK/blob/master/Android/TUIKit/TUIOfflinePush/tuiofflinepush/src/main/java/com/tencent/qcloud/tim/tuiofflinepush/TUIOfflinePushService.java).

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
// When the app is switched back to the foreground
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


### Step 7. Set offline push parameters when sending messages

When you call [sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) to send messages, you can use V2TIMOfflinePushInfo to set offline push parameters. For more information, see the sendMessage() method in [ChatProvider](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUIChat/tuichat/src/main/java/com/tencent/qcloud/tuikit/tuichat/model/ChatProvider.java).

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
// For OPPO, you must set the `ChannelID` to receive push messages. The `ChannelID` must be identical with that in the console.
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

### Step 8. Parse offline push messages

When a phone receives an offline push message, the message is displayed in the system notification bar. When you click the message in the notification bar, the system automatically redirects to the page configured in Step 4. On this page, you can call `getIntent().getExtras()` to get the offline push parameters configured in [Step 6](#step6). For sample code, see the [handleOfflinePush()](https://github.com/TencentCloud/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/main/MainActivity.java) method of the TUIKit demo.

```
private void handleOfflinePush() {
    // Determine whether to log in to IM again based on the login status
    // 1. If the login status is V2TIMManager.V2TIM_STATUS_LOGOUT, redirect to the login page and log in to IM again.
    if (V2TIMManager.getInstance().getLoginStatus() == V2TIMManager.V2TIM_STATUS_LOGOUT) {
        Intent intent = new Intent(MainActivity.this, SplashActivity.class);
        if (getIntent() != null) {
            intent.putExtras(getIntent());
        }
        startActivity(intent);
        finish();
        return;
    }
 
    // 2. If the login status is not V2TIMManager.V2TIM_STATUS_LOGOUT, the app runs in the background, and the offline push parameters can be parsed directly.
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
                TUIUtils.startChat(bean.sender, bean.nickname, bean.chatType);
            }
        }
}
		
```

>!
>
>- For Google FCM, clicking the message in the notification bar will redirect to the Launcher page of the app by default. On this page, you can call `getIntent().getExtras()` to get the offline push parameters configured in [Step 6](#step6), and then parse messages and customize the redirection.

Upon completion of the above configurations, when your app is switched to the background or the process is killed, the messages will be pushed offline and displayed in the notification bar. You can click the message in the notification bar to redirect to the specified app page.


## IM - Groups

Join a Tencent Cloud IM group for:

- Reliable technical support
- Product details
- Constant exchange of ideas

Telegram group: [join](https://t.me/tencent_imsdk)

Disacord group: [join](https://discord.com/invite/8EmN2ma25W)


## FAQs

### How could I customize alert tones for offline push？

SDK v6.1.2155 or a later version supports customizing alert tones on devices of Huawei, Mi, FCM and APNS. See the [setAndroidSound()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a3ff923225d5a79802a02c47a07e07fc5) and [setIOSSound()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#acffd09150398b06c3d7eb42baee5aee1) APIs of V2TIMOfflinePushInfo for specific methods.

### How could I troubleshoot if I cannot receive offline push messages?
#### 1. OPPO devices
This generally occurs for the following reasons:
- According to requirements on the official website of OPPO Push, ChannelID must be configured on OPPO mobile phones that run Android 8.0 or later versions. Otherwise, push messages cannot be displayed. For the configuration method, see [OPPO Push configuration](https://intl.cloud.tencent.com/document/product/1047/39156#oppo-.E6.8E.A8.E9.80.81).
- The [custom content in the message for pass-through offline push](https://intl.cloud.tencent.com/document/product/1047/39156#.E9.80.8F.E4.BC.A0.E8.87.AA.E5.AE.9A.E4.B9.89.E5.86.85.E5.AE.B93) is not in the JSON format. As a result, OPPO mobile phones do not receive push messages.
- The notification bar display feature is disabled by default for applications installed on the OPPO device. If this is the case, check the feature button status.

#### 2. Sending custom messages
The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages and determine the push content, custom messages are not pushed offline by default. If you need offline push for custom messages, set the [desc](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) when you call [sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe), and the `desc` information will be displayed by default in the push message.

#### 3. Effect of notification bar settings of the device
The offline push message can be intuitively expressed by the notification bar alert, so, just as other notifications, it is subject to the notification settings of the device. Take a Huawei device as an example.

- "Settings - Notifications - Notifications (Lock Screen) - Hide or Do not Disturb" will affect the display of offline push notifications when the screen is locked.
- "Settings - Notifications - Advanced Settings - Show Notification Icons (Status Bar)" will affect the showing of the offline push notification icon in the status bar.
- "Settings - Notifications - Application Notifications - Allow Notifications" will directly affect the display of offline push notifications.
-  "Settings - Notifications - Application Notifications - Notification Sound" and "Settings -  Notifications - Application Notifications - Notification Mute" will affect the effect of the offline push notification sound.

#### 4. The failure still exists after integration as instructed
- First, test whether messages can be properly pushed offline by using the [offline test tool](https://console.cloud.tencent.com/im/tool-push-check) in the IM console.
If offline push does not work properly, and the device status is exceptional, check the parameters in the IM console and then check the code initialization and registration logic, including the vendor push service registration and IM offline push configuration.
If offline push does not work properly but the device status is normal, check whether the ChannelID is correct or whether the backend service is working properly.
- The offline push feature relies on the vendor's capabilities. Some simple characters may be filtered by the vendor and cannot be passed through and pushed.
- If offline push messages are not pushed timely or cannot be received, you need to check the vendor's push restrictions.

### How could I troubleshoot redirection failure?

Page redirection is implemented as follows: The backend delivers the redirection modes and page parameters that you configure for various vendors in the console to vendor servers based on vendor API rules. When you click the notification bar for offline push messages, the system opens and redirects to the corresponding page. Opening of the corresponding page also depends on the manifest file. Only when the configuration in the manifest file is consistent with that in the console, the corresponding page can be opened and redirected properly.

1. First, you need to check whether the configuration in the console and that in the manifest file are correct and consistent with each other. For more information, see the configuration of the TUIKit demo. Note that the API modes may vary by vendor.
2. If the system redirects to the configuration page, you need to check whether the parsing of offline messages on the configuration page and the page redirection are proper.


### Vendor's push restrictions

1. All vendors in China have adopted message classification mechanisms, and different push policies are assigned for different types of messages. To make the push timely and reliable, you need to set the push message type of your app as the system message or important message with a high priority based on the vendor's rules. In turn, offline push messages are affected by the vendor's push message classification and may vary from your expectations.
2. In addition, some vendors set limits on the daily volumes of app push messages. You can check such limits in the vendor's console.
If offline push messages are not pushed timely or cannot be received, consider the following:
- Huawei: Push messages are classified into service & communication messages and information & marketing messages with different push effects and policies. In addition, message classification is associated with the self-help message classification permission.
  - If there is no self-help message classification permission, the vendor will perform secondary intelligent message classification on push messages.
  - If you have applied for the self-help message classification permission, push messages will be classified based on the custom classification and then pushed.
  For more information, see [Message Classification Criteria](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835).
- vivo: Push messages are classified into system messages and operational messages with different push effects and policies. The system messages are further subject to the vendor's intelligent classification for correction. A message that cannot be intelligently identified as a system message will be automatically corrected as an operational message. If the judgment is incorrect, you can give a feedback by email. In addition, the total number of push messages is subject to a daily limit determined based on the app subscription statistics by the vendor. 
See [vendor description 1](https://dev.vivo.com.cn/documentCenter/doc/359) or [vendor description 2](https://dev.vivo.com.cn/documentCenter/doc/156) for details.
- OPPO: Push messages are classified into private messages and public messages with different push effects and policies. Private messages are those that the user pays certain attention to and wants to receive in time. The private message channel permission needs to be applied for via email. The public message channel is subject to a number limit.
See [vendor description 1](https://open.oppomobile.com/wiki/doc#id=11227) or [vendor description 2](https://open.oppomobile.com/wiki/doc#id=11210) for details.
- Mi: Push messages are classified into important messages and general messages with different push effects and policies. In particular, only instant messages, dynamics reminders of the user's interest events, agenda reminders, order status change, financial reminders, personal status change, resource changes, and device reminders fall into the important message category. The important message channel can be applied for in the vendor's console. General push messages are subject to a number limit.
See [vendor description 1](https://dev.mi.com/console/doc/detail?pId=2422) or [vendor description 2](https://dev.mi.com/console/doc/detail?pId=2086) for details.
- Meizu: Push messages are subject to a number limit.
See [vendor description](http://open.res.flyme.cn/fileserver/upload/file/202201/85079f02ac0841da859c1da0ef351970.pdf) for details.
- FCM: Upstream message push is subject to a frequency limit.
See [vendor description](https://firebase.google.com/docs/cloud-messaging/concept-options?hl=zh-cn#upstream_throttling) for details.
