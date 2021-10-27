App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 화면 공유, 뷰티 필터, 저지연 회의 등 TRTC 다중 사용자 화상 회의 시나리오 관련 기능을 체험해 볼 수 있습니다.

[](id:DemoUI)
## App UI 인터페이스 재사용
[](id:ui.step1)
### 1단계: 신규 애플리케이션 생성

1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원]>[[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)]을 선택합니다.
2. 애플리케이션 이름(예: `TestMeetingRoom`)을 입력한 후 [생성]을 클릭합니다.
3. [다운로드 완료, 다음 단계]를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>! 본 기능은 기본 PaaS 서비스인 Tencent Cloud [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

[](id:ui.step2)
### 2단계: App 소스 코드 다운로드

[TRTCFlutterScenesDemo](https://github.com/tencentyun/TRTCFlutterScenesDemo)로 이동하여 Clone하거나 소스 코드를 다운로드합니다.

[](id:ui.step3)
### 3단계: App 파일 설정

1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `/lib/debug/GenerateTestUserSig.dart` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.dart` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0">
    <li>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
    <li>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</li>
</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣은 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)
### 4단계: 컴파일 실행

>! Android는 실제 기기에서 실행해야 하며, 시뮬레이터 디버깅을 지원하지 않습니다.

1. 'flutter pub get'을 실행합니다.
2. 컴파일 실행 디버깅:
<dx-tabs>
::: iOS\s
1. XCode(11.0 버전 이상)를 사용해 소스 코드 디렉터리에 있는 '/ios 프로그램'을 엽니다.
2. Demo 프로그램을 컴파일 및 실행합니다.
:::
:::  Android\s
1. 'flutter run'을 실행합니다.
2. Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램을 열고 [실행]을 클릭합니다.
:::

</dx-tabs>

[](id:ui.step5)
### 5단계: Demo 소스 코드 수정

소스 코드 TRTCMeetingDemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 코드입니다. 다음 표에는 2차 조정을 위한 각 파일 또는 폴더 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|-------|--------|
| TRTCMeetingIndex.dart | 회의 인터페이스 생성 또는 입장 |
| TRTCMeetingRoom.dart | 화상 회의 메인 인터페이스 |
| TRTCMeetingMemberList.dart | 참석자 목록 인터페이스 |
| TRTCMeetingSetting.dart | 화상 회의 관련 매개변수 설정 인터페이스 |

[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TRTCFlutterScenesDemo)의 TRTCMeetingDemo 폴더에는 ui 폴더와 model 폴더가 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TRTCMeeting이 포함되어 있습니다. `TRTCMeeting.dart` 파일에서 해당 컴포넌트가 제공하는 인터페이스 함수를 확인할 수 있으며, 해당 인터페이스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### 1단계: SDK 통합

ILVB 컴포넌트 TRTCMeeting은 [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)와 [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)에 종속되며, `pubspec.yaml` 설정을 통해 자동으로 다운로드 및 업데이트할 수 있습니다.

프로젝트의 `pubspec.yaml`에 다음과 같이 종속성을 작성합니다.
```
dependencies:
  tencent_trtc_cloud: 최신 버전 넘버
  tencent_im_sdk_plugin: 최신 버전 넘버
```

[](id:model.step2)
### 2단계: 권한 및 난독화 규칙 설정

<dx-tabs>
::: iOS\s
1. 'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
:::
:::  Android\s
1. '/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
2. 'xmlns:tools="http://schemas.android.com/tools"'를 manifest에 추가합니다.
3. 'tools:replace="android:label"'을 application에 추가합니다.
>? 이 단계를 수행하지 않으면 [Android Manifest merge failed 컴파일 실패](https://intl.cloud.tencent.com/document/product/647/39242) 문제가 발생합니다.

![이미지](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>

[](id:model.step3)
### 3단계: TRTCMeeting 컴포넌트 가져오기

다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
```
lib/TRTCMeetingDemo/model/
```

[](id:model.step4)

### 4단계: 컴포넌트 생성 및 로그인

1. `sharedInstance` 인터페이스를 호출하여 TRTCMeeting 컴포넌트의 인스턴스 객체를 생성합니다.
2. `registerListener` 함수를 호출하여 컴포넌트의 이벤트 알림을 등록합니다.
3. `login` 함수를 호출해 컴포넌트에 로그인하고, 다음 표를 참고해 핵심 매개변수를 입력합니다.
<table>
    <tr>
        <th>매개변수 이름</th>
        <th>역할</th>
    </tr>
    <tr>
        <td>sdkAppId</td>
        <td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
    </tr>
    <tr>
        <td>userId</td>
        <td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0~9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
    </tr>
    <tr>
        <td>userSig</td>
        <td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
    </tr>
</table>
<dx-codeblock>
::: dart dart
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance();
trtcMeeting.registerListener(onListener);
ActionCallback res = await trtcMeeting.login(
    GenerateTestUserSig.sdkAppId,
    userId,
    GenerateTestUserSig.genTestSig(userId),
);
if (res.code == 0) {
    // 로그인 성공
}
:::
</dx-codeblock>

[](id:model.step5)
### 5단계: 다중 사용자 회의 생성

1. 호스트는 [4단계](#model.step4) 로그인 실행 후 setSelfProfile을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트는 createMeeting을 호출하여 새 회의 방을 생성합니다.
3. 호스트는 startCameraPreview로 비디오 화면 수집을, startMicrophone으로 오디오 수집을 시작할 수 있습니다.
4. 호스트가 뷰티 필터 사용을 원할 경우 인터페이스에 뷰티 필터 조절 버튼 호출을 설정하고, getBeautyManager를 통해 뷰티 필터를 설정할 수 있습니다.
>? 엔터프라이즈 버전 이외의 SDK는 얼굴 변경 및 스티커 효과 기능을 지원하지 않습니다.

![](https://main.qcloudimg.com/raw/7d55d4983e6fe8da04e63babe5ab3822.png)

<dx-codeblock>
::: dart dart
// 1. 호스트 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile('my_name', 'my_avatar');

// 2. 호스트 회의 생성
ActionCallback res = await trtcMeeting.createMeeting(roomId);
if (res.code == 0) {
    // 회의 생성 성공
    // 3. 카메라 및 오디오 수집 활성화
    trtcMeeting.startCameraPreview(true, TRTCCloudVideoViewId);
    trtcMeeting.startMicrophone();
    // 4. 뷰티 필터 설정
    trtcMeeting.getBeautyManager().setBeautyStyle(TRTCCloudDef.TRTC_BEAUTY_STYLE_PITU);
    trtcMeeting.getBeautyManager().setBeautyLevel(6);
}
:::
</dx-codeblock>

[](id:model.step6)
### 6단계: 다중 사용자 회의에 참석자 입장

1. 참석자는 [4단계](#model.step4) 로그인 실행 후 setSelfProfile을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 참석자는 enterMeeting을 호출하고 회의 방 번호를 전송하여 회의 방에 입장할 수 있습니다.
3. 참석자는 startCameraPreview로 비디오 화면 수집을, startMicrophone을 호출하여 오디오 수집을 시작할 수 있습니다.
4. 다른 참석자가 카메라를 켜면 onUserVideoAvailable 이벤트가 수신됩니다. 이때 startRemoteView를 호출하고 userId를 전송하면 재생이 시작됩니다.

![](https://main.qcloudimg.com/raw/ce4bc9c134a94709c3f8e1768c65be88.png)

<dx-codeblock>
::: dart dart
// 1. 참석자 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile('my_name', 'my_avatar');

// 2. 참석자가 enterMeeting을 호출하여 회의 방 입장
ActionCallback res = await trtcMeeting.enterMeeting(roomId);
if (res.code == 0) {
    // 회의 입장 성공
    // 3. 카메라 및 오디오 수집 활성화
    trtcMeeting.startCameraPreview(true, TRTCCloudVideoViewId);
    trtcMeeting.startMicrophone();
    // 4. 뷰티 필터 설정
    trtcMeeting.getBeautyManager().setBeautyStyle(TRTCCloudDef.TRTC_BEAUTY_STYLE_PITU);
    trtcMeeting.getBeautyManager().setBeautyLevel(6);
}

// 5. 참석자가 다른 참석자의 카메라 활성화 알림을 수신하면 재생됨
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onUserVideoAvailable:
            if (param['available']) {
                trtcMeeting.startCameraPreview(
                    param['userId'],
                    TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG,
                    TRTCCloudVideoViewId
                );
            } else {
                trtcMeeting.stopRemoteView(
                    param['userId'],
                    TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG
                );
            }
            break;
    }
}
:::
</dx-codeblock>

[](id:model.step7)
### 7단계: 화면 공유

1. 화면 공유 기능은 시스템에 플로팅 창의 권한을 신청하고, UI에서 구체적인 로직을 구현해야 합니다.
2. startScreenCapture를 호출하여 인코딩 매개변수와 녹화 플로팅 창을 전송하면 화면 공유 기능을 구현할 수 있습니다. 자세한 정보는 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)를 참고하십시오.
3. 회의 중 다른 참석자들은 onUserVideoAvailable 이벤트 알림을 수신합니다.

>! 화면 공유 및 카메라 수집은 상호 충돌되는 작업입니다. 화면 공유 기능을 활성화하려면 먼저 stopCameraPreview를 호출하여 카메라 수집을 비활성화해야 합니다. 자세한 내용은 [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/39859)를 참고하십시오.

<dx-codeblock>
::: dart dart
await trtcMeeting.stopCameraPreview();
trtcMeeting.startScreenCapture(
    videoFps: 10,
    videoBitrate: 1600,
    videoResolution: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720,
    videoResolutionMode: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT,
    appGroup: iosAppGroup,
);
:::
</dx-codeblock>

[](id:model.step8)
### 8단계: 텍스트 채팅 및 금지어 메시지 구현

- sendRoomTextMsg를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 회의에 있는 모든 참석자는 onRecvRoomTextMsg 콜백을 수신하게 됩니다. IM의 백엔드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
<dx-codeblock>
::: dart dart
// 발신 측: 텍스트 메시지 발송
trtcMeeting.sendRoomTextMsg('Hello Word!');
// 수신 측: 텍스트 메시지 수신
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onRecvRoomTextMsg:
            print('발신자: ' + param['userName'] + '메시지: ' + param['message']);
            break;
    }
}
:::
</dx-codeblock>

- sendRoomCustomMsg를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 회의에 있는 모든 참석자는 onRecvRoomCustomMsg 콜백을 수신하게 됩니다. 사용자 정의 메시지는 주로 금지어 등 회의 제어용 사용자 정의 신호 전송에 사용됩니다.
<dx-codeblock>
::: dart dart
// 발신측: 사용자 정의 cmd로 금지어 알림 구분
// eg: "CMD_MUTE_AUDIO"는 금지어 알림을 의미함
trtcMeeting.sendRoomCustomMsg('CMD_MUTE_AUDIO', '1');
// 수신 측: 사용자 정의 메시지 수신
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onRecvRoomCustomMsg:
            if (param['command'] == 'CMD_MUTE_AUDIO') {
                // 금지어 알림 수신
                print('발신자: ' + param['userName'] + '금지어 알림: ' + param['message']);
                trtcMeeting.muteLocalAudio(message == '1');
            }
            break;
    }
}
:::
</dx-codeblock>
