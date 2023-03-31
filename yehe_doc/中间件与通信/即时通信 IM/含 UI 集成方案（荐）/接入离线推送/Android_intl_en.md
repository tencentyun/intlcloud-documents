````
## Overview
IM terminal users need to obtain the latest messages at any time. However, considering the limited performance and battery SOC of mobile devices, IM recommends you use the system-grade push channels provided by vendors for message notifications when the app is running in the background to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push channels, system-grade push channels provide more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

>!
>- If you want users to receive IM message notifications when, without proactive logout, the app is switched to the background, the mobile phone screen is locked, or the app process is killed by a user, you can enable the IM offline push.
>- If the `logout` API is called to log out proactively or you are forced to log out due to multi-device login, you cannot receive offline push messages even though IM offline push is enabled.

## Integrating TUIOfflinePush and Running the Offline Push Feature
Before integrating the TUIOfflinePush component, [register your application on the vendor push platform](https://intl.cloud.tencent.com/document/product/1047/39156), log in to your Tencent Cloud account, and configure the [IM console](https://intl.cloud.tencent.com/document/product/1047/39156) and [redirected-to page for offline push](https://intl.cloud.tencent.com/document/product/1047/39156). Then quickly integrate the IM offline push feature in the following steps.

>!
>- If you want to integrate the TUIOfflinePush component as easily as possible, you need to log in and log out using the login and logout APIs provided by [TUILogin](https://github.com/TencentCloud/TIMSDK/blob/master/Android/TUIKit/TUICore/tuicore/src/main/java/com/tencent/qcloud/tuicore/TUILogin.java) of the TUICore component, and the TUIOfflinePush component automatically senses the login and logout events. If you don't want to use the APIs provided by TUILogin, you need to manually call the `registerPush` and `unRegisterPush` APIs provided by [TUIOfflinePushManager](https://github.com/TencentCloud/TIMSDK/blob/master/Android/TUIKit/TUIOfflinePush/tuiofflinepush/src/main/java/com/tencent/qcloud/tim/tuiofflinepush/TUIOfflinePushManager.java) after login and logout respectively.
>- This plugin is supported by the following vendors: Mi, Huawei, Honor, OPPO, vivo, Meizu, and Google.

### Step 1. Integrate the TUIOfflinePush component
```
api project(':tuiofflinepush')
```

-  **vivo and Honor**
According to vendor integration guides of vivo and Honor, you need to add the `APPID` and `APPKEY` to the list file; otherwise, a compilation problem will occur.
<dx-tabs>
::: Method 1
<table> 
<tr> 
```
android {
    ...
    defaultConfig {
		    ...
        manifestPlaceholders = [
                "VIVO_APPKEY" : "`APPKEY` of the certificate assigned to your application",
                "VIVO_APPID" : "`APPID` of the certificate assigned to your application"
                "HONOR_APPID" : "`APPID` of the certificate assigned to your application"
        ]
    }
}
```
</tr> 
</table>
:::
::: Method 2
<table> 
<tr> 
```
// vivo start
<receiver android:name="com.tencent.qcloud.tim.demo.thirdpush.VIVOPushMessageReceiverImpl">
    <intent-filter>
        <!-- Receive push message -->
        <action android:name="com.vivo.pushclient.action.RECEIVE" />
    </intent-filter>
</receiver>

<meta-data tools:replace="android:value"
    android:name="com.vivo.push.api_key"
    android:value="`APPKEY` of the certificate assigned to your application" />
<meta-data tools:replace="android:value"
    android:name="com.vivo.push.app_id"
    android:value="`APPID` of the certificate assigned to your application" />
// vivo end

// Honor start
<service
    android:name="com.tencent.qcloud.tim.tuiofflinepush.oempush.MyHonorMessageService"
    android:exported="false">
    <intent-filter>
        <action android:name="com.hihonor.push.action.MESSAGING_EVENT" />
    </intent-filter>
 </service>
				
<meta-data tools:replace="android:value"
    android:name="com.hihonor.push.app_id"
    android:value="`APPID` of the certificate assigned to your application" />
// Honor end
```
</tr> 
</table>
:::
</dx-tabs>

-  **Adaptation to Huawei and Google FCM**
For Huawei and Google FCM, you need to integrate the corresponding plugin and JSON configuration files by the vendor's methods.

 1. Download the configuration file and place it under the root directory of the project.

 2. Add the following configuration under "buildscript -> dependencies" of the project-level `build.gradle` file.
```
repositories {
    ...
     // Configure the Maven repository address for the HMS Core SDK
     maven {url 'https://developer.huawei.com/repo/'}
}
    
dependencies {
    ...
    classpath 'com.google.gms:google-services:4.2.0'
    classpath 'com.huawei.agconnect:agcp:1.4.1.300'
}

```

3. Add the following configuration in the app-level `build.gradle` file.

```
apply plugin: 'com.google.gms.google-services'
apply plugin: 'com.huawei.agconnect'
```

### Step 2. Set push parameters
After a push certificate is added successfully as instructed, the IM console will assign a certificate ID that needs to be filled in as a configuration parameter in [PrivateConstants](https://github.com/TencentCloud/TIMSDK/blob/master/Android/TUIKit/TUIOfflinePush/tuiofflinepush/src/main/java/com/tencent/qcloud/tim/tuiofflinepush/PrivateConstants.java). This ID will be needed for registering the push service and reporting the token. Take Mi as an example.


**Parameters to be filled in:**

```
   public class PrivateConstants {
   /****** Mi offline push parameters start ******/
   // Certificate ID generated after uploading a third-party push certificate in the Tencent Cloud console
   public static final long XM_PUSH_BUZID = ID of the certificate assigned to your application
   // `APPID` and `APPKEY` assigned by the Mi open platform
   public static final String XM_PUSH_APPID = "`APPID` of the certificate assigned to your application";
   public static final String XM_PUSH_APPKEY = "`APPKEY` of the certificate assigned to your application";
   /****** Mi offline push parameters end ******/
   }

```
 
 After the above steps are performed, offline push notifications can be received.

### Step 3. Set offline push parameters when sending messages

When sending a message, set offline push parameters as instructed in [sendMessage](https://intl.cloud.tencent.com/document/product/1047/39156).

### Step 4. Parse offline push messages
When a phone receives an offline push message, the message is displayed in the notification bar. When you click the message in the notification bar, the system automatically gets the offline push message passed through. For more information, see [Step 8. Parse offline push messages](https://intl.cloud.tencent.com/document/product/1047/39156).

## FAQs

### How do I customize alert tones for offline push?

SDK v6.1.2155 or a later version supports customizing alert tones on devices of Huawei, Mi, FCM and APNs. See the [setAndroidSound()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a3ff923225d5a79802a02c47a07e07fc5) and [setIOSSound()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#acffd09150398b06c3d7eb42baee5aee1) APIs of V2TIMOfflinePushInfo for specific methods.

### How do I troubleshoot if I cannot receive offline push messages?
#### 1. OPPO devices
This generally occurs for the following reasons:
- As required by OPPO, `ChannelID` must be configured for OPPO Android 8.0 or later; otherwise, push messages cannot be displayed. For configuration directions, see [setAndroidOPPOChannelID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a32d340e95395bb64cc3e8f62321aafe1).
- The notification bar display feature is disabled by default for applications installed on the OPPO device. If this is the case, check the switch status.

#### 2. Google FCM
If push messages cannot be received, check whether the certificates are successfully uploaded to the IM console by referring to "[IM console configuration](https://intl.cloud.tencent.com/document/product/1047/39156) - Google FCM".

#### 3. Sending custom messages
The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the [desc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe), and the `desc` information will be displayed by default during push.

#### 4. Notification bar settings of the device
The offline push message can be intuitively displayed in the notification bar, so, just as other notifications, it is subject to the notification settings of the device. Take a Huawei device as an example.

- "Settings - Notifications - Notifications (Lock Screen) - Hide or Do not Disturb" will affect the display of offline push notifications when the screen is locked.
- "Settings - Notifications - Advanced Settings - Show Notification Icons (Status Bar)" will affect the showing of the offline push notification icon in the status bar.
- "Settings - Notifications - Application Notifications - Allow Notifications" will directly affect the display of offline push notifications.
- "Settings - Notifications - Application Notifications - Notification Sound" and "Settings - Notifications - Application Notifications - Notification Mute" will affect the offline push notification sound.

#### 5. The failure still exists after integration as instructed
- First, test whether messages can be properly pushed offline by using the [offline test tool](https://console.cloud.tencent.com/im/tool-push-check) in the IM console.
If offline push does not work properly, and the device status is exceptional, check the parameters in the IM console and then check the code initialization and registration logic, including the vendor push service registration and IM offline push configuration.
If offline push does not work properly but the device status is normal, check whether the ChannelID is correct or whether the backend service is working properly.
- The offline push feature relies on the vendor's capabilities. Some simple characters may be filtered by the vendor and cannot be passed through and pushed.
- If offline push messages are not pushed timely or cannot be received, you need to check the vendor's push restrictions.

### How do I troubleshoot redirection failure?

Page redirection is implemented as follows: The backend delivers the redirection modes and page parameters that you configure for various vendors in the console to vendor servers based on vendor API rules. When you click the notification bar for offline push messages, the system opens and redirects to the corresponding page. Opening of the corresponding page also depends on the manifest file. Only when the configuration in the manifest file is consistent with that in the console, the corresponding page can be opened and redirected properly.

1. First, you need to check whether the configuration in the console and that in the manifest file are correct and consistent with each other. For more information, see the configuration of the TUIKit demo. Note that the API modes may vary by vendor.
2. If the system redirects to the configuration page, you need to check whether the parsing of offline messages on the configuration page and the page redirection are proper.


### Vendor's push restrictions

1. All vendors in China have adopted message classification mechanisms, and different push policies are assigned for different types of messages. To make the push timely and reliable, you need to set the push message type of your app as the system message or important message with a high priority based on the vendor's rules. Otherwise, offline push messages are affected by the vendor's push message classification and may vary from your expectations.
2. In addition, some vendors set limits on the daily volumes of app push messages. You can check such limits in the vendor's console.
If offline push messages are not pushed timely or cannot be received, consider the following:
   - Huawei: Push messages are classified into service & communication messages and news & marketing messages with different push effects and policies. In addition, message classification is associated with the self-help message classification permission.
     - If there is no self-help message classification permission, the vendor will perform secondary intelligent message classification on push messages.
     - If you have applied for the self-help message classification permission, push messages will be classified based on the custom classification and then pushed.
For more information, see [Message Classification Criteria](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835).
   - vivo: Push messages are classified into system messages and operational messages with different push effects and policies. The system messages are further subject to the vendor's intelligent classification for correction. A message that cannot be intelligently identified as a system message will be automatically corrected as an operational message. If the judgment is incorrect, you can give a feedback by email. In addition, the total number of push messages is subject to a daily limit determined based on the app subscription statistics by the vendor. 
See [vendor description 1](https://dev.vivo.com.cn/documentCenter/doc/359) or [vendor description 2](https://dev.vivo.com.cn/documentCenter/doc/156) for details.
   - OPPO: Push messages are classified into private messages and public messages with different push effects and policies. Private messages are those that a user pays certain attention to and wants to receive in time. The private message channel permission needs to be applied for via email. The public message channel is subject to a number limit.
See [vendor description 1](https://open.oppomobile.com/wiki/doc#id=11227) or [vendor description 2](https://open.oppomobile.com/wiki/doc#id=11210) for details.
   - Mi: Push messages are classified into important messages and general messages with different push effects and policies. In particular, only instant messages, reminders of attracted events, agenda reminders, order status change, financial reminders, personal status change, resource changes, and device reminders fall into the important message category. The important message channel can be applied for in the vendor's console. General push messages are subject to a number limit.
See [vendor description 1](https://dev.mi.com/console/doc/detail?pId=2422) or [vendor description 2](https://dev.mi.com/console/doc/detail?pId=2086) for details.
   - Meizu: Push messages are subject to a number limit.
See [vendor description](http://open.res.flyme.cn/fileserver/upload/file/202201/85079f02ac0841da859c1da0ef351970.pdf) for details.
   - FCM: Upstream message push is subject to a frequency limit.
See [vendor description](https://firebase.google.com/docs/cloud-messaging/concept-options?hl=en#upstream_throttling) for details.




```xxxxxxxxxx   After the above steps are performed, offline push notifications can be received.### Step 3. Set offline push parameters when sending messagesWhen sending a message, set offline push parameters as instructed in [sendMessage](https://intl.cloud.tencent.com/document/product/1047/39156).### Step 4. Parse offline push messagesWhen a phone receives an offline push message, the message is displayed in the notification bar. When you click the message in the notification bar, the system automatically gets the offline push message passed through. For more information, see [Step 8. Parse offline push messages](https://intl.cloud.tencent.com/document/product/1047/39156).## FAQs### How do I customize alert tones for offline push?SDK v6.1.2155 or a later version supports customizing alert tones on devices of Huawei, Mi, FCM and APNs. See the [setAndroidSound()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a3ff923225d5a79802a02c47a07e07fc5) and [setIOSSound()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#acffd09150398b06c3d7eb42baee5aee1) APIs of V2TIMOfflinePushInfo for specific methods.### How do I troubleshoot if I cannot receive offline push messages?#### 1. OPPO devicesThis generally occurs for the following reasons:- As required by OPPO, `ChannelID` must be configured for OPPO Android 8.0 or later; otherwise, push messages cannot be displayed. For configuration directions, see [setAndroidOPPOChannelID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a32d340e95395bb64cc3e8f62321aafe1).- The notification bar display feature is disabled by default for applications installed on the OPPO device. If this is the case, check the switch status.#### 2. Google FCMIf push messages cannot be received, check whether the certificates are successfully uploaded to the IM console by referring to "[IM console configuration](https://intl.cloud.tencent.com/document/product/1047/39156) - Google FCM".#### 3. Sending custom messagesThe offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the [desc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a318c40c8547cb9e8a0de7b0e871fdbfe), and the `desc` information will be displayed by default during push.#### 4. Notification bar settings of the deviceThe offline push message can be intuitively displayed in the notification bar, so, just as other notifications, it is subject to the notification settings of the device. Take a Huawei device as an example.- "Settings - Notifications - Notifications (Lock Screen) - Hide or Do not Disturb" will affect the display of offline push notifications when the screen is locked.- "Settings - Notifications - Advanced Settings - Show Notification Icons (Status Bar)" will affect the showing of the offline push notification icon in the status bar.- "Settings - Notifications - Application Notifications - Allow Notifications" will directly affect the display of offline push notifications.- "Settings - Notifications - Application Notifications - Notification Sound" and "Settings - Notifications - Application Notifications - Notification Mute" will affect the offline push notification sound.#### 5. The failure still exists after integration as instructed- First, test whether messages can be properly pushed offline by using the [offline test tool](https://console.cloud.tencent.com/im/tool-push-check) in the IM console.If offline push does not work properly, and the device status is exceptional, check the parameters in the IM console and then check the code initialization and registration logic, including the vendor push service registration and IM offline push configuration.If offline push does not work properly but the device status is normal, check whether the ChannelID is correct or whether the backend service is working properly.- The offline push feature relies on the vendor's capabilities. Some simple characters may be filtered by the vendor and cannot be passed through and pushed.- If offline push messages are not pushed timely or cannot be received, you need to check the vendor's push restrictions.### How do I troubleshoot redirection failure?Page redirection is implemented as follows: The backend delivers the redirection modes and page parameters that you configure for various vendors in the console to vendor servers based on vendor API rules. When you click the notification bar for offline push messages, the system opens and redirects to the corresponding page. Opening of the corresponding page also depends on the manifest file. Only when the configuration in the manifest file is consistent with that in the console, the corresponding page can be opened and redirected properly.1. First, you need to check whether the configuration in the console and that in the manifest file are correct and consistent with each other. For more information, see the configuration of the TUIKit demo. Note that the API modes may vary by vendor.2. If the system redirects to the configuration page, you need to check whether the parsing of offline messages on the configuration page and the page redirection are proper.### Vendor's push restrictions1. All vendors in China have adopted message classification mechanisms, and different push policies are assigned for different types of messages. To make the push timely and reliable, you need to set the push message type of your app as the system message or important message with a high priority based on the vendor's rules. Otherwise, offline push messages are affected by the vendor's push message classification and may vary from your expectations.2. In addition, some vendors set limits on the daily volumes of app push messages. You can check such limits in the vendor's console.If offline push messages are not pushed timely or cannot be received, consider the following:   - Huawei: Push messages are classified into service & communication messages and news & marketing messages with different push effects and policies. In addition, message classification is associated with the self-help message classification permission.     - If there is no self-help message classification permission, the vendor will perform secondary intelligent message classification on push messages.     - If you have applied for the self-help message classification permission, push messages will be classified based on the custom classification and then pushed.For more information, see [Message Classification Criteria](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835).   - vivo: Push messages are classified into system messages and operational messages with different push effects and policies. The system messages are further subject to the vendor's intelligent classification for correction. A message that cannot be intelligently identified as a system message will be automatically corrected as an operational message. If the judgment is incorrect, you can give a feedback by email. In addition, the total number of push messages is subject to a daily limit determined based on the app subscription statistics by the vendor. See [vendor description 1](https://dev.vivo.com.cn/documentCenter/doc/359) or [vendor description 2](https://dev.vivo.com.cn/documentCenter/doc/156) for details.   - OPPO: Push messages are classified into private messages and public messages with different push effects and policies. Private messages are those that a user pays certain attention to and wants to receive in time. The private message channel permission needs to be applied for via email. The public message channel is subject to a number limit.See [vendor description 1](https://open.oppomobile.com/wiki/doc#id=11227) or [vendor description 2](https://open.oppomobile.com/wiki/doc#id=11210) for details.   - Mi: Push messages are classified into important messages and general messages with different push effects and policies. In particular, only instant messages, reminders of attracted events, agenda reminders, order status change, financial reminders, personal status change, resource changes, and device reminders fall into the important message category. The important message channel can be applied for in the vendor's console. General push messages are subject to a number limit.See [vendor description 1](https://dev.mi.com/console/doc/detail?pId=2422) or [vendor description 2](https://dev.mi.com/console/doc/detail?pId=2086) for details.   - Meizu: Push messages are subject to a number limit.See [vendor description](http://open.res.flyme.cn/fileserver/upload/file/202201/85079f02ac0841da859c1da0ef351970.pdf) for details.   - FCM: Upstream message push is subject to a frequency limit.See [vendor description](https://firebase.google.com/docs/cloud-messaging/concept-options?hl=en#upstream_throttling) for details.
````
