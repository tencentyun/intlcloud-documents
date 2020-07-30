### How do I disable the keep-alive feature of TPNS?

TPNS enables the keep-alive feature by default. Please call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in a `false` value:
```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```
If you use the automatic gradle integration method, please configure the following node under the <application> tag of the `AndroidManifest.xml` file of your application, where ```xxx``` is a custom name. If you use manual integration, please modify the node attributes as follows:

```xml
   <!-- Add the following node to the AndroidManifest.xml file of your application, where xxx is a custom name: -->    
   <!-- To disable the feature of keep-alive with TPNS application, please configure -->
   <provider
       android:name="com.tencent.android.tpush.XGPushProvider"
       tools:replace="android:authorities"
       android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
       android:exported="false" />   
```

If the following log is printed in the console, the session keep-alive feature has been disabled: `I/TPNS: [ServiceUtil] disable pull up other app`.

### Why can't push messages be received?
Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and use the obtained token for message push. If pushes cannot be received, please troubleshoot as follows:
- Please make sure that the SDK is on the latest version. Problems in legacy versions may have already been fixed in the latest version.
- If an error occurs during message push through web, please refresh the page and try again.


### Why can't pushes be received after registration succeeded?
- Please check whether the current application package name is the same as that entered when TPNS is registered, and if not, you are recommended to enable multi-package name push.
- Check whether the network is exceptional on the phone and switch to 4G network for testing.
- TPNS push includes **notification bar message** and **in-app message** (passthrough message). A notification bar message can be displayed on the notification bar, while an in-app message cannot.
- Confirm that the phone is in normal mode. Some phones may have restrictions on network and activity of the backend TPNS process when in Low Power or Do Not Disturb mode.
- Check whether the notification bar permission is granted on the phone. On some OPPO and Vivo phones, the notification bar permission has to be granted manually.


