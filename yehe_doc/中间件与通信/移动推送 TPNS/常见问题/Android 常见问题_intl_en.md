### How do I set a custom ringtone?

You can set a custom ringtone by creating a notification channel.
1. Create a notification channel with a specified custom ringtone file by calling the TPNS encapsulation API or Android native API. For more information, see the **Creating a notification channel** section in [API Documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
2. Call the TPNS push API and specify the same notification channel `n_ch_id` for push. For a vendor channel, you must specify the vendor channel ID. That is, for Huawei channel, specify `hw_ch_id`; for Mi channel, specify `xm_ch_id`.

>? Currently, only Huawei, Mi, FCM, and TPNS channels support custom ringtones. To apply for a vendor channel ID, see [Vendor Message Classification Feature Use Instructions](https://intl.cloud.tencent.com/document/product/1024/36250).
>

### How do I disable the session keep-alive feature of TPNS?

To disable the feature, call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in `false`:
>!The session keep-alive feature can be disabled only in SDK v1.1.6.0 and later versions. In SDK versions earlier than v1.1.6.0, the feature is enabled by default and cannot be disabled.

```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```

If you use Gradle automatic integration, configure the following node under the `<application>` tag of the `AndroidManifest.xml` file of your application, where `xxx` is a custom name. If you use manual integration, modify node attributes as follows:
```xml
<!-- Add the following node to the AndroidManifest.xml file of your application, where xxx is a custom name: -->     
<!-- To disable the feature of keep-alive with TPNS application, configure as follows: -->
<provider
		 android:name="com.tencent.android.tpush.XGPushProvider"
		 tools:replace="android:authorities"
		 android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
		 android:exported="false" />    
```

If the following log is printed in the console, the session keep-alive feature has been disabled: `I/TPush: [ServiceUtil] disable pull up other app`



### Does TPNS SDK support push via HarmonyOS?

HarmonyOS is fully compatible with the Android SDK, so HarmonyOS users can use the push feature normally.


### Do vendor push services need to be launched in application markets before they can be enabled?

| Vendor | Need to Be Launched to Application Markets |
|---------|---------|
| Mi | No. You only need an individual developer account to enable Mi Push. For details, see [here](https://dev.mi.com/console/doc/detail?pId=68). |
| Meizu | No. You only need an individual developer account to enable Meizu Push. For details, see [here](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf). |
| FCM | No. You only need an individual developer account to enable FCM Push. |
| Huawei | No. You only need an individual developer account to enable Huawei Push. For details, see [here](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-enable_service#enable-service). |
| OPPO | Yes. You need an enterprise developer account to enable OPPO PUSH. For details, see [here](https://open.oppomobile.com/wiki/doc/#id=10195). |
| vivo | Yes. You need an enterprise developer account to enable vivo Push. For details, see [here](https://dev.vivo.com.cn/documentCenter/doc/2). |



### What is the TPNS channel?

- The TPNS channel is a channel built by TPNS. It can deliver messages only when the TPNS service is online (maintaining a persistent connection with the TPNS backend server). Therefore, the actual delivery value of the TPNS channel is generally lower than that of other vendor channels.
- If you need to implement offline push, we recommend you integrate a vendor channel. For more information, see [here](https://intl.cloud.tencent.com/document/product/1024/30711).



### Why pushes cannot be received after the application is closed?

- Currently, third-party push services cannot guarantee that the pushes can be received after the application is closed. This problem is due to the restrictions of the mobile phone's custom ROM on the TPNS service. All pushes through the TPNS channel are on the basis that the TPNS service can maintain a persistent connection with the TPNS backend server. After the service is terminated, whether it can be restarted depends on the system settings, security programs, and user operations.
- After the TPNS service is disconnected from the TPNS server, messages delivered to the device will become offline messages, which can be retained for up to 72 hours. If there are multiple offline messages, only the three latest ones can be retained on each device. If messages are pushed after the application is closed, check whether the `XGPushManager.unregisterPush\(this\)` API has been called if the messages cannot be received when the application is launched again.
- If you have already integrated a vendor channel, but pushes still cannot be received offline, use the [troubleshooting tool](https://console.cloud.tencent.com/tpns/user-tools) to check whether the token has been successfully registered with the vendor, and if not, troubleshoot as instructed in [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).
- QQ and WeChat are in the system-level application allowlist, and the relevant service will not be terminated after the application is closed, so the user can still receive messages after closing the application, as the relevant service survives on the backend.

### Why does device registration fail?

- Data sync for newly created applications will take about one minute. During this period, the registration may return the error code 20. You can try again later.
- **Incorrect parameter**: check whether `Access ID` and `Access Key` are correctly configured. Common errors are that `Secret key` is used by mistake or `Access Key` contains spaces at the beginning and end.
- **Registration error:** if the console returns an error code such as 10004, 10002, or 20, please see [Error Code](https://intl.cloud.tencent.com/document/product/1024/30722).
- **No callback after registration:** check the current network condition. We recommend you use 4G network for testing. Wi-Fi used by many users may have insufficient network bandwidth.
- **Nubia phones:** models released in the second half of 2015 and 2016 cannot be registered, including Nubia Z11 series, Nubia Z11S series, and Nubia Z9S series.

### Why can't pushes be received after successful registration?

Perform automated troubleshooting with the troubleshooting tool as instructed [here](https://intl.cloud.tencent.com/document/product/1024/38389). General errors include the following:

- Check whether the current application package name is the same as that entered during TPNS registration, and if not, we recommend you enable multi-package name push.
- Check whether the mobile network has any exceptions: switch to 4G network for testing.
- TPNS push messages include **notification bar messages** and **in-app messages** (passthrough messages). A notification bar message can be displayed on the notification bar, while an in-app message cannot.
- Confirm that the phone is in normal mode. Some phones may have restrictions on network and activity of the backend TPNS process when in Low Power or Do Not Disturb mode.
- Check whether the notification bar permission is granted on the phone. On some OPPO and vivo phones, the notification bar permission has to be granted manually.

### Why can't pushes be received on a Nubia phone?
TPNS does not support Nubia phones released after 2015, as the new version of Nubia operating system has a super power-saving feature, which will kill background processes very quickly and prevent TPNS Service from being started, resulting in failures of registration with Nubia phones.



### I installed Huawei Mobile Service on a non-Huawei phone and integrated the TPNS SDK with my application, but this caused Huawei Push and other components to fail. How do I fix this problem?

Starting from TPNS SDK v1.1.6.3, in order to **avoid the situation where push services of other vendors auto-start and transfer user data on the background on a phone**, push service components of other vendors will be disabled on the phone.
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

### How do I set a message click event?

You can redirect subscribers who click your notification to a specified in-app page, HTML5 page, or Deeplink to meet your needs in different use cases. For more information, please see [Notification Tap-to-Redirect](https://intl.cloud.tencent.com/document/product/1024/38354).

### What notification event callbacks do vendor channels support?

| Callback | Arrival Callback | Click Callback |
|---------|---------|---------|
| Mi | Not supported | Supported |
| Meizu | Not supported | Supported |
| FCM | Not supported | Supported |
| Huawei | Not supported | Supported |
| OPPO | Not supported | Supported |
| vivo | Not supported | Supported |

>! Click callback of vendor channels is supported by SDK v1.2.0.1 and above. Legacy versions support this feature only for Huawei, Mi, Meizu, and vivo.
>


### Why `title` and `content` obtained by `onNotifactionClickedResult` and `onNotificationShowedResult` are empty when the application is closed?

For pushes through vendor channels, `title` and `content` are concatenated in `intent` and delivered. Therefore, they cannot be obtained by the `onNotifactionClickedResult` and `onNotificationShowedResult` methods. To obtain the two parameters, you need to use the Intent mode. For more information, please see [Notification Tap-to-Redirect](https://intl.cloud.tencent.com/document/product/1024/38354).


### How do I fix the problem of null `other push Token` that occurs during debugging after my application is integrated with a vendor channel?


Check whether the application operation logs contain information similar to the following: 
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: huawei
```

If such log information exists, it means that your application failed to register with the vendor channel. In that case, get the return code for vendor channel registration failure to locate and troubleshoot the problem. For more information, please see [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

### Large numbers of vendor conflicts occur after the simultaneous integration of IM and TPNS. What should I do?

Currently, IM uses the vendor JAR packages provided by TPNS. Please replace the relevant dependency packages according to the following table to fix the problem.

| Push Channel | System Requirement | Condition Description |
| --------------- | ------| -------------------------------------------- |
| Mi Push | MIUI | To use Mi Push, add the following dependency: `implementation 'com.tencent.tpns:xiaomi:1.2.1.3-release'` |
| Huawei Push | EMUI | To use Huawei Push, add the following dependencies:<li>`implementation 'com.tencent.tpns:huawei:1.2.1.3-release'`</li><li>`implementation 'com.huawei.hms:push:5.0.2.300'`</li> |
| Google FCM Push | Android 4.1 and above | The mobile phone needs to install Google Play Services and be used outside the Chinese mainland. Add the following dependency: `implementation 'com.google.firebase:firebase-messaging:20.2.3'` |
| Meizu Push | Flyme | To use Meizu Push, add the following dependency: `implementation 'com.tencent.tpns:meizu:1.2.1.3-release'` |
| OPPO PUSH | ColorOS | Not all OPPO models and versions support OPPO PUSH. To use OPPO PUSH, add the following dependency: `implementation 'com.tencent.tpns:oppo:1.2.1.3-release'` |
| vivo Push | FuntouchOS | Not all vivo models and versions support vivo Push. To use vivo Push, add the following dependency: `implementation 'com.tencent.tpns:vivo:1.2.1.3-release'` |

### How do I adapt to small icons?

- ROMs running native Android 5.0 or above will process the small icon of an application and add a layer of color if `target sdk` is greater than or equal to 21, causing the icon to be gray.
- If you want to display it as colored, you can set `target sdk` to below 21. If you don't want `target sdk` to be below 21, you can rename a small transparent background .png image to `notification_icon.png` (the filename must be unique) and place it in the `drawable` directory; in this way, the small icon will be displayed as gray (but shaped).
- Starting from TPNS SDK for Android v1.2.2.0, the `notification_icon.png` small icon resource will only take effect directly on Google Pixel phones by default. To achieve such small icon effect for custom notifications on other phones, you need to specify the resource filename (without the extension) as the `message.android.small_icon` field in the push API. In addition, the custom notification small icon supports solid colors by specifying a decimal value of an RGB color as the `message.android.icon_color` field in the push API.

Below is an example of push API fields, where `icon_color: 123456` indicates the RGB color 01e240:
```
{
    "message": {
        "android": {
            "small_icon": "notification_icon",
            "icon_color": 123456
        }
    }
}
```

The display effect after adaption is as shown below. We recommend you draw an icon based on the demo logo.


>?
>- The small icon must be a PNG image with an alpha channel.
>- The background must be transparent.
>- Do not leave too much padding around the icon.
>- We recommend you use an image with dimensions of 46x46, as smaller images will be blurry, while larger images will be automatically scaled down.
>

### Why can't messages be displayed in the notification bar after arriving at mobile phones on Meizu Flyme 6.0 or below?

1. Manual integration is used on Meizu phones on Flyme 6.0 and below.
2. Automatic integration is used on Meizu phones on Flyme 6.0 and below, and the version of the used TPNS SDK for Android is below 1.1.4.0.

In the above two cases, you need to place an image exactly named `stat_sys_third_app_notify` in the `drawable` folders with different resolutions. The image is stored in the `flyme-notification-res` folder of the Meizu vendor dependency directory of [TPNS Android SDK](https://console.cloud.tencent.com/tpns/sdkdownload).


### How do I fix the exception that occurs when I use quick integration in the console?

1. If an exception occurs during integration, set the `debug` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, use the `TpnsPlugin` keyword for analysis.
2. Click the **sync projects** icon.
![](https://main.qcloudimg.com/raw/5fecbe6b63374e7e0e58c4b2cd215acb.png)
3. Check whether relevant dependencies exist in **External Libraries** of the project.
![](https://main.qcloudimg.com/raw/485c7595f1b478a6fad725d38deb87b4.png)


### How do I convert Android extension library v4 to AndroidX?

Add the following attributes to the `gradle.properties` file of the AndroidX project:
```
android.useAndroidX=trueandroid.enableJetifier=true
```

> ? 
> - `android.useAndroidX=true`: to enable AndroidX for the current project.
> - `android.enableJetifier=true`: to migrate the dependency package to AndroidX. 
> 

### What should I do if "the application transferred information over HTTP in plaintext" is reported for vendor channel push SDKs?

After you integrate the push services of various vendor channels, certain security detection tools may prompt that "the application transferred information over HTTP in plaintext". HTTP addresses involved are as follows:
1. Mi Push SDK: `http://new.api.ad.xiaomi.com/logNotificationAdActions，http://resolver.msg.xiaomi.net/psc/?t=a`
2. Meizu Push SDK: `http://norma-external-collect.meizu.com/android/exchange/getpublickey.do，http://norma-external-collect.meizu.com/push/android/external/add.do`

All the above HTTP URLs are from the push SDKs of relevant vendors. The TPNS team is unable to clarify their purposes or control their behaviors but is actively contacting them and promoting the adoption of transfer over HTTPS. Currently, you should evaluate and choose whether to continue to use the above vendors' push services.


### What should I do if Android v4.4.4 reports a compiling error?

If the number of loaded methods in the project exceeds 65,000, please create subpackages for the project.

### What should I do if I specified to open an `Activity` page but it often cannot be redirected to normally?

On some phones, redirection upon click on the notification bar may experience permission issues.
Solution: in `androidManifest.xml`, add `android:exported="true"` to the `Activity` to be opened.

### Can the registration method be created in a thread?
The registration method can be called anywhere, but applicationContext must be input.

