본문에서는 Tencent Cloud TRTC Demo(React Native)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- ReactNative 0.63 이상 버전.
- Node & Watchman, node v12 이상 버전.
- **Android 개발:**
  - Android Studio 3.5 이상 버전.
  - Android 4.1 이상 버전의 디바이스.
- **iOS & macOS 개발:**
  - Xcode 11.0 이상 버전.
  - osx 시스템 10.11 이상 버전.
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- 환경 설치는 [공식 홈페이지 문서](https://reactnative.cn/docs/environment-setup)를 참고하십시오.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com) 계정이 있으며, 실명인증을 완료해야 합니다.

## 작업 단계
[](id:step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, **개발 지원>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. **애플리케이션 생성**을 클릭하고 `TestTRTC`와 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 생성된 경우 **기존 애플리케이션 선택**을 클릭합니다.
3. 실제 비즈니스 요구에 따라 태그를 추가하거나 편집하고 **생성**을 클릭합니다.


>?
>- 애플리케이션 이름은 숫자, 중국어, 영어, 언더바만 포함할 수 있으며 15자를 초과할 수 없습니다.
>- 태그는 Tencent Cloud에서 다양한 리소스를 식별하고 구성하는 데 사용됩니다. 예를 들어, 기업이 여러 사업부를 가지고 있고, 각 부서에는 하나 이상의 TRTC 애플리케이션이 있을 수 있는데, 이 경우 기업은 TRTC 애플리케이션에 태그를 추가하여 부서 정보를 표시할 수 있습니다. 태그는 필수 사항이 아니며, 실제 비즈니스 니즈에 따라 추가하거나 편집할 수 있습니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 니즈에 따라 SDK 및 관련 [Demo 소스 코드](https://github.com/c1avie/TRTCReactNativeDemo)를 다운로드합니다.
2. 다운로드 완료 후 **다운로드 완료, 다음 단계**를 클릭합니다.

>! 콘솔에서 일시적으로 ReactNative Demo를 다운로드할 수 없습니다. **상기 링크에서 직접 Demo 소스 코드를 다운로드하십시오**.

[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `/debug/config.js` 파일을 찾아 엽니다.
3. `SDKAPPID` 및 `SECRETKEY` 매개변수를 설정합니다.
<ul><li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
    <li/>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
    <img src="https://main.qcloudimg.com/raw/fba60aa9a44a94455fe31b809433cfa4.png"/>
4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계** 를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>?
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:step4)
### 4단계: 권한 설정
실행하려면 App 권한을 구성해야 합니다.
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
'Info.plist'에서 App 권한을 구성하려면 TRTC SDK에 다음 권한이 필요합니다.
```objectiveC
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
:::
</dx-tabs>

[](id:step5)
### 5단계: 컴파일 실행
Metro를 시작하고 React Native 프로젝트 디렉터리에서 `npx react-native start`를 실행합니다.
<dx-tabs>
:::  Android
새 창을 열고 개발 및 디버깅을 실행합니다.
```
npx react-native run-android
```
:::
::: iOS
1. iOS 디렉터리에서 `pod install`을 실행하여 종속 항목을 설치합니다.
2. iOS 디렉터리에서 `.xcworkspace`를 열고 iOS 프로젝트를 실행하고 iOS 프로젝트 디렉터리에 빈 swift 파일을 생성합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1b243c324d9e1e93d113d2431922c4de.jpeg)
3. 그 후 새 브리징 파일을 만들 것인지 묻는 팝업 창이 나타나면 **Create Bridging Header**를 클릭하여 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8329b913890721ceef19be314462905d.png)
2. 새 창을 열고 개발 및 디버깅을 시작합니다.
```
npx react-native run-ios
```
::: 
</dx-tabs>

​                   