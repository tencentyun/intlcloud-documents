## 컴포넌트 개요

TUILiveRoom은 오픈 소스 비디오 라이브 스트리밍 시나리오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 App이 ‘인터랙티브 비디오 라이브 스트리밍’ 시나리오를 추가할 수 있습니다. Android, iOS 및 미니프로그램 플랫폼용 소스 코드를 제공합니다. 기본 기능은 다음과 같습니다.

>?TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 내역은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)
## 컴포넌트 통합
[](id:model.step1)
### 1단계: TUILiveRoom 컴포넌트 다운로드 및 가져오기
클릭하여 [Github](https://github.com/tencentyun/TUILiveRoom)으로 이동하고 클론/다운로드 코드를 선택한 다음 `Android/debug`, `Android/tuiaudioeffect`, `Android/tuibarrage`, `Android/tuibeauty`, `Android/tuigift` 및 `Android/tuiliveroom` 디렉터리를 프로젝트에 복사하고 다음 가져오기 작업을 완료합니다.

- 아래와 같이 `setting.gradle`에서 가져오기를 완료합니다.
```
include ':debug'
include ':tuibeauty'
include ':tuibarrage'
include ':tuiaudioeffect'
include ':tuigift'
include ':tuiliveroom'
```
- `app`의 `build.gradle` 파일에 `tuiliveroom`에 대한 종속성을 추가합니다.
```
api project(":tuiliveroom")
```
- 루트 디렉터리의 `build.gradle` 파일에 `TRTC SDK` 및 I`IM SDK`에 대한 종속성을 추가합니다.
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

[](id:model.step2)
### 2단계: 권한 요청 및 난독화 규칙 구성
1. AndroidManifest.xml에서 App에 대한 권한 요청을 구성합니다. SDK에는 다음 권한이 필요합니다(Android 6.0 이상에서는 런타임 시 카메라 및 저장소 읽기 권한 요청 필요).
```java
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
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. proguard-rules.pro 파일에서 SDK 클래스를 난독화 금지 목록에 추가합니다.
```java
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### 3단계: 컴포넌트 초기화 및 로그인
```java
// 1.이벤트 로그인 리스너 추가
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

// 2.TUILiveRoom 컴포넌트 초기화
TUILiveRoom mLiveRoom = TUILiveRoom.sharedInstance(mContext);
```

**매개변수 설명:**
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 현재 사용자의 ID로, 문자(a-z 및 A-Z), 숫자(0-9), 하이픈(-) 및 언더바(\_)만 포함할 수 있는 문자열입니다. 사용자 계정 시스템과 일관성을 유지하는 것이 좋습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.


[](id:model.step4)
### 4단계: 인터랙티브 비디오 라이브 룸 구현
1. **앵커 방송 시작**
```java
mLiveRoom.createRoom(int roomId, String roomName, String coverUrl);
```
2. **시청자 시청**
```java
mLiveRoom.enterRoom(roomId);
```
3. **[TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37333)를 통해 시청자와 앵커가 함께 공동 앵커링합니다.**
```java
// 1.시청자가 공동 앵커링 요청 발송
// LINK_MIC_TIMEOUT은 시간 초과 기간
TRTCLiveRoom mTRTCLiveRoom=TRTCLiveRoom.sharedInstance(mContext);
mTRTCLiveRoom.requestJoinAnchor(mSelfUserId + "공동 앵커 요청", LINK_MIC_TIMEOUT
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 앵커가 요청 수락
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 시청자가 카메라를 켜고 스트림을 푸시 시작
            mTRTCLiveRoom.startCameraPreview(true, view, null);
            mTRTCLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2.앵커가 공동 앵커 요청 수신
mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 공동 앵커 요청에 동의
        mTRTCLiveRoom.responseJoinAnchor(userInfo.userId, true, "공동 앵커에 동의");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 앵커는 공동 앵커 시청자가 마이크를 켰다는 알림 수신
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 앵커가 시청자 화면 재생
        mTRTCLiveRoom.startPlay(userId, view, null);
    }
});
```
4. **앵커는 [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37333#requestroompk)를 통해 PK합니다.**
```java
// 12345 방 생성
mLiveRoom.createRoom(12345, "roomA", "Your coverUrl");
// 54321 방 생성
mLiveRoom.createRoom(54321, "roomB", "Your coverUrl");

// 앵커 A:
TRTCLiveRoom mTRTCLiveRoom=TRTCLiveRoom.sharedInstance(mContext);

// 1.앵커 B에 PK 요청 보내기
mTRTCLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5.앵커 B가 요청을 수락했는지 여부에 대한 콜백 수신
        if (code == 0) {
            // 사용자 수락
        } else {
            // 사용자 거부
        }
    }
});

mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6.앵커 B의 진입에 대한 알림 수신
        mTRTCLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 앵커 B:
// 2.앵커 A의 요청 수신
mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3.앵커 A의 요청 수락
        mTRTCLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4.앵커 A 진입 알림 수신 및 앵커 A 영상 재생
        mTRTCLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 문의하십시오.
