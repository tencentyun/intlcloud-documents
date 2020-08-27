## Overview

Instant Messaging (IM) end users need to obtain latest messages at all times. However, due to the limited performance and battery power of mobile devices, when the app is running in the background, IM recommends that you use system-grade push channels provided by vendors for message notifications to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

Currently, IM supports various offline push services including Mi Push, Huawei Push, Meizu Push, vivo Push, OPPO Push, and Google FCM Push.

<table> 
   <tr> 
     <th nowrap="nowrap">Push Channel</th> 
     <th nowrap="nowrap">System Requirements</th> 
     <th>Conditions</th> 
   </tr> 
   <tr> 
     <td>Mi Push</td> 
     <td>MIUI</td> 
     <td>Use Mi Push MiPush_SDK_Client_3_6_12.jar.</td> 
   </tr> 
   <tr> 
     <td>Huawei Push</td> 
     <td>EMUI</td> 
     <td>Use Huawei mobile service versions 20401300 and later, and the SDK version is push:2.6.3.301.</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap">Google FCM Push</td> 
     <td nowrap="nowrap">Android 4.1 and later</td> 
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
     <td>Not all OPPO models and versions support OPPO push. The required SDK version is mcssdk-2.0.2.jar.</td> 
   </tr>  
   <tr> 
     <td nowrap="nowrap">vivo Push</td> 
     <td nowrap="nowrap">FuntouchOS</td> 
     <td>Not all vivo models and versions support vivo push. The required SDK version is vivo_pushsdk_v2.3.1.jar.</td> 
   </tr> 
</table>

Here, "offline" means that the app is closed by the system or user without logging out. In such cases, if you want to receive IM SDK message reminders, you can integrate IM offline push.

>Users who have logged out normally or have been forced offline will not receive any message notifications.

The process of implementing offline message push is as follows:

