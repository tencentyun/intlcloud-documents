## Process

The following is the process of offline message push:
1. Register with the vendor and complete the developer verification process. Apply to enable the push service.
2. Create a push service and bind app information to obtain the push certificate, password, key, and other data.
3. Log in to the [IM Console](https://console.qcloud.com/avc) to upload the certificate and enter other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Integrate the push messaging SDK provided by the vendor with your project and configure it according to the vendor’s instructions.
5. Send your certificate ID and device information to IM server. 
6. If the user did not log out of IM but the client was terminated by the system or user, the IM server will send push messages as notifications.

## Procedure
MIUI is a highly customized Android system, with very strict management of the auto-start permissions for third-party apps. By default, third-party apps are not placed in the auto-start allowlist of the system. As apps running in the background are often killed by the system, we recommend that the MI push service MiPush be integrated on MI devices. MiPush is a system-grade service of MIUI, with a relatively high push delivery rate. Currently, **IM only supports the notification bar messages of MiPush**.
>!
>- This guide was prepared with direct reference to MI’s official documentation. If MiPush is changed, please refer to the [MiPush documentation on the official website](https://dev.mi.com/console/doc/detail?pId=230).
>- If you do not plan to implement a Xiaomi-specific offline push solution, skip this section.

### Step 1: Apply for a MiPush certificate
1. Access the [MI open platform website](https://dev.mi.com/console/) to register an account and pass the developer verification.
 >? The verification process takes about 2 days. Be sure to read the [MiPush Service Launch Guide](https://dev.mi.com/console/doc/detail?pId=68) beforehand to facilitate access to the service.
2. Log in to the console of the MI open platform, choose **App Service** -> **Push Service**, and create a MiPush service app.
 After the MiPush service app is created, you can view detailed app information on the app details page.
[](id:Step1_3)
3. Record the **`Primary package name`**, **`AppID`**, and **`AppSecret`** information.


[](id:Step2)
### Step 2: Generate a Certificate ID 
1. Log in to the [IM Console](https://console.qcloud.com/avc) and click the desired app. The app configuration page appears.
2. Click **Add a certificate** under **Android push configuration**.
 >? If you already have a certificate and only need to change its information, click **Edit**.
 >
 ![](https://main.qcloudimg.com/raw/31bac91d9ffa638ff3ef584496ef2cf3.png)
3. Use the information you obtained in [Step 1](#Step1_3) to configure the following parameters:
 - **Push platform**: select **Xiaomi**.
 - **Package name**: the name of the MiPush service app.
 - **AppID**: enter the **AppID** you got from MiPush.
 - **AppSecret**: enter the **AppSecret** you got from MiPush.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, refer to [Configuring Click Event](#click).
    **Open app** or **Open specific app interface** allows [custom content pass through](#section4).
 ![](https://main.qcloudimg.com/raw/d2341570851aa707916a9127a47a2171.png)
4. Click **OK** to save the information. Certificate information takes effect 10 minutes after you save it.
5. Record the Certificate ID once it is generated.
 


[](id:Step3)
### Step 3: Integrate push SDK
>?
> - The default title of IM push notifications is `a new message`.
> - Before reading this section, make sure that you have integrated and tested the IM SDK.
> - You can find a sample for MiPush implementation in our demo. Note that the features of MiPush may be adjusted during MiPush version updates. If you find any inconsistencies with the content of this section, please refer to the [MiPush documentation on the official website](https://dev.mi.com/console/doc/detail?pId=230) and notify us of the difference so that we can make the necessary modifications.

#### Step 3.1: Download the MiPush SDK and reference it in your project
1. Access the [MiPush operation platform](http://dev.xiaomi.com/mipush/downpage/) and download the MiPush SDK package.
2. Decompress the MiPush SDK package to obtain the `MiPush_SDK_client_**.jar` library file.
3. Copy these library files to `libs` under your project folder and reference them in your project.

#### Step 3.2: Modify AndroidManifest.xml

Add the permissions required for MiPush:

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
<uses-permission android:name="android.permission.READ_PHONE_STATE" /> 
<uses-permission android:name="android.permission.GET_TASKS" /> 
<uses-permission android:name="android.permission.VIBRATE"/> 

<!--Here, change com.tencent.qcloud.tim.tuikit to the package name of your app-->
<permission
    android:name="com.tencent.qcloud.tim.tuikit.permission.MIPUSH_RECEIVE"
    android:protectionLevel="signature" />
    <uses-permission android:name="com.tencent.qcloud.tim.tuikit.permission.MIPUSH_RECEIVE" />
<!--Here, change com.tencent.qcloud.tim.tuikit to the package name of your app-->
```

Configuring the service and receiver required for MiPush service:

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
    android:process=":pushservice" /> <!--Note: this service must be added for versions 3.0.1 and later-->
<service
     android:name="com.xiaomi.mipush.sdk.PushMessageHandler"
    android:enabled="true"
    android:exported="true" />

<service
    android:name="com.xiaomi.mipush.sdk.MessageHandleService"
    android:enabled="true" /> <!--Note: this service must be added for versions 2.2.5 and later-->

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
    android:process=":pushservice" >
    <intent-filter>
        <action android:name="com.xiaomi.push.PING_TIMER" />
    </intent-filter>
</receiver>
```

<span id="Step3_3"></span>
#### Step 3.3: Define a BroadcastReceiver class

To receive messages, you need to customize a BroadcastReceiver inherited from the `PushMessageReceiver` class, implement the `onReceiveRegisterResult` method in it, and register this receiver to AndroidManifest.xml.

The following is sample code from the demo:

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
        ThirdPushTokenMgr.getInstance().setThirdPushToken(mRegId); // The regId is passed in here. It needs to be used for subsequent reporting of push information.
        ThirdPushTokenMgr.getInstance().setPushTokenToTIM();
    }

}
```

Register the custom BroadcastReceiver to AndroidManifest.xml:

```xml
<!--Here, change com.tencent.qcloud.uipojo.thirdpush.XiaomiMsgReceiver to the complete class name in your app-->
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

#### Step 3.4: Register MiPush in your app
If you choose to enable MI offline push, you need to register the MiPush service with the MI server by calling `MiPushClient.registerPush` to initialize the MiPush service. `MiPushClient.registerPush` can be called anywhere. To enhance the registration success rate, we recommend that you call it in `onCreate` of the Application.
After successful registration, you will receive the registration result in `onReceiveRegisterResult` of the BroadcastReceiver customized in [Step 3.3](#Step3_3). The `regId` in it is the unique identifier of the current app on the current device. Please record the `regId` information.

The following is sample code from the demo:

```java
public class DemoApplication extends Application {

    private static DemoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Determine whether this is the main thread
        if (SessionWrapper.isMainProcess(getApplicationContext())) {
            /**
             * TUIKit initialization function
             *
             * @param context  App context, usually corresponds to ApplicationContext
             * @param sdkAppID, the SDKAppID assigned to you when registering the app in Tencent Cloud
             * @param configs, TUIKit configuration options. The default values are suitable in most cases. See the API documentation if you want to customize them.
             */
            long current = System.currentTimeMillis();
            TUIKit.init(this, Constants.SDKAPPID, BaseUIKitConfigs.getDefaultConfigs());
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));
            // Add custom initialization configurations
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

[](id:Step4)
### Step 4: Report the push information to the IM server

If you need to use MiPush to push IM message notifications, then after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **regId** generated by the MiPush server to the IM server.

>! After the regId and certificate ID are correctly reported, the IM service binds users with the corresponding device information, This enables the use of the MiPush service to push notifications.

The following is sample code from the demo:

- Define Certificate ID as a constant:
```java
/**
 * We first define some constant information in Constants.java.
 */
/****** Xiaomi offline push parameters start ******/
// Use your certificate ID in the MiPush certificate information on the IM console
public static final long XM_PUSH_BUZID = 6666;
// APPID and APPKEY assigned by the Xiaomi open platform
public static final String XM_PUSH_APPID = "1234512345123451234";
public static final String XM_PUSH_APPKEY = "1234512345123";
/****** Xiaomi offline push parameters end ******/
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

### Step 5: Offline push

After the certificate ID and regId are successfully reported, the IM server sends messages via MiPush notifications to the user when the app has been killed but the user has not logged out of IM.

>?
> - MiPush is not 100% successful in reaching the target users.
> - MiPush may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the MiPush service.
> - If the IM user has logged out or was force logged out by the IM server (for example, due to login on other terminals), the device will not receive push messages.

[](id:click)
## Configuring Click Events
You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

### Open app
If you choose **Open App**, the onNotificationMessageClicked method of MI will be called back, and the app itself can process app opening in this method.
![](https://main.qcloudimg.com/raw/d2341570851aa707916a9127a47a2171.png)

 ### Open URL
You need to select **Open URL** in [Step 2](#Step2) and enter a URL that starts with either `http` or `https`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/3c8f71b696f39117105d0e67813aaa0f.png)

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
 ![](https://main.qcloudimg.com/raw/94c3abe8ab0cb8c72ee79687d0ffe8d3.png)

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

- If you selected **Open app** in [Step 2](#Step2), clicking the notification bar message triggers the `onNotificationMessageClicked(Context, MiPushMessage miPushMessage)` callback. The custom content can be obtained from `miPushMessage`.
	
    ```
    Map extra = miPushMessage.getExtra();
    String extContent = extra.get("ext");
    ```
	
- If you selected **Open app** in [Step 2](#Step2), `MiPushMessage`, which is the object that encapsulates the message, is passed to the client through `Intent`. The client then obtains the custom content from `Activity`.
	
	  ```
	  Bundle bundle = getIntent().getExtras(); 
	  MiPushMessage miPushMessage = (MiPushMessage)bundle.getSerializable(PushMessageHelper.KEY_MESSAGE); 
	  Map extra = miPushMessage.getExtra(); 
	  String extContent = extra.get("ext");
	```

## FAQ
### If the app uses obfuscation, how can I prevent exceptions in the MI offline push feature?

If your app uses obfuscation, to prevent exceptions in the MI offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
>? The following code is an official sample from MI. Please modify it according to your actual situation before use.

```
# Change com.tencent.qcloud.tim.demo.thirdpush.XiaomiMsgReceiver to the complete class name defined in your app.
-keep com.tencent.qcloud.tim.demo.thirdpush.XiaomiMsgReceiver {*;}
# If the Android version used for compilation is 23, adding this can prevent compilation failure caused by a misreported warning.
-dontwarn com.xiaomi.push.**
```

### Can I set a custom notification sound?
Xiaomi does not support custom notification sounds.

### I cannot receive push messages. What should I do?
1. No push service is 100% successful in reaching target users, and vendor push is no exception. Therefore, if one or two push messages fail to reach users during a fast, continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. Make sure the correct push certificate information from Xiaomi is properly configured in the [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [MiPush SDK integration](#Step3) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported push information](#Step4) to the IM server correctly.
5. Manually kill the app on your device, send a few messages, and confirm whether you receive notifications within one minute.

