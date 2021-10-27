## 효과
App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 화면 공유, 뷰티 필터, 저지연 회의 등 TRTC 다중 사용자 화상 회의 시나리오 관련 기능을 체험해 볼 수 있습니다.


빠른 다중 사용자 화상 회의 기능이 필요한 경우, Tencent Cloud에서 제공하는 App을 기반으로 설정을 적절히 수정하거나, TRTCMeeting 컴포넌트를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:DemoUI)
## App UI 인터페이스 재사용
[](id:ui.step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원]>[[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)]을 선택합니다.
2. 애플리케이션 이름(예: `TestMeetingRoom`)을 입력한 후 [생성]을 클릭합니다.
3. [다운로드 완료, 다음 단계]를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!  본 기능은 기본 PaaS 서비스인 Tencent Cloud [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://cloud.tencent.com/document/product/269)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

[](id:ui.step2)
### 2단계: App 소스 코드 다운로드
[TUIMeeting](https://github.com/tencentyun/TUIMeeting)을 클릭하여 Clone하거나 소스 코드를 다운로드합니다.

[](id:ui.step3)

### 3단계: App 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 플레이스 홀더(PLACEHOLDER)로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣은 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.


>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)
### 4단계: App 실행
Android Studio(3.5 이후 버전)를 사용하여 소스 코드 프로젝트인 `TUIMeeting`을 열고 [실행]을 클릭하면 즉시 해당 App이 디버깅됩니다.

[](id:ui.step5)
### 5단계: App 소스 코드 수정
소스 폴더 `Source`에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더에는 인터페이스 코드가 포함되어 있습니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| remote | 원격 사용자의 리스트 인터페이스 |
| widget | 범용 UI 컴포넌트 |
| CreateMeetingActivity.java | 회의 생성 인터페이스 |
| MeetingMainActivity.java | 화상 회의 메인 인터페이스 |
| MeetingVideoView.java | TRTC의 TXCloudVideoView를 캡슐화하여 사용자 및 원격 사용자의 비디오 데이터를 표시하는 데 사용 |
| MemberEntity.java | UI 레이어의 사용자 데이터 |
| MemberListAdapter.java | 화상 회의 메인 인터페이스의 Adapter |



## 애플리케이션 체험

> ! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A
1. 다음과 같이 사용자 이름을 입력하고 로그인합니다. **사용자 이름의 고유성을 확보하십시오. 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 아래 이미지와 같이 회의 ​​번호를 입력하고 [회의 입장]을 클릭합니다.
3. 방 주제를 입력하고 [채팅 시작]을 클릭합니다.

### 사용자 B
1. 다음과 같이 사용자 이름을 입력하고 로그인합니다. **사용자 이름의 고유성을 확보하십시오. 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 사용자 A가 생성한 회의 번호를 입력하고 [회의 입장]을 클릭합니다. <br>

[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUIMeeting/tree/master/Android/Source/src/main/java/com/tencent/liteav/meeting)의 `Source` 폴더에는 ui 폴더와 model 폴더가 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TRTCMeeting이 포함되어 있습니다. `TRTCMeeting.java` 파일에서 해당 컴포넌트에서 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### 1단계: SDK 통합
다중 사용자 화상 회의 컴포넌트 TRTCMeeting은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 단계에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: Maven 웨어하우스를 통한 종속**
1. dependencies에 TRTCSDK 및 IMSDK 종속을 추가합니다.
<dx-codeblock>
::: java java
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
:::
</dx-codeblock>
>?두 SDK의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 Github 메인 페이지에서 가져올 수 있습니다.
2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. [Sync Now]를 클릭하면 SDK가 자동으로 다운로드되고 프로그램에 통합됩니다.

**방법2: 로컬 AAR을 통한 종속**
Maven 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참고하여 프로젝트에 통합할 수 있습니다.
<table>
<tr>
<th>SDK</th>
<th>다운로드 페이지</th>
<th>가이드 통합</th>
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

[](id:model.step2)
### 2단계: 권한 및 난독화 규칙 설정
AndroidManifest.xml에서 App 권한을 설정합니다. SDK에는 다음 권한(6.0 이상 Android 시스템의 경우 카메라 및 스토리지 읽기 동적 권한 신청 필요)이 필요합니다.
<dx-codeblock>
::: java java
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
:::
</dx-codeblock>

proguard-rules.pro 파일에서 SDK 관련 유형을 비난독화 리스트에 추가합니다.
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### 3단계: TRTCMeeting 컴포넌트 가져오기
다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
<dx-codeblock>
::: java java
src/main/java/com/tencent/liteav/meeting/model
:::
</dx-codeblock>

[](id:model.step4)
### 4단계: 컴포넌트 생성 및 로그인
1. sharedInstance 인터페이스를 호출하여 TRTCMeeting 컴포넌트의 인스턴스 객체를 생성합니다.
2. setDelegate 함수를 호출해 컴포넌트의 이벤트 알림을 등록합니다.
3. login 함수를 호출해 컴포넌트에 로그인하고, 다음 표를 참고하여 핵심 매개변수를 입력합니다.
<table>
<tr><th>매개변수 이름</th><th>역할</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
</tr><tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance(this);
trtcMeeting.login(SDKAPPID, userId, userSig, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //로그인 성공
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### 5단계: 다중 사용자 회의 생성
1. 호스트는 [4단계](#model.step4) 로그인 실행 후 setSelfProfile을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트는 setDelegate로 이벤트를 호출합니다. createMeeting으로 새로운 회의 방을 생성할 수 있습니다.
3. 호스트는 startCameraPreview로 비디오 화면 수집을, startMicrophone으로 오디오 수집을 시작할 수 있습니다.
4. 호스트가 뷰티 필터 사용을 원할 경우 인터페이스에 뷰티 필터 조절 버튼 호출을 설정하고, getBeautyManager를 통해 뷰티 필터를 설정할 수 있습니다.
>?엔터프라이즈 버전 이외의 SDK는 얼굴 변경과 스티커 효과 기능을 지원하지 않습니다.

![](https://main.qcloudimg.com/raw/7d55d4983e6fe8da04e63babe5ab3822.png)


<dx-codeblock>
::: java java
// 1. 호스트 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. 호스트 방 생성
trtcMeeting.createMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. 카메라 및 오디오 수집 활성화
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            // 4. 뷰티 필터 설정
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step6)
### 6단계: 다중 사용자 회의에 참석자 입장
1. 참석자는 [4단계](#model.step4) 로그인 실행 후 setSelfProfile을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 참석자는 enterMeeting을 호출하고 회의 방 번호를 전송하여 회의 방에 입장할 수 있습니다.
3. 참석자는 startCameraPreview로 비디오 화면 수집을, startMicrophone으로 오디오 수집을 시작할 수 있습니다.
4. 다른 참석자가 카메라를 켜면 onUserVideoAvailable 이벤트가 수신됩니다. 이때 startRemoteView를 호출하고 userId를 전송하면 재생이 시작됩니다.

![](https://main.qcloudimg.com/raw/ce4bc9c134a94709c3f8e1768c65be88.png)

<dx-codeblock>
::: java java
// 1. 참석자 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. enterMeeting을 호출한 참석자가 회의 방 번호로 입장
trtcMeeting.enterMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. 방 입장 후 카메라와 마이크를 켜면 뷰티 필터 기능 활성화 가능
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});

// 3. 참석자가 다른 참석자의 카메라 활성화 알림을 수신하면 재생됨
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onUserVideoAvailable(String userId, boolean available) {
        if (available) {
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startRemoteView(userId, txCloudVideoView);
        } else {
            trtcMeeting.stopRemoteView(userId, null);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step7)
### 7단계: 화면 공유

1. 화면 공유 기능은 시스템에 플로팅 창 권한을 신청해야 하며, UI에서 구체적인 로직을 구현해야 합니다.
2. startScreenCapture를 호출하여 인코딩 매개변수와 녹화 플로팅 창을 전송하면 화면 공유 기능을 구현할 수 있습니다. 자세한 정보는 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)를 참고하십시오.
3. 회의 중 다른 참석자들은 onUserVideoAvailable 이벤트 알림을 수신합니다.

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
        mTRTCMeeting.stopCameraPreview();
        mTRTCMeeting.startScreenCapture(encParams, params);
}
:::
</dx-codeblock>

[](id:model.step8)
### 8단계: 텍스트 채팅 및 금지어 메시지 구현
- sendRoomTextMsg를 통해 일반 텍스트 메시지를 발송할 수 있으며 해당 방에 있는 모든 호스트와 시청자가 onRecvRoomTextMsg 콜백을 수신하게 됩니다.
 IM의 백엔드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
 <dx-codeblock>
 ::: java java
 // 발신 측: 텍스트 메시지 발송
 trtcMeeting.sendRoomTextMsg("Hello Word!", null);
 // 수신측: 텍스트 메시지 수신
 trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomTextMsg(
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        Log.d(TAG,"발신자: " + userInfo.userName + "메시지: " + message);
    }
 });
 :::
 </dx-codeblock>
- sendRoomCustomMsg를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 호스트와 시청자 모두가 onRecvRoomCustomMsg 콜백을 수신하게 됩니다.
사용자 정의 메시지는 주로 금지어 사용 제한 등과 같은 사용자 정의 신호 전송에 사용됩니다.
<dx-codeblock>
::: java java
// 발신 측: 사용자 정의 Cmd로 금지어 알림 구분
// eg:"CMD_MUTE_AUDIO" 금지어 알림
trtcMeeting.sendRoomCustomMsg("CMD_MUTE_AUDIO", "1", null);
// 수신측: 사용자 정의 메시지 수신
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, 
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        if ("CMD_MUTE_AUDIO".equals(cmd)) {
            // 금지어 알림 수신
            Log.d(TAG,"발신자: " + userInfo.userName + "금지어 알림: " + message);
            trtcMeeting.muteLocalAudio("1".equals(message));
        }
    }
});
:::
</dx-codeblock>
