This document describes how to quickly integrate the TRTC SDK for React Native into your project.

## Environment Requirements
- React Native 0.63 or above
- Node (above v12) & Watchman
- **Developing for Android:**
  - Android Studio 3.5 or above
  - Devices with Android 4.1 or above
  - Java Development Kit
- **Developing for iOS and macOS:**
  - Xcode 11.0 or above
  - OS X 10.11 or above
  - A valid developer signature for your project
- For how to set up the environment, see the React Native [official document](https://reactnative.dev/docs/environment-setup).

## Integrating SDK
We have released the TRTC SDK for React Native to [npm](https://www.npmjs.com/package/trtc-react-native). You can configure `package.json` to install the SDK.
1. Add the following dependencies to `package.json` of your project:
```
"dependencies": {
  "trtc-react-native": "^2.0.0"
},
```
2. Grant **camera** and **mic** permissions to enable the audio and video call features.
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
1. Add requests for camera and mic permissions in `Info.plist`:
```objectiveC
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
2. Link native libraries. For detailed directions, see [Linking Libraries](https://reactnative.dev/docs/linking-libraries-ios).
::: 
</dx-tabs>



