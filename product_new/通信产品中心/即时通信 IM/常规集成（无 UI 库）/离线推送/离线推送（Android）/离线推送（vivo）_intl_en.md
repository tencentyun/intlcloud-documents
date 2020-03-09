## Process Description
The process of implementing offline message push is as follows:
1. A developer registers an account on a vendor’s platform, and after passing developer verification, the developer applies for the push service.
2. Create the push service, bind it with an app, and obtain information such as the push certificate, password, and key.
3. Log in to [IM Console](https://console.qcloud.com/avc) and specify the push certificate and relevant information. The IM server generates a different certificate ID for each certificate.
4. Integrate the push SDK provided by the vendor with the developer’s project and configure it based on the vendor’s requirements.
5. After integrating the IM SDK with the project, report the certificate ID, device information, and other information to the IM server.
6. When the client app is killed by the system or user without IM logout, the IM server sends notifications to the user through message push.

## Directions

vivo mobile phones use a highly customized Android system, with very strict management of the auto-start permissions of third-party apps. By default, third-party apps are not included in the auto-start whitelist of the system. As apps running in the background are often killed by the system, we recommend that vivo push be integrated on vivo devices. vivo push is a system-grade service for vivo devices, with a high delivery rate. Currently, **IM only supports the notification bar messages of vivo push**.

>
>- This document was prepared with direct reference to the official documentation of vivo push. If vivo push is updated, refer to [vivo push documentation on the official website](https://dev.vivo.com.cn/documentCenter/doc/180).
>- If you do not need to implement special offline push adaptation for vivo devices, ignore this section.

<span id="Step1"></span>
### Step 1: Apply for a vivo push certificate
1. Access the [vivo open platform website](https://dev.vivo.com.cn/home) to register an account and pass developer verification.
 > The verification process takes about 3 days. Be sure to read [vivo push service description](https://dev.vivo.com.cn/documentCenter/doc/180) beforehand to facilitate access to the service.
2. Log in to the console of the vivo open platform, choose **Message Push** > **Create** > **Test Push**, and create a vivo push service app.
 After the vivo push service app is created, you can view detailed app information on the app details page.
<span id="Step1_3"></span>
3. Record the **`APP ID`**, **`APP key`**, and **`APP secret`** items.

<span id="Step2"></span>
### Step 2: Host the certificate to IM
1. Log in to Tencent Cloud [IM Console](https://console.qcloud.com/avc) and click the target app card to go to the basic configuration page of the app.
2. Click **Add Certificate** in the **Android Platform Push Settings** area.
 > If you already have a certificate and only want to modify its information, you can click **Edit** in the corresponding certificate area to modify and update the certificate.
 >
 ![](https://main.qcloudimg.com/raw/aaa40b3c7e43f99b7e36c8b7589e54e0.png)
3. Set the following parameters based on the information obtained in [Step 1](#Step1_3):
 - **Push Platform**: select **vivo**.
 - **AppKey**: enter the **APP key** of the vivo push service app.
 - **AppID**: enter the **APP ID** of the vivo push service app.
 - **AppSecret**: enter the **APP secret** of the vivo push service app.
 - **After Clicking Notification**: select the response operation when users click notification bar messages. Available options are **Open App**, **Open Web Page**, and **Open Specified Interface in App**. For more details, see [Configuring the Notification Bar Message Click Event](#click).
 ![](https://main.qcloudimg.com/raw/ac890d834dd7f069f936094180634cd7.png)
4. Click **OK** to save the settings. The certificate information will take effect within 10 minutes after being saved.
5. Record the **`ID`** of the certificate after the push certificate information is generated.
 ![](https://main.qcloudimg.com/raw/3442e00debac668c42fa4be89903ac90.png)

<span id="Step3"></span>
### Step 3: Integrate the push SDK
>
> - The default notification title for IM push messages is `a new message`.
> - Before reading this section, ensure that you have correctly integrated and used the IM SDK.
> - You can find a sample for the implementation of vivo push in our demo. Note that the features of vivo push may be adjusted during vivo push version updates. If you find any inconsistencies with the content of this section, refer to [vivo push documentation on the official website](https://dev.vivo.com.cn/documentCenter/doc/155) and notify us of the difference so that we can make necessary modifications.

#### Step 3.1: Download the vivo push SDK and add references
1. Visit the [vivo push operation platform](https://dev.vivo.com.cn/documentCenter/doc/232) and download the vivo push SDK package.
2. Decompress the vivo push SDK package to extract the `vivo_pushsdk_xxx.jar` library file.
3. Add the `vivo_pushsdk_xxx.jar` library file to the `libs` directory in your project and add references in the project.


#### Step 3.2: Configure the AndroidManifest.xml file

Add the configuration required for the vivo push service:

```xml
<!-- ******** Start of vivo push settings ******** -->
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
<!-- ******** End of vivo push settings ******** -->
<!-- Here, com.vivo.push.app_id and com.vivo.push.api_key are generated by the vivo open platform -->
```

#### Step 3.3: Customize a BroadcastReceiver class

To receive messages, you need to customize a BroadcastReceiver inherited from the `OpenClientPushMessageReceiver` class, implement the `onReceiveRegId` and `onNotificationMessageClicked` methods in it, and register this receiver to AndroidManifest.xml.

Sample code in the demo:

```java
public class VIVOPushMessageReceiverImpl extends OpenClientPushMessageReceiver {
    private static final String TAG = "VIVOPushMessageReceiver";
    @Override
    public void onNotificationMessageClicked(Context context, UPSNotificationMessage upsNotificationMessage) {
        Log.i(TAG, "onNotificationMessageClicked");
    }

    @Override
    public void onReceiveRegId(Context context, String regId) {
        // This callback is called if the vivo regId is changed. According to the documentation on the official website, to obtain the regId, you need to call PushClient.getInstance(getApplicationContext()).getRegId() in the callback for enabling push. For more information, see LoginActivity.
        Log.i(TAG, "onReceiveRegId = " + regId);
    }
}
```

Register the custom BroadcastReceiver to AndroidManifest.xml:

```xml
<!--Here, replace com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl with the complete class name in your app-->
<!-- Declaration defining the message receiver in the push app -->
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl">
    <intent-filter>
        <!-- Receive push messages -->
        <action android:name="com.vivo.pushclient.action.RECEIVE" />
    </intent-filter>
</receiver>
```

#### Step 3.4: Register the vivo push service in the app

If you choose to enable vivo offline push, you need to register the vivo push service with the vivo server by calling `PushClient.getInstance(getApplicationContext()).initialize()` to initialize the vivo push service. `PushClient.getInstance(getApplicationContext()).initialize()` can be called anywhere. To enhance the registration success rate, we recommend that you call it in `onCreate` of Application.

After successful registration, you need to obtain the registration result on the main UI of the app. The `regId` in it is the unique identifier of the current app on the current device, which needs to be recorded.

Sample code in the demo:

```java
public class DemoApplication extends Application {

    private static PojoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Check whether the current thread is the main thread
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

Launch the vivo push service on the main UI:

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
                // According to the vivo push documentation, state = 101 indicates that the vivo model or version does not support vivo push. For details, see <a href="https://dev.vivo.com.cn/documentCenter/doc/156">vivo Push FAQs</a>.
                QLog.i(TAG, "vivopush open vivo push fail state = " + state);
            }
        }
    });
</pre>

<span id="Step4"></span>
### Step 4: Report the push information to the IM server
If you need to use vivo push to push IM message notifications, after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **regId** returned by the vivo push service, to the IM server.
> After the regId and certificate ID are correctly reported, IM service binds users with the corresponding device information. This enables the use of the vivo push service to push notifications.

Sample code in the demo:

- Define the certificate ID constant:
```java
/**
 * First, define some constant information in Constants.java
 */
/****** Start of vivo offline push parameters ******/
// Certificate ID assigned for the third-party push certificate uploaded to the Tencent Cloud console
public static final long VIVO_PUSH_BUZID = 6666;
// APPID and APPKEY assigned by the vivo open platform
public static final String VIVO_PUSH_APPID = "1234512345123451234"; // See the manifest file
public static final String VIVO_PUSH_APPKEY = "12345abcde"; // See the manifest file
/****** End of vivo offline push parameters ******/
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
        this.mThirdPushToken = mThirdPushToken;  // Here, the regId value is specified. Describe it in based on the aforementioned custom BroadcastReciever class documentation.
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

After the certificate ID and regId are successfully reported, the IM server sends messages through vivo push notifications to the user when the app has been killed but the user has not logged out of IM.

>
>- vivo push supports only some vivo mobile phones. For details, see [vivo Push FAQs]( https://dev.vivo.com.cn/documentCenter/doc/156).
>- vivo push does not guarantee 100% success in reaching target users.
>- vivo push may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the vivo push service.
>- If the IM user has logged out or was force logout by the IM server (for example, due to login on another terminal), the device will not receive push messages.

<span id="click"></span>
## Configuring the Notification Bar Message Click Event
You can choose to **Open App**, **Open Web Page**, or **Open Specified Interface in App** to follow the notification bar message click event.

### Opening the app
The default option is **Open App**.
![](https://main.qcloudimg.com/raw/ac890d834dd7f069f936094180634cd7.png)

### Opening webpages
When [adding a certificate](#Step2), you need to select **Open Web Page** and enter a website URL starting with `http://` or `https://`, for example, `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/76ebc2f58623241c685ebffab6b4c2f6.png)

### Opening a specified UI in the app

1. In manifest, configure the `intent-filter` of the Activity to be opened. The sample code is as follows:
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
    ![](https://main.qcloudimg.com/raw/1ab25b8c52b953014786682bce43c2ed.png)

## FAQs

### If the app uses obfuscation, how can I prevent exceptions when using the vivo offline push feature?

If your app uses obfuscation, to prevent exceptions when using the vivo offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
> The following code is an official sample from vivo. Please modify it based on your actual situation before use.

```
# Replace com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl with the complete class name defined in your app
# vivo push
-dontwarn com.vivo.push.**
-keep class com.vivo.push.**{*; }
-keep class com.vivo.vms.**{*; }
-keep class com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl{*;}
```


### Can I customize push notification sounds?

Currently, vivo push does not support custom notification sounds.

### How can I identify the cause to failures to receive push messages?
1. No push service guarantees 100% success in reaching target users and zero vendor push exceptions. Therefore, if one or two push messages fail to reach users during a fast and continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. According to the push process, confirm whether the vivo push certificate information is correctly configured in [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [vivo push SDK integration](#Step3) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported push information](#Step4) to the IM server correctly.
5. Manually kill the app on your device, send several messages, and confirm whether you can receive notifications within one minute.
6. If you still cannot receive push messages after the preceding steps, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the specific `time`, `SDKAppID`, `certificate ID`, and `push receiving UserID` for processing.
