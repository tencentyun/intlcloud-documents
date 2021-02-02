## Overview

IM terminal users need to obtain the latest messages at any time. However, due to the limited performance and battery power of mobile devices, when the app is running in the background, IM recommends that you use the system-grade push channels provided by vendors for message notifications to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

IM currently supports Mi Push, Huawei Push, Meizu Push, vivo Push, OPPO Push, and Google FCM Push. The vendor channel dependencies used by IM are provided and maintained by [TPNS](https://intl.cloud.tencent.com/product/tpns) in a unified manner, without the need for extra integration of vendor channels. After you add the vendor channel dependencies of [TPNS](https://intl.cloud.tencent.com/product/tpns), you can use the IM offline push feature. If you use only the IM offline push feature, no extra cost will be incurred. The vendor channels currently supported are as follows:

>? If you need to improve the push delivery rate or implement diversified push, we recommend that you install the [SDK](https://intl.cloud.tencent.com/document/product/1024/34673) of [TPNS](https://intl.cloud.tencent.com/product/tpns) to enjoy the complete push service. If you use IM and [TPNS](https://intl.cloud.tencent.com/product/tpns) at the same time, you do not need to repeatedly integrate vendor channels.
<table> 
   <tr> 
     <th nowrap="nowrap">Push Channel</th> 
     <th nowrap="nowrap">System Requirements</th> 
     <th>Conditions</th> 
   </tr> 
   <tr> 
     <td>Mi Push</td> 
     <td>MIUI</td> 
     <td>To use Mi Push, add the dependency: implementation 'com.tencent.tpns:xiaomi:1.2.1.2-release'.
</td> 
   </tr> 
   <tr> 
     <td>Huawei Push</td> 
     <td>EMUI</td> 
     <td>To use Huawei Push, add the dependencies: implementation 'com.tencent.tpns:huawei:1.2.1.2-release' and implementation 'com.huawei.hms:push:5.0.2.300'.
</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap">Google FCM Push</td> 
     <td nowrap="nowrap">Android 4.1 and later versions</td> 
     <td>To use mobile phones installed with Google Play Services outside the Chinese mainland, add the dependency: implementation 'com.google.firebase:firebase-messaging:20.2.3'.
</td> 
   </tr> 
   <tr> 
     <td>Meizu Push</td> 
     <td>Flyme</td> 
     <td>To use Meizu Push, add the dependency: implementation 'com.tencent.tpns:meizu:1.2.1.2-release'.
</td> 
   </tr> 
   <tr> 
     <td nowrap="nowrap">OPPO Push</td> 
     <td>ColorOS</td> 
     <td>Not all OPPO models and versions support OPPO Push. To use OPPO Push, add the dependency: implementation 'com.tencent.tpns:oppo:1.2.1.2-release'.
</td> 
   </tr>  
   <tr> 
     <td nowrap="nowrap">vivo Push</td> 
     <td nowrap="nowrap">FuntouchOS</td> 
     <td>Not all vivo models and versions support vivo Push. To use vivo Push, add the dependency: implementation 'com.tencent.tpns:vivo:1.2.1.2-release'.
</td> 
   </tr> 
</table>

Here, “offline” means that the app is closed by the system or user without logging out. In such cases, if you want to receive IM SDK message reminders, you can integrate IM offline push.

>!
>- Users who have logged out or have been forced offline will not receive any message notifications.
>- For Mi and Huawei vendors, if a ChannelID has been configured on the official website of the vendor developer, you need to configure the same ChannelID on the [IM console](https://console.qcloud.com/avc). Otherwise, push may fail. If you do not configure the ChannelID, you will be limited by the frequency limit.

The process of implementing offline message push is as follows:

1. Register with the vendor, apply to enable the push service and create an app. Obtain information such as AppID, AppKey, and AppSecret.
2. Integrate the push SDK provided by the vendor with your project. Use the vendor’s console to test notification messages to ensure the SDK was integrated properly.
3. Log in to the [IM console](https://console.qcloud.com/avc) and specify the push certificate and relevant information. The IM server will generate a unique certificate ID for each certificate.
4. Send your certificate ID and device information to IM server.

When the client app is killed by the system or user without IM logout, the IM server will push the messages sent by other accounts through vendor’s channel.

## Mi Push

### Configuring the push certificate

<span id="xiaomiStep1_1"></span>

1. Access the [Mi open platform website](https://dev.mi.com/console/) to register an account and pass the developer verification. Log in to the console of the Mi open platform, choose **App Service** > **Push Service**, and create a MiPush service app. Take note of the **`Primary package name`**, **`AppID`**, and **`AppSecret`** information.
   ![](https://main.qcloudimg.com/raw/7a291196c6f4800d5d1c9b9e23aed617.jpg)
   <span id="xiaomiStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information you obtained in [step 1](#Step1_1) to configure the following parameters:

 - **Push Platform**: choose **Mi**.
 - **Package name**: the name of the MiPush service app.
 - **AppID**: enter the **AppID** you got from MiPush.
 - **AppSecret**: enter the **AppSecret** you got from MiPush.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Event](#xiaomi_click).
   **Open app** or **Open specific app interface** allows [custom content pass through(#xiaomi_custom).
    ![](https://main.qcloudimg.com/raw/b9acf23fb00144aa86be20dba7627699.png)
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect within 10 minutes after you save it.
    ![](https://main.qcloudimg.com/raw/2a28ec48998579c84a3f3786c9a4b667.png)

### Integrating the push SDK
1. Add the Mi dependency: implementation 'com.tencent.tpns:xiaomi:1.2.1.2-release'.
2. Refer to the [Integration Guide for Mi Push](https://dev.mi.com/console/doc/detail?pId=41), and use the Mi console to test notification messages to ensure that the SDK was integrated properly.
3. Call `MiPushClient.registerPush` to initialize the Mi Push service. After successful registration, you will receive the registration result in `onReceiveRegisterResult` of the custom `BroadcastReceiver`. `regId` is the unique identifier of the current app on the current device. After successful login to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via Mi Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

If you choose **Open app**, the `onNotificationMessageClicked` method of Mi will be called back, and the app itself can process app opening in this method.
![](https://main.qcloudimg.com/raw/fa0fbe98e40da37808a1d646b313783c.png)

#### Open URL

You need to select **Open URL** in [Step 2: add a certificate](#xiaomiStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/bb336d3e2bd799b4dfe443833782e322.png)

#### Open specific app interface

1. In manifest, configure the `intent-filter` of the Activity to be opened. See the sample code below. You can refer to [AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/AndroidManifest.xml) of the demo:

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

3. Select **Open specific app interface** in [Step 2: add a certificate](#xiaomiStep1_2) and enter the result above.
   ![](https://main.qcloudimg.com/raw/26a2bb370cfb5525f3eb1ddeef47c490.png)

<span id="xiaomi_custom"></span>

### Custom content pass through

Select **Open app** or **Open specific app interface** when configuring **Click event** in [Step 2: add a certificate](#Step2) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Below is a simple example on the Android platform. You can also refer to the corresponding logic in the `sendMessage()` method in the [ChatManagerKit.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/base/ChatManagerKit.java) class in the TUIKit:

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

- If you selected **Open app** in [Step 2: add a certificate](#xiaomiStep1_2), clicking the notification bar message triggers the `onNotificationMessageClicked(Context context, MiPushMessage miPushMessage)` callback. The custom content can be obtained from `miPushMessage`. You can refer to the parsing implementation in [XiaomiMsgReceiver.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/XiaomiMsgReceiver.java).

  ```
  Map extra = miPushMessage.getExtra();
  String extContent = extra.get("ext");
  ```

- If you selected **Open specific app interface** in [Step 2: add a certificate](#xiaomiStep1_2), `MiPushMessage`, which is the object that encapsulates the message, is passed to the client through `Intent`. The client then obtains the custom content from `Activity`. You can refer to the implementation of the `parseOfflineMessage(Intent intent)` method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class.

  ```
    Bundle bundle = getIntent().getExtras(); 
    MiPushMessage miPushMessage = (MiPushMessage)bundle.getSerializable(PushMessageHelper.KEY_MESSAGE); 
    Map extra = miPushMessage.getExtra(); 
    String extContent = extra.get("ext");
  ```

## Huawei Push

### Configuring the push certificate

<span id="huaweiStep1_1"></span>

1. Access the [official website of the Huawei Developers Alliance](https://developer.huawei.com/consumer/cn/), register an account, and pass the developer verification. Log in to the console of the Huawei Developers Alliance, choose **App Service** > **Development Service** > **PUSH**, and create a Huawei push service app. Take note of the **`Package name`**, **`APP ID`**, and **`APP SECRET`**.
   ![](https://main.qcloudimg.com/raw/50d36c2cfb7a32acefd8ace44e1ef71f.png)
   <span id="huaweiStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information you obtained in [step 1](#huaweiStep1_1) to configure the following parameters:

 - **Push platform**: select **Huawei**.
 - **Package name**: the name of the Huawei Push service app.
 - **AppID**: enter the **App ID** you got from Huawei Push.
 - **AppSecret**: enter the **APP SECRET** you got from Huawei Push.
 - **Badge Parameter**: enter the full `Activity` class name of the app entry, which will be used as the Huawei desktop app badge for display. See [Huawei Desktop Badge Development Guide](https://developer.huawei.com/consumer/cn/doc/development/system-References/30802).
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, refer to [Configuring Click Event](#huawei_click).
   **Open app** or **Open specific app interface** allows [custom content pass through(#huawei_custom).
    ![](https://main.qcloudimg.com/raw/852b40d2a8a5aacd4327f94130976563.png)
   Click **Save** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect within 10 minutes after you save it.
   ![](https://main.qcloudimg.com/raw/4f4b2a5c01c524d13434f0b5ca4c4b2c.png)

### Integrating the push SDK
1. Add the Huawei dependencies: implementation 'com.tencent.tpns:huawei:1.2.1.2-release' and implementation 'com.huawei.hms:push:5.0.2.300'.
2. Refer to the [Integration Guide for Huawei Push](https://developer.huawei.com/consumer/cn/doc/development/HMS-3-Guides/push-Preparations) and use the Huawei console to test notification messages to ensure that the SDK was integrated properly.
3. Call the Huawei `HmsInstanceId.getToken` API to request the unique app identifier Push Token from the server. `Push Token` is the unique identifier of the current app on the current device. After successful login to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **Push Token** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via Huawei Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="xiaomi_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [Step 2: add a certificate](#huaweiStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/bb336d3e2bd799b4dfe443833782e322.png)

#### Open specific app interface

1. In manifest, configure the `intent-filter` of the Activity to be opened. See the sample code below. You can refer to [AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/AndroidManifest.xml) of the demo:

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

3. Select **Open specific app interface** in [Step 2: add a certificate](#huaweiStep1_2) and enter the result above.

<span id="huawei_custom"></span>

### Custom content pass through

>! Due to the compatibility issues of Huawei Push, the pass-through content can only be received on some EUI10+ devices.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Below is a simple example on the Android platform. You can also refer to the corresponding logic in the `sendMessage()` method in the [ChatManagerKit.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/base/ChatManagerKit.java) class in the TUIKit:

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

- If you selected **Open app** or **Open specific app interface** in [Step 1: add a certificate](#huaweiStep1_1), the client can obtain the custom content from `Activity` when the notification bar message is clicked. You can refer to the parseOfflineMessage(Intent intent) implementation method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class.

```
Bundle bundle = getIntent().getExtras();
String value = bundle.getString("ext"); 
```


## OPPO Push

### Configuring the push certificate

<span id="oppoStep1_1"></span>

1. Refer to [How to enable OPPO Push](https://open.oppomobile.com/wiki/doc#id=10195) for instructions on how to enable OPPO Push. Go to [OPPO push platform](https://push.oppo.com/) > **Configuration Management** > **App Configuration** to view detailed app information. Take note of `AppId`, `AppKey`, `AppSecret`, and `MasterSecret`.
   <span id="oppoStep1_2"></span>

2. The official OPPO documentation states that ChannelIDs are required for push messages on OPPO Android 8.0 and above. Therefore, create a ChannelID for your app. Below is a sample code that creates a ChannelID called `tuikit`:

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

   <span id="oppoStep1_3"></span>

3. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information you obtained in [step 1](#oppoStep1_1) to configure the following parameters:

 - **Push platform**: select **OPPO**.
 - **AppKey**: enter the **AppKey** you got from OPPO PUSH.
 - **AppID**: enter the **AppID** you got from OPPO PUSH.
 - **MasterSecret**: enter the **MasterSecret** you got from OPPO PUSH.
 - **ChannelID**: enter the **ChannelID** generated in Step 2.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, refer to [Configuring Click Event](#oppo_click).
   **Open app** or **Open specific app interface** allows [custom content pass through(#oppo_custom).
    ![](https://main.qcloudimg.com/raw/8b94fde206c9fa8cd0dee774e12df0ac.png)
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect within 10 minutes after you save it.
    ![](https://main.qcloudimg.com/raw/23dc3500472be773bf5499299e511444.png)

### Integrating the push SDK
1. Add the OPPO dependency: implementation 'com.tencent.tpns:oppo:1.2.1.2-release'.
2. Refer to the [OPPO PUSH SDK API Documentation](https://open.oppomobile.com/wiki/doc#id=10704) and use the OPPO console to test notification messages to ensure that the SDK was integrated properly.
3. Call `HeytapPushManager.register(…)` in the OPPO SDK to initialize the Opush service.
   After successful registration, you can obtain `regId` in the `onRegister` callback method of `ICallBackResultService`. `regId` is the unique identifier of the current app on the current device. After successful login to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via OPPO Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="oppo_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [Step 2](#oppoStep1_3) and enter a URL that starts with either `http` or `https`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/bb336d3e2bd799b4dfe443833782e322.png)

#### Open specific app interface

These are the ways you can open a specific app interface:

**Activity** (recommended)
  This is rather simple. Enter the whole name of an Activity, such as `com.tencent.qcloud.tim.demo.SplashActivity`

**Intent action**

1. In AndroidManifest, set the following configuration in the Activity to be opened and add category without data. You can refer to [AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/AndroidManifest.xml) of the demo:

```
<intent-filter>
		<action android:name="android.intent.action.VIEW" />
		<category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```

2. Enter `android.intent.action.VIEW` in the console.

<span id="oppo_custom"></span>

### Custom content pass through

Select **Open app** or **Open specific app interface** when configuring **Click event** in [Step 2: add a certificate](#oppoStep1_3) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Below is a simple example on the Android platform. You can also refer to the corresponding logic in the `sendMessage()` method in the [ChatManagerKit.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/base/ChatManagerKit.java) class in the TUIKit:

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
When the notification bar message is clicked, the client can obtain the custom content from the launched `Activity`. You can refer to the `parseOfflineMessage(Intent intent)` implementation method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class.

```
Bundle bundle = intent.getExtras();
	Set<String> set = bundle.keySet();
	if (set != null) {
			for (String key : set) {
				// key and value correspond to extKey and ext content set in Step 1.
					String value = bundle.getString(key);
					Log.i("oppo push custom data", "key = " + key + ":value = " + value);
			}
	}
```

## vivo Push

### Configuring the push certificate

<span id="vivoStep1_1"></span>

1. Visit the [vivo open platform official website](https://dev.vivo.com.cn/home) and register for an account. Complete developer verification. Log in to the console of the vivo open platform, choose **Message Push** > **Create** > **Test Push**, and create a vivo push service app. Take note of **APP ID**, **APP key**, and **APP secret**.
   <span id="vivoStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information you obtained in [step 1](#vivoStep1_1) to configure the following parameters:

 - **Push platform**: select **vivo**.
 - **AppKey**: enter the **AppKey** you got from vivo Push.
 - **AppID**: enter the **AppID** you got from vivo Push.
 - **AppSecret**: enter the **APP secret** you got from vivo Push.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, refer to [Configuring Click Event](#vivo_click).
   **Open app** or **Open specific app interface** allows [custom content pass through(#vivo_custom).
    ![](https://main.qcloudimg.com/raw/ac890d834dd7f069f936094180634cd7.png)
   Click **OK** to save the information. Take note of the **ID** of the certificate. Certificate information takes effect 10 minutes after you save it.
    ![](https://main.qcloudimg.com/raw/3442e00debac668c42fa4be89903ac90.png)

### Integrating the push SDK
1. Add vivo dependency: implementation 'com.tencent.tpns:vivo:1.2.1.2-release'.
2. Refer to the [Integration Guide for vivo Push](https://dev.vivo.com.cn/documentCenter/doc/233#w2-08354405), and use the vivo console to test notification messages to ensure that the SDK was integrated properly.
3. Call `PushClient.getInstance(getApplicationContext()).initialize()` to initialize the vivo Push service and call `PushClient.getInstance(getApplicationContext()).turnOnPush()` to launch push. If this succeeds, you will receive the `regId` in the `onReceiveRegId` of the custom `BroadcastReceiver`. `regId` is the unique identifier of the current app on the current device. After successful login to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom11tencent11imsdk11v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **regId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via vivo Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="vivo_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the app once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [Step 2: add a certificate](#vivoStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/bb336d3e2bd799b4dfe443833782e322.png)

#### Open specific app interface

1. In manifest, configure the `intent-filter` of the Activity to be opened. See the sample code below. You can refer to [AndroidManifest.xml](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/AndroidManifest.xml) of the demo:

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

3. Select **Open specific app interface** in [Step 2: add a certificate](#vivoStep1_2) and enter the result above.

<span id="vivo_custom"></span>

### Custom content pass through

Select **Open app** or **Open specific app interface** when configuring **Click event** in [Step 2: add a certificate](#vivoStep1_2) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Below is a simple example on the Android platform. You can also refer to the corresponding logic in the `sendMessage()` method in the [ChatManagerKit.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/base/ChatManagerKit.java) class in the TUIKit:

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
When the notification bar message is clicked, the `onNotificationMessageClicked(Context context, UPSNotificationMessage upsNotificationMessage)` callback of the vivo Push SDK is triggered. The custom content can be obtained from `upsNotificationMessage`. You can refer to the parsing implementation in [VIVOPushMessageReceiverImpl.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/VIVOPushMessageReceiverImpl.java).

```
Map<String, String> paramMap = upsNotificationMessage.getParams();
String extContent = paramMap.get("ext");
```

## Meizu Push

### Configuring the push certificate

<span id="meizuStep1_1"></span>

1. Access the [Meizu open platform website](http://open.flyme.cn) to register an account and pass the developer verification. Log in to the Meizu console, choose **Development Service** > **Flyme Push** and create a Meizu push service app. Take note of the **`app package name`**, **`App ID`**, and **`App Secret`**.
   ![](https://main.qcloudimg.com/raw/e0674cc1bca92fd549c03a3523b2144c.png)
   <span id="meizuStep1_2"></span>
2. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Use the information you obtained in [step 1](#meizuStep1_1) to configure the following parameters:

 - **Push Platform**: choose **Meizu**.
 - **App Package Name**: enter the **App package name** of the Meizu push service app.
 - **AppID**: enter the **App ID** of the Meizu push service app.
 - **AppSecret**: enter the **App Secret** of the Meizu push service app.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, refer to [Configuring Click Event](#meizu_click).
   **Open app** or **Open specific app interface** allows [custom content pass through(#meizu_custom).
    ![](https://main.qcloudimg.com/raw/7151cfff6d8e82a41bfb9b718a49bf2f.png)
   Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect within 10 minutes after you save it.
    ![](https://main.qcloudimg.com/raw/b8701c4c69847ae711055df0727f01ab.png)

### Integrating the push SDK

1. Add Meizu dependency: implementation 'com.tencent.tpns:meizu:1.2.1.2-release'.
2. Refer to [Meizu Push Integration](http://open-wiki.flyme.cn/doc-wiki/index#id?129), and use the Meizu console to test notification messages to ensure that the SDK was integrated properly.
3. Call `PushManager.register` to initialize the Meizu Push service. After successful registration, you will receive the registration result in `onRegisterStatus` of the custom `BroadcastReceiver`. `registerStatus.getPushId()`is the unique identifier of the current app on the current device. After successful login to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **PushId** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via Meizu Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="meizu_click"></span>

### Configuring click events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

#### Open app

This is the default event, which opens the App once the notification bar message is clicked.

#### Open URL

You need to select **Open URL** in [Step 2: add a certificate](#meizuStep1_2) and enter a URL that starts with either `http://` or `https://`, such as `https://cloud.tencent.com/document/product/269`.
![](https://main.qcloudimg.com/raw/bb336d3e2bd799b4dfe443833782e322.png)

#### Open specific app interface

When [adding a certificate](#meizuStep1_2), you need to choose **Open specific app interface** and enter the complete class name of the Activity to be opened, for example, `com.tencent.qcloud.tim.demo.chat.ChatActivity`.
![](https://main.qcloudimg.com/raw/64d67e324cc53b0ff0631586d9ec1ef5.png)

<span id="meizu_custom"></span>

### Custom content pass through

Select **Open app** or **Open specific app interface** when configuring **Click event** in [Step 2: add a certificate](#meizuStep1_2) to support custom content pass through.

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Below is a simple example on the Android platform. You can also refer to the corresponding logic in the `sendMessage()` method in the [ChatManagerKit.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/base/ChatManagerKit.java) class in the TUIKit:

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

Clicking a notification bar message triggers a callback of `onNotificationClicked(Context context, MzPushMessage mzPushMessage)`, which is part of the Meizu Push SDK. The custom content can be obtained from the value of `mzPushMessage` .

```
String extContent = mzPushMessage.getSelfDefineContentString();
```

Alternatively, the client can obtain the custom content from the opened `Activity`. You can refer to the `parseOfflineMessage(Intent intent)` implementation method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class.

```
Bundle bundle = getIntent().getExtras();
String extContent = bundle.getString("ext"); 
```

## Google FCM Push

### Integrating the SDK

<span id="fcmStep1_1"></span>
1. Register with [Firebase Cloud Messaging](https://firebase.google.com) and create an app.
<span id="fcmStep1_2"></span>
2. Log in to the [Firebase console](https://console.firebase.google.com) and click your app card to go to the app configuration page. Click <img src="https://main.qcloudimg.com/raw/0d062411405553c9fae29f8e0daf02ad.png"  style="margin:0;"> on the right side of **Project Overview**, choose **Project Settings** > **Service Account**, and click **Generate New Private Key** to generate a new private key file.
<span id="fcmStep1_3"></span>
3. Log in to the Tencent Cloud [IM console](https://console.qcloud.com/avc) and click the target app card to go to the basic configuration page of the app. Click **Add a certificate** under **Android push configuration**. Upload the private key file obtained in [Step 2](#fcmStep1_2).
 ![](https://main.qcloudimg.com/raw/b18e2414561c6733b24c56cd1e866f21.png)
4. Click **OK** to save the information. Take note of the **`ID`** of the certificate. Certificate information takes effect within 10 minutes after you save it.
 ![](https://main.qcloudimg.com/raw/2199bbf955cf52f09b78af6a97ab8122.png)

### Integrating the push SDK

1. Add the FCM dependency: implementation 'com.google.firebase:firebase-messaging:20.2.3'.
1. Refer to [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/android/client) to set up Firebase. Refer to the [FCM Testing Guide](https://firebase.google.com/docs/cloud-messaging/android/first-message?authuser=0) to test notification messages to ensure that FCM was integrated properly.
2. After calling `FirebaseInstanceId.getInstance().getInstanceId()`, you can obtain the token in the callback. The token is the unique identifier of the current app. After successful login to the IM SDK, you need to call [setOfflinePushConfig](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e) to report the **certificate ID** and **token** to the IM server.

After the certificate ID and regId are successfully reported, the IM server sends messages via FCM Push notifications to the user when the app has been killed but the user has not logged out of IM.

<span id="fcm_custom"></span>

### Custom content pass through

**Step 1: custom content configuration (sender)**
Set the custom content for the notification bar message before sending the message.

- Below is a simple example on the Android platform. You can also refer to the corresponding logic in the sendMessage() method in the [ChatManagerKit.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/qcloud/tim/uikit/modules/chat/base/ChatManagerKit.java) class in the TUIKit:

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
When the notification bar message is clicked, the client can obtain the custom content from the corresponding `Activity`. You can refer to the `parseOfflineMessage(Intent intent)` implementation method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class.

```
Bundle bundle = getIntent().getExtras();
String value = bundle.getString("ext"); 
```

## Setting Custom iOS Push Alert Sound

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use the [setIOSSound](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#acffd09150398b06c3d7eb42baee5aee1) API in `V2TIMOfflinePushInfo` to set the sound for push notifications on iOS devices.

## Setting Custom Display for Offline Push

When calling [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe) to send messages, use [setTitle](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a7d4a73d6a1db487dd96f658bdbc98ae9) and [setDesc](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) in `V2TIMOfflinePushInfo` to set the title and content of notification bar messages respectively.

## FAQ

### How to set a custom sound for push notifications on Android phones?

Currently, most vendors do not support setting a custom sound for push notifications, therefore it is not supported by the IM SDK.

### Why do OPPO mobile phones fail to receive offline push messages?

This generally occurs for the following reasons:

- According to requirements on the official website of OPPO Push, ChannelID must be configured on OPPO mobile phones that run Android 8.0 or later versions. Otherwise, push messages cannot be displayed. For the configuration method, see [OPPO Push configuration](#oppoStep1_2).
- The [custom content in the message for pass-through offline push](#oppo_custom) is not in the JSON format. As a result, OPPO mobile phones do not receive the push message.

### Why doesn’t offline push work for custom messages?

The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the [desc](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field in [offlinePushInfo](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) during [sendMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe), and the desc information will be displayed by default during push.
