## Overview

IM terminal users need to obtain the latest messages at all times. However, due to the limited performance and battery power of mobile devices, when the app is running in the background, IM recommends that you use the system-grade push channels provided by vendors for message notifications to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

Currently, Instant Messaging (IM) supports various offline push services including Mi Push, Huawei Push, Meizu Push, Vivo Push, OPPO Push, and Google FCM Push.

<table> 
   <tr> 
     <th nowrap="nowrap">Push Channel</th> 
     <th nowrap="nowrap">System Requirements</th> 
     <th>Conditions</th> 
   </tr> 
   <tr> 
     <td>Mi Push</td> 
     <td>MIUI</td> 
     <td>Use MiPush MiPush_SDK_Client_3_6_12.jar.</td> 
   </tr> 
   <tr> 
     <td>Huawei Push</td> 
     <td>EMUI</td> 
     <td>Huawei mobile service versions 20401300 and later, SDK version: push:2.6.3.301</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap">Google FCM Push</td> 
     <td nowrap="nowrap">Android 4.1 and later versions</td> 
     <td>The mobile phone needs to install Google Play Services and be used outside Mainland China.</td> 
   </tr> 
   <tr> 
     <td>Meizu Push</td> 
     <td>Flyme</td> 
     <td>Use Meizu Push push-internal:3.6.+.</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap">OPPO Push</td> 
     <td>ColorOS</td> 
     <td>Not all OPPO models and versions support OPPO push. SDK version: mcssdk-2.0.2.jar</td> 
   </tr>  
   <tr> 
     <td nowrap="nowrap">vivo Push</td> 
     <td nowrap="nowrap">FuntouchOS</td> 
     <td>Not all vivo models and versions support vivo push. SDK version: vivo_pushsdk_v2.3.1.jar.</td> 
   </tr> 
</table>

Here, "offline" means that the app is closed by the system or user without logging out. In such cases, if you want to receive IM SDK message reminders, you can integrate IM offline push.

>Users who have logged out normally or have been forced offline will not receive any message notifications.

The process of implementing offline message push is as follows:

