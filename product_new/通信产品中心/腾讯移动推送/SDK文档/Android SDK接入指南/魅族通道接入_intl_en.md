## Operation Scenarios
The Meizu push channel is a system-level push channel **officially provided by Meizu**. On a Meizu phone, push messages can be delivered through Meizu's system channel without opening the app.

>
>- For the Meizu push channel, the notification title cannot contain more than 32 characters, and the notification content cannot contain more than 100 characters.
>- The Meizu push channel does not support message passthrough.
>- The Meizu channel supports arrival callback and click callback but not passthrough.

## Directions
### Getting key
Enter [Meizu Push's official website](https://open.flyme.cn/open-web/views/push.html), sign up for a developer account and log in, and get the `AppID`, `AppKey`, and `AppSecret`. For more information, please see the [Meizu development documentation](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf).


### Integration steps
#### Integrating through Android Studio
```js
implementation 'com.tencent.tpns:meizu:[VERSION]-release'// Meizu Push [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
```

#### Integrating through Eclipse
1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the jar packages related to Meizu Push. Import `mz4tpns1.1.2.1.jar` to the project folder:
3. Configure the following content under Android manifest:

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
 <!-- Note: this is the beginning of permission required by Meizu Push -->
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
<!-- Note: this is the end of permission required by Meizu Push -->
```
4. For the Meizu message receiver, add ```Receiver``` in ```AndroidManifest.xml``` with the following configuration:

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

### Enabling Meizu Push
Configure the following code before starting TPNS and calling `XGPushManager.registerPush`:

```java
// Set Meizu `APPID` and `APPKEY`
XGPushConfig.enableOtherPush(context, true);
XGPushConfig.setMzPushAppId(this, APP_ID);
XGPushConfig.setMzPushAppKey(this, APP_KEY);
```

The log of successful registration is as follows:

```java
// The tokens of TPNS and Meizu are successfully obtained, and the binding is successful, indicating that the registration is successful.
INFO16:24:27.94313075XINGE[a] >> bind OtherPushToken success ack with [accId = 2100273138 , rsp = 0] token = 08d7ea8e4b93952cbfdd2cb68461342c314d281a otherPushType = meizu otherPushToken = ULY6c5968627059714a475c63517f675b7f655e62627e
```

If you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so. For more information, please see [FAQs for Android](https://intl.cloud.tencent.com/document/product/1024/32624#.E5.A6.82.E4.BD.95.E8.AE.BE.E7.BD.AE.E6.B6.88.E6.81.AF.E7.82.B9.E5.87.BB.E4.BA.8B.E4.BB.B6.EF.BC.9F).

### Obfuscating code
```xml
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}
```

>Obfuscation rules must be stored in the `proguard-rules.pro` file at the app project level.

