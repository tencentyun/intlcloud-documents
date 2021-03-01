## Offline Push Process

The process of implementing offline message push is as follows:
1. Register with the vendor and complete the developer verification process. Apply to enable the push service.
2. Create a push service and bind app information to obtain the push certificate, password, key, and other data.
3. Log in to the [IM console](https://console.qcloud.com/avc) to upload the certificate and enter other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Integrate the push messaging SDK provided by the vendor with your project and configure it according to the vendor’s instructions.
5. Send your certificate ID and device information to IM server.
6. When the client app is killed by the system or user without IM logout, the IM server will remind the user via message push.

## Configuring Offline Push
MIUI is a highly customized Android system with very strict auto-start permission management. By default, no third-party apps are in the system’s auto-start allowlist. As a result, background third-party apps are likely to be killed by the system. Therefore, you are advised to integrate Mi Push on Mi devices. Mi Push is a system service of MIUI, which has a high delivery rate for pushes. **IM only supports Mi Push notification bar messages**.
>!
>- This document was written with reference to the official Mi Push documentation. In case of any change, the latest information can be found in the [official Mi Push documentation](https://dev.mi.com/console/doc/detail?pId=230).
>- If you do not plan to implement a Mi device-specific offline push solution, skip this section.

### Step 1. Apply for a Mi Push certificate
1. Visit the [Mi open platform website](https://dev.mi.com/console/), register an account, and complete developer verification.
 >?The verification process takes about two days. Please read the [Mi Push Service Activation Guide](https://dev.mi.com/console/doc/detail?pId=68) in advance to avoid any effect on your connection progress.
2. Log in to the console of the Mi open platform, choose **App Service** -> **Push Service**, and create a Mi Push service app.
 Once the app is created, you can view detailed app information under the app details.
[](id:Step1_3)
3. Record the **`primary package name`**, **`AppID`**, **`AppSecret`** information.


[](id:Step2)
### Step 2. Generate a certificate ID 
1. Log in to the [IM console](https://console.qcloud.com/avc) and click the desired app to go to the configuration page of the app.
2. Click **Add Certificate** under **Android Platform Push Settings**.
 >?If you already have a certificate and only want to change its information, you can click **Edit** in **Android Platform Push Settings** to modify and update the certificate.
 >
 ![](https://main.qcloudimg.com/raw/45179a95132b2a02456af4371323cca1.png)
3. Use the information you obtained in [Step 1](#Step1_3) to configure the following parameters:
 - **Push Platform**: choose **Mi**.
 - **Package name**: enter the **primary package name** of the Mi Push service app.
 - **AppID**: enter the **AppID** of the Mi Push service app.
 - **AppSecret**: enter the **AppSecret** of the Mi Push service app.
 - **Response after Click**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open webpage**, and **Open specified in-app page**. For more information, refer to [Configuring Click Event](#click).
    **Open app** or **Open specified in-app page** allows [custom content pass through](#section4).
 ![](https://main.qcloudimg.com/raw/d2341570851aa707916a9127a47a2171.png)
4. Click **Confirm** to save the information. Certificate information takes effect 10 minutes after you save it.
5. Record the certificate ID once it is generated.
 ![](https://main.qcloudimg.com/raw/e29d1090b8c9d69d18b1341192690383.png)


[](id:Step3)
### Step 3. Integrate the push SDK
>?
> - The default title of IM push notifications is `a new message`.
> - Before reading this section, make sure that you have integrated and tested the IM SDK.
> - You can find a sample for Mi Push implementation in our demo. Note that the features of Mi Push may be adjusted during Mi Push version updates. If you find any inconsistencies with the content of this section, please refer to the [official Mi Push documentation](https://dev.mi.com/console/doc/detail?pId=230) and notify us of the difference so that we can make the necessary modifications in time.

#### Step 3.1. Download the Mi Push SDK and reference it in your project
1. Visit the [Mi Push operations platform](http://dev.xiaomi.com/mipush/downpage/) to download the Mi Push SDK.
2. Decompress the Mi Push SDK to obtain the `MiPush_SDK_client_**.jar` library files.
3. Copy these library files to `libs` under your project folder and reference them in your project.

#### Step 3.2. Configure the `AndroidManifest.xml` file

Add the necessary permissions for Mi Push:

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />​
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
<uses-permission android:name="android.permission.READ_PHONE_STATE" /> 
<uses-permission android:name="android.permission.GET_TASKS" /> 
<uses-permission android:name="android.permission.VIBRATE"/> 

<!--Change `com.tencent.qcloud.tim.tuikit` to your app package name.-->
<permission
    android:name="com.tencent.qcloud.tim.tuikit.permission.MIPUSH_RECEIVE"
    android:protectionLevel="signature" />
    <uses-permission android:name="com.tencent.qcloud.tim.tuikit.permission.MIPUSH_RECEIVE" />
<!--Change `com.tencent.qcloud.tim.tuikit` to your app package name.-->
```

Configure the services and receivers required by the Mi Push service:

```xml
<service
    android:enabled="true"
    android:process=":pushservice"
    android:name="com.xiaomi.push.service.XMPushService" />
<service
    android:name="com.xiaomi.push.service.XMJobService"
    android:enabled="true"
    android:exported="false"
    android:permission="android.permission.BIND_JOB_SERVICE"
    android:process=":pushservice" /> <!--Note: this service must be added for 3.0.1 and later versions.-->
<service
     android:name="com.xiaomi.mipush.sdk.PushMessageHandler"
    android:enabled="true"
    android:exported="true" />

<service
    android:name="com.xiaomi.mipush.sdk.MessageHandleService"
    android:enabled="true" /> <!--Note: this service must be added for 2.2.5 and later versions.-->

<receiver
    android:name="com.xiaomi.push.service.receivers.NetworkStatusReceiver"
    android:exported="true" >
    <intent-filter>
        <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</receiver>

<receiver
    android:name="com.xiaomi.push.service.receivers.PingReceiver"
    android:exported="false"
    android:process=":pushservice">
    <intent-filter>
        <action android:name="com.xiaomi.push.PING_TIMER" />
    </intent-filter>
</receiver>
```

[](id:Step3_3)
#### Step 3.3. Customize a `BroadcastReceiver` class

In order to receive messages, you need to customize a `BroadcastReceiver` class which inherits `PushMessageReceiver` and implements the `onReceiveRegisterResult` method. Also, register the `BroadcastReceiver` in `AndroidManifest.xml`.

The following is the sample code from the demo:

```java
public class XiaomiMsgReceiver extends PushMessageReceiver {
    private static final String TAG = "XiaomiMsgReceiver";
    private String mRegId;

    @Override
    public void onReceiveRegisterResult(Context context, MiPushCommandMessage miPushCommandMessage) {
        Log.d(TAG, "onReceiveRegisterResult is called. " + miPushCommandMessage.toString());
        String command = miPushCommandMessage.getCommand();
        List<String> arguments = miPushCommandMessage.getCommandArguments();
        String cmdArg1 = ((arguments != null && arguments.size() > 0) ? arguments.get(0) : null);

        Log.d(TAG, "cmd: " + command + " | arg: " + cmdArg1
                + " | result: " + miPushCommandMessage.getResultCode() + " | reason: " + miPushCommandMessage.getReason());

        if (MiPushClient.COMMAND_REGISTER.equals(command)) {
            if (miPushCommandMessage.getResultCode() == ErrorCode.SUCCESS) {
                mRegId = cmdArg1;
            }
        }

        Log.d(TAG, "regId: " + mRegId);
        ThirdPushTokenMgr.getInstance().setThirdPushToken(mRegId); // Pass in `regId` here, which is required for subsequent push information reporting.
        ThirdPushTokenMgr.getInstance().setPushTokenToTIM();
    }

}
```

Register the custom `BroadcastReceiver` in `AndroidManifest.xml`:

```xml
<!--Change `com.tencent.qcloud.uipojo.thirdpush.XiaomiMsgReceiver` to the complete class name in your app.-->
<receiver
    android:name="com.tencent.qcloud.uipojo.thirdpush.XiaomiMsgReceiver"
    android:exported="true">
    <intent-filter>
        <action android:name="com.xiaomi.mipush.RECEIVE_MESSAGE" />
    </intent-filter>
    <intent-filter>
        <action android:name="com.xiaomi.mipush.MESSAGE_ARRIVED" />
    </intent-filter>
    <intent-filter>
        <action android:name="com.xiaomi.mipush.ERROR" />
    </intent-filter>
</receiver>
```

#### Step 3.4. Register Mi Push in your app
To enable Mi offline push, you need to register the push service with the Mi server, and initialize the Mi Push service by calling `MiPushClient.registerPush`. `MiPushClient.registerPush` can be called anywhere. To improve the registration success rate, Mi recommends calling in `onCreate` of `Application`.
After successful registration, you will receive the registration result in `onReceiveRegisterResult` of the `BroadcastReceiver` customized in [Step 3.3](#Step3_3). The `regId` in it is the unique identifier of the current app on the current device. Please record the `regId` information.

The following is the sample code from the demo:

```java
public class DemoApplication extends Application {

    private static DemoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Determine whether this is the main thread.
        if (SessionWrapper.isMainProcess(getApplicationContext())) {
            /**
             * Initialization function of TUIKit
             *
             * @param context  app context, usually corresponds to `ApplicationContext`.
             * @param sdkAppID The `SDKAppID` assigned to you when registering the app in Tencent Cloud
             * @param configs  Relevant configuration items of TUIKit. Usually, you can use the default configuration. For special configuration, refer to the API Documentation.
             */
            long current = System.currentTimeMillis();
            TUIKit.init(this, Constants.SDKAPPID, BaseUIKitConfigs.getDefaultConfigs());
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));
            // Add custom initialization configuration.
            customConfig();
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));

            if(IMFunc.isBrandXiaoMi()){
                // Mi offline push
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

[](id:Step4)
### Step 4. Report the push information to the IM server

If you want to use IM to send notifications to a user through Mi Push, you need to use `setOfflinePushToken`, part of `TIMManager`, to send your **certificate ID**, generated by the IM console, and **regId**, generated by the Mi Push server, to the IM server, after the user has successfully logged in.

>!IM is only able to bind the user to the appropriate device and send notifications through Mi Push after the correct certificate ID and regId are sent.

The following is the sample code from the demo:

- Define certificate ID as a constant:

```java
/**
 * Define some constant information in `Constants.java` first.
 */
/****** Mi offline push parameters start ******/
// Use your certificate ID in the Mi Push certificate information on the IM console.
public static final long XM_PUSH_BUZID = 6666;
// APPID and APPKEY assigned by the Mi open platform
public static final String XM_PUSH_APPID = "1234512345123451234";
public static final String XM_PUSH_APPKEY = "1234512345123";
/****** Mi offline push parameters end ******/
```
- Report certificate ID and regId:

```java
/**
 * Report the push certificate ID and device information in `ThirdPushTokenMgr.java`.
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
        this.mThirdPushToken = mThirdPushToken;  // The regId value is passed here. Describe it in accordance with the above-mentioned custom `BroadcastReciever` class documentation.
    }

    public void setPushTokenToTIM(){
        String token = ThirdPushTokenMgr.getInstance().getThirdPushToken();
        if(TextUtils.isEmpty(token)){
            QLog.i(TAG, "setPushTokenToTIM third token is empty");
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

### Step 5. Push messages offline

After the certificate ID and regId are successfully reported, the IM server sends messages via Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

> ?
> - Mi Push does not guarantee 100% deliverability.
> - Messages pushed via Mi Push may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the Mi Push service.
> - If the IM user has logged out or been forced offline by the IM server (for example, due to login on another device), the device cannot receive push messages.

[](id:click)
## Configuring Click Events
You can select one of the following events: **Open app**, **Open webpage**, or **Open specified in-app page**.

### Open app
If you choose **Open app**, the `onNotificationMessageClicked` method of Mi Push will be called back, and the app itself can process app opening in this method.
![](https://main.qcloudimg.com/raw/d2341570851aa707916a9127a47a2171.png)

 ### Open webpage
You need to select **Open webpage** when [adding a certificate](#Step2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/3c8f71b696f39117105d0e67813aaa0f.png)

### Open specified in-app page

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
   
   // Print results.
   intent://com.tencent.qcloud.tim/detail#Intent;scheme=pushscheme;launchFlags=0x4000000;component=com.tencent.qcloud.tim.tuikit/com.tencent.qcloud.tim.demo.chat.ChatActivity;end
   ```
   
3. Select **Open specified in-app page** when [adding a certificate](#Step2) and enter the result above.
 ![](https://main.qcloudimg.com/raw/94c3abe8ab0cb8c72ee79687d0ffe8d3.png)

[](id:section4)
## Custom Content Pass Through
Select **Open app** or **Open specified in-app page** in **Response after Click** when [adding a certificate](#Step2) to support custom content pass through.

### Step 1. Set custom content (sender)
Set the custom content for the notification bar message before sending the message.
- Sample on Android:

  ```
  String extContent = "ext content";
  TIMMessageOfflinePushSettings settings = new TIMMessageOfflinePushSettings();
  settings.setExt(extContent.getBytes());
  timMessage.setOfflinePushSettings(settings);
  mConversation.sendMessage(false, timMessage, callback);
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

### Step 2. Set custom content (receiver)

- If you selected **Open app** in **Response after Click** when [adding a certificate](#Step2), clicking the notification bar message triggers the `onNotificationMessageClicked(Context, MiPushMessage miPushMessage)` callback of Mi Push SDK. The custom content can be obtained from `miPushMessage`.
```
Map extra = miPushMessage.getExtra();
String extContent = extra.get("ext");
```

- If you selected **Open specified in-app page** in **Response after Click** when [adding a certificate](#Step2), `MiPushMessage`, which is the object that encapsulates the message, is passed to the client through `Intent`. The client then obtains the custom content from `Activity`.
```
Bundle bundle = getIntent().getExtras(); 
MiPushMessage miPushMessage = (MiPushMessage)bundle.getSerializable(PushMessageHelper.KEY_MESSAGE); 
Map extra = miPushMessage.getExtra(); 
String extContent = extra.get("ext");
```

## FAQs
### If the app uses obfuscation, how can I prevent exceptions in the Mi offline push feature?

If your app uses obfuscation, to prevent exceptions in the Mi offline push feature, you need to keep the custom `BroadcastReceiver` and add obfuscation rules by referring to the following:
>?The following code is a sample provided by Mi. Please modify it as needed before using it.

```
# Change `com.tencent.qcloud.tim.demo.thirdpush.XiaomiMsgReceiver` to the complete class name defined in your app.
-keep com.tencent.qcloud.tim.demo.thirdpush.XiaomiMsgReceiver {*;}
# If the Android v23 is used for compilation, adding this can prevent failed compilation caused by a false warning.
-dontwarn com.xiaomi.push.**
```

### Can I set a custom notification sound?
Mi Push does not support custom notification sounds.

### I cannot receive push messages. What should I do?
1. No push message is 100% successful, even those from the vendor. If one or two push messages was not notified during a slew of rapid push messages, it is usually due to rate limiting measures put in place by the vendor.
2. Make sure the correct Mi Push certificate information is properly configured in the [IM console](https://console.qcloud.com/avc).
3. Confirm that your project’s [Mi Push SDK integration](#Step3) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported the correct push information](#Step4) to the IM server.
5. Manually kill the app on your device, send a few messages, and confirm whether you receive notifications within one minute.