1. Register with the vendor, apply to enable the push service, and create an app. Obtain information such as the AppID, AppKey, and AppSecret.
2. Integrate the push SDK provided by the vendor into your project. Use the vendor's console to test notification messages to ensure the SDK was integrated properly.
3. Log in to the [IM Console](https://console.cloud.tencent.com/im) to upload the certificate and enter other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Send your certificate ID and device information to the IM server.

When the client app is killed by the system or user without IM logout, the IM server will push the messages sent by other accounts through the vendor's channel.

## Mi Push

### Configuring the push certificate

<span id="xiaomiStep1_1"></span>

1. Access the [MI open platform website](https://dev.mi.com/console/) to register an account and pass the developer verification. Log in to the console of the MI open platform, choose **App Service** -> **Push Service**, and create a Mi Push service app. Take note of the **`Primary package name`**, **`AppID`**, and **`AppSecret`** information.
   <span id="xiaomiStep1_2"></span>
2. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add Certificate** under **Android Platform Push Settings**. Use the information you obtained in [step 1](#Step1_1) to configure the following parameters:

 - **Push Platform**: choose **Xiaomi**.
 - **SDKAppID**: the name of the Mi Push service app.
 - **APPID**: enter the **App ID** you got from Mi Push.
 - **AppSecret**: enter the **App Secret** you got from Mi Push.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open webpage**, and **Open specified in-app page**. For more information, refer to [Configuring Click Events](#xiaomi_click).
   **Open Application** and **Open specified in-app page** allow [custom content pass through](#xiaomi_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Integration Guide for Mi Push](https://dev.mi.com/console/doc/detail?pId=41) to integrate the SDK. Use the Mi console to test notification messages to ensure the SDK was integrated properly.
2. Call `MiPushClien.registerPush` to initialize the Mi Push service. After the push service is registered, you will receive the registration result in `onReceiveRegisterResult` of the custom `BroadcastReceiver`. `regId` is the unique identifier of the current app running on the current device. After logging in to the IM SDK, [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) needs to be called to report the **Certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages through Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_click"></span>

### Configuring click events

You can select one of the following events: **Open Application**, **Open webpage**, or **Open specified in-app page**.

#### Open application

If you choose **Open Application**, the Xiaomi onNotificationMessageClicked method is called back. Apps can be opened using this method.

#### Open webpage

You need to select **Open webpage** in [Step 2: add a certificate](#xiaomiStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specified in-app page

1. Open manifest in a text editor and configure the `intent-filter` of the `Activity` you want to open as shown:

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

3. Select **Open specified in-app page** in [Step 2: add a certificate](#xiaomiStep1_2) and enter the result above.

<span id="xiaomi_custom"></span>

### Custom content pass through

Select **Open Application** or **Open specified in-app page** when configuring **Click event** in [Step 2: add a certificate](#Step2) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Sample on Android:

  ```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("extKey", "ext content");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();
  
  V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
  v2TIMOfflinePushInfo.setExt(extContent.getBytes());
  V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, userID, null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
  	@Override
  	public void onError(int code, String desc) {}
  	@Override
  	public void onSuccess(V2TIMMessage v2TIMMessage) {}
  	@Override
  	public void onProgress(int progress) {}
  });
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: custom content configuration (receiver)**

- If you selected **Open Application** when configuring **Click event** in [Step 2: add a certificate](#xiaomiStep1_2), clicking the notification bar message triggers the `onNotificationMessageClicked(Context context, MiPushMessage miPushMessage)` callback. The custom content can be obtained from `miPushMessage`.

  ```
  Map extra = miPushMessage.getExtra();
  String extContent = extra.get("ext");
  ```

- If you selected **Open specified in-app page** when configuring **Click event** in [Step 2: add a certificate](#xiaomiStep1_2), `MiPushMessage`, which is the object that encapsulates the message, is passed to the client through `Intent`. The client then obtains the custom content from `Activity`.

  ```
    Bundle bundle = getIntent().getExtras(); 
    MiPushMessage miPushMessage = (MiPushMessage)bundle.getSerializable(PushMessageHelper.KEY_MESSAGE); 
    Map extra = miPushMessage.getExtra(); 
    String extContent = extra.get("ext");
  ```

## Huawei Push

### Configuring the push certificate

<span id="huaweiStep1_1"></span>

1. Access the [official website of the Huawei Developers Alliance](https://developer.huawei.com/consumer/cn/), register an account, and pass the developer verification. Log in to the console of the Huawei Developers Alliance, choose **App Service** -> **Development Service** -> **PUSH**, and create a Huawei push service app. Take note of the **`Package name`**, **`APP ID`**, and **`APP SECRET`**.
   <span id="huaweiStep1_2"></span>
2. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add Certificate** under **Android Platform Push Settings**. Use the information you obtained in [step 1](#huaweiStep1_1) to configure the following parameters:

 - **Push Platform**: select **Huawei**.
 - **SDKAppID**: the name of the Huawei Push service app.
 - **APPID**: enter the **App ID** you got from Huawei Push.
 - **AppSecret**: enter the **APP Secret** you got from Huawei Push.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open Application**, **Open webpage**, and **Open specified in-app page**. For more information, see [Configuring Click Events](#huawei_click).
   **Open Application** and **Open specified in-app page** allow [custom content pass through](#huawei_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Integration Guide for Huawei Push](https://developer.huawei.com/consumer/cn/doc/development/HMS-3-Guides/push-Preparations) to integrate the SDK. Use the Huawei console to test notification messages to ensure the SDK was integrated properly.
2. Call Huawei `HmsInstanceId.getToken` to get `Push Token`, which is the unique identifier of the current app running on the current device. After logging in to the IM SDK, [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) needs to be called to report the **Certificate ID** and **Push Token** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages through Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_click"></span>

### Configuring click events

You can select one of the following events: **Open Application**, **Open webpage**, or **Open specified in-app page**.

#### Open application

This is the default event, which opens the App once the notification bar message is clicked.

#### Open webpage

You need to select **Open webpage** in [Step 2: add a certificate](#huaweiStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specified in-app page

1. Open manifest in a text editor and configure the `intent-filter` of the `Activity` you want to open as shown:

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

3. Select **Open specified in-app page** in [Step 2: add a certificate](#huaweiStep1_2) and enter the result above.

<span id="huawei_custom"></span>

### Custom content pass through

Due to the compatibility issues of Huawei Push, some machines cannot receive the content that is passed through. We are working on this issue with Huawei and will provide an example here as soon as we have the solution.
	

## OPPO Push

### Configuring the push certificate

<span id="oppoStep1_1"></span>

1. Refer to [How to enable OPPO Push](https://open.oppomobile.com/wiki/doc#id=10195) for instructions on how to enable OPPO Push. Go to [OPPO push platform](https://push.oppo.com/) -> **Configuration Management** -> **App Configuration** to view detailed app information. Take note of the `AppId`, `AppKey`, `AppSecret`, and `MasterSecret`.
   <span id="oppoStep1_2"></span>

2. The official OPPO documentation states that ChannelIDs are required for pushing messages on OPPO Android 8.0 and above. Therefore, create a ChannelID for your app. Below is a sample code that creates a ChannelID called `tuikit`:

   ```
   public void createNotificationChannel(Context context) {
   				// Create the NotificationChannel, but only on API 26+ because
   				// the NotificationChannel class is new and not in the support library
   				if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
   						CharSequence name = "oppotest";
   						String description = "this is opptest";
   						int importance = NotificationManager.IMPORTANCE_DEFAULT;
   						NotificationChannel channel = new NotificationChannel("tuikit", name, importance);
   						channel.setDescription(description);
   						// Register the channel with the system; you can't change the importance
   						// or other notification behaviors after this
   						NotificationManager notificationManager = context.getSystemService(NotificationManager.class);
   						notificationManager.createNotificationChannel(channel);
   				}
   		}
   ```

   <span id="oppoStep1_3"></span>

3. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add Certificate** under **Android Platform Push Settings**. Use the information you obtained in [step 1](#oppoStep1_1) to configure the following parameters:

 - **Push Platform**: select **OPPO**.
 - **AppKey**: enter the **AppKey** you got from OPPO PUSH.
 - **APPID**: enter the **App ID** you got from OPPO PUSH.
 - **MasterSecret**: enter the **MasterSecret** you got from OPPO PUSH.
 - **ChannelID**: enter the **ChannelID** generated in the previous step.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open Application**, **Open webpage**, and **Open specified in-app page**. For more information, refer to [Configuring Click Events](#oppo_click).
   **Open Application** and **Open specified in-app page** allow [custom content pass through](#oppo_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [OPPO PUSH SDK API documentation](https://open.oppomobile.com/wiki/doc#id=10196) to integrate the SDK. Use the OPPO console to test notification messages to ensure the SDK was integrated properly.
2. Use `PushManager.getInstance().register(…)`, which is part of the OPPO PUSH SDK, to initialize the Opush service.
   After the push service is registered, you will get the `regId` from the `onRegister` callback method of `PushCallback`. `regId` is the unique identifier of the app running on the current device. After logging in to the IM SDK, [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) needs to be called to report the **Certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages through Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="oppo_click"></span>

### Configuring click events

You can select one of the following events: **Open Application**, **Open webpage**, or **Open specified in-app page**.

#### Open application

This is the default event, which opens the App once the notification bar message is clicked.

#### Open webpage

You need to select **Open webpage** when you [add a certificate](#oppoStep1_3) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specified in-app page

These are the ways you can open a specific app interface:

**Activity** (recommended)
  This is rather simple. Enter the whole name of an `Activity`, such as `com.tencent.qcloud.tim.demo.SplashActivity`

**Intent action**

1. Open AndroidManifest with a text editor and configure the `Activity`, as follows. You must add category but no data.

```
<intent-filter>
		<action android:name="android.intent.action.VIEW" />
		<category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```

2. Enter `android.intent.action.VIEW` in the console.

<span id="oppo_custom"></span>

### Custom content pass through

Select **Open Application** or **Open specified in-app page** when configuring **Click event** in [adding a certificate](#oppoStep1_3) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Sample on Android:

  ```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("extKey", "ext content");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();
  
  V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
  v2TIMOfflinePushInfo.setExt(extContent.getBytes());
  V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, userID, null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
  	@Override
  	public void onError(int code, String desc) {}
  	@Override
  	public void onSuccess(V2TIMMessage v2TIMMessage) {}
  	@Override
  	public void onProgress(int progress) {}
  });
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: custom content configuration (receiver)**
The client will obtain the custom content from the started `Activity` once the notification bar message is clicked.

```
Bundle bundle = intent.getExtras();
	Set<String> set = bundle.keySet();
	if (set != null) {
			for (String key : set) {
				// key and value correspond to extKey and ext content set in Step 1
					String value = bundle.getString(key);
					Log.i("oppo push custom data", "key = " + key + ":value = " + value);
			}
	}
```

## Vivo Push

### Configuring the push certificate

<span id="vivoStep1_1"></span>

1. Visit the [vivo open platform official website](https://dev.vivo.com.cn/home) and register for an account. Complete developer verification. Log in to the console of the vivo open platform, choose **Message Push** -> **Create** -> **Test Push**, and create a vivo push service app. Take note of the **APP ID**, **APP key**, and **APP secret**.
   <span id="vivoStep1_2"></span>
2. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add Certificate** under **Android Platform Push Settings**. Use the information you obtained in [step 1](#vivoStep1_1) to configure the following parameters:

 - **Push Platform**: select **Vivo**.
 - **AppKey**: enter the **AppKey** you got from vivo Push.
 - **APPID**: enter the **App ID** you got from vivo Push.
 - **AppSecret**: enter the **APP Secret** you got from vivo Push.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open Application**, **Open webpage**, and **Open specified in-app page**. For more information, refer to [Configuring Click Events](#vivo_click).
   **Open Application** and **Open specified in-app page** allow [custom content pass through](#vivo_custom).
   Click **OK** to save the information. Take note of the **ID** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Integration Guide for vivo Push](https://dev.vivo.com.cn/documentCenter/doc/233#w2-08354405) to integrate the SDK. Use the vivo console to test notification messages to ensure the SDK was integrated properly.
2. Call `PushClient.getInstance(getApplicationContext()).initialize()` to initialize the vivo push service and call `PushClient.getInstance(getApplicationContext()).turnOnPush()` to enable the push service. You will then get `regId` from `onReceiveRegId` of `BroadcastReceiver`. `regId` is the unique identifier of the current app running on the current device. After logging in to the IM SDK, [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom11tencent11imsdk11v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) needs to be called to report the **Certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages through Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="vivo_click"></span>

### Configuring click events

You can select one of the following events: **Open Application**, **Open webpage**, or **Open specified in-app page**.

#### Open application

This is the default event, which opens the App once the notification bar message is clicked.

#### Open webpage

You need to select **Open webpage** in [Step 2: add a certificate](#vivoStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specified in-app page

1. Open manifest in a text editor and configure the `intent-filter` of the `Activity` you want to open as shown:

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

3. Select **Open specified in-app page** in [Step 2: add a certificate](#vivoStep1_2) and enter the result above.

<span id="vivo_custom"></span>

### Custom content pass through

Select **Open Application** or **Open specified in-app page** when configuring **Click event** in [Step 2: add a certificate](#vivoStep1_2) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Sample on Android:

  ```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("extKey", "ext content");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();
  
  V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
  v2TIMOfflinePushInfo.setExt(extContent.getBytes());
  V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, userID, null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
  	@Override
  	public void onError(int code, String desc) {}
  	@Override
  	public void onSuccess(V2TIMMessage v2TIMMessage) {}
  	@Override
  	public void onProgress(int progress) {}
  });
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: custom content configuration (receiver)**
Clicking a notification bar message triggers a callback of `onNotificationMessageClicked(Context context, UPSNotificationMessage upsNotificationMessage)`, which is part of the vivo Push SDK. The custom content can be obtained from the value of `upsNotificationMessage`.

```
Map<String, String> paramMap = upsNotificationMessage.getParams();
String extContent = paramMap.get("ext");
```

## Meizu Push

### Configuring the push certificate

<span id="meizuStep1_1"></span>

1. Access the [Meizu open platform website](http://open.flyme.cn) to register an account and pass the developer verification. Log in to the Meizu console, choose **Development Service** -> **Flyme Push**, and create a Meizu push service app. Take note of the **`app package name`**, **`App ID`**, and **`App Secret`**.
   <span id="meizuStep1_2"></span>
2. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add Certificate** under **Android Platform Push Settings**. Use the information you obtained in [step 1](#meizuStep1_1) to configure the following parameters:

 - **Push Platform**: choose **Meizu**.
 - **SDKAppID**: enter the **App package name** of the Meizu push service app.
 - **APPID**: enter the **App ID** of the Meizu push service app.
 - **AppSecret**: enter the **App Secret** of the Meizu push service app.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open Application**, **Open webpage**, and **Open specified in-app page**. For more information, refer to [Configuring Click Events](#meizu_click).
   **Open Application** and **Open specified in-app page** allow [custom content pass through](#meizu_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Meizu Push Access Guide](http://open-wiki.flyme.cn/doc-wiki/index#id?129) to integrate the SDK. Use the Meizu console to test notification messages to ensure the SDK was integrated properly.
2. Call `PushManager.register` to initialize the Meizu push service. After the push service is registered, you will receive the registration result in `onRegisterStatus` of the custom `BroadcastReceiver`. `registerStatus.getPushId()` is the unique identifier of the current app running on the current device. After logging in to IM SDK, [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) needs to be called to report the **Certificate ID** and **PushId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages through Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="meizu_click"></span>

### Configuring click events

You can select one of the following events: **Open Application**, **Open webpage**, or **Open specified in-app page**.

#### Open application

This is the default event, which opens the App once the notification bar message is clicked.

#### Open webpage

You need to select **Open webpage** in [Step 2: add a certificate](#meizuStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specified in-app page

When you [add a certificate](#meizuStep1_2), choose **Open specified in-app page** and enter the complete class name of the `Activity` to be opened, for example, `com.tencent.qcloud.tim.demo.chat.ChatActivity`.

<span id="meizu_custom"></span>

### Custom content pass through

Select **Open Application** or **Open specified in-app page** when configuring **Click event** in [Step 2: add a certificate](#meizuStep1_2) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Sample on Android:

  ```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("extKey", "ext content");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();
  
  V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
  v2TIMOfflinePushInfo.setExt(extContent.getBytes());
  V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, userID, null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
  	@Override
  	public void onError(int code, String desc) {}
  	@Override
  	public void onSuccess(V2TIMMessage v2TIMMessage) {}
  	@Override
  	public void onProgress(int progress) {}
  });
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: custom content configuration (receiver)**

Clicking a notification bar message triggers a callback of `onNotificationClicked(Context context, MzPushMessage mzPushMessage)`, which is part of the Meizu Push SDK. The custom content can be obtained from the value of `mzPushMessage`.

```
String extContent = mzPushMessage.getSelfDefineContentString();
```

Alternatively, the client can obtain the custom content from the opened `Activity`.

```
Bundle bundle = getIntent().getExtras();
String extContent = bundle.getString("ext"); 
```

## Google FCM Push

### Integrating the SDK

<span id="fcmStep1_1"></span>
1. Register with [Firebase Cloud Messaging](https://firebase.google.com) and create an app.
<span id="fcmStep1_2"></span>
2. Log in to the [Firebase console](https://console.firebase.google.com) and click your app card to go to the app configuration page. Click <img src="https://main.qcloudimg.com/raw/0d062411405553c9fae29f8e0daf02ad.png"  style="margin:0;"> on the right side of Project Overview and choose **Project Settings** -> **Service Account**. Click **Generate New Private Key** to download the private key.
<span id="fcmStep1_3"></span>
3. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add Certificate** under **Android Platform Push Settings**. Upload the private key you obtained in [step 2](#fcmStep1_2).
4. Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/android/client) to set up Firebase and integrate the FCM SDK. Refer to the [FCM Testing Guide](https://firebase.google.com/docs/cloud-messaging/android/first-message?authuser=0) to test notification messages to ensure FCM was integrated properly.
2. Call `FirebaseInstanceId.getInstance().getInstanceId()`, and from the callback, get the token which is the unique identifier of the current app running on the current device. After logging in to IM SDK, [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) needs to be called to report the **Certificate ID** and **token** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages through Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="fcm_custom"></span>

### Custom content pass through

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Sample on Android:

  ```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("extKey", "ext content");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();
  
  V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
  v2TIMOfflinePushInfo.setExt(extContent.getBytes());
  V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, userID, null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
  	@Override
  	public void onError(int code, String desc) {}
  	@Override
  	public void onSuccess(V2TIMMessage v2TIMMessage) {}
  	@Override
  	public void onProgress(int progress) {}
  });
  ```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: custom content configuration (receiver)**
The client will obtain the custom content from the corresponding `Activity` once the notification bar message is clicked.

```
Bundle bundle = getIntent().getExtras();
String value = bundle.getString("ext"); 
```

## Setting Custom iOS Push Alert Sounds

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use the [setIOSSound](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#acffd09150398b06c3d7eb42baee5aee1) API in `V2TIMOfflinePushInfo` to set the sound for push notifications on iOS devices.

## Setting Custom Display for Offline Push

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use [setTitle](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a7d4a73d6a1db487dd96f658bdbc98ae9) and [setDesc](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) in `V2TIMOfflinePushInfo` to set the title and content of notification bar messages respectively.

## Setting Custom Click-to-Redirect Logic

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use [setExt](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a9346ecab2e35ff516b24c27b0584a9a2) in `V2TIMOfflinePushInfo` to set the custom content. When the user receives notification bar messages and starts the app, the user will be redirected to the UI as specified by `ext`.

The following example assumes that Denny sends a message to Vinson.

- Sender: Denny needs to set `ext` before sending a message.

  ```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("action", "jump to denny");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();
  V2TIMOfflinePushInfo v2TIMOfflinePushInfo = new V2TIMOfflinePushInfo();
  v2TIMOfflinePushInfo.setExt(extContent.getBytes());
  
  V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "vinson", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false,  v2TIMOfflinePushInfo, new V2TIMSendCallback<V2TIMMessage>() {
  	@Override
  	public void onError(int code, String desc) {}
  	@Override
  	public void onSuccess(V2TIMMessage v2TIMMessage) {}
  	@Override
  	public void onProgress(int progress) {}
  });
  ```

- Recipient: although Vinson's app is not online, it can still receive the notification messages pushed offline by mobile phone vendors (for example, OPPO). When Vinson clicks the pushed message, the app is started.

  ```
  // After starting the app, Vinson obtains the custom content from the opened Activity.
  Bundle bundle = intent.getExtras();
  Set<String> set = bundle.keySet();
  if (set != null) {
  	for (String key : set) {
  		// key and value correspond to extKey and ext content set in Step 1
  		String value = bundle.getString(key);
  		if (value.equals("jump to denny")) {
  			// Go to the chat window with Denny
  			...
  		}
  	}
  }
  ```

## FAQs

### How do you set a custom sound for push notifications on Android phones?

Currently, most vendors do not support setting a custom sound for push notifications, therefore it is not supported by the IM SDK.

### Why can't OPPO phones receive push notifications?

Generally, this happens due to one of the following reasons:

- According to OPPO's requirements, mobile phones running Android 8.0 and higher must be configured with ChannelID, otherwise pushed messages cannot be displayed. See [OPPO Push Configuration](#oppoStep1_2) for configuration details.
- If the [passed through custom offline push content](#oppo_custom) of messages is not in the JSON format, OPPO phones cannot receive push notifications.

### Why doesn't offline push work for custom messages?

The offline push feature for custom messages is different from ordinary messages. Since we are not able to resolve the content of custom messages and determine what to push, we simply do not push custom messages by default. If you want to enable offline push for custom messages, set the [desc](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field of [offlinePushInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) when calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe). Then the content of desc will be used for display during offline push.

