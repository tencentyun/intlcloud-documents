## Offline Push Process
The process of implementing offline message push is as follows:
1. Register with the vendor and complete the developer verification process. Apply to enable the push service.
2. Create a push service and bind app information to obtain the push certificate, password, key, and other data.
3. Log in to the [IM Console](https://console.qcloud.com/avc) to upload the certificate and enter other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Integrate the push messaging SDK provided by the vendor with your project and configure it according to the vendor’s instructions.
5. Send your certificate ID and device information to IM server. 
6. When the client App is killed by the system or user without IM logout, the IM server will remind the user via message push.

## Configuring Offline Push
Huawei EMUI is a highly customized Android system with strict backend policies. By default, third-party apps do not have auto-start permissions. As apps running in the background are often forcibly killed by the system, we recommend that the Huawei push service be integrated on Huawei devices. The Huawei push service is part of the Huawei Mobile Service (HMS) and a system-grade service of EMUI. Its delivery rate is higher than those of third-party push services. Currently, **IM only supports the notification bar messages of Huawei push**.

>
>- This guide was prepared with direct reference to the official documentation of Huawei push. If Huawei push is changed, please refer to the [official website of Huawei push](https://developer.huawei.com/consumer/cn/hms/huawei-pushkit).
>- If you do not plan to implement a Huawei-specific offline push solution, skip this section.

### Step 1: Apply for a Huawei push certificate
1. Access the [official website of the Huawei Developers Alliance](https://developer.huawei.com/consumer/cn/), register an account, and pass the developer verification.
2. Log in to the console of the Huawei Developers Alliance, choose **App Service** -> **Development Service** -> **PUSH**, and create a Huawei push service app.
 When applying for the Huawei push service, you need to provide a maximum of five SHA256 fingerprints for the app signature certificates. After the Huawei push service app is created, you can view detailed app information on the app details page.
<span id="Step1_3"></span>
3. Record the **`Package name`**, **`APP ID`**, and **`APP Secret`** information.

<span id="Step2"></span>
### Step 2: Generate a certificate ID

1. Log in to the [IM Console](https://console.qcloud.com/avc) and click the desired app. The app configuration page appears.
2. Click **Add a certificate** under **Android push configuration**.
 > If you already have a certificate and only want to change its information, you can click **Edit** in **Android push configuration** to modify and update the certificate.
 >
3. Use the information you obtained in [Step 1](#Step1_3) to configure the following parameters:
 - **Push platform**: select **Huawei**.
 - **Package name**: the name of the Huawei Push service app.
 - **AppID**: enter the **App ID** you got from Huawei Push.
 - **AppSecret**: enter the **APP SECRET** you got from Huawei Push.
 - **Badge Parameter**: enter the complete class name of `Activity` for the app entry as the application badge on Huawei Desktop. For more information, see [Interface Description for Badging on Huawei Desktop](https://developer.huawei.com/consumer/cn/doc/development/system-References/30802)
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open App**, **Open URL**, and **Open specific App interface**. For more information, refer to [Configuring the Notification Bar Message Click Event](#click).
    **Open App** or **Open specific App interface** allows [custom content pass through](#section4).
4. Click **OK** to save the information. Certificate information takes effect 10 minutes after you save it.
5. Record the Certificate ID once it is generated.

<span id="Step3"></span>
### Step 3: Integrate push SDK

>
> - The default title of IM push notifications is `a new message`.
> - Before reading this section, make sure that you have integrated and tested the IM SDK.
> - You can find a sample for Huawei push implementation in our demo. Note that the features of Huawei push may be adjusted during Huawei push version updates. If you find any inconsistencies with the content of this section, please refer to the [official website of Huawei push](https://developer.huawei.com/consumer/cn/hms/huawei-pushkit) and notify us of the difference so that we can make the necessary modifications in time.

#### Step 3.1: Download the Huawei Push SDK and reference it in your project

1. Visit the [official website of Huawei push](https://developer.huawei.com/consumer/cn/hms/huawei-pushkit) to download the **HMS Agent**.
2. Decompress the HMS Agent.
3. Copy the files under `hmsagents\src\main\java` to your project’s src\main\java directory.
 ![](https://main.qcloudimg.com/raw/3c9bca5dea731eeb4cb70e73e56d28b4.png)
4. Use Gradle to integrate the Huawei push SDK. Add the following code in the build.gradle of your project:
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
    // Huawei Push SDK. Replace 2.6.3.301 with the actual version number.
    implementation 'com.huawei.android.hms:push:2.6.3.301'
    // If an error occurs indicating that com.huawei.hms.api does not exist, this line of code also needs to be added. Note that the version number must be the same.
    // implementation 'com.huawei.android.hms:base:2.6.3.301'
}
```

#### Step 3.2: Modify AndroidManifest.xml
1. Add necessary permissions for Huawei Push:

```xml
<!--HMS-SDK guides the upgrade of the HMS feature. Accessing the OTA server requires network permissions-->    
<uses-permission android:name="android.permission.INTERNET" />    
<!--HMS-SDK guides the upgrade of the HMS feature. Saving the downloaded upgrade package requires the SD card write permissions-->    
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />    
<!--Check the network status-->  
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>  
<!--Check the Wi-Fi status-->  
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>  
<!--Obtain the user’s mobile phone IMEI to uniquely mark the user-->  
<uses-permission android:name="android.permission.READ_PHONE_STATE"/> 

<!--If the Android version is 8.0 with targetSdkVersion>=26 for application compilation configuration, you must add the following permissions -->
<uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />

<!--Change com.tencent.qcloud.tim.tuikit to your App package name.-->
<permission
    android:name="com.tencent.qcloud.tim.tuikit.permission.PROCESS_PUSH_MSG"
    android:protectionLevel="signatureOrSystem"/>
<uses-permission android:name="com.tencent.qcloud.tim.tuikit.permission.PROCESS_PUSH_MSG" />
<!--Change com.tencent.qcloud.tim.tuikit to your App package name.-->
```

2. Add the following content under application. For a detailed description, see the [official website of Huawei push](https://developer.huawei.com/consumer/cn/hms/huawei-pushkit).

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
#### Step 3.3: Define a BroadcastReceiver class

To receive messages, you need to customize a BroadcastReceiver inherited from the `PushReceiver` class, implement the `onToken` method in it, and register this receiver to AndroidManifest.xml.

The following is sample code from the demo:

```java
public class HUAWEIPushReceiver extends PushReceiver {
    private static final String TAG = "HUAWEIPushReceiver";

    @Override
    public void onToken(Context context, String token, Bundle extras) {
        Log.i(TAG, "onToken:" + token);
        ThirdPushTokenMgr.getInstance().setThirdPushToken(token);  // The token is passed in here. It needs to be used for subsequent reporting of push information.
        ThirdPushTokenMgr.getInstance().setPushTokenToTIM();
    }
}
```

Register the custom BroadcastReceiver to AndroidManifest.xml:

```xml
<!--Here, change com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver to the complete class name in your App-->
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver"
    android:permission="com.tencent.qcloud.tim.tuikit.permission.PROCESS_PUSH_MSG">
    <intent-filter>
        <!-- Required; used for receiving the token -->
        <action android:name="com.huawei.android.push.intent.REGISTRATION" />
        <!-- Required; used for receiving pass-through messages -->
        <action android:name="com.huawei.android.push.intent.RECEIVE" />
        <!-- Required; used for receiving notification bar message click events. Developers do not need to handle the event. Only registration is required.-->
        <action android:name="com.huawei.intent.action.PUSH_DELAY_NOTIFY"/>
    </intent-filter>
</receiver>
```

#### Step 3.4: Register Huawei Push in your App

If you choose to enable the Huawei push service, you need to call `HMSAgent.init` in `onCreate` of the Application to initialize the Huawei push service.

After successful registration, you will receive the registration result in `onToken` of the BroadcastReceiver customized in [Step 3.3](#Step3_3). The `token` in it is the unique identifier of the current App on the current device. Please record the `token` information.

The following is sample code from the demo:

```java
public class DemoApplication extends Application {

    private static PojoApplication instance;

    @Override
    public void onCreate() {
        super.onCreate();
        // Determine whether this is the main thread
        if (SessionWrapper.isMainProcess(getApplicationContext())) {
            /**
             * TUIKit initialization function
             *
             * @param context  App context, usually corresponds to ApplicationContext
             * @param sdkAppID The SDKAppID assigned to you when registering the App in Tencent Cloud
             * @param configs  Relevant configuration items of TUIKit. Usually, you can use the default configuration. For special configuration, refer to the API Documentation.
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

Obtaining the token from the main interface:

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

If you need to use Huawei push to push IM message notifications, then after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **token** returned by the Huawei push service to the IM server.
> After the token and certificate ID are correctly reported, IM service binds users with the corresponding device information. This enables the use of the Huawei push service to push notifications.

The following is sample code from the demo:

- Define Certificate ID as a constant:
```java
/**
 * We first define some constant information in Constants.java.
 */
/****** Huawei offline push parameters start ******/
 // Use your certificate ID in the Huawei push certificate information on the IM console
public static final long HW_PUSH_BUZID = 6666;
// APPID assigned by the Huawei Developers Alliance
public static final String HW_PUSH_APPID = "1234567890"; // See the checklist.
/****** Huawei offline push parameters end ******/
```

- Report the push certificate ID and token:
```java
/**
 * Report the push certificate ID and device information in ThirdPushTokenMgr.java
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
        this.mThirdPushToken = mThirdPushToken;  // token value is specified here. Describe it in accordance with the above-mentioned custom BroadcastReciever class documentation.
    }

    public void setPushTokenToTIM(){
        String token = ThirdPushTokenMgr.getInstance().getThirdPushToken();
        if(TextUtils.isEmpty(token)){
            QLog.i(TAG, "setPushTokenToTIM third token is empty");
            mIsTokenSet = false;
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

After the certificate ID and token are successfully reported, the IM server sends messages via Huawei push notifications to the user when the App has been killed but the user has not logged out of IM.

>
> - Huawei push is not 100% successful in reaching the target users.
> - Huawei push may be delayed. Usually, this is related to the timing of App killing. In some cases, it is related to the Huawei push service.
> - If the IM user has logged out or been forced offline by the IM server (for example, due to login on another device), the device cannot receive push messages.

<span id="click"></span>
## Configuring the Notification Bar Message Click Event
You can select one of the following events: **Open App**, **Open URL**, or **Open specific App interface**.

### Open App
This is the default event, which opens the App once the notification bar message is clicked.

 ### Open URL
You need to select **Open URL** in [Step 2: Add a certificate](#Step2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

### Open specific App interface
1. In manifest, configure the `intent-filter` of the Activity to be opened. The sample code is as follows:
  
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

3. Select **Open specific App interface** in [Step 2: Add a certificate](#Step2) and enter the result above.

<span id="section4"></span>
## Custom Content Pass Through
Select **Open App** or **Open specific App interface** when configuring **Click event** in [Step 2: Add a certificate](#Step2) to support custom content pass through.

### Step 1: Custom content configuration (Sender)
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

### Step 2: Custom content configuration (receiver)
The client will obtain the custom content from the corresponding `Activity` once the notification bar message is clicked.

  ```
  Bundle bundle = getIntent().getExtras();
  String extContent = bundle.get("ext");
  ```

## FAQs

### If the App uses obfuscation, how can I prevent exceptions in the Huawei offline push feature?

If your App uses obfuscation, to prevent exceptions in the Huawei offline push feature, you need to keep the custom BroadcastReceiver and add obfuscation rules by referring to the following:
> The following code is an official sample from Huawei. Please modify it according to your actual situation before use.

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
# Change com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver to the complete class name defined in your App.
-keep com.tencent.qcloud.tim.demo.thirdpush.HUAWEIPushReceiver {*;}
```

### Can I set a custom notification sound?

Huawei does not support custom notification sounds.

### I cannot receive push messages. What should I do?
1. No push service is 100% successful in reaching target users, and vendor push is no exception. Therefore, if one or two push messages fail to reach users during a fast, continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. According to the push process, confirm whether the Huawei push certificate information is correctly configured on the [IM console](https://console.qcloud.com/avc).
3. Confirm that your project’s [Huawei push SDK integration](#Step3) configuration is correct and that you have obtained the token.
4. Confirm that you have [reported push information](#Step4) to the IM server correctly.
5. Manually kill the App on your device, send a few messages, and confirm whether you receive notifications within one minute.

