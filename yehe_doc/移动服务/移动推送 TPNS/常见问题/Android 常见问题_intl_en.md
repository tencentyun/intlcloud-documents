
### How do I disable the keep-alive feature of TPNS?

TPNS enables the keep-alive feature by default. Please call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in a `false` value:

```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```

If you use the automatic gradle integration method, please configure the following node under the <application> tag of the `AndroidManifest.xml` file of your application, where `xxx` is a custom name. If you use manual integration, please modify the node attributes as follows:
```xml
<!-- Add the following node to the AndroidManifest.xml file of your application, where xxx is a custom name: -->     
<!-- To disable the feature of keep-alive with TPNS application, please configure -->
<provider
		 android:name="com.tencent.android.tpush.XGPushProvider"
		 tools:replace="android:authorities"
		 android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
		 android:exported="false" />    
```

If the following log is printed in the console, the session keep-alive feature has been disabled: `I/TPush: [ServiceUtil] disable pull up other app`.

### Why does device registration fail?

- Data sync for newly created applications will take about one minute. During this period, the registration may return the error code 20. You can try again later.
- **Incorrect parameter:** check whether the `Access ID` and `Access Key` are correctly configured. Common errors are that the `Secret key` is misused or the `Access Key` contains spaces.
- **Registration error:** if the console returns an error code such as 10004, 10002, or 20, please see [SDK for Android Error Codes](https://intl.cloud.tencent.com/document/product/1024/30722).
- **No callback after registration:** check the current network condition. We recommend you use 4G network for testing. Wi-Fi used by many users may have insufficient network bandwidth.
- **Nubia phones:** models released in the second half of 2015 and 2016 cannot be registered, including Nubia Z11 series, Nubia Z11S series, and Nubia Z9S series.

### Why can't pushes be received after registration succeeded?

Please perform automated troubleshooting with the troubleshooting tool as instructed [here](https://intl.cloud.tencent.com/document/product/1024/38389). General errors include the following:

- Please check whether the current application package name is the same as that entered when TPNS is registered, and if not, we recommend you enable multi-package name push.
- Check whether the network is exceptional on the phone and switch to 4G network for testing.
- TPNS push includes **notification bar message** and **in-app message** (passthrough message). A notification bar message can be displayed on the notification bar, while an in-app message cannot.
- Confirm that the phone is in normal mode. Some phones may have restrictions on network and activity of the backend TPNS process when in Low Power or Do Not Disturb mode.
- Check whether the notification bar permission is granted on the phone. On some OPPO and Vivo phones, the notification bar permission has to be granted manually.



### What is the TPNS channel?

- The TPNS channel is a channel built by TPNS. It can deliver messages only when the TPNS service is online (maintaining a persistent connection with the TPNS backend server). Therefore, the value of the "Sent To" metric of the TPNS channel is generally lower than that of other vendor channels.
- If you need to implement offline push, we recommend you integrate a vendor channel. For more information, please see [Huawei Channel v5 Integration](https://intl.cloud.tencent.com/document/product/1024/37176).



### Why pushes can't be received after the application is closed?

- At present, third-party push services cannot guarantee that the pushes can be received after the application is closed. This problem is due to the restrictions of the mobile phone's custom ROM on the TPNS service. All pushes through the TPNS channel are on the basis that the TPNS service can maintain a persistent connection with the TPNS backend server. After the service is terminated, whether it can be restarted depends on the system settings, security programs, and user operations.
- After the TPNS service is disconnected from the TPNS server, messages delivered to the device will become offline messages, which can be retained for up to 72 hours. If there are multiple offline messages, only the three latest ones can be retained on each device. If messages are pushed after the application is closed, please check whether the `XGPushManager.unregisterPush\(this\)` API has been called if the messages cannot be received when the application is launched again.
- If you have already integrated a vendor channel, but pushes still cannot be received offline, please use the [troubleshooting tool](https://console.cloud.tencent.com/tpns/user-tools) to check whether the token has been successfully registered with the vendor, and if not, please troubleshoot as instructed in [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).
- QQ and WeChat are in the system-level application allowlist, and the relevant service will not be terminated after the application is closed, so the user can still receive messages after closing the application, as the relevant service survives on the backend.

### I installed Huawei Mobile Service on a non-Huawei phone and integrated the TPNS SDK with my application, but this caused Huawei Push and other components to fail. How do I fix it?

Starting from TPNS SDK v1.1.6.3, in order to avoid the situation **where push services of other vendors auto-start and transfer user data on the background on a phone**, push service components of other vendors will be disabled on the phone.
Huawei uses some public components for different features such as account, game, and push. Disabling the push component by TPNS may make other service features unable to start on a non-Huawei phone. If you need to turn off this disablement feature, you can configure the following:
Add the following node configuration under the `application` tag of the `AndroidManifest.xml` file, uninstall the application, and reinstall it.
```xml
<meta-data
		android:name="tpns-disable-component-huawei-v2"
		android:value="false" />
<meta-data
		android:name="tpns-disable-component-huawei-v4"
		android:value="false" />
```

### How do I set the message click event?

TPNS recommends using Intent for redirection (note: the SDK supports click events by default upon message click, and the corresponding homepage will be opened. If the redirection operation is set in `onNotifactionClickedResult`, it will conflict with the custom redirection specified in the console/API, resulting in failure of the custom redirection).
**Guide for redirection through Intent:**
You need to configure the page to redirect to in the client app's manifest:

- For example, if you want to redirect to the page specified by `AboutActivity`, use the following sample code:

```
<activity
            android:name="com.qq.xg.AboutActivity"
            android:theme="@android:style/Theme.NoTitleBar.Fullscreen" >
            <intent-filter >
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT"/>
                <!-- Specify your complete scheme by customizing the content of the data block. According to your configuration, a URL identifier in the format of "semantic name://host name/path name" will be formed -->
                <!-- To avoid conflicts with the redirect destination pages of other applications, you can use fields that can uniquely identify the application for configuration, such as those with the application name or application package name -->
                <data
                    android:scheme="Semantic name"
                    android:host="Host name"
                    android:path="/Path name" />
            </intent-filter>
</activity>
```

- If you use the TPNS Console to set the intent for redirect, enter in the following way:
  ![](https://main.qcloudimg.com/raw/5c7339b703864377ed2bc6463faddce1.png)
- If you use a server SDK, you can set the intent for redirect as follows (with the SDK for Java as an example):
```
action.setIntent("xgscheme://com.tpns.push/notify_detail");
```

- If you want to bring parameters such as `param1` and `param2`, you can set as follows:
```
action.setIntent("xgscheme://com.tpns.push/notify_detail?param1=aa&param2=bb");
```

**Get the parameters on the device**:

1. In the `onCreate` method of the page you specify for redirect to, add the following code:

```
Uri uri = getIntent().getData();
    if (uri != null) {                
String url = uri.toString();
String p1= uri.getQueryParameter("param1");
String p2= uri.getQueryParameter("param2");
 }
```

2. If the parameters passed in contain special characters such as # and &, they can be parsed by using the following method:

```
Uri uri = getIntent().getData();
    if (uri != null) {                
 String url = uri.toString();
 UrlQuerySanitizer sanitizer = new UrlQuerySanitizer();
 sanitizer.setUnregisteredParameterValueSanitizer(UrlQuerySanitizer.getAllButNulLegal());
   sanitizer.parseUrl(url);
   String value1 = sanitizer.getValue("key1");
   String value2 = sanitizer.getValue("key2");
   Log.i("TPNS" , "value1 = " + value1 + " value2 = " + value2);
}
```

### What notification event callbacks do vendor channels support?

| Callback | Arrival Callback | Click Callback |
|---------|---------|---------|
| Mi | Supported | Supported |
| Meizu | Supported | Supported |
| FCM | Supported | Supported |
| Huawei | Not supported | Supported |
| OPPO | Not supported | Supported |
| Vivo | Not supported | Supported |

>! Click callback of vendor channels is supported by SDK v1.2.0.1 and above. Legacy versions only supports this feature for Huawei, Mi, Meizu, and Vivo.



### How do I fix the problem of null `other push Token` that occurs during debugging after my application is integrated with a vendor channel?


A log similar to the following one is found in the application operation logs: 

```
[OtherPushClient] handleUpdateToken other push token is :  other push type: huawei
```



Then it means that your application failed to register with the vendor channel. You can locate and troubleshoot the problem by getting the return code for vendor channel registration failure. For more information, please see [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

### Both IM and TPNS are integrated, but there are a lot of vendor conflicts. How do I fix this problem?

Currently, IM uses the vendor jar packages provided by TPNS. Please replace the relevant dependency packages according to the following table to fix the problem.

| Push Channel | System Requirements | Condition Description |
| --------------- | ------| -------------------------------------------- |
| Mi Push | MIUI | To use Mi Push, add the following dependency: `implementation 'com.tencent.tpns:xiaomi:1.2.1.3-release'`|
| Huawei Push | EMUI | To use Huawei Push, add the following dependencies: <li>`implementation 'com.tencent.tpns:huawei:1.2.1.3-release'`  <li> `implementation 'com.huawei.hms:push:5.0.2.300'`|
| Google FCM Push | Android 4.1 and above | The mobile device needs to have Google Play Services installed and use it outside the Chinese Mainland. Add the following dependency: `implementation 'com.google.firebase:firebase-messaging:20.2.3'`|
| Meizu Push | Flyme | To use Meizu Push, add the following dependency: `implementation 'com.tencent.tpns:meizu:1.2.1.3-release'` |
| OPPO PUSH | ColorOS | Not all OPPO models and versions support OPPO PUSH. To use OPPO PUSH, add the following dependency: `implementation 'com.tencent.tpns:oppo:1.2.1.3-release'`|
| Vivo Push | FuntouchOS | Not all Vivo models and versions support Vivo Push. To use Vivo Push, add the following dependency: `implementation 'com.tencent.tpns:vivo:1.2.1.3-release'`|






### Why can't messages be displayed on the notification bar after arriving at phones on Meizu Flyme 6.0 or below?

1. Manual integration is used on Meizu phones on Flyme 6.0 and below.
2. Automatic integration is used on Meizu phones on Flyme 6.0 and below, and the version of the used TPNS SDK for Android is below 1.1.4.0.

In the above two cases, you need to place an image exactly named `stat_sys_third_app_notify` in the drawable folders with different resolutions. For more information, please see the `flyme-notification-res` folder in the [TPNS SDK for Android](https://console.cloud.tencent.com/tpns/sdkdownload).




### How do I fix the exception that occurs when I use quick integration in the console?

1. If an exception occurs during integration, set the `"debug"` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, use the `"TpnsPlugin"` keyword for analysis.
2. Click the **sync projects** icon.
   ![](https://main.qcloudimg.com/raw/5fecbe6b63374e7e0e58c4b2cd215acb.png)
3. Check whether there are relevant dependencies in the external libraries of the project.
   ![](https://main.qcloudimg.com/raw/485c7595f1b478a6fad725d38deb87b4.png)



### How do I convert Android extension library v4 to AndroidX?

Add the following property to the `gradle.properties` file of the AndroidX project:

```
android.useAndroidX=trueandroid.enableJetifier=true
```
> ? 
>- `android.useAndroidX=true` indicates to enable `AndroidX` for the current project.
>- `android.enableJetifier=true` indicates to migrate the dependency package to `AndroidX`. 


### What should I do if a vendor channel's push SDK "transfers information over HTTP in plaintext"?

After you integrate the push services of various vendor channels, some security detection tools may prompt that "the application transfers information over HTTP in plaintext". The specific HTTP addresses include:
1. Mi Push SDK: `http://new.api.ad.xiaomi.com/logNotificationAdActions, http://resolver.msg.xiaomi.net/psc/?t=a`
2. Meizu Push SDK: `http://norma-external-collect.meizu.com/android/exchange/getpublickey.do, http://norma-external-collect.meizu.com/push/android/external/add.do`
All the above HTTP URLs are from the push SDKs of relevant vendors. The TPNS team is unable to clarify their purposes or control their behaviors but is actively contacting them and promoting the adoption of transfer over HTTPS. Currently, you should evaluate and choose whether to continue to use the above vendors' push services.
