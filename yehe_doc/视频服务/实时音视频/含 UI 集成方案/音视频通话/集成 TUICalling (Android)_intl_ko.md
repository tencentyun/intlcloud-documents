## 컴포넌트 개요

TUICalling은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성 만으로 ‘1:1 음성/영상 통화’ 및 오프라인 통화와 같은 App 지원 시나리오를 만들 수 있습니다. 또한 iOS, Web, Flutter 및 UniApp 플랫폼을 지원합니다. 기본 기능은 다음과 같습니다.

>?TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 내역은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png" </td>
</tr>
</tbody></table>

>?TUICalling 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 내역은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

## 컴포넌트 통합

### 1단계: TUICalling 컴포넌트 다운로드 및 가져오기
[GitHub](https://github.com/tencentyun/TUICalling)으로 이동하여 코드를 복제하거나 다운로드하고 Android 디렉터리의 tuicaling 및 debug 디렉터리를 app과 동일한 수준의 프로젝트에 복사하고 다음 가져오기 작업을 완료합니다.
- 아래와 같이 `setting.gradle`에서 가져오기를 완료합니다.
```java
include ':tuicalling'
include ':debug'
```
- app의 build.gradle 파일에 tuicaling에 대한 종속성 추가:
```java
api project(':tuicalling')
```
- 루트 디렉터리의 `build.gradle` 파일에 `TRTC SDK` 및 I`IM SDK`에 대한 종속성을 추가합니다.
```java
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### 2단계: 권한 요청 및 난독화 규칙 구성

1. AndroidManifest.xml에서 App 권한 요청을 설정합니다. SDK에는 다음 권한이 필요합니다.(Android 6.0 이상에서는 런타임 시 카메라, 마이크 및 저장소 읽기 권한 요청 필요)
```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // 사용 사례: 플로팅 창. 이 권한은 백그라운드의 애플리케이션이 통화 페이지를 표시하는 데 필요;
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // 사용 사례: 블루투스 헤드셋 사용 시 이 권한 필요;
<uses-permission android:name="android.permission.READ_PHONE_STATE" />          // 사용 사례: 이 권한은 전화 수신으로 인해 현재 통화가 중단되었는지 여부를 확인하는 데 필요;
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. proguard-rules.pro 파일에서 SDK 클래스를 난독화 금지 목록에 추가합니다.
```
-keep class com.tencent.** { *; }
```

### 3단계: 컴포넌트 생성 및 초기화

```java
// 1. 이벤트 로그인 리스너 추가
TUILogin.addLoginListener(new TUILoginListener() {
    @Override
    public void onConnecting() {      // 연결 중
        super.onConnecting();
    }
    @Override
    public void onConnectSuccess() {  // 연결 성공 알람
        super.onConnectSuccess();
    }
    @Override
    public void onConnectFailed(int errorCode, String errorMsg) {  // 연결 실패 알람
        super.onConnectFailed(errorCode, errorMsg);
    }
    @Override
    public void onKickedOffline() {  // 강제 로그아웃 콜백(예: 계정이 다른 장치에서 로그인됨)
        super.onKickedOffline();
    }
    @Override
    public void onUserSigExpired() { // userSig 만료 콜백
        super.onUserSigExpired();
    }
});
TUILogin.login(mContext, "Your SDKAppID", "Your userId", "Your userSig", new TUICallback() {
    @Override
    public void onSuccess() {
    }
    @Override
    public void onError(int errorCode, String errorMsg) {
        Log.d(TAG, "errorCode: " + errorCode + " errorMsg:" + errorMsg);
    }
});
// 2. TUICalling 인스턴스 초기화
TUICalling callingImpl = TUICallingImpl.sharedInstance(context);
```
**매개변수 설명**:
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 문자열이며 최대 32바이트의 문자와 숫자를 포함할 수 있는 현재 사용자 ID입니다(특수 기호는 지원되지 않음). 실제 계정 시스템에 따라 사용자 정의할 수 있습니다.
- **userSig**: SDKAppID, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool) 를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [TUICalling 데모 프로젝트](https://github.com/tencentyun/TUICalling/blob/main/Android/app/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://cloud.tencent.com/document/product/647/17275)를 참고하십시오.


### 4단계: 음성/영상 통화 걸기
**[TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43140)을 통한 1:1 음성/영상 통화**
```java
// 1대1 영상 통화를 시작합니다. userId가 1111이라고 가정합니다.
callingImpl.call(["1111"], TUICalling.Type.VIDEO);
```


>? 
>- 수신자가 3단계를 완료한 후(즉, 로그인 성공 후) 다시 전화 요청을 수신하면 TUICalling 컴포넌트는 해당 호출 응답 UI를 자동으로 표시합니다.    
>- 음성 통화를 시작하려면 유형을 `TUICalling.Type.AUDIO`로 변경하기만 하면 됩니다.

### 5단계: 오프라인 푸시 기능 추가(옵션)

상기 4단계가 완료되면 음성/영상 통화를 걸고 받을 수 있습니다. 그러나 비즈니스 시나리오에서 ‘App 프로세스가 종료’되거나 ‘백그라운드에서 실행’된 후에도 음성/영상 통화 요청을 정상적으로 수신하려면 TUICalling 컴포넌트에 오프라인 푸시 기능을 추가해야 합니다. 자세한 내용은 [**Android 오프라인 푸시 연결 가이드**](https://github.com/tencentyun/TUICalling/blob/main/Android/Android%E7%A6%BB%E7%BA%BF%E6%8E%A8%E9%80%81%E6%8E%A5%E5%85%A5%E6%8C%87%E5%BC%95.md)를 참고하십시오.

### 6단계: 상태 수신 기능 추가(옵션)
비즈니스에서 통화 시작 및 종료 등 [통화 상태 수신](https://intl.cloud.tencent.com/document/product/647/43140)을 위해서는 다음 이벤트를 수신해야 합니다.
```
callingImpl.setCallingListener(new TUICalling.TUICallingListener() {
    @Override
    public boolean shouldShowOnCallView() {
        return true;
    }

    @Override
    public void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView) {

    }

    @Override
    public void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime) {

    }

    @Override
    public void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message) {
        Log.d(TAG, "onCallEvent: event = " + event + " ,message = " + message);
    }
});
```

### 7단계: 플로팅 창 기능 추가(옵션)
비즈니스에서 플로팅 창 기능을 활성화해야 하는 경우 TUICalling 컴포넌트 초기화 시 `callingImpl.enableFloatWindow(true)`를 호출할 수 있습니다.

현재 이 컴포넌트는 다음 두 가지 플로팅 창 유형을 지원합니다.
- 시스템 플로팅 창(배경으로 전환하려면 home을 클릭): 애플리케이션에 플로팅 창 권한을 부여해야 합니다.
- 인앱 플로팅 창(최소화하고 이전 UI로 돌아가기): 애플리케이션에 플로팅 창 권한을 부여하고 이전 UI가 반환되도록 설정해야 합니다.
플로팅 창 권한 부여 방법: **설정**, **애플리케이션 관리**를 선택하고 애플리케이션을 찾아 **권한**을 클릭한 후 **플로팅 창 허용**을 클릭합니다(설정 경로는 휴대폰 브랜드 및 플랫폼에 따라 다를 수 있음).

반환될 이전 UI 설정: `AndroidManifest.xml`의 타깃 페이지에 대한 리디렉션 작업 `com.tencent.trtc.tuicalling`을 다음과 같이 구성합니다.
```
<activity
    android:name="{packageName}.MainActivity"
    android:launchMode="singleTop">
    <intent-filter>
        <action android:name="com.tencent.trtc.tuicalling" /> 
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```

## FAQ

### TUICalling 컴포넌트는 프로필 사진 및 닉네임 사용자 지정을 지원합니까?

지원합니다. `setUserNickname/setUserAvatar`를 호출하여 이를 구현할 수 있습니다.

### TUICalling 컴포넌트는 사용자 정의 벨소리를 지원합니까?
지원합니다. [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140)을 호출하여 이를 구현할 수 있습니다.

>? 요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의하십시오.
