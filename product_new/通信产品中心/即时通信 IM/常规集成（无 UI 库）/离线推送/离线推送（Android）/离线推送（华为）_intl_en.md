## Process Description
The process of implementing offline message push is as follows:
1. A developer registers an account on a vendor’s platform, and after passing developer verification, the developer applies for the push service.
2. Create the push service, bind it with an app, and obtain information such as the push certificate, password, and key.
3. Log in to [IM Console](https://console.qcloud.com/avc) and specify the push certificate and relevant information. The IM server generates a different certificate ID for each certificate.
4. Integrate the push SDK provided by the vendor with the developer’s project and configure it based on the vendor’s requirements.
5. After integrating the IM SDK with the project, report the certificate ID, device information, and other information to the IM server.
6. When the client app is killed by the system or user without IM logout, the IM server sends notifications to the user through message push.

## Huawei Push
Huawei EMUI is a highly customized Android system with strict backend policies. By default, third-party apps do not have auto-start permissions. As apps running in the background are often forcibly killed by the system, we recommend that the Huawei push service be integrated on Huawei devices. The Huawei push service is part of Huawei Mobile Service (HMS) and a system-grade service of EMUI. Its delivery rate is higher than those of third-party push services. Currently, **IM only supports the notification bar messages of Huawei push**.

>
>- This document was prepared with direct reference to the official documentation of Huawei push. If Huawei push is updated, refer to [Huawei push documentation on the official website](https://developer.huawei.com/consumer/cn/service/hms/catalog/huaweisns_agent.html?page=hmssdk_huaweisns_devguide_agent).
>- If you do not need to implement special offline push adaptation for Huawei devices, ignore this section.

### Step 1: Apply for a Huawei push certificate
1. Access the [official website of the Huawei Developers Alliance](https://developer.huawei.com/consumer/cn/), register an account, and pass developer verification.
 > The verification process takes about 30 minutes. Be sure to read the [Huawei Push Service Activation Guide](https://developer.huawei.com/consumer/cn/help/60101) beforehand to facilitate access to the service.
2. Log in to the console of the Huawei Developers Alliance, choose **App Service** > **Development Service** > **PUSH**, and create a Huawei push service app.
 When applying for the Huawei push service, you need to provide a maximum of five SHA256 fingerprints for app signature certificates. After the Huawei push service app is created, you can view detailed app information on the app details page.
<span id="Step1_3"></span>
3. Record the **`Package name`**, **`APP ID`**, and **`APP Secret`** items.


<span id="Step2"></span>
### Step 2: Host the certificate to IM

1. Log in to Tencent Cloud [IM Console](https://console.qcloud.com/avc) and click the target app card to go to the basic configuration page of the app.
2. Click **Add Certificate** in the **Android Platform Push Settings** area.
 > If you already have a certificate and only want to modify its information, you can click **Edit** in the **Android Platform Push Settings** area to modify and update the certificate.
 >

3. Set the following parameters based on the information obtained in [Step 1](#Step1_3):
 - **Push Platform**: select **Huawei**.
 - **App Package Name**: enter the **Package name** of the Huawei push service app.
 - **AppID**: enter the **APP ID** of the Huawei push service app.
 - **AppSecret**: enter the **APP SECRET** of the Huawei push service app.
 - **After Clicking Notification**: select the response operation when users click notification bar messages. Available options are **Open App**, **Open Web Page**, and **Open Specified Interface in App**. For more details, see [Configuring the Notification Bar Message Click Event](#click).

4. Click **OK** to save the settings. The certificate information will take effect within 10 minutes after being saved.
5. Record the **`ID`** of the certificate after the push certificate information is generated.


<span id="Step3"></span>
### Step 3: Integrate the push SDK

>
> - The default notification title for IM push messages is `a new message`.
> - Before reading this section, ensure that you have correctly integrated and used the IM SDK.
> - You can find a sample for Huawei push implementation in our demo. Note that the features of Huawei push may be adjusted during Huawei push version updates. If you find any inconsistencies with the content of this section, refer to [Huawei push documentation on the official website](https://developer.huawei.com/consumer/cn/service/hms/catalog/huaweisns_agent.html?page=hmssdk_huaweisns_devguide_agent) and notify us of the difference so that we can make the necessary modifications.

#### Step 3.1: Download the Huawei push SDK and add references

1. Access the [Huawei push operation platform](https://developer.huawei.com/consumer/cn/service/hms/catalog/huaweipush_agent.html?page=hmssdk_huaweipush_sdkdownload_agent) and download the **HMS Agent kit**.
2. Decompress the HMS Agent kit.
3. Copy files in the `hmsagents\src\main\java` folder to the src\main\java directory of your project.
 ![](https://main.qcloudimg.com/raw/3c9bca5dea731eeb4cb70e73e56d28b4.png)
4. Use Gradle to integrate the Huawei push SDK by adding the following code in the build.gradle file of your project:
```
allprojects {
    repositories {
        jcenter()
        maven {url 'http://developer.huawei.com/repo/'}
    }
}    
```

5. Add the following information in build.gradle of the sub-project:
```
dependencies {
    // Huawei push SDK, where version 2.6.3.301 can be replaced with the actually used version
    implementation 'com.huawei.android.hms:push:2.6.3.301'
    // If an error stating that com.huawei.hms.api does not exist occurs, this line of code is also required. Note that the actual version number must be used here.
    // implementation 'com.huawei.android.hms:base:2.6.3.301'
}
```

#### Step 3.2: Configure the AndroidManifest.xml file
1. Add permissions required for Huawei push:

```xml
<!--HMS-SDK guides the upgrade of the HMS feature, and accessing the OTA server requires network permissions-->    
<uses-permission android:name="android.permission.INTERNET" />    
<!--HMS-SDK guides the upgrade of the HMS feature, and saving the downloaded upgrade package requires the SD card write permission-->    
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />    
<!--Check the network status-->  
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>  
<!--Check the Wi-Fi status-->  
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>  
<!--Obtain the user’s mobile phone IMEI to uniquely identify the user-->  
<uses-permission android:name="android.permission.READ_PHONE_STATE"/> 

<!--If you are using Android 8.0 with targetSdkVersion>=26 for app compilation configuration, you must add the following permissions-->
<uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />

<!--Here, change com.tencent.qcloud.tim.tuikit to the package name of your app-->
<permission
    android:name="com.tencent.qcloud.tim.tuikit.permission.PROCESS_PUSH_MSG"
    android:protectionLevel="signatureOrSystem"/>
<uses-permission android:name="com.tencent.qcloud.tim.tuikit.permission.PROCESS_PUSH_MSG" />
<!--Here, change com.tencent.qcloud.tim.tuikit to the package name of your app-->
```

2. Add the following content under application. For detailed description, see the [description of the Huawei push configuration manifest file](https://developer.huawei.com/consumer/cn/service/hms/catalog/huaweisns_agent.html?page=hmssdk_huaweisns_devprepare_agent#5%20配置manifest文件).

```xml
<meta-data
    android:name="com.huawei.hms.client.appid"
    android:value="appid=1234567890"/> <!--Here, change the appid to your Huawei push App ID-->
<provider
    android:name="com.huawei.hms.update.provider.UpdateProvider"
    android:authorities="com.tencent.qcloud.tim.tuikit.hms.update.provider"
    android:exported="false"
    android:grantUriPermissions="true"/>
<provider
    android:name="com.huawei.updatesdk.fileprovider.UpdateSdkFileProvider"
    android:authorities="com.tencent.qcloud.tim.tuikit.updateSdk.fileProvider"
    android:exported="false"
    android:grantUriPermissions="true">
</provider>
<activity
    android:name="com.huawei.android.hms.agent.common.HMSAgentActivity"
    android:configChanges="orientation|locale|screenSize|layoutDirection|fontScale"
    android:excludeFromRecents="true"
    android:exported="false"
    android:hardwareAccelerated="true"
    android:theme="@android:style/Theme.Translucent" >
    <meta-data
        android:name="hwc-theme"
        android:value="androidhwext:style/Theme.Emui.Translucent" />
</activity>
<activity
    android:name="com.huawei.hms.activity.BridgeActivity"
    android:configChanges="orientation|locale|screenSize|layoutDirection|fontScale"
    android:excludeFromRecents="true"
    android:exported="false"
    android:hardwareAccelerated="true"
    android:theme="@android:style/Theme.Translucent" >
    <meta-data
        android:name="hwc-theme"
        android:value="androidhwext:style/Theme.Emui.Translucent" />
</activity>

<service
    android:name="com.huawei.hms.support.api.push.service.HmsMsgService"
    android:enabled="true"
    android:exported="true"
    android:process=":pushservice">
    <intent-filter>
        <action android:name="com.huawei.push.msg.NOTIFY_MSG" />
        <action android:name="com.huawei.push.msg.PASSBY_MSG" />
    </intent-filter>
</service>
```

<span id="Step3_3"></span>
#### Step 3.3: Customize a BroadcastReceiver class

To receive messages, you need to customize a BroadcastReceiver that is inherited from the `PushReceiver` class, implement the `onToken` method in it, and register this receiver to AndroidManifest.xml.

Sample code in the demo:

```java
public class HUAWEIPushReceiver extends PushReceiver {
    private static final String TAG = "HUAWEIPushReceiver";

    @Override
    public void onToken(Context context, String token, Bundle extras) {
        Log.i(TAG, "onToken:" + token);
        ThirdPushTokenMgr.getInstance().setThirdPushToken(token);  // The token is passed in here. It is required for the subsequent reporting of push information.
        ThirdPushTokenMgr.getInstance().setPushTokenToTIM();
    }
}
```

Register the custom BroadcastReceiver to AndroidManifest.xml:

```xml
<!--Here, change com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver to the complete class name in your app-->
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver"
    android:permission="com.tencent.qcloud.tim.tuikit.permission.PROCESS_PUSH_MSG">
    <intent-filter>
        <!-- This is required and is for receiving the token -->
        <action android:name="com.huawei.android.push.intent.REGISTRATION" />
        <!-- This is required and is for receiving pass-through messages -->
        <action android:name="com.huawei.android.push.intent.RECEIVE" />
        <!-- This is required and is for receiving notification bar message click events. Developers do not need to handle the event. Only registration is required. -->
        <action android:name="com.huawei.intent.action.PUSH_DELAY_NOTIFY"/>
    </intent-filter>
</receiver>
```

#### Step 3.4: Register the Huawei push service in the app

If you choose to enable the Huawei push service, you need to call `HMSAgent.init` in `onCreate` of Application to initialize the Huawei push service.

After successful registration, you will receive the registration result in `onToken` of the BroadcastReceiver customized in [Step 3.3](#Step3_3). The `token` in it is the unique identifier of the current app on the current device, which needs to be recorded.

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

Obtain the token from the main UI:

```
if (IMFunc.isBrandHuawei()) {
	// Huawei offline push
    HMSAgent.connect(this, new ConnectHandler() {
    @Override
    public void onConnect(int rst) {
        QLog.i(TAG, "huawei push HMS connect end:" + rst);
        }
    });
    getHuaWeiPushToken();
}
```

<span id="Step4"></span>
### Step 4: Report the push information to the IM server

If you need to use Huawei push to push IM message notifications, after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **token** returned by the Huawei push service, to the IM server.
> After the token and certificate ID are correctly reported, IM service binds users with the corresponding device information. This enables the use of the Huawei push service to push notifications.

Sample code in the demo:

- Define the certificate ID constant
```java
/**
 * First, define some constant information in Constants.java
 */
/****** Start of Huawei offline push parameters ******/
 // Use your certificate ID in the Huawei push certificate information in IM console
public static final long HW_PUSH_BUZID = 6666;
// APPID assigned by the Huawei Developers Alliance
public static final String HW_PUSH_APPID = "1234567890"; // See the manifest file
/****** End of Huawei offline push parameters ******/
```

- Report the push certificate ID and token
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
        this.mThirdPushToken = mThirdPushToken;  // Here, the token value is specified. Describe it based on the aforementioned custom BroadcastReciever class documentation.
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

After the certificate ID and token are successfully reported, the IM server sends messages through Huawei push notifications to the user when the app has been killed but the user has not logged out of IM.

>
> - Huawei push does not guarantee 100% success in reaching target users.
> - Huawei push may be delayed. Usually, this is related to the timing of app killing. In some cases, it is related to the Huawei push service.
> - If the IM user has logged out or was forced logout by the IM server (for example, due to login on another terminal), the device will not receive push messages.

<span id="click"></span>
## Configuring the Notification Bar Message Click Event
You can choose to **Open App**, **Open Web Page**, or **Open Specified Interface in App** to follow the notification bar message click event.

### Opening the app
The default option is **Open App**.


 ### Opening webpages
When [adding a certificate](#Step2), you need to choose **Open Web Page** and enter a website starting with `http://` or `https://`, for example, `https://cloud.tencent.com/document/product/269`.


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

### If the app uses obfuscation, how can I prevent exceptions when using the Huawei offline push feature?

If your app uses obfuscation, to prevent exceptions when using the Huawei offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
> The following code is an official sample from Huawei. Please modify it based on your actual situation before use.

```
-ignorewarning
-keepattributes *Annotation*
-keepattributes Exceptions
-keepattributes InnerClasses
-keepattributes Signature
-keepattributes SourceFile,LineNumberTable
-keep class com.hianalytics.android.**{*;}
-keep class com.huawei.updatesdk.**{*;}
-keep class com.huawei.hms.**{*;}
-keep class com.huawei.android.hms.agent.**{*;}  
# Replace com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver with the complete class name defined in your app.
-keep com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver {*;}
```

### Can I customize push notification sounds?

Currently, Huawei push does not support custom notification sounds.

### How can I identify the cause to failures to receive push messages?
1. No push service guarantees 100% success in reaching target users and zero vendor push exceptions. Therefore, if one or two push messages fail to reach users during a fast and continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. According to the push process, confirm whether the Huawei push certificate information is correctly configured in [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [Huawei push SDK integration](#Step3) configuration is correct and that you have obtained the token.
4. Confirm that you have [reported push information](#Step4) to the IM server correctly.
5. Manually kill the app on your device, send several messages, and check whether you can receive notifications within one minute.
6. If you still cannot receive push messages after the preceding steps, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the specific `time`, `SDKAppID`, `certificate ID`, and `push receiving UserID` for processing.
