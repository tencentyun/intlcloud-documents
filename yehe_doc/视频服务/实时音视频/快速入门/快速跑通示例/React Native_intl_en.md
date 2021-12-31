This document describes how to quickly run the TRTC demo for React Native.

## Environment Requirements
- React Native 0.63 or above
- Node (above v12) & Watchman
- **Developing for Android:**
  - Android Studio 3.5 or above
  - Devices with Android 4.1 or above
- **Developing for iOS and macOS:**
  - Xcode 11.0 or above
  - OS X 10.11 or above
  - A valid developer signature for your project
- For how to set up the environment, see the React Native [official document](https://reactnative.dev/docs/environment-setup).

## Prerequisites
You have [signed up for a Tencent Cloud account(https://intl.cloud.tencent.com) and verified your identity.

## Directions
[](id:step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTRTC` and click **Create**. If you have already created an application, click **Existing** to select it.
3. Add or edit tags for your application if necessary, and click **Create**.


>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and [demo source code](https://github.com/c1avie/TRTCReactNativeDemo) for your platform.
2. Click **Next**.

>! You cannot download the demo for React Native via the console at the moment. **Please download the source code via the above link**.

[](id:step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `/debug/config.js`.
3. Set the `SDKAPPID` and `SECRETKEY` parameters:
<ul><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
    <li>`SECRETKEY`: a placeholder by default. Set it to the actual key.</ul>
    <img src="https://main.qcloudimg.com/raw/fba60aa9a44a94455fe31b809433cfa4.png"/>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step4)
### Step 4. Configure permission requests
You need to configure permission requests in order to run the demo.
<dx-tabs>
::: Android
1. Configure application permissions in `AndroidManifest.xml`. The TRTC SDK requires the following permissions:
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```
>! Do not set `android:hardwareAccelerated="false"`. Disabling hardware acceleration will result in failure to render remote users’ videos.
2. Manually configure audio and video permission requests.
```java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //For audio calls
    PermissionsAndroid.PERMISSIONS.CAMERA, // For video calls
  ]);
}
```
:::
::: iOS
Configure application permissions in `Info.plist`. The TRTC SDK requires the following permissions:
```objectiveC
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
:::
</dx-tabs>

[](id:step5)
### Step 5. Build and run the demo
Launch Metro and run `npx react-native start` under your React Native project directory.
<dx-tabs>
:::  Android
Open a new window and start debugging:
```
npx react-native run-android
```
:::
::: iOS
1. Run `pod install` in the iOS directory to install dependencies.
2. Open the `.xcworkspace` file in the iOS directory to start the iOS project and create an empty Swift file under the iOS project directory.
![](https://qcloudimg.tencent-cloud.cn/raw/1b243c324d9e1e93d113d2431922c4de.jpeg)
3. In the window that pops up, click **Create Bridging Header**.
![](https://qcloudimg.tencent-cloud.cn/raw/8329b913890721ceef19be314462905d.png)
2. Open a new window and start debugging:
```
npx react-native run-ios
```
::: 
</dx-tabs>

​                   