본문에서는 Tencent Cloud TRTC SDK(React Native)를 프로젝트에 빠르게 통합하는 방법을 소개합니다. 다음 단계에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

## 환경 요건
- ReactNative 0.63 이상 버전.
- Node & Watchman, node v12 이상 버전.
- **Android 개발:**
  - Android Studio 3.5 또는 이후 버전.
  - Android 4.1 또는 이후 버전의 디바이스.
  - Java Development Kit
- **iOS & macOS 개발:**
  - Xcode 11.0 또는 이후 버전.
  - osx 시스템 버전은 10.11 및 이후 버전이 요구됩니다.
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- 환경 설치는 [공식 홈페이지 문서](https://reactnative.cn/docs/environment-setup)를 참고하십시오.

## SDK 통합
ReactNative SDK는 [npm](https://www.npmjs.com/package/trtc-react-native)으로 배포되었으며 `package.json`을 구성하여 설치할 수 있습니다.
1. 프로젝트의 `package.json`에 다음 종속성을 작성합니다.
```
"dependencies": {
  "trtc-react-native": "^2.0.0"
},
```
2. **카메라**와 **마이크**의 권한을 활성화하면, 음성 통화 기능을 활성화할 수 있습니다.
<dx-tabs>
::: Android 
1. `AndroidManifest.xml`에서 App 권한을 설정합니다. TRTC SDK는 다음 권한이 필요합니다.
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
>! `android:hardwareAccelerated="false"`를 설정하지 마십시오. 하드웨어 가속을 비활성화하면 상대방의 비디오 스트리밍을 렌더링할 수 없습니다.
2. Android 오디오 및 비디오 권한은 수동으로 적용해야 합니다.
```java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //오디오 요구 사항
    PermissionsAndroid.PERMISSIONS.CAMERA, // 비디오 요구 사항
  ]);
}
```
:::
::: iOS
1. 'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```objectiveC
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
2. 네이티브 라이브러리 링크는 [네이티브 라이브러리](https://reactnative.cn/docs/linking-libraries-ios)를 참고하십시오.
::: 
</dx-tabs>



