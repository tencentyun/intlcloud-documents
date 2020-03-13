## Process Description

The process of implementing offline message push is as follows:
1. A developer registers an account on a vendor’s platform, and after passing developer verification, the developer applies for the push service.
2. Create the push service, bind it with an app, and obtain information such as the push certificate, password, and key.
3. Log in to [IM Console](https://console.qcloud.com/avc) and specify the push certificate and relevant information. The IM server generates a different certificate ID for each certificate.
4. Integrate the push SDK provided by the vendor with the developer’s project and configure it based on the vendor’s requirements.
5. After integrating the IM SDK with the project, report the certificate ID, device information, and other information to the IM server.
6. When the client app is killed by the system or user without IM logout, the IM server sends notifications to the user through message push.

## Directions
MIUI is a highly customized Android system, with very strict management of the auto-start permissions for third-party apps. By default, third-party apps are not included in the auto-start whitelist of the system. As apps running in the background are often killed by the system, we recommend that the MI push service MiPush be integrated on MI devices. MiPush is a system-grade service of MIUI, with a relatively high push delivery rate. Currently, **IM only supports the notification bar messages of MiPush**.
>
>- This document was prepared with direct reference to MI’s official documentation. 
>- If you do not need to implement special offline push adaptation of MI devices, ignore this section.

### Step 1: Apply for a MiPush certificate
1. Access the MI open platform website to register an account and pass developer verification.
 > The verification process takes about 2 days. 
2. Log in to the console of the MI open platform, choose **App Service** > **Push Service**, and create a MiPush service app.
 After the MiPush service app is created, you can view detailed app information on the app details page.
<span id="Step1_3"></span>
3. Record the **`Primary package name`**, **`AppID`**, and **`AppSecret`** items.


<span id="Step2"></span>
### Step 2: Host the certificate to IM 
1. Log in to Tencent Cloud [IM Console](https://console.qcloud.com/avc) and click the target app card to enter the basic configuration page of the app.
2. Click **Add Certificate** in the **Android Platform Push Settings** area.
 > If you already have a certificate and only want to modify its information, you can click **Edit** in the **Android Platform Push Settings** area to modify and update the certificate.
 >

3. Set the following parameters based on the information obtained in [Step 1](#step-1.3A-apply-for-a-mipush-certificate):
 - **Push Platform**: select **MI**.
 - **App Package Name**: enter the **Primary package name** of the MiPush service.
 - **AppID**: enter the **AppID** of the MiPush service app.
 - **AppSecret**: enter the **AppSecret** of the MiPush service app.
 - **After Clicking Notification**: select the response operation when users click notification bar messages. Available options are **Open App**, **Open Web Page**, and **Open Specified Interface in App**. For more details, see [Configuring the Notification Bar Message Click Event](#configuring-the-notification-bar-message-click-event).

4. Click **OK** to save the settings. The certificate information will take effect within 10 minutes after being saved.
5. Record the **`ID`** of the certificate after the push certificate information is generated.

 
<span id="Step3"></span>
### Step 3: Integrate the push SDK
>
> - The default notification title for IM push messages is `a new message`.
> - Before reading this section, ensure that you have correctly integrated and used the IM SDK.
> - You can find a sample for MiPush implementation in our demo. Note that the features of MiPush may be adjusted during MiPush version updates. If you find any inconsistencies with the content of this section.

#### Step 3.1: Download the MiPush SDK and add references
1. Access the MiPush operation platform and download the MiPush SDK package.
2. Decompress the MiPush SDK package to extract the `MiPush_SDK_client_**.jar` library file.
3. Add the `MiPush_SDK_client_**.jar` library file to the `libs` directory in your project and add references in the project.

#### Step 3.2: Configure the AndroidManifest.xml file

Add the permissions required for MiPush:

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />​
<uses-permission android:name="android.permission.INTERNET" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
<uses-permission android:name="android.permission.READ_PHONE_STATE" /> 
<uses-permission android:name="android.permission.GET_TASKS" /> 
<uses-permission android:name="android.permission.VIBRATE"/> 

<!--Here, replace com.tencent.qcloud.tim.tuikit with the package name of your app-->
<permission
    android:name="com.tencent.qcloud.tim.tuikit.permission.MIPUSH_RECEIVE"
    android:protectionLevel="signature" />
    <uses-permission android:name="com.tencent.qcloud.tim.tuikit.permission.MIPUSH_RECEIVE" />
<!--Here, replace com.tencent.qcloud.tim.tuikit with the package name of your app-->
```

Configure the service and receiver required for the MiPush service:

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
#### Step 3.3: Customize a BroadcastReceiver class

To receive messages, you need to customize a BroadcastReceiver that is inherited from the `PushMessageReceiver` class, implement the `onReceiveRegisterResult` method in it, and register this receiver to AndroidManifest.xml.

Sample code in the demo:

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
        ThirdPushTokenMgr.getInstance().setThirdPushToken(mRegId); // Here, the regId is passed in. It is required for the subsequent reporting of push information.
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

#### Step 3.4: Register the MiPush service in the app
If you choose to enable MI offline push, you need to register the MiPush service with the MI server by calling `MiPushClient.registerPush` to initialize the MiPush service. `MiPushClient.registerPush` can be called anywhere. To enhance the registration success rate, we recommend that you call it in `onCreate` of Application.
After successful registration, you will receive the registration result in `onReceiveRegisterResult` of the BroadcastReceiver customized in [Step 3.3](#Step3_3). The `regId` in the result is the unique identifier of the current app on the current device, which needs to be recorded.

Sample code in the demo:

```java
public class DemoApplication extends Application {

    private static DemoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Determine whether the current thread is the main thread
        if (SessionWrapper.isMainProcess(getApplicationContext())) {
            /**
             * TUIKit initialization function
             *
             * @param context App context, which normally corresponds to ApplicationContext
             * @param sdkAppID SDKAppID assigned to the app that you registered in Tencent Cloud
             * @param configs Relevant configuration items of TUIKit. Usually, you can use the default configuration. For special configurations, refer to "API Documentation".
             */
            long current = System.currentTimeMillis();
            TUIKit.init(this, Constants.SDKAPPID, BaseUIKitConfigs.getDefaultConfigs());
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));
            // Add custom initial configuration
            customConfig();
            System.out.println(">>>>>>>>>>>>>>>>>>"+(System.currentTimeMillis()-current));

            if(IMFunc.isBrandXiaoMi()){
                // MI offline push
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

<span id="Step4"></span>
### Step 4: Report the push information to the IM server

If you need to use MiPush to push IM message notifications, after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **regId** generated by the MiPush server, to the IM server.

> After the regId and certificate ID are correctly reported, the IM service binds users with the corresponding device information, This enables the use of the MiPush service to push notifications.

Sample code in the demo:

- Define the certificate ID constant:
```java
/**
 * First, define some constant information in Constants.java
 */
/****** Start of MI offline push parameters ******/
// Use your certificate ID in the MiPush certificate information in the IM console
public static final long XM_PUSH_BUZID = 6666;
// APPID and APPKEY assigned by the MI open platform
public static final String XM_PUSH_APPID = "1234512345123451234";
public static final String XM_PUSH_APPKEY = "1234512345123";
/****** End of MI offline push parameters ******/
```
- Report the push certificate ID and regId:
```java
/**
 * Report the push certificate ID and device information in ThirdPushTokenMgr.java
 */
public class ThirdPushTokenMgr {
    private static final String TAG = "ThirdPushTokenMgr";

    private String mThirdPushToken;

    private boolean mIsTokenSet = false;
    private boolean mIsLogin = false;

    public static ThirdPushTokenMgr getInstance () {
        return ThirdPushTokenHolder.instance;
    }

    private static class ThirdPushTokenHolder {
        private static final ThirdPushTokenMgr instance = new ThirdPushTokenMgr();
    }

    public void setIsLogin(boolean isLogin){
        mIsLogin = isLogin;
    }

    public String getThirdPushToken() {
        return mThirdPushToken;
    }

    public void setThirdPushToken(String mThirdPushToken) {
        this.mThirdPushToken = mThirdPushToken;  // Here, the regId value is specified. Describe it based on the aforementioned custom BroadcastReciever class documentation.
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
        if(IMFunc.isBrandXiaoMi()){     // Identify the vendor brand and choose different push services for different vendors
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

After the certificate ID and regId are successfully reported, the IM server sends messages through MiPush notifications to the user when the app has been killed but the user has not logged out of IM.

>
> - MiPush does not guarantee 100% success in reaching target users.
> - MiPush may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the MiPush service.
> - If the IM user has logged out or was forced logout by the IM server (for example, due to login on another terminal), the device will not receive push messages.

<span id="click"></span>
## Configuring the Notification Bar Message Click Event
You can choose to **Open App**, **Open Web Page**, or **Open Specified Interface in App** to follow the notification bar message click event.

### Opening the app
If you select **Open App**, the onNotificationMessageClicked method of MI will be called back, and the app itself can complete app opening in this method.


 ### Opening webpages
When [adding a certificate](#Step2), you need to select **Open Web Page** and enter a website URL starting with `http://` or `https://`, for example, `https://cloud.tencent.com/document/product/269`.

### Opening a specified UI in the app

1. In manifest, configure the `intent-filter` of Activity to be opened. The sample code is as follows:
	```
	<activity
		android:name="com.tencent.qcloud.tim.demo.chat.ChatActivity"
		android:launchMode="singleTask"
		android:screenOrientation="portrait"
		android:windowSoftInputMode="adjustResize|stateHidden">

		<intent-filter>
			<action android:name="android.intent.action.View" />
			<data
				android:host="com.tencent.qcloud.tim"
				android:path="/detail"
				android:scheme="pushscheme" />
		</intent-filter>

	</activity>
	```
   
2. Obtain the intent URL as follows:
   
   ```
   Intent intent = new Intent(this, ChatActivity.class);
   intent.setData(Uri.parse("pushscheme://com.tencent.qcloud.tim/detail?title=testTitle"));
   intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
   String intentUri = intent.toUri(Intent.URI_INTENT_SCHEME);
   Log.i(TAG, "intentUri = " + intentUri);
   
   // Print results
   intent://com.tencent.qcloud.tim/detail?title=testTitle#Intent;scheme=pushscheme;launchFlags=0x4000000;component=com.tencent.qcloud.tim.tuikit/com.tencent.qcloud.tim.demo.chat.ChatActivity;end
   ```
   
3. When [adding a certificate](#Step2), select **Open Specified Interface in App** and enter the printed results.


## FAQs
### If the app uses obfuscation, how can I prevent exceptions when using the MI offline push feature?

If your app uses obfuscation, to prevent exceptions when using the MI offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
> The following code is an official sample from MI. Please modify it based on your actual situation before use.

```
# Change com.tencent.qcloud.tim.demo.thirdpush.XiaomiMsgReceiver to the complete class name defined in your app.
-keep com.tencent.qcloud.tim.demo.thirdpush.XiaomiMsgReceiver {*;}
# If the Android version used for compilation is 23, adding this can prevent compilation failures caused by a false-positive warning.
-dontwarn com.xiaomi.push.**
```

### Can I customize push notification sounds?
Currently, MiPush does not support custom notification sounds.

### How can I identify the cause to failures to receive push messages?
1. No push service guarantees 100% success in reaching target users and zero vendor push exceptions. Therefore, if one or two push messages fail to reach users during a fast and continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. According to the push process, confirm whether the MiPush certificate information is correctly configured in [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [MiPush SDK integration](#step-3.3A-integrate-the-push-sdk) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported push information](#step-4.3A-report-the-push-information-to-the-im-server) to the IM server correctly.
5. Manually kill the app on your device, send several messages, and check whether you can receive notifications within one minute.
6. If you still cannot receive push messages after the preceding steps, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the specific `time`, `SDKAppID`, `certificate ID`, and `push receiving UserID` for processing.
