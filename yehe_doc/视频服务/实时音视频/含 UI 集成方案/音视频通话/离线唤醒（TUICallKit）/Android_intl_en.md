 The offline call push feature enables your application to receive audio/video calls even if it runs in the background or is offline. `TUICallKit` integrates the `TUIOfflinePush` component to implement the offline call push feature. This document describes how to integrate the `TUIOfflinePush` component in your audio/video call project.

## Preparations

1. **Register your application on vendors' push platforms.** The offline push feature relies on the vendors' own channels. You need to register your application on the vendors' push platforms to get parameters such as `APPID` and `APPKEY`.

>! **The following two files will be used in subsequent steps:**
>- When registering on Huawei Push, download and save the `agconnect-services.json` file.
>- When registering on Google FCM, download and save the `google-services.json` file.
> | Google FCM                                                   |
   > | ------------------------------------------------------------ |
   > | ![img](https://qcloudimg.tencent-cloud.cn/raw/aa734c4d4a8c1c2580b964360ad66304.png) |


2. **Configure in the IM console** 

You need to enter the same package name when registering on each vendor channel for message interconnection. Record the generated ID, `APPID`, and `APPKEY`, which will be used in subsequent steps. 

## Step 1. Download and import the component

1. Go to [GitHub](https://github.com/tencentyun/TUICalling), clone or download the code, and copy the `tuiofflinepush` subdirectory in the `Android` directory to the same directory as `app` in your project, as shown below.

![img](https://qcloudimg.tencent-cloud.cn/raw/8ce4eb830c8880f523e3aa833150c864.png)﻿﻿

2. Find the `setting.gradle` file in the project root directory and add the following code:

```java
include ':tuiofflinepush'
```

3. Find the `build.gradle` file in the `app` directory and add the following code to declare the dependencies of the current application on the `TUIOfflinePush` component just added:

```java
api project(':tuiofflinepush')
```

## Step 2. Configure the project

1. In the `app` directory, find the `build.gradle` file and rename the application package as needed.

```java
applicationId 'com.****.trtc'
```

2. In the `app` directory, find the `build.gradle` file and set `ViVo` access parameters `VIVO_APPKEY`, `VIVO_APPID`, and `HONOR_APPID` to avoid compilation or execution errors.

```java
manifestPlaceholders = [
    "VIVO_APPKEY": "PLACEHOLDER", 
    "VIVO_APPID" : "PLACEHOLDER",
    "HONOR_APPID": "PLACEHOLDER"
]
```

3. Configure the files for **Huawei** and **Google** push platforms: In the `app` directory, replace the `google-services.json` file, which is the one saved when you registered on Google FCM during [Preparations](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87). In the `app` directory, add the `agconnect-services.json` file, which is the one saved when you registered on Huawei Push during [Preparations](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87).

4. Enter the ID, `APPID`, `APPKEY` recorded during [Preparations](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87) in the `PrivateConstants` file and check whether the parameter configuration is correct. **Enter the following parameters:**

```java
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

>! This step is very important. Carefully check whether the parameter configuration is correct.

 After you complete the above steps, your project can use the offline call push feature of `TUICallKit`.

## Step 3. Customize the offline notification content

`TUICallKit` provides the default notification format. However, if you want to customize the notification content, modify the [OfflinePushInfoConfig.java](https://github.com/tencentyun/TUICallKit/blob/main/Android/tuicallkit/src/main/java/com/tencent/qcloud/tuikit/tuicallkit/config/OfflinePushInfoConfig.java) file.

```java
public static TUIOfflinePushInfo createOfflinePushInfo(Context context) {    
    TUIOfflinePushInfo pushInfo = new TUIOfflinePushInfo();    
    pushInfo.setTitle("mike");    
    pushInfo.setDesc("You have receive a new call");    
    // For OPPO, you must set the `ChannelID` to receive push messages. The `ChannelID` must be identical with that in the console.    
    // OPPO must set a ChannelID to receive push messages. This channelID needs to be the same as the console.    
    pushInfo.setAndroidOPPOChannelID("tuikit");    
    pushInfo.setIgnoreIOSBadge(false);    
    pushInfo.setIOSSound("phone_ringing.mp3");  
    return pushInfo;
}
```

## FAQs

If users cannot receive offline push notifications, [contact us](https://intl.cloud.tencent.com/contact-us) for troubleshooting.

### 1. What should I do if notifications cannot be received?

Test the push service in the vendor console. If notifications can be pushed successfully, the vendor channel is normal. Then, check whether vendor parameters are configured correctly in the `TUIOfflinePush` console, and if not, enter the parameters as required. (As tested, you must configure the message type in the console for vivo X9).

Some phones will send notifications to the `Unimportant Notifications` folder. In this case, drag down the status bar and check whether the notifications are in the `Unimportant Notifications` folder.

Filter the following log to check whether `TUIOfflinePush` is registered successfully:

```java
TUIOfflinePush
```

### 2. Why can't the locked screen turn on when a notification is received?

Due to restrictions imposed by the vendor and platform, Android phones require different permissions when their screen is locked. Troubleshoot as follows:

**Check whether the system lock screen notification permission is enabled.** Some vendors have imposed unified restrictions. For example, if a Mi phone doesn't turn on its screen when receiving offline notifications, select **Settings** > **Lock screen** and toggle on **Wake Lock screen for notifications**.

**Check whether the lock screen notification permission of the application is enabled.** For example, on a Mi phone, you need to toggle on **Allow Lock screen notifications**.

>? If you need compatibility processing for this problem, contact us for assistance.

### 3. Why can't the call UI be pulled when I click an offline push notification?

Filter the following log to check whether the call request is detected:

```java
onReceiveNewInvitation
```

### 4. Why can't the call UI be pulled to the foreground when the application is running in the background?

**To automatically pull the application from the background to the foreground, it is necessary to check whether the "background autostart" or "floating window" permission is enabled on the application.**

Note that different vendors or even different Android versions from the same vendor offers different permissions and permission names. For example, you only need to enable the **background pop-up window** permission for Mi 6, while you need to enable both the **background pop-up window** and **floating window display** permissions.

>? If you manually enable all permissions during the test, the call UI still cannot be automatically pulled to the foreground, and compatibility processing is required.


