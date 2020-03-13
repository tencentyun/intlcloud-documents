## Process Description

The process of implementing offline message push is as follows:
1. A developer registers an account on a vendor’s platform, and after passing developer verification, the developer applies for the push service.
2. Create the push service, bind it with an app, and obtain information such as the push certificate, password, and key.
3. Log in to [IM Console](https://console.qcloud.com/avc) and specify the push certificate and relevant information. The IM server generates a different certificate ID for each certificate.
4. Integrate the push SDK provided by the vendor with the developer’s project and configure it based on the vendor’s requirements.
5. After integrating the IM SDK with the project, report the certificate ID, device information, and other information to the IM server.
6. When the client app is killed by the system or user without IM logout, the IM server sends notifications to the user through message push.

## Directions

Flyme is a highly customized Android system, with very strict management of the auto-start permissions of third-party apps. By default, third-party apps are not included in the auto-start whitelist of the system. As apps running in the background are often killed by the system, we recommend that Meizu push be integrated on Meizu devices. Meizu push is a system-grade service of Flyme, with a high push delivery rate. Currently, **IM only supports the notification bar messages of Meizu push**.
>
>- This document was prepared with direct reference to the official documentation of Meizu. If Meizu push is updated, refer to Meizu push documentation on the official website.
>- This document was prepared based on the Flyme push access guide. It is intended for the Flyme system only and is not a unified push platform for Meizu (but the integration for different vendors).
>- If you do not need to implement special offline push adaptation for Meizu devices, ignore this section.

### Step 1: Apply for a Meizu push certificate

1. Access the Meizu open platform website to register an account and pass developer verification.
 > The verification process takes about 3 days. Be sure to read the Meizu Push Service Activation Guide to facilitate access to the service.
2. Log in to the console of the Meizu open platform, choose **Service** > **Integrate Push Service** > **Push Backend**, and create a Meizu push service app.
 After the Meizu push service app is created, you can view detailed app information on the app details page.
<span id="Step1_3"></span>
3. Record the **`App package name`**, **`App ID`**, and **`App Secret`** items.

<span id="Step2"></span>
### Step 2: Host the certificate to IM
1. Log in to Tencent Cloud [IM Console](https://console.qcloud.com/avc) and click the target app card to enter the basic configuration page of the app.
2. Click **Add Certificate** in the **Android Platform Push Settings** area.
 > If you already have a certificate and only want to modify its information, you can click **Edit** in the **Android Platform Push Settings** area to modify and update the certificate.
 >

3. Set the following parameters based on the information obtained in [Step 1](#step-1.3A-apply-for-a-meizu-push-certificate):
 - **Push Platform**: select **Meizu**.
 - **App Package Name**: enter the **App package name** of the Meizu push service app.
 - **AppID**: enter the **App ID** of the Meizu push service app.
 - **AppSecret**: enter the **App Secret** of the Meizu push service app.
 - **After Clicking Notification**: select the response operation when users click notification bar messages. Available options are **Open App**, **Open Web Page**, and **Open Specified Interface in App**. For more details, see [Configuring the Notification Bar Message Click Event](#configuring-the-notification-bar-message-click-event).

4. Click **OK** to save the settings. The certificate information will take effect within 10 minutes after being saved.
5. Record the **`ID`** of the certificate after the push certificate information is generated.


<span id="Step3"></span>
### Step 3: Integrate the push SDK
>
> - The default notification title for IM push messages is `a new message`.
> - Before reading this section, ensure that you have correctly integrated and used the IM SDK.
> - You can find a sample for Meizu push implementation in our demo. Note that the features of Meizu push may be adjusted during Meizu push version updates. If you find any inconsistencies with the content of this section, refer to Meizu push documentation on the official website and notify us of the difference so that we can make the necessary modifications.

#### Step 3.1: Download the Meizu push SDK and add references
Access the Meizu push operation platform and download the aar package of the Meizu Flyme push SDK or use jcenter integration.
```
dependencies {
    // MEIZU push sdk
    compile 'com.meizu.flyme.internet:push-internal:3.6.+@aar'
}
```

#### Step 3.2: Configure the AndroidManifest.xml file

Add the permissions required for Meizu push:

```xml
<!-- ********Start of Meizu push permission settings******** -->
<!-- The following settings are compatible with versions earlier than Flyme5.0 and are required for Meizu’s internal pushSDK integration; otherwise, messages cannot be received-->
<uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
<permission
        android:name="com.tencent.qcloud.tim.tuikit.push.permission.MESSAGE"
        android:protectionLevel="signature"/>
<uses-permission android:name="com.tencent.qcloud.tim.tuikit.push.permission.MESSAGE"></uses-permission>

<!-- The following settings are compatible with Flyme3.0 -->
<uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
<permission
            android:name="com.tencent.qcloud.tim.tuikit.permission.C2D_MESSAGE"
            android:protectionLevel="signature"></permission>
<uses-permission android:name="com.tencent.qcloud.tim.tuikit.permission.C2D_MESSAGE"/>
<!-- ********End of Meizu push permission settings******** -->
<!--Here, replace com.tencent.qcloud.tim.tuikit with the package name of your app-->
```

<span id="Step3_3"></span>
#### Step 3.3: Customize a BroadcastReceiver class

To receive messages, you need to customize a BroadcastReceiver that is inherited from the `MzPushMessageReceiver` class, implement the `onRegisterStatus` method in it, and register this receiver to AndroidManifest.xml.

Sample code in the demo:

```java
public class MEIZUPushReceiver extends MzPushMessageReceiver {
    private static final String TAG = "MEIZUPushReceiver";

    @Override
    public void onRegisterStatus(Context context, RegisterStatus registerStatus) {
        QLog.i(TAG, "onRegisterStatus token = " + registerStatus.getPushId());
        ThirdPushTokenMgr.getInstance().setThirdPushToken(registerStatus.getPushId());
        ThirdPushTokenMgr.getInstance().setPushTokenToTIM();
    }

}
```

Register the custom BroadcastReceiver to AndroidManifest.xml:

```xml
<!--Here, change com.tencent.qcloud.tim.demo.thirdpush.MEIZUPushReceiver to the complete class name in your app -->
<!-- ********Start of Meizu push settings******** -->
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.MEIZUPushReceiver">
    <intent-filter>
        <!-- Receive push messages -->
        <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
        <!-- Receive register messages -->
        <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK" />
        <!-- Receive unregister messages -->
        <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK"/>
        <!-- The following settings are compatible with earlier Flyme3 push service configurations -->
        <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
        <action android:name="com.meizu.c2dm.intent.RECEIVE" />
        <category android:name="com.tencent.qcloud.tim.demo.thirdpush"></category>
    </intent-filter>
</receiver>
<!-- ********End of Meizu push settings******** -->
```

#### Step 3.4: Register the Meizu push service in the app
If you choose to enable Meizu offline push, you need to register the Meizu push service with the Meizu server by calling `PushManager.register` to initialize the Meizu push service. `PushManager.register` can be called anywhere. To enhance the registration success rate, we recommend that you call it in `onCreate` of Application.
After successful registration, you will receive the registration result in `onRegisterStatus` of the BroadcastReceiver customized in [Step 3.3](#Step3_3). `registerStatus.getPushId()` indicates the unique identifier of the current app on the current device, and the `PushId` information needs to be recorded.

Sample code in the demo:

```java
public class DemoApplication extends Application {

    private static PojoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Determine whether the current thread is the main thread
        if (SessionWrapper.isMainProcess(getApplicationContext())) {
            /**
             * TUIKit initialization function
             *
             * @param context App context, which usually corresponds to ApplicationContext
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

If you need to use Meizu push to push IM message notifications, after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **PushID** returned by the Meizu push service, to the IM server.

> After the PushId and certificate ID are correctly reported, IM service binds users with the corresponding device information. This enables the use of the Meizu push service to push notifications.

Sample code in the demo:
- Define the certificate ID constant:
```java
/**
 * First, define some constant information in Constants.java
 */
/****** Start of Meizu offline push parameters ******/
// Use your certificate ID in the Meizu push certificate information in the IM console
public static final long MZ_PUSH_BUZID = 6666;
// APPID and APPKEY assigned by the Meizu open platform
public static final String MZ_PUSH_APPID = "1234512345123451234";
public static final String MZ_PUSH_APPKEY = "1234512345123";
/****** End of Meizu offline push parameters ******/
```
- Report the push certificate ID and PushId:
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
        this.mThirdPushToken = mThirdPushToken;  // Here, the PushId value is specified. Describe it based on the aforementioned custom BroadcastReciever class documentation.
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

After the certificate ID and PushID are successfully reported, the IM server sends messages through Meizu push notifications to the user when the app has been killed but the user has not logged out of IM.

>
> - Meizu push does not guarantee 100% success in reaching target users.
> - Meizu push may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the Meizu push service.
> - If the IM user has logged out or was forced logout by the IM server (for example, due to login on another terminal), the device will not receive push messages.

<span id="click"></span>
## Configuring the Notification Bar Message Click Event
You can choose to **Open App**, **Open Web Page**, or **Open Specified Interface in App** to follow the notification bar message click event.

### Opening the app
The default option is **Open App**.


 ### Opening webpages
When [adding a certificate](#Step2), you need to select **Open Web Page** and enter a website URL starting with `http://` or `https://`, for example, `https://intl.cloud.tencent.com/document/product/269`.


### Opening a specified UI in the app
When [adding a certificate](#Step2), you need to select **Open Specified Interface in App** and enter the complete class name of Activity to be opened, for example, `com.tencent.qcloud.tim.demo.chat.ChatActivity`.


## FAQs

### If the app uses obfuscation, how can I prevent exceptions when using the Meizu offline push feature?

If your app uses obfuscation, to prevent exceptions when using the Meizu offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
> The following code is an official sample from Meizu. Please modify it based on your actual situation before use.

```
# Change com.tencent.qcloud.tim.demo.thirdpush.MEIZUPushReceiver to the complete class name defined in your app.
-keep com.tencent.qcloud.tim.demo.thirdpush.MEIZUPushReceiver {*;}
```

### Can I customize push notification sounds?

Currently, Meizu push does not support custom notification sounds.

### How can I identify the cause to failures to receive push messages?
1. No push service guarantees 100% success in reaching target users and zero vendor push exceptions. Therefore, if one or two push messages fail to reach users during a fast and continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. According to the push process, confirm whether the Meizu push certificate information is correctly configured in [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [Meizu push SDK integration](#step-3.3A-integrate-the-push-sdk) configuration is correct and that you have obtained the PushId.
4. Confirm that you have [reported push information](#step-4.3A-report-the-push-information-to-the-im-server) to the IM server correctly.
5. Manually kill the app on your device, send several messages, and check whether you can receive notifications within one minute.
6. If you still cannot receive push messages after the preceding steps, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the specific `time`, `SDKAppID`, `certificate ID`, and `push receiving UserID` for processing.
