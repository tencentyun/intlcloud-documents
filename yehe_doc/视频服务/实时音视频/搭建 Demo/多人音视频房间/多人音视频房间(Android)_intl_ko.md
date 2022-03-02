## 효과
App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 화면 공유, 뷰티 필터, 저지연 영상 통화 등 TRTC 그룹 멀티미디어 룸의 음성/영상 통화 기능 효과를 경험해 볼 수 있습니다.

## 솔루션 장점
- 초저지연 음성 및 영상 통화, 화면 공유, 뷰티필터, 등과 같은 기능을 통합하여 그룹 멀티미디어 방의 공통 기능을 다룹니다.
- 수요의 2차 개발에 따라 사용자 정의 UI 인터페이스 및 레이아웃을 빠르게 실현할 수 있으며 비즈니스가 빠르게 런칭 되도록 도울 수 있습니다.
- TRTC 및 IM 기본 SDK를 캡슐화하여 기본 로직 제어를 구현하며, 편리한 호출을 위한 인터페이스를 제공합니다.

## 연결 가이드
그룹 멀티미디어 룸 기능에 빠르게 액세스하려면 당사에서 제공하는 App을 기반으로 직접 수정 및 조정하거나 App의 Module을 사용하여 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:step1_1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, **개발 지원** > [**Demo 빠른 실행**](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예시: `TestTUIRoom`)을 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/10479)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

[](id:step1_2)
### 2단계: App 소스 코드 다운로드
[TUIRoom](https://github.com/tencentyun/TUIRoom)을 클릭하여 이동하거나, 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:step1_3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>? 
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:step1_4)
### 4단계: App 실행
Android Studio(3.5 이후 버전)를 사용하여 소스 코드 프로젝트인 `TUIRoom`을 열고 **실행**을 클릭하면 즉시 해당 App이 디버깅됩니다.

[](id:step1_5)
### 5단계: 프로젝트 소스 코드 수정
소스 폴더 `Source`에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더에는 인터페이스 코드가 포함되어 있습니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| remote | 원격 사용자의 리스트 인터페이스 |
| widget | 범용 UI 컴포넌트 |
| CreateRoomActivity.java | 멀티미디어 룸의 인터페이스 생성 |
| RoomMainActivity.java | 멀티미디어 룸의 메인 인터페이스 |
| RoomVideoView.java | TRTC의 TXCloudVideoView를 캡슐화하여 사용자 및 원격 사용자의 비디오 데이터를 표시하는 데 사용 |
| MemberEntity.java | UI 레이어의 사용자 데이터 |
| MemberListAdapter.java | 멀티미디어 룸 메인 인터페이스의 Adapter |

## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.
### 게이트 인터페이스
이미지와 같이 ‘방 생성’ 또는 ‘방 추가’를 선택하십시오.


### 방 페이지 생성
사용자 A 생성, 방 번호는 기본적으로 생성됩니다. **방 생성**을 클릭하여 메인 페이지로 들어갑니다.


### 방 추가 페이지
사용자 B는 사용자 A의 방 번호를 입력하고 **방 추가**를 클릭하여 메인 페이지로 들어갑니다.


### 메인 페이지(사용자 A)
<img src="https://qcloudimg.tencent-cloud.cn/raw/eebab2b82db719000f0dc376070a25e7.png" width=300px>

### 마이크 목록
마이크 목록은 현재 방에 있는 참석자를 표시할 수 있으며, 상대방이 카메라와 마이크를 켜면 상대방의 사진을 보고 상대방의 음성을 들을 수 있습니다.

### 상단 컨트롤 바
헤드셋 전환, 전후면 카메라 전환, 방 정보, 퇴실 기능을 구현합니다.

### 하단 툴바
마이크/카메라, 뷰티 필터, 참석자 목록, 설정 등 제어 기능이 있습니다.

### 뷰티 필터
라이브 방송 중 화면에 뷰티 필터와 특수 효과를 표시할 수 있습니다.


### 설정 창
멀티미디어 관련 매개변수를 설정할 수 있으며 **화면 공유**를 활성화할 수 있습니다.


### 방 퇴장
- **호스트**: 방 삭제, 즉, 모든 사람이 방에서 나옵니다.
- **비 호스트**: 혼자 방에서 퇴장합니다.

## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUIRoom)의 `Source` 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TUIRoomCore이 포함되어 있습니다. `TUIRoomCore.java` 파일에서 해당 컴포넌트가 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![#600px](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:step2_1)
### 1단계: SDK 통합
그룹 멀티미디어 룸 컴포넌트 TUIRoomCore은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

- **방법1: Maven 라이브러리를 통한 종속**
	1. dependencies에 TRTCSDK와 IMSDK의 종속 패키지를 추가합니다.
