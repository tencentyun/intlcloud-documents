# Meizu Push Channel Integration Guide

Meizu push channel is a system-level push channel **powered by Meizu**. On a Meizu phone, push messages can be delivered through Meizu's system channel without opening the app.

**\[Notes\]**

1. For the Meizu push channel, the notification title cannot contain more than 32 characters, and the notification content cannot contain more than 100 characters.

2. The Meizu push channel does not support passthrough messages.

## Getting Meizu Push Key

1. Go to [Meizu Push official website](https://open.flyme.cn/open-web/views/push.html).

2. Sign up for or log in to a developer account. (Your identity needs to be verified if it is a new account registration, and it takes about 2 days. Contact Meizu for more information.)

3. Create an app on the [Meizu Push platform](http://push.meizu.com). Note: The "app package name" must be the same as that entered in TPNS console.

4. Get app-related information and copy it into "App configuration > Vendor-specific and global channels" in TPNS console, including AppID, AppKey, and AppSecret.

Note: For more details, see the [Meizu development documentation](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf).

5. Enter the relevant push key in TPNS console > App configuration > Vendor-specific and global channels > Meizu push channel.

## Integration Steps

### Android Studio Integration Method



```js
/* Meizu v3.2.7-release
 * Note: If the Meizu channel uses this version, the TPNS SDK also needs to use v3.2.7-release at the same time.
 */
 compile 'com.tencent.xinge:xgmz:3.2.7-Release'
/* Meizu v3.2.8-release
 * Note: If the Meizu channel uses this version, the TPNS SDK also needs to use v4.0.5 at the same time.
 */
 compile 'com.tencent.xinge:xgmz:3.2.8-release'
```

### Eclipse Integration Method

1. Import the jar package (pushsdk-3.3.170110.jar) required by the Meizu channel to the libs directory.

2. Add the following configuration to Androidmanifest.

```xml
<application>
<service
    android:name="com.meizu.cloud.pushsdk.NotificationService"
     android:exported="true"/>

<receiver android:name="com.meizu.cloud.pushsdk.SystemReceiver" >
     <intent-filter>
      <action android:name="com.meizu.cloud.pushservice.action.PUSH_SERVICE_START"/>
      <category android:name="android.intent.category.DEFAULT" />
     </intent-filter>
 </receiver>
</application>

 <!-- Note: This is the beginning of permission required by Meizu Push -->
 <!-- Compatible with Flyme versions below 5.0. Meizu's internal integration pushSDK is required; otherwise, messages cannot be received -->

  <uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>

  <permission android:name="app package name.push.permission.MESSAGE" 

                   android:protectionLevel="signature"/>

  <uses-permission android:name="app package name.push.permission.MESSAGE"></uses-permission>

  <!-- Compatible with Flyme 3.0 configuration permissions -->

  <uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />

  <permission android:name="app package name.permission.C2D_MESSAGE"

              android:protectionLevel="signature">
  </permission>

  <uses-permission android:name="app package name.permission.C2D_MESSAGE"/>

<!-- Note: This is the end of permission required by Meizu Push -->
```

#### Meizu Message Receiver

Add a custom ```Receiver``` in ```AndroidManifest.xml``` with the following configuration:

```xml
<receiver android:name="com.tencent.android.mzpush.MZPushMessageReceiver">
    <intent-filter>
        <!-- Receive push message -->
        <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
        <!-- Receive register message -->
         <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK"/>
        <!-- Receive unregister message -->
         <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK"/>

         <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
         <action android:name="com.meizu.c2dm.intent.RECEIVE" />

         <category android:name="app package name"></category>
     </intent-filter>
</receiver>
```

## Code Start and Registration Log Output

Configure the following code before starting TPNS by \(calling `XGPushManager.registerPush` \):

```java
// Set Meizu APPID and APPKEY
XGPushConfig.enableOtherPush(context, true);
XGPushConfig.setMzPushAppId(this, APP_ID);
XGPushConfig.setMzPushAppKey(this, APP_KEY);
```

The log of successful registration is as follows:

```java
// The tokens of TPNS and Meizu are successfully obtained, and the binding is successful, indicating that the registration is successful.
INFO16:24:27.94313075XINGE[a] >> bind OtherPushToken success ack with [accId = 2100273138 , rsp = 0] token = 08d7ea8e4b93952cbfdd2cb68461342c314d281a otherPushType = meizu otherPushToken = ULY6c5968627059714a475c63517f675b7f655e62627e
```

**Note: If you need to get parameters through tap callback or redirect to a custom page, you can use the Intent to do so. Click [here](http://docs.developer.qq.com/xg/android_access/android_faq.html#消息点击事件以及跳转页面方法) to view the tutorials.**

## Code Obfuscation

```xml
-dontwarn com.meizu.cloud.pushsdk.**

-keep class com.meizu.cloud.pushsdk.**{*;}
```

## Vendor-specific Channel Testing Method \(Generic\)

1. Integrate the TPNS SDK v3.2.1 or higher in your app and integrate the required vendor-specific SDK according to the Integration Guide for Vendor-specific Channels.

2. Confirm that the relevant app information has been enter in "App configuration > Vendor-specific and global channels" in the TPNS console. Usually, the relevant configuration will take effect after 1 hour. Please wait patiently and proceed to the next step after it takes effect.

3. Install the integrated app (testing version) on a test device and run the app.

4. Keep the app running in the foreground and try to make unicast/full push to the device.

5. If the app receives the message, switch the app to the background and end all app processes.

6. Make unicast/full push again, and if the push is received, the vendor-specific channel integration is successful.



