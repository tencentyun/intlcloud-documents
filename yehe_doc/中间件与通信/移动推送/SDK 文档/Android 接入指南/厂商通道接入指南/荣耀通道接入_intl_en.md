## Overview
Starting from v1.3.3.0, the Tencent Push Notification Service SDK supports connection to the HONOR Push channel. The HONOR channel is a system-level push channel officially provided by HONOR. On an HONOR phone, push messages can be delivered through HONOR's system channel without opening the application. For more information, see [HONOR Push Overview](https://developer.hihonor.com/doc/guides/100220).

>?
> - Currently, the HONOR channel only supports HONOR devices on Magic UI 6.0 or later, while older HONOR devices can use the Huawei Push channel instead. In the future, the HONOR channel will also support HONOR devices on Magic UI 5.0 and 4.0.
> - To apply for the activation of the HONOR Push service, you need an HONOR business/organization developer account.
> - For HONOR Push, you can successfully register with the vendor channel and push messages through it only in a signed package environment.

## Directions

### Step 1. Get the key
1. Sign up for an HONOR developer account [here](https://developer.hihonor.com/) and log in. For more information, see [Registration](https://developer.hihonor.com/cn/doc/guides/100084). (To use HONOR Push, you need to register a business/organization developer account.)
2. Create an application on the HONOR Developers platform, enter the application information such as application package name and certificate fingerprint, and activate the push service. For more information, see [here](https://developer.hihonor.com/doc/guides/100221). For how to get the application certificate fingerprint, see the **1.1 Development Environment** section in [HONOR Push Android Development Documentation](https://developer.hihonor.com/doc/guides/100223).
3. Copy the application's `AppId`, `Client ID`, and `Client Secret` and paste them into the `AppId`, `ClientId`, and `SecretKey` fields in **[Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **HONOR Official Push Channel**.


### Step 2. Configure items
Choose either of the following integration methods.
#### Integrating through Android Studio

Complete the configuration required by Tencent Push Notification Service in the `build.gradle` file in the **Application** module and then add the following nodes:
1. Configure the HONOR Push `AppID`. The sample code is as follows:
```xml
 manifestPlaceholders = [
	 HONOR_APPID  : "xxxx"
        ]
```
2. Import the dependencies related to HONOR. The sample code is as follows:
```groovy
implementation 'com.tencent.tpns:honor:[VERSION]-release'
```

>? 
> - For HONOR Push, [VERSION] is the version number of the current SDK and can be obtained from the [SDK for Android](https://intl.cloud.tencent.com/document/product/1024/36191), which is supported starting from v1.3.3.0.
> - HONOR Push is compatible with the preset `<queries>` tag on Android 11. Upgrade Android Studio to v3.6.1 or later, and upgrade the Android Gradle plugin to v3.5.4 or later; otherwise, an error may occur when you build the project.


### Integrating through Eclipse
After getting the Tencent Push Notification Service SDK package for HONOR Push, configure the major Tencent Push Notification Service version and the following content in the manual integration method detailed on Tencent Push Notification Service's official website.

1. Download the [SDK installation package](https://console.cloud.tencent.com/tpns/sdkdownload).
2. Open the `Other-Push-jar` folder and import the HONOR Push-related jar package.
3. Add the following configuration to the `Androidmanifest.xml` file:
```xml
    <application>
        <receiver
            android:name="com.hihonor.push.sdk.PushReceiver"
            android:exported="true"
            android:permission="${applicationId}.hihonor.permission.PROCESS_PUSH_MSG">
            <intent-filter>
                <action android:name="com.hihonor.push.action.REGISTRATION" />
                <action android:name="com.hihonor.push.action.RECEIVE" />
            </intent-filter>
        </receiver>

        <provider
            android:name="com.hihonor.push.sdk.init.AutoInitProvider"
            android:authorities="${applicationId}.hihonor.autoinitprovider"
            android:exported="false"
            android:initOrder="500" />

        <!-- Custom HONOR push callback service -->
        <service
            android:name="com.tencent.android.tpush.honor.HonorMessageService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.hihonor.push.action.MESSAGING_EVENT" />
            </intent-filter>
        </service>

        <meta-data
            android:name="com.hihonor.push.sdk_version"
            android:value="6.0.3.102" />

        <!-- HONOR Push appId -->
        <meta-data
            android:name="com.hihonor.push.app_id"
            android:value="HONOR Push AppId"
    </application>

    <permission
        android:name="${applicationId}.hihonor.permission.PROCESS_PUSH_MSG"
        android:protectionLevel="signatureOrSystem" />

    <uses-permission android:name="com.hihonor.push.permission.READ_PUSH_NOTIFICATION_INFO" />

    <queries>
        <intent>
            <action android:name="com.hihonor.push.action.BIND_PUSH_SERVICE" />
        </intent>
    </queries>
```


### Step 3. Enable HONOR Push
Enable the third-party push API before calling Tencent Push Notification Service's `XGPushManager.registerPush`:
```java
// Enable third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);


// The log of successful registration is as follows:
I/TPush: [OtherPushClient] handleUpdateToken other push token is : IQAAAACy0Ps******GlJi_5-0rpskunnNMcat35HA  other push type: honor
I/TPush: [PushServiceBroadcastHandler] >> bind OtherPushToken success ack with [accId = 150000****  , rsp = 0]  token = 01a22******ed343 otherPushType = honor otherPushToken = IQAAAACy0Ps******GlJi_5-0rpskunnNMcat35HA 

```

### Step 4. Obfuscate the code
```xml
-ignorewarnings
-keepattributes *Annotation*
-keepattributes Exceptions
-keepattributes InnerClasses
-keepattributes Signature
-keepattributes SourceFile,LineNumberTable

-keep class com.hihonor.push.framework.aidl.**{*;}
-keep class com.hihonor.push.sdk.**{*;}
```

>? Obfuscation rules must be stored in the `proguard-rules.pro` file at the application project level.
>

### Step 5. Configure arrival receipt for HONOR channel
The arrival receipt for the HONOR channel should be configured by yourself. After configuring this feature as instructed in [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246), you can view the arrival data for the HONOR push channel in the push records.

## Troubleshooting

### Querying HONOR Push registration error codes

If you observe logs similar to the following, it indicates that registration with the HONOR channel fails. In this case, you can use the method described to get the HONOR Push registration error code.
```
[OtherPushClient] handleUpdateToken other push token is :  other push type: honor
```

In debugging mode of the push service, filter logs by the keyword `OtherPush` to view the return code logs. Then, locate the error cause and fix the error by referring to [Troubleshooting Vendor Channel Registration Failures](https://intl.cloud.tencent.com/document/product/1024/37006).

