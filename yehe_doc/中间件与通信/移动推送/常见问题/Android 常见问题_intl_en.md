### Why was the Implicit PendingIntent Vulnerability error reported when I published my application on Google Play?
1. The Tencent Push Notification Service SDK uses an implicit PendingIntent in `TPushAlarmManager.set` in the code to trigger SDK internal heartbeats.
You can address the issue by referring to Google's [Remediation for Implicit PendingIntent Vulnerability](https://support.google.com/faqs/answer/10437428). The following self-check has been performed for the SDK:
a. The `setAction` used is a static broadcast action declared by the SDK and poses no exposure risk.
b. The target of the PendingIntent is the SDK's internal static broadcast action, and the broadcast permission declared by SDK has been added.

2. Google's documentation mentions the following: "Fixing this issue is recommended but not mandatory. The publication status of your app will be unaffected by the presence of this issue."

The current PendingIntent used by Tencent Push Notification Service is a trusted and secure PendingIntent, and Google claimed that the issue will not affect the publication of your application. You can ignore this message and continue to publish your application.

### How do I set a custom ringtone?

You can set a custom ringtone by creating a notification channel.
1. Create a notification channel for a specified custom ringtone file by calling the API encapsulated in Tencent Push Notification Service or the Android native API. For more information, see the **Creating a notification channel** section in [API Documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
2. Call the push Restful API of Tencent Push Notification Service and specify the same notification channel `n_ch_id` for push. For a vendor channel, you must specify the vendor channel ID, such as `hw_ch_id` for the Huawei channel and `xm_ch_id` for the Mi channel.

>?
- Currently, only Huawei, Mi, FCM, and Tencent Push Notification Service channels support custom ringtones.
- For some vendor channels, before using the push channels of some vendors, you need to apply for notification classification permissions. For details and application steps, see [Vendor Message Classification Feature Use Instructions](https://intl.cloud.tencent.com/document/product/1024/36250).
- For Huawei push channel, if you select China as the data processing location when you apply for the Huawei push service for your application in the Huawei push console, the channel customization feature is no longer applicable to your application. That is, you cannot use the notification channel capability to customize notification ringtones. For more information, see [Notification Channel Customization](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/android-custom-chan-0000001050040122).

### How do I disable the session keep-alive feature of Tencent Push Notification Service?

To disable the feature, call the following API in `onCreate` of `Application` or `LauncherActivity` during application initialization and pass in `false`:
>! The session keep-alive feature can be disabled only in SDK v1.1.6.0 or later. In SDKs earlier than v1.1.6.0, the feature is enabled by default and cannot be disabled.

```java
XGPushConfig.enablePullUpOtherApp(Context context, boolean pullUp);
```

If you use Gradle automatic integration, configure the following node under the `<application>` tag of the `AndroidManifest.xml` file of your application, where `xxx` is a custom name. For manual integration, modify node attributes as follows:
```xml
<!-- Add the following node to the `AndroidManifest.xml` file of your application, where xxx is a custom name: -->     
<!-- To disable the feature of keep-alive with Tencent Push Notification Service, configure as follows: -->
<provider
		 android:name="com.tencent.android.tpush.XGPushProvider"
		 tools:replace="android:authorities"
		 android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
		 android:exported="false" />    
```

If the following log is printed in the console, the session keep-alive feature has been disabled: `I/TPush: [ServiceUtil] disable pull up other app`

### How do I configure not to automatically enable the push service at the first start of the application after installation?

For the scenario where the user agrees to the Terms of Service and Privacy Policy, you can add the following node to the `AndroidManifest.xml` file, so that the push service is not automatically enabled at the first start of the application after installation until the push service registration API `XGPushManager.registerPush()` is called:

```
<meta-data
android:name="XG_SERVICE_PULL_UP_OFF"
android:value="true" />
```
### Does the Tencent Push Notification Service SDK support push from HarmonyOS?

HarmonyOS is fully compatible with the Android SDK, so HarmonyOS users can use the push feature normally.


### Do vendor push services need to be launched in application markets before they can be enabled?

| Vendor | Need to Be Launched to Application Markets |
|---------|---------|
| Mi | Yes. You need an enterprise developer account to enable Mi Push. For details, see [here](https://dev.mi.com/console/doc/detail?pId=68). | 
| Meizu | No. You only need an individual developer account to enable Meizu Push. For details, see [here](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf). | 
| FCM | No. You only need an individual developer account to enable FCM Push. |
| Huawei | No. You only need an individual developer account to enable Huawei Push. For details, see [here](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-enable_service#enable-service). | 
| OPPO | Yes. You need an enterprise developer account to enable OPPO PUSH. For details, see [here](https://open.oppomobile.com/wiki/doc/#id=10195). | 
| vivo | Yes. You need an enterprise developer account to enable vivo Push. For details, see [here](https://dev.vivo.com.cn/documentCenter/doc/2). |


### What should I do if "the application contains unused permission strings" is reported after the vivo channel is integrated?

After you integrate the push services of the vivo channel, certain security detection tools may prompt that "the application contains unused permission strings". Details are as follows: 
Cause: vivo channel push SDK v2.3.4
Class file involved: `com.vivo.push.util.z`; sensitive permission string involved: `android.permission.GET_ACCOUNTS`
>! Inspection found that the problem still persists in the vivo channel push SDK v3.0.0.3.

The defective code is from the vivo channel push SDK. The Tencent Push Notification Service team is unable to change the code and has reported it to vivo. vivo replied that the relevant static fields are the legacy code of the SDK and are not actually used, and they will schedule to fix the problem as soon as possible. The following are quick solutions for your reference:
- Solution 1 (recommended): Add the [Privacy Policy](https://www.tencentcloud.com/document/product/1024/36175?lang=en&pg=) to the App Privacy Statement. 
- Solution 2 (not recommended): Remove vivo-related JAR packages, which will make the vivo channel unavailable.

### What is the Tencent Push Notification Service channel?

- The Tencent Push Notification Service channel deeply relies on the Tencent Push Notification Service, and messages can be delivered only when the Service is online (maintaining a persistent connection with the backend server). Thus, the actual delivery of this channel is generally lower than that of a vendor channel.
- If you need to implement offline push, we recommend you integrate a vendor channel. For more information, see [here](https://intl.cloud.tencent.com/document/product/1024/37176).



### Why pushes cannot be received after the application is closed?

- Currently, almost all third-party push services cannot guarantee that the pushes can be received after the application is closed. This problem arises from the restrictions of the mobile phone's custom ROM on the Service. All pushes through the Tencent Push Notification Service channel can be delivered only when the Service maintains a persistent connection with the backend server. After the Service is terminated, whether to restart it depends on the system settings, security programs, and user operations.
- After the Service is disconnected from the server, messages delivered to the device will become offline messages and can be retained for up to 72 hours. If there are multiple offline messages, only the latest three can be retained on the device. If messages pushed when the application is closed cannot be received after the application is launched again, check whether the `XGPushManager.unregisterPush\(this\)` API has been called.
- If you have already integrated a vendor channel, but pushes still cannot be received offline, use the [troubleshooting tool](https://console.cloud.tencent.com/tpns/user-tools) to check whether the token has been successfully registered with the vendor, and if not, troubleshoot as instructed in [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).
- QQ and Weixin are in the system-level application allowlist, and their services will not be terminated but survive on the backend after they are closed, so the user can still receive messages.

### Why does device registration fail?

- Data sync for newly created applications will take about one minute. During this period, the registration may return the error code 20. You can try again later.
- **Incorrect parameter**: Check whether `Access ID` and `Access Key` are correctly configured. Common errors include misuse of `Secret key` instead of `Access Key` or spaces before and/or after `Access Key`.
- **Registration error:** If the console returns an error code such as 10004, 10002, or 20, see [Error Code](https://intl.cloud.tencent.com/document/product/1024/30722).
- **No callback after registration:** Check the current network condition. We recommend you test with a 4G network, because the bandwidth of the Wi-Fi used by many users may be insufficient.
- **Nubia phones:** Models released in the second half of 2015 and in 2016 cannot be registered, including Nubia Z11 series, Nubia Z11S series, and Nubia Z9S series.

### Why can't pushes be received after successful registration?

Perform automated troubleshooting with the troubleshooting tool as instructed [here](https://intl.cloud.tencent.com/document/product/1024/38389). General errors include the following:

- Check whether the current app package name is the same as that entered when the application is registered, and if not, you are recommended to enable multi-package name push.
- Check whether the mobile network has any exceptions: switch to 4G network for testing.
- Push messages include **notification bar message** and **in-app message** (passthrough message). A notification bar message can be displayed in the notification bar, while an in-app message cannot.
- Confirm that the phone is in the normal mode. Some phones may have restrictions on network and activity of the Tencent Push Notification Service process in the backend when in the Low Power or Do Not Disturb mode.
- Check whether the notification bar permission is granted on the phone. For some OPPO and vivo phones, the notification bar permission has to be granted manually.

### Why can't pushes be received on a Nubia phone?
Tencent Push Notification Service is not available on Nubia phones released after 2015, because the new version of Nubia operating system added a super power-saving feature that kills background processes quickly and prevent the Service from being started, resulting in failures of registration with Nubia phones.



### I installed Huawei Mobile Service on a non-Huawei phone and integrated the Tencent Push Notification Service SDK with my application, but this made Huawei Push and other components fail. How do I fix this problem?

From SDK v1.1.6.3, in order to avoid **the situation where push services of other vendors auto-start and transfer user data on the background on a phone**, push service components of other vendors will be disabled on the phone.
Huawei uses some common components for different features such as account, game, and push. Disabling the push component by Tencent Push Notification Service may make other service features unable to start on a non-Huawei phone. To disable this disablement feature, configure the following:
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

>! Click callback of vendor channels is supported by SDK v1.2.0.1 and later. Legacy versions support this feature only for Huawei, Mi, Meizu, and vivo.
>


### Why `title` and `content` obtained by `onNotifactionClickedResult` and `onNotificationShowedResult` are empty when the application is closed?

To obtain the `title` and `content` of the offline push via a vendor channel, concatenate `title` and `content` parameters to the `intent uri` of notification tap-to-redirect, and obtain them after notification tap-to-redirect. See [Notification Tap-to-Redirect](https://intl.cloud.tencent.com/document/product/1024/38354) for details.


### How do I fix the problem of null `other push Token` that occurs during debugging after my application is integrated with a vendor channel?


Check whether the application operation logs contain information similar to the following: 
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: huawei
```

Such log information means that your application failed to register with the vendor channel. In that case, get the return code for vendor channel registration failure to locate and troubleshoot the problem. For more information, see [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).


### How do I adapt small icons?

- ROMs running native Android 5.0 or later will process the small icon of an application and add a layer of color if `target sdk` is greater than or equal to 21, making the icon gray.
- If you want to display it as colored, you can set `target sdk` to a value smaller than 21. If you don't want `target sdk` to be below 21, you can rename a small .png image with a transparent background to `notification_icon.png` (the filename must be unique) and place it in the `drawable` directory; in this way, the small icon will be displayed as gray (but shaped).
- Starting from Tencent Push Notification Service SDK v1.2.2.0 for Android, the `notification_icon.png` small icon resource will only take effect directly on Google Pixel phones by default. To achieve such small icon effect for custom notifications on other phones, you need to specify the resource filename (without the extension) as the value of the `message.android.small_icon` field in the push API. In addition, the custom notification small icon supports solid colors by specifying the decimal value of an RGB color as the value of the `message.android.icon_color` field in the push API.

Below is an example of push API fields, where `icon_color: 123456` indicates the RGB color #01e240:
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

The display effect after adaption is as shown below. [We recommend you draw an icon based on the demo logo](https://git.code.tencent.com/tpns/tpns-Demo-Android/blob/master/app/src/main/res/drawable/notification_icon.png).

<img src="https://qcloudimg.tencent-cloud.cn/raw/f3df2a69acc72d182fd74a6799734dd9.jpg" width="60%"></img>


>?
- The small icon must be a PNG image with an alpha channel.
- The background must be transparent.
- Do not leave too much padding around the icon.
- We recommend you use an image with dimensions of 46x46, as smaller images will be blurry, while larger images will be automatically scaled down.


### Why can't messages be displayed in the notification bar after arriving at mobile phones on Meizu Flyme 6.0 or earlier?

1. Manual integration is used on Meizu phones on Flyme 6.0 and earlier.
2. Automatic integration is used on Meizu phones on Flyme 6.0 and earlier, but the version of the used Tencent Push Notification Service SDK for Android is earlier than 1.1.4.0.

In the above two cases, you need to place an image exactly named `stat_sys_third_app_notify` in the `drawable` folders named at different resolutions. You can get the image from the `flyme-notification-res` folder under `meizu` of [Tencent Push Notification Service Android SDK](https://console.cloud.tencent.com/tpns/sdkdownload).


### How do I fix the exception that occurs when I use quick integration in the console?

1. If an exception occurs during integration, set the `debug` field in the `tpns-configs.json` file to `true` and run the following command: 
```
./gradlew --rerun-tasks :app:processReleaseManifest 
```
Then, analyze with the `TpnsPlugin` keyword.
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
1. Mi Push SDK: http://new.api.ad.xiaomi.com/logNotificationAdActions, http://resolver.msg.xiaomi.net/psc/?t=a
2. Meizu Push SDK: http://norma-external-collect.meizu.com/android/exchange/getpublickey.do, http://norma-external-collect.meizu.com/push/android/external/add.do

All the above HTTP URLs are from the push SDKs of relevant vendors. The Tencent Push Notification Service team is unable to clarify their purposes or control their behaviors, but is actively contacting them and promoting the adoption of transfer over HTTPS. Currently, you should evaluate and choose whether to continue to use the above vendors' push services.


### What should I do if Android v4.4.4 reports a compiling error?

If the number of loaded methods in the project exceeds 65,000, please create subpackages for the project.

### What should I do if I specified the redirection action as opening an `Activity` page, but the redirection fails frequently?

On some phones, redirection upon click on the notification bar may experience permission issues.
Solution: In `androidManifest.xml`, add `android:exported="true"` to the `Activity` page to be opened.

### Can the registration method be created in a thread?
The registration method can be called anywhere, but `applicationContext` must be input.

### Can I use the FCM channel without Google services installed on my phone?
No. Google services and a network with normal access to Google are necessary for using the FCM channel.

### What clusters is the FCM channel applicable to?
The FCM channel is applicable to clusters in Hong Kong (China) and Singapore.


### Why "no message arrival data" is reported after a message is delivered successfully?
**Troubleshooting process:**
**Vendor channel delivery failure**:
1. Check whether the limit on the number of messages pushed per device per day of the vendor channel is exceeded. For the message count limits of different vendors, see [Vendor Message Classification Feature Use Instructions](https://intl.cloud.tencent.com/document/product/1024/36250). For example, Huawei's return code 256 indicates that the limit on the information and marketing messages sent in the current day is exceeded and that the message sending policy needs to be adjusted.
2. Check whether [the display of message arrival receipts](https://intl.cloud.tencent.com/document/product/1024/35246) is configured for the Huawei, HONOR, and Meizu push channels. If not, arrival data cannot be reported (without affecting the actual push results).
3. The vendor delays the message delivery. If Tencent Push Notification Service has delivered the message to the vendor in time but the vendor does not deliver the message to the device, you can contact the vendor for reasons.
4. Check whether the notification bar is enabled. For some vivo and OPPO models, the notification bar is disabled by default. Determine whether to manually enable the notification bar.

**Tencent Push Notification Service channel delivery failure**:
Possible case 1: The Tencent Push Notification Service backend delivered the message via the Tencent Push Notification Service channel when the link between the Tencent Push Notification Service SDK and the backend was actually disconnected. As a result, the message failed to reach the device.
Possible case 2: By default, the Tencent Push Notification Service SDK sends a heartbeat at an interval of five minutes to maintain a persistent connection. When it fails to send a heartbeat, the SDK immediately rebuilds the persistent connection. For example, if the SDK receives five push messages from the backend before the persistent connection is rebuilt successfully, only the latest three push messages will be delivered after the persistent connection is rebuilt. As a result, the first two push messages are delivered through the Tencent Push Notification Service channel and fail to reach the device.
Possible case 3: No arrival event was reported but the message actually reached the device (the actual push effect is not affected).