1. Register with the vendor, apply to enable the push service, and create an app. Obtain information such as the AppID, AppKey, and AppSecret.
2. Integrate the push SDK provided by the vendor into your project. Use the vendor’s console to test notification messages to ensure that the SDK has been correctly integrated.
3. Log in to the [IM console](https://console.qcloud.com/avc) to upload the certificate and complete other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Send your certificate ID and device information to the IM server.

When the client app is killed by the system or user without IM logout, the IM server will push the messages sent by other accounts through the vendor’s channel.

## Mi Push

### Configuring the push certificate

<span id="xiaomiStep1_1"></span>

1. Access the [official website of Mi open platform](https://dev.mi.com/console/) to register for an account and pass the developer verification. Log in to the console of the Mi open platform, choose **App Service** > **Push Service**, and create a MiPush service app. Take note of the **`Primary package name`**, **`AppID`**, and **`AppSecret`**.
   <span id="xiaomiStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information obtained in [step 1](#Step1_1) to configure the following parameters:

 - **Push Platform**: choose **Mi**.
 - **Package name**: indicates the name of the MiPush service app.
 - **AppID**: enter the **AppID** obtained from MiPush.
 - **AppSecret**: enter the **AppSecret** obtained from MiPush.
 - **Click event**: indicates the event that is triggered after the notification bar message is clicked. Valid values are **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Events](#xiaomi_click).
   **Open app** and **Open specific app interface** allow [custom content passthrough](#xiaomi_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Integration Guide for Mi Push](https://dev.mi.com/console/doc/detail?pId=41) to integrate the SDK. Use the Mi console to test notification messages to ensure that the SDK has been correctly integrated.
2. Call `MiPushClien.registerPush` to initialize the MiPush service. After the push service is registered, you will receive the registration result in `onReceiveRegisterResult` of the custom `BroadcastReceiver`. Here, `regId` indicates the unique identifier of the current app running on the current device. After logging in to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via FCM notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

If you choose **Open app**, the onNotificationMessageClicked method of MI will be called back, and the app itself can process app opening in this method.

#### Open URL

You need to select **Open URL** in [step 2](#xiaomiStep1_2) and enter a URL that starts with `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specific app interface

1. Open the manifest file in a text editor and configure the `intent-filter` of the Activity that you want to open, as shown below:

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

3. Select **Open specific app interface** in [step 2](#xiaomiStep1_2) and enter the preceding result.

<span id="xiaomi_custom"></span>

### Custom content passthrough

Select **Open app** or **Open specific app interface** when configuring **Click event** in [step 2](#Step2) to support custom content passthrough.

**Step 1: Custom content configuration (sender)**
Set custom content for the notification bar message before sending the message.

- Example for Android:

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

- For information on configurations for the IM server, see the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: Custom content configuration (receiver)**

- If you selected **Open app** in [step 2](#xiaomiStep1_2), clicking the notification bar message triggers the `onNotificationMessageClicked(Context context, MiPushMessage miPushMessage)` callback. The custom content can be obtained from `miPushMessage`.

  ```
  Map extra = miPushMessage.getExtra();
  String extContent = extra.get("ext");
  ```

- If you selected **Open app** in [step 2](#xiaomiStep1_2), `MiPushMessage`, which is the object that encapsulates the message, is passed to the client through `Intent`. The client then obtains the custom content from `Activity`.

  ```
    Bundle bundle = getIntent().getExtras(); 
    MiPushMessage miPushMessage = (MiPushMessage)bundle.getSerializable(PushMessageHelper.KEY_MESSAGE); 
    Map extra = miPushMessage.getExtra(); 
    String extContent = extra.get("ext");
  ```

## Huawei Push

### Configuring the push certificate

<span id="huaweiStep1_1"></span>

1. Visit the [official website of the Huawei Developers Alliance](https://developer.huawei.com/consumer/cn/), register for an account, and pass the developer verification. Log in to the console of the Huawei Developers Alliance, choose **App Service** > **Development Service** > **PUSH**, and create a Huawei push service app. Take note of the **`Package name`**, **`APP ID`**, and **`APP SECRET`**.
   <span id="huaweiStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information that you obtained in [step 1](#huaweiStep1_1) to configure the following parameters:

 - **Push platform**: select **Huawei**.
 - **Package name**: indicates the name of the Huawei Push service app.
 - **AppID**: enter the **App ID** obtained from Huawei Push.
 - **AppSecret**: enter the **APP SECRET** obtained from Huawei Push.
 - **Badge Parameter**: enter the complete class name of `Activity` for the app entry as the application badge on Huawei Desktop. For more information, see [Interface Description for Badging on Huawei Desktop](https://developer.huawei.com/consumer/cn/doc/development/system-References/30802)
 - **Click event**: indicates the event that is triggered after the notification bar message is clicked. Valid values are **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Events](#huawei_click).
   **Open app** and **Open specific app interface** allow [custom content passthrough](#huawei_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Integration Guide for Huawei Push](https://developer.huawei.com/consumer/cn/doc/development/HMS-3-Guides/push-Preparations) to integrate the SDK. Use the Huawei console to test notification messages to ensure that the SDK has been correctly integrated.
2. Call Huawei `HmsInstanceId.getToken` to obtain `Push Token`, which is the unique identifier of the current app running on the current device. After logging in to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **Push Token** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via Huawei Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [step 2](#huaweiStep1_2) and enter a URL that starts with `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specific app interface

1. Open the manifest file in a text editor and configure the `intent-filter` of the Activity that you want to open, as shown below:

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

3. Select **Open specific app interface** in [step 2](#huaweiStep1_2) and enter the preceding result.

<span id="huawei_custom"></span>

### Custom content passthrough

Due to the compatibility issues of Huawei Push, some devices cannot receive the passed-through content. We are working on this issue with Huawei and will provide an example as soon as we come to the solution.
	

## OPPO Push

### Configuring the push certificate

<span id="oppoStep1_1"></span>

1. See [How to Enable OPPO Push](https://open.oppomobile.com/wiki/doc#id=10195) for instructions on how to enable OPPO Push. Log in to the [OPPO push platform](https://push.oppo.com/) and choose **Configuration Management** > **App Configuration** to view detailed app information. Take note of the `AppId`, `AppKey`, `AppSecret`, and `MasterSecret`.
   <span id="oppoStep1_2"></span>

2. Official OPPO documentation states that ChannelIDs are required for push messages on Android 8.0 and later for OPPO. Therefore, you need to create a ChannelID for your app. The following gives a sample code that creates a ChannelID called `tuikit`:

   ```
   public void createNotificationChannel(Context context) {
   				// Create the NotificationChannel, but only on API 26+ because
   				// the NotificationChannel class is new and not in the support library.
   				if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
   						CharSequence name = "oppotest";
   						String description = "this is opptest";
   						int importance = NotificationManager.IMPORTANCE_DEFAULT;
   						NotificationChannel channel = new NotificationChannel("tuikit", name, importance);
   						channel.setDescription(description);
   						// Register the channel with the system, and you cannot change the importance
   						// or other notification behaviors after this.
   						NotificationManager notificationManager = context.getSystemService(NotificationManager.class);
   						notificationManager.createNotificationChannel(channel);
   				}
   		}
   ```

   <span id="oppoStep1_3"></span>

3. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information that you obtained in [step 1](#oppoStep1_1) to configure the following parameters:

 - **Push platform**: select **OPPO**.
 - **AppKey**: enter the **AppKey** obtained from OPPO PUSH.
 - **AppID**: enter the **AppID** obtained from OPPO PUSH.
 - **MasterSecret**: enter the **MasterSecret** obtained from OPPO PUSH.
 - **ChannelID**: enter the **ChannelID** generated in step 2.
 - **Click event**: indicates the event that is triggered after the notification bar message is clicked. Valid values are **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Events](#oppo_click).
   **Open app** and **Open specific app interface** allow [custom content passthrough](#oppo_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in [OPPO PUSH SDK API documentation](https://open.oppomobile.com/wiki/doc#id=10196) to integrate the SDK. Use the OPPO console to test notification messages to ensure that the SDK has been correctly integrated.
2. Use `PushManager.getInstance().register(…)`, which is part of the OPPO PUSH SDK, to initialize the Opush service.
   After the push service is registered, you can obtain `regId` from the `onRegister` callback method of `PushCallback`. Here, `regId` is the unique identifier of the app running on the current device. After logging in to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via OPPO Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="oppo_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [step 2](#oppoStep1_3) and enter a URL that starts with `http` or `https`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specific app interface

You can open a specific app interface in one of the following ways:

**Activity** (recommended)
  This method is very simple. To use it, enter the whole name of an Activity, such as `com.tencent.qcloud.tim.demo.SplashActivity`.

**Intent action**

1. Open AndroidManifest in a text editor and configure the Activity as follows. Note that you must add a category without data.

```
<intent-filter>
		<action android:name="android.intent.action.VIEW" />
		<category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```

2. Enter `android.intent.action.VIEW` in the console.

<span id="oppo_custom"></span>

### Custom content passthrough

Select **Open app** or **Open specific app interface** when configuring **Click event** in [step 2](#oppoStep1_3) to support custom content passthrough.

**Step 1: Custom content configuration (sender)**
Set custom content for the notification bar message before sending the message.

- Example for Android:

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

- For information on configurations for the IM server, see the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: Custom content configuration (receiver)**
The client obtains the custom content from the started `Activity` once the notification bar message is clicked.

```
Bundle bundle = intent.getExtras();
	Set<String> set = bundle.keySet();
	if (set != null) {
			for (String key : set) {
				// Here, the key and value correspond to extKey and ext content set in step 1.
					String value = bundle.getString(key);
					Log.i("oppo push custom data", "key = " + key + ":value = " + value);
			}
	}
```

## vivo Push

### Configuring the push certificate

<span id="vivoStep1_1"></span>

1. Visit the [official website of vivo open platform](https://dev.vivo.com.cn/home) and register for an account. Complete the developer verification. Log in to the console of the vivo open platform, choose **Message Push** > **Create** > **Test Push**, and create a vivo push service app. Take note of the **APP ID**, **APP key**, and **APP secret**.
   <span id="vivoStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information that you obtained in [step 1](#vivoStep1_1) to configure the following parameters:

 - **Push platform**: select **vivo**.
 - **AppKey**: enter the **AppKey** obtained from vivo Push.
 - **AppID**: enter the **AppID** obtained from vivo Push.
 - **AppSecret**: enter the **APP secret** obtained from vivo Push.
 - **Click event**: indicates the event that is triggered after the notification bar message is clicked. Valid values are **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Events](#vivo_click).
   **Open app** and **Open specific app interface** allow [custom content passthrough](#vivo_custom).
   Click **OK** to save the information. Take note of the **ID** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Integration Guide for vivo Push](https://dev.vivo.com.cn/documentCenter/doc/233#w2-08354405) to integrate the SDK. Use the vivo console to test notification messages to ensure that the SDK has been correctly integrated.
2. Call `PushClient.getInstance(getApplicationContext()).initialize()` to initialize the vivo push service and call `PushClient.getInstance(getApplicationContext()).turnOnPush()` to enable the push service. You will then obtain `regId` from the `onReceiveRegId` of `BroadcastReceiver`. Here, `regId` is the unique identifier of the current app running on the current device. After logging in to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom11tencent11imsdk11v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via vivo Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="vivo_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [step 2](#vivoStep1_2) and enter a URL that starts with `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specific app interface

1. Open the manifest file in a text editor and configure the `intent-filter` of the Activity that you want to open, as shown below:

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

3. Select **Open specific app interface** in [step 2](#vivoStep1_2) and enter the preceding result.

<span id="vivo_custom"></span>

### Custom content passthrough

Select **Open app** or **Open specific app interface** when configuring **Click event** in [step 2](#vivoStep1_2) to support custom content passthrough.

**Step 1: Custom content configuration (sender)**
Set custom content for the notification bar message before sending the message.

- Example for Android:

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

- For information on configurations for the IM server, see the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: Custom content configuration (receiver)**
Clicking a notification bar message triggers a callback of `onNotificationMessageClicked(Context context, UPSNotificationMessage upsNotificationMessage)`, which is part of the vivo Push SDK. The custom content can be obtained from the value of `upsNotificationMessage`.

```
Map<String, String> paramMap = upsNotificationMessage.getParams();
String extContent = paramMap.get("ext");
```

## Meizu Push

### Configuring the push certificate

<span id="meizuStep1_1"></span>

1. Visit the [official website of Meizu open platform](http://open.flyme.cn) to register for an account and pass the developer verification. Log in to the Meizu console, choose **Development Service** > **Flyme Push**, and create a Meizu push service app. Take note of the **`app package name`**, **`App ID`**, and **`App Secret`**.
   <span id="meizuStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information that you obtained in [step 1](#meizuStep1_1) to configure the following parameters:

 - **Push Platform**: select **Meizu**.
 - **App Package Name**: enter the **App package name** of the Meizu push service app.
 - **AppID**: enter the **App ID** of the Meizu push service app.
 - **AppSecret**: enter the **App Secret** of the Meizu push service app.
 - **Click event**: indicates the event that is triggered after the notification bar message is clicked. Valid values are **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Events](#meizu_click).
   **Open app** and **Open specific app interface** allow [custom content passthrough](#meizu_custom).
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in the [Meizu Push Access Guide](http://open-wiki.flyme.cn/doc-wiki/index#id?129) to integrate the SDK. Use the Meizu console to test notification messages to ensure that the SDK has been correctly integrated.
2. Call `PushManager.register` to initialize the Meizu push service. After the push service is registered, you will receive the registration result in `onRegisterStatus` of the custom `BroadcastReceiver`. Here, `registerStatus.getPushId()` is the unique identifier of the current app running on the current device. After logging in to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **PushId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via Meizu Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="meizu_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [step 2](#meizuStep1_2) and enter a URL that starts with `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.

#### Open specific app interface

When [adding a certificate](#meizuStep1_2), you need to select **Open specific app interface** and enter the complete class name of the Activity to be opened, for example, `com.tencent.qcloud.tim.demo.chat.ChatActivity`.

<span id="xiaomi_custom"></span>

### Custom content passthrough

Select **Open app** or **Open specific app interface** when configuring **Click event** in [step 2](#Step2) to support custom content passthrough.

**Step 1: Custom content configuration (sender)**
Set custom content for the notification bar message before sending the message.

- Example for Android:

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

- For information on configurations for the IM server, see the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: Custom content configuration (receiver)**

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
2. Log in to the [Firebase console](https://console.firebase.google.com) and click your app card to go to the app configuration page. Click <img src="https://main.qcloudimg.com/raw/0d062411405553c9fae29f8e0daf02ad.png"  style="margin:0;"> to the right of "Project Overview" and choose **Project Settings** > **Firebase Cloud Messaging**. Take note of the **Legacy Server Key** and **Sender ID**.
   <span id="fcmStep1_2"></span>
3. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information that you obtained in [step 1](#fcmStep1_2) to configure the following parameters:

 - **Push Platform**: select **Google**.
 - **Application Package Name**: enter the name of the client app package.
 - **Sender ID**: enter the **Sender ID** of the Google push service app.
 - **Legacy Server Key**: enter the **Legacy Server Key** of the Google push service app.
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect 10 minutes after you save it.

### Integrating the push SDK

1. Follow the instructions in [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/android/client) to set up Firebase and integrate the FCM SDK. Refer to the [FCM Testing Guide](https://firebase.google.com/docs/cloud-messaging/android/first-message?authuser=0) to test notification messages to ensure that FCM has been correctly integrated.
2. Call `FirebaseInstanceId.getInstance().getInstanceId()`. Then, obtain the token that is the unique identifier of the current app running on the current device from the callback. After logging in to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **token** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via FCM notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_custom"></span>

### Custom content passthrough

Select **Open app** or **Open specific app interface** when configuring **Click event** in [step 2](#Step2) to support custom content passthrough.

**Step 1: Custom content configuration (sender)**
Set custom content for the notification bar message before sending the message.

>
> OPPO requires custom data to be in JSON format, otherwise push notifications cannot be received.

- Example for Android:

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

- For information on configurations for the IM server, see the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527). 

**Step 2: Custom content configuration (receiver)**
The client obtains the custom content from the corresponding `Activity` once the notification bar message is clicked.

```
Bundle bundle = getIntent().getExtras();
String value = bundle.getString("ext"); 
```

## Setting Custom iOS Push Alert Sounds

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use the [setIOSSound](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#acffd09150398b06c3d7eb42baee5aee1) API in `V2TIMOfflinePushInfo` to set the sound for push notifications on iOS devices.

## Setting Custom Display for Offline Push

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use [setTitle](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a7d4a73d6a1db487dd96f658bdbc98ae9) and [setDesc](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) in `V2TIMOfflinePushInfo` to set the title and content of notification bar messages respectively.

## Setting Custom Click-to-Redirect Logic

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use [setExt](https://docs-1252463788.cos.ap-shanghai.myqcloud.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a9346ecab2e35ff516b24c27b0584a9a2) in `V2TIMOfflinePushInfo` to set custom content. When the user receives notification bar messages and starts the app, the user will be redirected to the UI as specified by `ext`.

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
  // After starting the app, Vinson obtains the custom content from the opened `Activity`.
  Bundle bundle = intent.getExtras();
  Set<String> set = bundle.keySet();
  if (set != null) {
  	for (String key : set) {
  		// The key and value correspond to extKey and ext content set in step 1.
  		String value = bundle.getString(key);
  		if (value.equals("jump to denny")) {
  			// Jump to the chat window with Denny.
  			...
  		}
  	}
  }
  ```

## FAQs

### How do I set a custom sound for push notifications on Android mobile phones?

Currently, most vendors do not support setting a custom sound for push notifications, and therefore this feature is currently not supported by the IM SDK.

### Why cannot I receive push notifications on an OPPO mobile phone?

Generally, this happens due to one of the following reasons:

- According to OPPO’s requirements, mobile phones running Android 8.0 or later must be configured with ChannelID, otherwise pushed messages cannot be displayed. See [OPPO Push Configuration](#oppoStep1_2) for configuration details.
- If the [passed-through custom offline push content](#oppo_custom) of messages is not in JSON format, OPPO mobile phones cannot receive push notifications.

### Why does not offline push work for custom messages?

The offline push feature for custom messages is different from ordinary messages. Since we are not able to resolve the content of custom messages and determine what to push, we simply do not push custom messages by default. If you do need to enable offline push for custom messages, set the [desc](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field of [offlinePushInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) when calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe). Then, the content of desc will be used for display during offline push.