### Why does device registration fail?
- Data sync for newly created applications will take about one minute. During this period, the registration may return the error code 20. You can try again later.
- **Incorrect parameter:** check whether the `Access ID` and `Access Key` are correctly configured. Common errors are that the `Secret key` is misused or the `Access Key` contains spaces.
- **Registration error:** if the console returns an error code such as 10004, 10002, or 20, please see [SDK for Android Error Codes](https://intl.cloud.tencent.com/document/product/1024/30722).
- **No callback after registration:** check the current network condition. You are recommended to use 4G network for testing. Wi-Fi used by many users may have insufficient network bandwidth.
- **Nubia phones:** models released in the second half of 2015 and 2016 cannot be registered, including Nubia Z11 series, Nubia Z11S series, and Nubia Z9S series.

### Why pushes can't be received after the application is closed?
- At present, third-party push services cannot guarantee that the pushes can be received after the application is closed. This problem is due to the limitation of the mobile phone's custom ROM on the TPNS service. All activities of TPNS are on the basis that the TPNS service can connect to the internet and run properly. After the service is terminated, whether it can be restarted depends on the system settings, security programs, and user operations.
- QQ and WeChat are in the system-level application allowlist, and the relevant service will not be terminated after the application is closed, so the user can still receive messages after closing the app, and in fact, the relevant service survives on the backend.
- On Android, after the user exits the application and the TPNS service is disconnected from the TPNS server, messages delivered to the device will become offline messages, which can be retained for up to 72 hours. If there are multiple offline messages, only two can be retained on each device. If messages are pushed after the application is closed, please check whether the `XGPushManager.unregisterPush\(this\)` API has been called if the messages cannot be received when the application is launched again.


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
<data android:scheme="xgscheme"
android:host="com.xg.push"
android:path="/notify_detail" />
</intent-filter>
</activity>
```
 - If you use the TPNS Console to set the intent for redirect, enter in the following way:
![](https://main.qcloudimg.com/raw/5c7339b703864377ed2bc6463faddce1.png)
 - If you use a server SDK, you can set the intent for redirect as follows (with the SDK for Java as an example):
```
action.setIntent("xgscheme://com.xg.push/notify_detail");
```
 - If you want to bring parameters such as `param1` and `param2`, you can set as follows:
```
action.setIntent("xgscheme://com.xg.push/notify_detail?param1=aa&param2=bb");
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
   Log.i("XG" , "value1 = " + value1 + " value2 = " + value2);
}
```






### What callbacks are supported by vendor channels?
- The Mi channel supports arrival callback and passthrough but not click callback.
- The Huawei channel supports click callback (custom parameters required) and passthrough (custom parameters ignored) but not arrival callback.
- The Meizu channel supports arrival callback and click callback but not passthrough.
- The Vivo channel supports click callback but not arrival callback or passthrough.
- The OPPO channel does not support click callback, arrival callback, or passthrough.

>Note: if you need to get parameters through the click callback or redirect to a custom page, you can use the intent to do so.



### How do I fix the problem of `otherpushToken = null` that may be encountered during debugging?
#### Troubleshooting for Mi channel
- Check whether the application package name is the same as that registered on Mi Open Push Platform.
- Check whether message push has been enabled on Mi Open Push Platform.
- For manual connection, check the manifest file configuration against the development documentation, especially the places where the package name needs to be modified:
```
<permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" android:protectionLevel="signature" />
<!-- Here, change `com.example.mipushtest` to the application package name -->
<uses-permission android:name="com.example.mipushtest.permission.MIPUSH_RECEIVE" />
<!-- Here, change `com.example.mipushtest` to the application package name -->
```
- Check whether you have set the `APPID` and `APPKEY` of Mi before the registration and whether third-party push has been enabled:
```
// Enable third-party push
XGPushConfig.enableOtherPush(this,true);
// Set the `APPID` and `APPKEY` of Mi
XGPushConfig.setMiPushAppId(this,MIPUSH_APPID);
XGPushConfig.setMiPushAppKey(this,MIPUSH_APPKEY);
```
- Listen on the registration result of Mi by implementing the custom broadcast that inherits `PushMessageReceiver` and check the registration return code.
- Start Logcat and check the log with the tag of `PushService` to see what error message exists.

#### Troubleshooting for Huawei channel
- Check whether the version in **Settings** > **App Management** > **Huawei Mobile Service** on the Huawei phone is above 2.5.3.
- Check whether the application package has been signed.
- Check whether an SHA256 certificate fingerprint has been configured at Huawei's official website.
- Check the manifest file configuration against the Huawei channel connection guide in the development documentation.
- Check whether the third-party push has been enabled before the TPNS registration and whether the Huawei `AppID` is configured correctly.
- Check whether the application package name is the same as that registered at Huawei Push's official website and in the TPNS Console.
- Call `XGPushConfig.setHuaweiDebug\(true\)` before registering the code, manually confirm that the storage permission is granted to the app, check the cause of Huawei registration failure output in the `huawei.txt` file in the SD card directory, and then find the cause corresponding to the [error code](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-References/hmssdk_huaweipush_api_reference_errorcode) in Huawei development documentation.
- In CMD, run ```adb shell setprop log.tag.hwpush VERBOSE``` and
  ```adb shell logcat -v time &gt; D:/log.txt``` to start capturing logs, conduct the test, and close the CMD window. Then, send the log to technical support.


#### Troubleshooting for Meizu channel
- It is similar to the troubleshooting method for the Mi channel. For more information, please see troubleshooting for the Mi channel.

### Why aren't messages displayed in the notification bar when they arrive on the Meizu mobiles of version Flyme 6.0 or earlier?
1.  Meizu mobiles of version Flyme 6.0 or earlier use manual integration.
2.  Meizu mobiles of version Flyme 6.0 or earlier use automatic integration, and TPNS Android SDK 1.1.4.0 or earlier versions.
In both cases, you need to place a picture named "stat_sys_third_app_notify" under `drawable` folder with different resolutions. For details, see `flyme-notification-res` folder in [TPNS Android SDK](https://console.cloud.tencent.com/tpns/sdkdownload).


### How do I solve the conflict between component dependencies when integrating with the Huawei push channel?
If your project uses Huawei HMS 2.x.x, Game Suite, Huawei Pay, Huawei ID, or other Huawei service components and a conflict between component dependencies occurs when you integrate with the Huawei push channel based on `com.tencent.tpns:huawei:1.1.x.x-release`, please follow the steps below for integration:
1. Cancel the project's dependency on the single dependency package `"com.tencent.tpns:huawei:[VERSION]-release"`.
2. When integrating with the official Huawei SDK by referring to the official documentation of Huawei Developers, please select the push module to add the push feature to the SDK.
3. In the source code of the HMSAgent module, modify the tool class `com.huawei.android.hms.agent.common.StrUtils` as follows to fix Huawei token registration failure caused by an exception in the Huawei SDK.
Before modification:
```java
package com.huawei.android.hms.agent.common;
public final class StrUtils {
    public static String objDesc(Object object) {
        return object == null ? "null" : (object.getClass().getName()+'@'+ Integer.toHexString(object.hashCode()));
    }
}
```
After modification:
```java
package com.huawei.android.hms.agent.common;
public final class StrUtils {
    public static String objDesc(Object object) {
        String s = "";
        try {
            s = Integer.toHexString(object.hashCode());
        } catch (Throwable e) {
        }
        return object == null ? "null" : (object.getClass().getName()+'@'+ s);
    }
}
```


### How do I fix the exception that occurs when I use quick integration in the console?
1. If an exception occurs during integration, set the `"debug"` field in the `tpns-configs.json` file to `true` and run the following command:
```
./gradlew --rerun-tasks :app:processReleaseManifest
```
Then, use the `"TpnsPlugin"` keyword for analysis.
2. Click "sync projects".
![](https://main.qcloudimg.com/raw/5fecbe6b63374e7e0e58c4b2cd215acb.png)

3. Check whether there are relevant dependencies in the external libraries of the project.
![](https://main.qcloudimg.com/raw/485c7595f1b478a6fad725d38deb87b4.png)