```java
dependencies {
	 compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
	 compile 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?두 SDK의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 Github 메인 페이지에서 가져올 수 있습니다.

	2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
```java
defaultConfig {
	ndk {
			abiFilters "armeabi-v7a"
	}
}
```
	3. **Sync Now**를 클릭하면 SDK가 자동으로 다운로드되고 프로그램에 통합됩니다.
- **방법2: 로컬 AAR을 통한 종속**
Maven 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참고하여 프로젝트에 통합할 수 있습니다.
<table>
<tr>
<th>SDK</th>
<th>다운로드 페이지</th>
<th>통합 가이드</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">통합 가이드 문서</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">통합 가이드 문서</a></td>
</tr>
</table>

[](id:step2_2)
### 2단계: 권한 및 난독화 규칙 설정
1. `AndroidManifest.xml`에서 App 권한을 설정합니다. SDK에는 다음 권한(6.0 이후 버전 Android 시스템의 경우 카메라 및 스토리지 읽기 동적 권한 신청 필요)이 필요합니다.
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
2. proguard-rules.pro 파일에서 SDK 관련 유형을 비난독화 리스트에 추가합니다.
```java
-keep class com.tencent.** { *; }
```

[](id:step2_3)
### 3단계: TUIRoomCore 컴포넌트 가져오기
다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
```java
src/main/java/com/tencent/liteav/tuiroom/model
```

[](id:step2_4)
### 4단계: 컴포넌트 생성 및 로그인
TUICore에서 TUILogin을 호출하여 로그인합니다. 다음 예를 참고하십시오.
```java
TUILogin.init(this, "sdkAppid", null, new V2TIMSDKListener() {

		@Override
		public void onKickedOffline() {

		}

		@Override
		public void onUserSigExpired() {

		}
	});
TUILogin.login("userId", "userSig", new V2TIMCallback() {
	@Override
	public void onError(int code, String msg) {

	}

	@Override
	public void onSuccess() {

	}
});
```

[](id:step2_5)
### 5단계: 대화명 설정
로그인 성공 후 setSelfProfile을 호출하여 사용자 정보를 설정합니다.

[](id:step2_6)

### 6단계: 방 생성
1. 참석자는 createRoom 인터페이스를 호출하여 새로운 방을 생성하고, 성공적으로 방이 생성되면 채팅방과 TRTC 방을 포함한 방에 호스트로 입장합니다.
```java
TUIRoomCore tuiRoomCore = TUIRoomCore.getInstance(context);
tuiCore.setListener(listener);
tuiCore.createRoom("roomId", TUIRoomCoreDef.SpeechMode.FREE_SPEECH,
        new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // 방 생성 성공
            } else {
		}
	}
});

```
2. startCameraPreview API를 호출하여 로컬 비디오 캡처 및 표시를 시작합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8c3391905188089fecd17e23477d34ea.png)

[](id:step2_7)
### 7단계: 방 삭제
- 호스트가 destoryRoom 인터페이스를 호출하여 방, IM 그룹 채팅을 삭제하고 TRTC 방에서 퇴장합니다.
- 참석자는 그룹 삭제 및 TRTC 방 퇴장을 알리는 onDestroyRoom 콜백 메시지를 받게 됩니다.

[](id:step2_8)
### 8단계: 방 입장
1. 방에 참여하는 과정은 기본적으로 방 생성 과정과 동일하며, 참석자는 enterRoom 인터페이스를 호출해야 방에 입장할 수 있습니다.
2. 다른 참석자는 참석자 입장을 알리는 onRemoteUserEnter 콜백을 수신합니다.
```java
TUIRoomCore tuiRoomCore = TUIRoomCore.getInstance(context);
tuiCore.setListener(listener);
tuiCore.enterRoom("roomId", new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // 방 입장 성공
            } else {
		}
	}
});
```
![](https://qcloudimg.tencent-cloud.cn/raw/ffbda4de381ea198bf808de7d823ab59.png)

[](id:step2_9)
### 9단계: 방 퇴장
1. 참석자는 leaveRoom 인터페이스를 호출하여 IM 방과 TRTC 방에서 퇴장합니다.
2. 다른 참석자는 참석자 퇴장을 알리는 onRemoteUserLeave 콜백을 수신합니다.

[](id:step2_10)
### 10단계: 화면 공유

1. 화면 공유 기능은 시스템에 플로팅 창 권한을 신청해야 하며, UI에서 구체적인 로직을 구현해야 합니다.
2. TUIRoomCore의 'startScreenCapture'를 호출하여 공유하고, 인코딩 매개변수와 녹화 플로팅 창을 전송하면 화면 공유 기능을 구현할 수 있습니다. 자세한 정보는 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)를 참고하십시오.
3. 방의 다른 참석자는 onRemoteUserScreenVideoAvailable의 이벤트 알림을 받습니다.

>! 화면 공유와 카메라 수집은 상호 충돌되는 작업입니다. 화면 공유 기능을 활성화하고 싶은 경우, 먼저 stopCameraPreview를 호출하여 카메라 수집을 비활성화해야 합니다.

<dx-codeblock>
::: java java
// 1. AndroidManifest.xml 파일에 SDK 녹화 기능의 activity 및 권한 추가
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>
:::
</dx-codeblock>
<dx-codeblock>
::: java java
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
:::
</dx-codeblock>
