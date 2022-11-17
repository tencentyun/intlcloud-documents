This document describes how to quickly run the TRTC demo for React Native.

## Environment Requirements
- React Native 0.63 or later
- Node (later than v12) & Watchman
- **Developing for Android:**
  - Android Studio 3.5 or later
  - Devices with Android 4.1 or later
- **Developing for iOS and macOS:**
  - Xcode 11.0 or later
  - OS X 10.11 or later
  - A valid developer signature for your project
- For how to set up the environment, see the React Native [official document](https://reactnative.dev/docs/environment-setup).

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com).

## Directions

### Step 1. Create an application

1. Log in to the TRTC console and select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar.
2. Click **Create application**, enter an application name such as `APIExample`. If you already have an application, select **Existing** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### Step 2. Download the sample code

1. Select **No UI**, and go to [GitHub](https://github.com/LiteAVSDK/TRTC_ReactNative/tree/main/TRTC-Simple-Demo) to download the SDK and demo source code.
2. Click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### Step 3. Configure the project

1. If you are running a demo project, select **Testing**. Note the `SDKAppID` and secret key.
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. Open the file downloaded previously, find and open `/TRTC-Simple-Demo/debug/config.js`, and set the following parameters:
   - `SDKAPPID`: A placeholder by default. Set it to the actual `SDKAppID`.
   - `SECRETKEY`: A placeholder by default. Set it to the actual key.
3. Click **Next**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of TRTC-Simple-Demo**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://www.tencentcloud.com/document/product/647/35166).

### Step 4. Configure permission requests

You need to configure permission requests in order to run the demo.

#### Android

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

- Do not use `android:hardwareAccelerated="false"`. Disabling hardware acceleration will result in failure to render remote videos.
- You need to request audio and video permissions manually for Android.

```Java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //For audio calls
    PermissionsAndroid.PERMISSIONS.CAMERA, // For video calls
  ]);
}
```

#### iOS

1. Configure application permissions in `Info.plist`. The TRTC SDK requires the following permissions:

```ObjectiveC
<key>NSCameraUsageDescription</key>
<string>You can make video calls only if you grant the app camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>You can make audio calls only if you grant the app mic permission.</string>
```

### Step 5. Build and run the project

Run `npm install`.

#### Android

1. Start Metro in the demo directory.

```
npx react-native start
```

2. Open a new window in the demo directory and start debugging.

```
npx react-native run-android
```

#### iOS

1. Run `pod install` in the demo iOS directory to install dependencies.
2. Start Metro in the demo directory.

```
npx react-native start
```

3. Open a new window in the demo directory and start debugging (if an error occurs, please use Xcode to debug your project).

```
npx react-native run-ios
```
