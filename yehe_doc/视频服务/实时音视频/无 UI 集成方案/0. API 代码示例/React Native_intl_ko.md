본문에서는 Tencent Cloud TRTC Demo(React Native)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- ReactNative 0.63 이상 버전
- Node & Watchman, node v12 이상 버전
- **Android 개발:**
  - Android Studio 3.5 이상 버전
  - Android 4.1 이상 버전의 디바이스
- **iOS & macOS 개발:**
  - Xcode 11.0 이상 버전
  - osx 시스템 10.11 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- 환경 설정 방법은 React Native [공식 문서](https://reactnative.cn/docs/environment-setup)를 참고하십시오.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com) 계정이 있어야 합니다.

## 작업 단계

### 1단계: 애플리케이션 생성

1. TRTC 콘솔에 로그인하고 [[애플리케이션 관리](https://console.tencentcloud.com/trtc/app)]를 선택합니다.
2. [애플리케이션 생성]을 클릭하고 'APIExample'과 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 있는 경우 [기존 애플리케이션 선택]을 선택하고 [다음]을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### 2단계: 샘플 코드 다운로드

1. UI 없음을 선택하고 [[Github](https://github.com/LiteAVSDK/TRTC_ReactNative/tree/main/TRTC-Simple-Demo)]으로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
2. [다음]을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### 3단계: 프로젝트 구성

1. 데모 프로젝트를 실행 중인 경우 [테스트]를 선택합니다. SDKAppID와 Secret key를 기록해 둡니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 이전에 다운로드한 파일을 열고 `/TRTC-Simple-Demo/debug/config.js`를 찾아 열고 다음 매개변수를 설정합니다.
   - SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
   - SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 Secret key로 설정하십시오.
3. [다음]을 클릭합니다.

>?
>- 이 문서에서 설명하는 UserSig를 생성하는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 쉽게 디컴파일되고 역전될 수 있으며, 키가 공개되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 TRTC-Simple-Demo의 로컬 실행 및 디버깅에만 적합합니다**.
>- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

### 4단계: 권한 요청 구성

데모를 실행하려면 App 권한 요청을 구성해야 합니다.

#### Android

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

- android:hardwareAccelerated="false"를 사용하지 마십시오. 하드웨어 가속을 비활성화하면 원격 비디오를 렌더링하지 못합니다.
- Android의 경우 오디오/비디오 권한을 수동으로 요청해야 합니다.

```Java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //오디오 요구 사항
    PermissionsAndroid.PERMISSIONS.CAMERA, // 비디오 요구 사항
  ]);
}
```

#### iOS

1. 'Info.plist'에서 App 권한을 구성합니다. TRTC SDK에는 다음 권한이 필요합니다.

```ObjectiveC
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```

### 5단계: 컴파일 실행

`npm install` 실행

#### Android

1. Demo 디렉터리에서 Metros 실행

```
npx react-native start
```

2. Demo 디렉터리에서 새 창을 열고 디버깅 실행

```
npx react-native run-android
```

#### iOS

1. Demo ios 디렉터리에서 `pod install`을 실행하여 종속성을 설치합니다.
2. Demo 디렉터리에서 Metros 실행

```
npx react-native start
```

3. Demo 디렉터리에서 새 창을 열고 디버깅을 시작합니다(오류가 발생하면 xcode를 사용하여 프로젝트를 디버깅하십시오).

```
npx react-native run-ios
```
