## Process
The following is the process of offline message push:
1. Register with the vendor and complete the developer verification process. Apply to enable the push service.
2. Create a push service and bind app information to obtain the push certificate, password, key, and other data.
3. Log in to the [IM Console](https://console.qcloud.com/avc) to upload the certificate and enter other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Integrate the push messaging SDK provided by the vendor with your project and configure it according to the vendor’s instructions.
5. Send your certificate ID and device information to IM server. 
6. If the user did not log out of IM but the client was terminated by the system or user, the IM server will send push messages as notifications.

## Procedure

vivo mobile phones use a highly customized Android system, with very strict management of the auto-start permissions of third-party apps. By default, third-party apps are not placed in the auto-start allowlist of the system. As apps running in the background are often killed by the system, we recommend that vivo push be integrated on vivo devices. vivo push is a system-grade service for vivo devices, with a high delivery rate. Currently, **IM only supports the notification bar messages of vivo push**.

>!
>- This guide was prepared with direct reference to the official documentation of vivo push. If vivo push is changed, please refer to the [vivo push documentation on the official website](https://dev.vivo.com.cn/documentCenter/doc/180).
>- If you do not plan to implement a vivo-specific offline push solution, skip this section.

[](id:Step1)
### Step 1: Apply for a vivo Push certificate
1. Visit the [vivo open platform official website](https://dev.vivo.com.cn/home) and register for an account. Complete developer verification. 
 >? The verification process takes about 3 days. Be sure to read the [vivo push service description](https://dev.vivo.com.cn/documentCenter/doc/180) beforehand to facilitate access to the service.
2. Log in to the console of the vivo open platform, choose **Message Push** -> **Create** -> **Test Push**, and create a vivo push service app.
 Once the app is created, you can view detailed app information under **App details**.
[](id:Step1_3)
3. Record the following: **`APP ID`**, **`APP key`**, and **`APP secret`**.

[](id:Step2)
### Step 2: Generate a Certificate ID
1. Log in to the [IM Console](https://console.qcloud.com/avc) and click the desired app. The app configuration page appears.
2. Click **Add a certificate** under **Android push configuration**.
 >? If you already have a certificate and only want to change its information, you can click **Edit** in the corresponding certificate area to modify and update the certificate.

 ![](https://main.qcloudimg.com/raw/91a37ef3b610e49b2b80cb3683170d8b.png)
3. Use the information you obtained in [Step 1](#Step1_3) to configure the following parameters:
 - **Push platform**: select **vivo**.
 - **AppKey**: enter the **AppKey** you got from vivo Push.
 - **AppID**: enter the **AppID** you got from vivo Push.
 - **AppSecret**: enter the **APP secret** you got from vivo Push.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, refer to [Configuring Click Event](#click).
    **Open app** or **Open specific app interface** allows [custom content pass through](#section4).
 ![](https://main.qcloudimg.com/raw/32bdacc570cf25e074bb7bc1ca78f90e.png)
4. Click **OK** to save the information. Certificate information takes effect 10 minutes after you save it.
5. Record the Certificate ID once it is generated.
 ![](https://main.qcloudimg.com/raw/0dd67469033b90045402908e14bf935e.png)

[](id:Step3)
### Step 3: Integrate push SDK
>?
>- The default title of IM push notifications is `a new message`.
>- Before reading this section, make sure that you have integrated and tested the IM SDK.
>- You can find a sample for implementation of vivo push in our demo. Note that the features of vivo push may be adjusted during vivo push version updates. If you find any inconsistencies with the content of this section, please refer to the [vivo push documentation on the official website](https://dev.vivo.com.cn/documentCenter/doc/155) and notify us of the difference so that we can make the necessary modifications.

#### Step 3.1: Download the vivo Push SDK and reference it in your project
1. Use [vivo Push platform](https://dev.vivo.com.cn/documentCenter/doc/232) and download the SDK.
2. Decompress the SDK package and find the library file named `vivo_pushsdk_xxx.jar`.
3. Copy `vivo_pushsdk_xxx.jar` to the library folder (`libs`) of your project and add a reference to it in your project.


#### Step 3.2: Modify AndroidManifest.xml

Open AndroidManifest.xml in a text editor and add the following:

```xml
<!-- ********vivo Push configuration start******** -->
<service
         android:name="com.vivo.push.sdk.service.CommandClientService"
         android:exported="true" />
<activity
          android:name="com.vivo.push.sdk.LinkProxyClientActivity"
          android:exported="false"
          android:screenOrientation="portrait"
          android:theme="@android:style/Theme.Translucent.NoTitleBar" />
<meta-data
           android:name="com.vivo.push.api_key"
           android:value="a90685ff-ebad-4df3-a265-3d4bb8e3a389" />
<meta-data
           android:name="com.vivo.push.app_id"
           android:value="11178" />
<!-- ********vivo Push configuration end******** -->
<!--com.vivo.push.app_id and com.vivo.push.api_key are generated by the vivo Push open platform-->
```

#### Step 3.3: Define a BroadcastReceiver class

In order to receive messages, you need to define a BroadcastReceiver class which inherits `OpenClientPushMessageReceiver` and implements the `onReceiveRegId` and `onNotificationMessageClicked` methods. Also, register the BroadcastReceiver in AndroidManifest.xml.

The following is sample code from the demo:

```java
public class VIVOPushMessageReceiverImpl extends OpenClientPushMessageReceiver {
    private static final String TAG = "VIVOPushMessageReceiver";
    @Override
    public void onNotificationMessageClicked(Context context, UPSNotificationMessage upsNotificationMessage) {
        Log.i(TAG, "onNotificationMessageClicked");
    }

    @Override
    public void onReceiveRegId(Context context, String regId) {
        // Use this method as a callback if vivo regId changes. According to official vivo documentation, to obtain regId, you need to call PushClient.getInstance(getApplicationContext()).getRegId() in the enable push callback. Also see LoginActivity.
        Log.i(TAG, "onReceiveRegId = " + regId);
    }
}
```

Register the custom BroadcastReceiver to AndroidManifest.xml:

```xml
<!--Change com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl to the full class name in your app-->
<!-- Deceleration of message receiver-->
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl">
    <intent-filter>
        <!-- Receive push messages -->
        <action android:name="com.vivo.pushclient.action.RECEIVE" />
    </intent-filter>
</receiver>
```

#### Step 3.4: Register vivo Push in your app

To use vivo offline push, you need to register your push service with vivo’s server. To do this, use `PushClient.getInstance(getApplicationContext()).initialize()` to initialize your push service. `PushClient.getInstance(getApplicationContext()).initialize()` can be called anywhere in your code. However, to improve the registration success rate, the vivo official documentation suggests that you call it in your app’s `onCreate`.

After the push service is registered, obtain the results in the main interface of your app. `regId` is the unique identifier of the app on the current device. Record it for later use.

The following is sample code from the demo:

```java
public class DemoApplication extends Application {

    private static PojoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Determines whether this is the main thread
        if (SessionWrapper.isMainProcess(getApplicationContext())) {
            /**
             * Initializes TUIKit
             *
             * @param context  App context, usually corresponds to ApplicationContext
             * @param sdkAppID, the SDKAppID assigned to you when registering the app in Tencent Cloud
             * @param configs, TUIKit configuration options. The default values are suitable in most cases. See the API documentation if you want to customize them.
             */
            long current = System.currentTimeMillis();
            TUIKit.init(this, Constants.SDKAPPID, BaseUIKitConfigs.getDefaultConfigs());
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));
            // Add custom initialization configuration
            customConfig();
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));

            if(IMFunc.isBrandXiaoMi()){
                // Xiaomi offline push
                MiPushClient.registerPush(this, Constants.XM_PUSH_APPID, Constants.XM_PUSH_APPKEY);
            }
            if(IMFunc.isBrandHuawei()){
                // Huawei offline push
                HMSAgent.init(this);
            }
            if(MzSystemUtils.isBrandMeizu(this)){
                // Meizu offline push
                PushManager.register(this, Constants.MZ_PUSH_APPID, Constants.MZ_PUSH_APPKEY);
            }
            if(IMFunc.isBrandVivo()){
                // vivo offline push
                PushClient.getInstance(getApplicationContext()).initialize();
            }
        }
        instance = this;
	}
}
```

Open vivo Push in the main interface

<pre>
if (IMFunc.isBrandVivo()) {
    // vivo offline push
    PushClient.getInstance(getApplicationContext()).turnOnPush(new IPushActionListener() {
        @Override
        public void onStateChanged(int state) {
            if (state == 0) {
                String regId = PushClient.getInstance(getApplicationContext()).getRegId();
                QLog.i(TAG, "vivopush open vivo push success regId = " + regId);
                ThirdPushTokenMgr.getInstance().setThirdPushToken(regId);
                ThirdPushTokenMgr.getInstance().setPushTokenToTIM();
            } else {
                // According to the vivo documentation, state = 101 means this particular vivo device or system version does not support vivo Push. See <a href="https://dev.vivo.com.cn/documentCenter/doc/156">vivo Push FAQ</a> for more information.
                QLog.i(TAG, "vivopush open vivo push fail state = " + state);
            }
        }
    });
</pre>

<span id="Step4"></span>
### Step 4: Report the push information to the IM server
If you need to use vivo push to push IM message notifications, then after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **regId** returned by the vivo push service to the IM server.
>! After the regId and certificate ID are correctly reported, IM service binds users with the corresponding device information. This enables the use of the vivo push service to push notifications.

The following is sample code from the demo:

- Define Certificate ID as a constant:
```java
/**
 * We first define some constant information in Constants.java.
 */
/****** vivo offline push parameters start ******/
// Certificate ID generated after uploading a third-party push certificate in the Tencent Cloud console
public static final long VIVO_PUSH_BUZID = 6666;
// APPID and APPKEY assigned by the vivo open platform
public static final String VIVO_PUSH_APPID = "1234512345123451234"; // See the checklist
public static final String VIVO_PUSH_APPKEY = "12345abcde"; // See the checklist
/****** vivo offline push parameters end ******/
```

- Report Certificate ID and regId:
```java
/**
 * Report Certificate ID and regId to IM in ThirdPushTokenMgr.java
 */
public class ThirdPushTokenMgr {
    private static final String TAG = "ThirdPushTokenMgr";

    private String mThirdPushToken;

    public static ThirdPushTokenMgr getInstance () {
        return ThirdPushTokenHolder.instance;
    }

    private static class ThirdPushTokenHolder {
        private static final ThirdPushTokenMgr instance = new ThirdPushTokenMgr();
    }

    public void setThirdPushToken(String mThirdPushToken) {
        this.mThirdPushToken = mThirdPushToken;  // The regId value is passed here Describe it in accordance with the above-mentioned custom BroadcastReciever class documentation.
    }

    public void setPushTokenToTIM(){
        if(mIsTokenSet){
            QLog.i(TAG, "setPushTokenToTIM mIsTokenSet true, ignore");
            return;
        }
        String token = ThirdPushTokenMgr.getInstance().getThirdPushToken();
        if(TextUtils.isEmpty(token)){
            QLog.i(TAG, "setPushTokenToTIM third token is empty");
            mIsTokenSet = false;
            return;
        }
        if( !mIsLogin ){
            QLog.i(TAG, "setPushTokenToTIM not login, ignore");
            return;
        }
        TIMOfflinePushToken param = null;
        if(IMFunc.isBrandXiaoMi()){     // Select different push services for different vendors.
            param = new TIMOfflinePushToken(Constants.XM_PUSH_BUZID, token);
        }else if(IMFunc.isBrandHuawei()){
            param = new TIMOfflinePushToken(Constants.HW_PUSH_BUZID, token);
        }else if(IMFunc.isBrandMeizu()){
            param = new TIMOfflinePushToken(Constants.MZ_PUSH_BUZID, token);
        }else if(IMFunc.isBrandOppo()){
            param = new TIMOfflinePushToken(Constants.OPPO_PUSH_BUZID, token);
        }else if(IMFunc.isBrandVivo()){
            param = new TIMOfflinePushToken(Constants.VIVO_PUSH_BUZID, token);
        }else{
            return;
        }
        TIMManager.getInstance().setOfflinePushToken(param, new TIMCallBack() {
            @Override
            public void onError(int code, String desc) {
                Log.d(TAG, "setOfflinePushToken err code = " + code);
            }

            @Override
            public void onSuccess() {
                Log.d(TAG, "setOfflinePushToken success");
                mIsTokenSet = true;
            }
        });
    }
}
```

### Step 5: Offline push

After the certificate ID and regId are successfully reported, the IM server sends messages via vivo push notifications to the user when the app has been killed but the user has not logged out of IM.

>?
>- Not all vivo devices support vivo Push. For more information, see [vivo Push FAQ](https://dev.vivo.com.cn/documentCenter/doc/156).
>- vivo push is not 100% successful in reaching the target users.
>- vivo push may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the vivo push service.
>- If the user logs out, or is logged out by IM (such as when the user logs in on another device), the device will no longer receive push messages.

[](id:click)
## Configuring Click Events
You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

### Open app
This is the default event, which opens the app once the notification bar message is clicked.
![](https://main.qcloudimg.com/raw/32bdacc570cf25e074bb7bc1ca78f90e.png)

### Open URL
You need to select **Open URL** in [Step 2](#Step2) and enter a URL that starts with either `http` or `https`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/2bbfac1ddbd47123002844dc6dd768e9.png)

### Open specific app interface

1. Open manifest in a text editor and configure the `intent-filter` of the Activity you want to open as shown:
	```
	<activity
		android:name="com.tencent.qcloud.tim.demo.chat.ChatActivity"
		android:launchMode="singleTask"
		android:screenOrientation="portrait"
		android:windowSoftInputMode="adjustResize|stateHidden">
		   
		<intent-filter>
			<action android:name="android.intent.action.VIEW" />
			<data
				android:host="com.tencent.qcloud.tim"
				android:path="/detail"
				android:scheme="pushscheme" />
		</intent-filter>
		   
	</activity>
	```

2. Obtain the intent URL, as shown below:
    ```
    Intent intent = new Intent(this, ChatActivity.class);
    intent.setData(Uri.parse("pushscheme://com.tencent.qcloud.tim/detail"));
    intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    String intentUri = intent.toUri(Intent.URI_INTENT_SCHEME);
    Log.i(TAG, "intentUri = " + intentUri);
      
    // Print results
    intent://com.tencent.qcloud.tim/detail#Intent;scheme=pushscheme;launchFlags=0x4000000;component=com.tencent.qcloud.tim.tuikit/com.tencent.qcloud.tim.demo.chat.ChatActivity;end
    ```

3. Select **Open specific app interface** in [Step 2](#Step2) and enter the result above.
    ![](https://main.qcloudimg.com/raw/4dcbd70d1ed28881e76e252c49e3675b.png)

[](id:section4)
## Custom Content Pass Through
Select **Open app** or **Open specific app interface** when configuring **Click event** in [Step 2](#Step2) to use custom content pass through.

### Step 1: Custom content configuration (Sender)
Set the custom content for the notification bar message before sending the message.
- Android sample:

  ```
  String extContent = "ext content";
  TIMMessageOfflinePushSettings settings = new TIMMessageOfflinePushSettings();
  settings.setExt(extContent.getBytes());
  timMessage.setOfflinePushSettings(settings);
  mConversation.sendMessage(false, timMessage, callback);
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527).

### Step 2: Custom content configuration (receiver)
Clicking a notification bar message triggers a callback of `onNotificationMessageClicked(Context, UPSNotificationMessage upsNotificationMessage)`, which is part of the vivo Push SDK. The custom content can be obtained from the value of `upsNotificationMessage`.

  ```
  Map<String, String> paramMap = upsNotificationMessage.getParams();
  String extContent = paramMap.get("ext");
  ```

## FAQ

### If the app uses obfuscation, how can I prevent exceptions in the vivo offline push feature?

If your app uses obfuscation, to prevent exceptions in the vivo offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
>? The following code is an official sample from vivo. Please modify it according to your actual situation before use.

```
# Change com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl to the complete class name defined in your app.
# vivo Push
-dontwarn com.vivo.push.**
-keep class com.vivo.push.**{*; }
-keep class com.vivo.vms.**{*; }
-keep class com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl{*;}
```


### Can I set a custom notification sound?

vivo does not support custom notification sounds.

### I cannot receive push messages. What should I do?
1. No push service is 100% successful in reaching target users, and vendor push is no exception. Therefore, if one or two push messages fail to reach users during a fast, continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. Make sure the correct push certificate information from vivo is properly configured in the [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [vivo push SDK integration](#Step3) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported push information](#Step4) to the IM server correctly.
5. Manually kill the app on your device, send a few messages, and confirm whether you receive notifications within one minute.
