## 컴포넌트 개요
TUIRoom은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 화면 공유, 뷰티 필터 및 저지연 영상 통화와 같은 기능을 App에 추가할 수 있습니다. [iOS](https://intl.cloud.tencent.com/document/product/647/37284), [Windows](https://intl.cloud.tencent.com/document/product/647/44071) 및 [Mac](https://intl.cloud.tencent.com/document/product/647/44071) 플랫폼도 지원합니다. 기본 기능은 다음과 같습니다.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2944bac3c5d348b06d2a11c439783b48.png"></td>
</tr>
</tbody></table>

## 컴포넌트 통합
### 1단계: TUIRoom 컴포넌트 다운로드 및 가져오기
[Github](https://github.com/tencentyun/TUIRoom)로 이동하여 코드를 복제하거나 다운로드하고 Android 디렉터리에서 tuiroom, debug, tuibeauty 디렉터리를 프로젝트로 복사한 후 다음 가져오기 작업을 완료합니다.
- 아래와 같이 `setting.gradle`에서 가져오기 완료:

```
include ':tuiroom'
include ':debug'
include ':tuibeauty'
```
- app의 `build.gradle` 파일에 tuiroom, debug 및 tuibeauty에 대한 종속성을 추가합니다.
```
api project(':tuiroom')
api project(':debug')
api project(':tuibeauty')
```
- 루트 디렉터리의 `build.gradle` 파일에 `TRTC SDK` 및 I`IM SDK`에 대한 종속성을 추가합니다.
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### 2단계: 권한 요청 및 난독화 규칙 구성
1. AndroidManifest.xml에서 App에 대한 권한 요청을 구성합니다. SDK에는 다음 권한이 필요합니다(Android 6.0 이상에서는 런타임 시 마이크 액세스를 요청해야 함).
```
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. proguard-rules.pro 파일에서 SDK 클래스를 난독화 금지 목록에 추가합니다.
```
-keep class com.tencent.** { *; }
```

### 3단계: TUI 컴포넌트 생성 및 초기화
```java
// 1. 컴포넌트에 로그인
TUILogin.addLoginListener(new TUILoginListener() {
    @Override
    public void onKickedOffline() {  // 강제 로그아웃 콜백(예시: 계정이 다른 디바이스에서 로그인된 경우)
    }

    @Override
    public void onUserSigExpired() { // userSig 만료 콜백
    }
});

TUILogin.login(context, "귀하의 SDKAppId", "귀하의 userId", "귀하의 userSig", null);


// 2. TUIRoom 인스턴스 초기화
TUIRoom tuiRoom = TUIRoom.sharedInstance(this);
```

#### 매개변수 설명
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 현재 사용자의 ID로, 문자(a-z 및 A-Z), 숫자(0-9), 하이픈(-) 및 언더바(\_)만 포함할 수 있는 문자열입니다. 사용자 계정 시스템과 일관성을 유지하는 것이 좋습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [데모 프로젝트](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.


### 4단계: 그룹 오디오/비디오 인터랙션 구현
1. **방 주인은 그룹 오디오/비디오 대화방을 생성합니다**.
```java
tuiRoom.createRoom("12345", TUIRoomCoreDef.SpeechMode.FREE_SPEECH, true, true);
```
2. **다른 사용자가 오디오/비디오 룸에 입장합니다**.
```java
tuiRoom.enterRoom("12345", true, true);
```

### 5단계: 방 관리(옵션)
1. **방 소유자는 [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37281)을 통해 방을 해산합니다**.
```java
// 1. 방 소유자가 API를 호출하여 방 해산
mTUIRoomCore.destroyRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

방 구성원은 방 해산을 알리는 onDestroyRoom 콜백 메시지 수신
@Override
public void onDestroyRoom() {
    //방 소유자가 방을 해산하고 퇴장
}
```
2. **다른 구성원은 [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37281)을 통해 방을 나갑니다**.
```java
// 1. 방 구성원이 API를 호출하여 방 퇴장
mTUIRoomCore.leaveRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

//방 구성원은 구성원 퇴장을 알리는 onRemoteUserLeave 콜백 메시지 수신
@Override
public void onRemoteUserLeave(String userId) {
        Log.d(TAG, "onRemoteUserLeave userId: " + userId);
}
```

### 6단계: 화면 공유(옵션)
[TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37281)를 통해 화면 공유를 구현합니다.
```java
// 1. AndroidManifest.xml 파일에 SDK 녹화 기능의 activity 및 권한 추가
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>

// 2. 인터페이스에서 플로팅 창 권한 신청
if (Build.VERSION.SDK_INT >= 23) {
    if (!Settings.canDrawOverlays(getApplicationContext())) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, 100);
    } else {
        startScreenCapture();
    }
} else {
    startScreenCapture();
}

// 3. 시스템 콜백 결과
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == 100) {
        if (Build.VERSION.SDK_INT >= 23) {
            if (Settings.canDrawOverlays(this)) {
                // 사용자 권한 부여 성공
                startScreenCapture();
            } else {
            }
        }
    }
}

// 4. 화면 공유 활성화
private void startScreenCapture() {
        TRTCCloudDef.TRTCVideoEncParam encParams = new TRTCCloudDef.TRTCVideoEncParam();
        encParams.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720;
        encParams.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
        encParams.videoFps = 10;
        encParams.enableAdjustRes = false;
        encParams.videoBitrate = 1200;

        TRTCCloudDef.TRTCScreenShareParams params = new TRTCCloudDef.TRTCScreenShareParams();
        mTUIRoom.stopCameraPreview();
        mTUIRoom.startScreenCapture(encParams, params);
}
```

### 7단계: 뷰티 필터 특수 효과(옵션)[](id:XMagic)
TUIRoom 뷰티 필터는 Tencent 특수 효과 SDK를 사용하며, 뷰티 필터 기능을 사용하려면 먼저 XMagic License를 설정해야 합니다.
```java
TUIBeautyView.getBeautyService().setLicense(context, “XMagicLicenseURL”, “XMagicLicenseKey”);
```


## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 문의하십시오.
