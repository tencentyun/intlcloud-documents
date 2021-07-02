## 효과
Demo를 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 화면 공유, 뷰티 필터, 저 딜레이 회의 등 TRTC 그룹 화상 회의 시나리오 관련 기능을 체험해 볼 수 있습니다.

빠른 그룹 화상 회의 기능 액세스를 위해 직접 Tencent Cloud에서 제공하는 Demo를 기반으로 적합하게 수정하거나, TRTCMeeting 모듈을 사용해 UI 인터페이스를 사용자 정의할 수도 있습니다.

## Demo UI 인터페이스 재사용
[](id:ui_step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후 [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예: `TestMeetingRoom`)을 입력한 후 [생성]을 클릭합니다.

>! 해당 기능은 기본 PaaS 서비스인 Tencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [인스턴트 메시지 IM](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. 인스턴트 메시지 IM은 부가 서비스이며, 자세한 과금 규정은 [인스턴트 메시지 IM 요금 가이드](https://intl.cloud.tencent.com/document/product/1047/34350)를 참조하십시오.

[](id:ui_step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 수요에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:ui_step3)
### 3단계: Demo 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.h` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.


>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 지향의 인터페이스를 제공합니다. UserSig가 필요한 경우 App에서 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

### 4단계: Demo 실행
Xcode(11.0 버전 이상)를 사용하여 소스 코드 프로그램인 `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`를 열고 [실행]을 클릭하면 Demo를 디버깅할 수 있습니다.

### 5단계: Demo 소스 코드 수정
소스 코드 ``trtcmeetingdemo``에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 코드입니다. 2차 수정을 위해 다음과 같이 각 파일 또는 폴더와 그에 해당하는 UI 화면에 대한 설명을 제공합니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| SegmentVC | 인터페이스 설정 관련 UI 구현 코드 |
| TRTCBroadcastExtensionLauncher.swift | 녹화 팝업창 관련 UI 구현 코드 |
| TRTCMeetingNewViewController | 화상 회의 생성 인터페이스 UI 구현 코드 |
| TRTCMeetingMainViewController | 회의룸 인터페이스 UI 구현 코드 |
| TRTCMeetingMemberViewController | 참여자 리스트 인터페이스 UI 구현 코드 |
| TRTCMeetingMoreViewController | 인터페이스 설정 관련 UI 구현 코드  |


[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드]의 trtcmeetingdemo 폴더에는 ui 폴더와 model 폴더가 있으며, model 폴더에는 재사용 가능한 오픈 소스 모듈인 TRTCMeeting이 포함되어 있습니다. `TRTCMeeting.h` 파일에서 해당 모듈이 제공하는 인터페이스 함수를 확인할 수 있으며, 해당 인터페이스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


[](id:model.step1)
### 1단계: SDK 통합
그룹 화상 회의 모듈 TRTCMeeting은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: cocoapods 라이브러리를 통한 종속**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 Github 메인 페이지에서 획득할 수 있습니다.

**방법2: 로컬을 통한 종속**
cocoapods 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참조하여 프로젝트에 통합할 수 있습니다.

| SDK | 다운로드 페이지 | 통합 가이드 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### 2단계: 권한 설정
info.plist 파일에 Privacy > Camera Usage Description, Privacy > Microphone Usage Description을 추가하고 카메라 및 마이크 권한을 신청해야 합니다.

[](id:model.step3)
### 3단계: TRTCMeeting 모듈 가져오기
`iOS/LiteAVDemo/TXLiteAVDemo/TRTCMeetingDemo/model` 디렉터리의 모든 파일을 프로젝트에 복사합니다.

<span id="model.step4"></span>
### 4단계: 모듈 생성 및 로그인
1. `sharedInstance` 인터페이스를 호출하여 TRTCMeeting 모듈의 인스턴스 객체를 생성합니다.
2. `setDelegate` 함수를 호출하여 모듈의 이벤트 공지를 등록합니다.
3. `login` 함수를 호출해 모듈에 로그인하고, 다음 표를 참고하여 핵심 매개변수를 입력합니다.
<table> 
<tr>
<th>매개변수 이름</th>
<th>역할</th>
</tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 조회할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr><tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr>
</table>

```swift
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)

TRTCMeeting.sharedInstance().login(SDKAPPID, userId: userID, userSig: userSig, callback: { code, message in
    if code == 0 {
        //로그인 성공
    }
})
```

[](id:model.step5)
### 5단계: 그룹 회의 생성
1. 호스트는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트는 `setDelegate`로 이벤트를 호출합니다. `createMeeting` 로 새로운 회의룸을 생성할 수 있습니다.
3. 호스트는 `startCameraPreview`로 비디오 화면 수집을, `startMicrophone`으로 오디오 수집을 시작할 수 있습니다.
4. 호스트가 뷰티 필터 사용을 원할 경우 인터페이스에 뷰티 필터 조절 버튼 호출을 설정하고, `getBeautyManager`를 통해 뷰티 필터를 설정할 수 있습니다.
>? 엔터프라이즈 버전 이외의 SDK는 얼굴 변경 및 스티커 효과 기능을 지원하지 않습니다.

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```
// 1. 호스트 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. 호스트 방 생성
trtcMeeting.createMeeting(roomId) { (code, msg) in
 if code == 0 {
   // 방 생성 성공
  let localPreviewView=getRenderView(userId: selfUserId)!
  TRTCMeeting.sharedInstance().startCameraPreview(true, view: localPreviewView)
  TRTCMeeting.sharedInstance().startMicrophone();

  // 기본 뷰티 필터 매개변수 사용
  beautyPannel.resetAndApplyValues()
  return;
 }
}
```


[](id:model.step6)
### 6단계: 그룹 회의룸에 참여자 입장
1. 참여자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 참여자는 `enterMeeting`을 호출하고 회의룸 번호를 전송하여 회의룸에 입장할 수 있습니다.
3. 참여자는 `startCameraPreview`로 비디오 화면 수집을, `startMicrophone`으로 오디오 수집을 시작할 수 있습니다.
4. 다른 참여자가 카메라를 켜면 `onUserVideoAvailable` 이벤트가 수신됩니다. 이때 `startRemoteView`를 호출하고 userId를 전송하면 재생이 시작됩니다.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```
// 1. 참여자 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.enterMeeting 함수 구현
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("회의룸 입장 실패:" + msg!)
   }
}
```

```
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  //콜백을 수신하고 startRemoteView를 호출하여 userId를 전송해 재생을 시작합니다.
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
} else {
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
//현재 인터페이스 새로고침
renderView?.refreshVideo(isVideoAvailable: available)
```

[](id:model.step7)
### 7단계: 화면 공유
1. `startScreenCapture`를 호출하여 인코딩 매개변수와 녹화 플로팅 창을 전송하면 화면 공유 기능을 구현할 수 있습니다. 자세한 정보는 [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)를 참조하십시오.
2. 회의 중 다른 참여자들은 `onUserVideoAvailable` 이벤트 공지를 수신합니다.

>!화면 공유와 카메라 수집은 상호 충돌되는 작업입니다. 화면 공유 기능을 활성화하고 싶은 경우, 먼저 `stopCameraPreview`를 호출하여 카메라 수집을 비활성화해야 합니다.

```
// 1. 버튼을 클릭하여 화면 공유 활성화
if #available(iOS 12.0, *) {
  // 녹화 전에는 반드시 먼저 카메라 수집을 비활성화해야 합니다.
  self.setLocalVideo(isVideoAvailable: false)

  // 화면 공유
  let params = TRTCVideoEncParam()
  params.videoResolution = TRTCVideoResolution._1280_720
  params.videoFps = 10
  params.videoBitrate = 1800
  TRTCMeeting.sharedInstance().startScreenCapture(params)
  TRTCBroadcastExtensionLauncher.launch()
} else {
  self.view.makeToast("시스템 버전이 12.0 이하입니다. 시스템을 업데이트하십시오.")
}     
```

[](id:model.step8)
### 8단계: 텍스트 채팅 및 금지어 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 호스트와 시청자 모두가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
IM의 백그라운드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
```
// 발신 측: 텍스트 메시지 발송
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}
// 수신 측: 텍스트 메시지 수신
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint(":\(String(describing: userInfo.userId))님이 발송한 메시지\(String(describing: message))")
}
```
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 호스트와 시청자 모두가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
사용자 정의 메시지는 주로 금지어 사용 제한 등과 같은 사용자 정의 신호 전송에 사용됩니다.
```
// 발신 측: 사용자 정의 Cmd로 금지어 공지 구분
// eg:"CMD_MUTE_AUDIO"는 금지어 공지를 의미함
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}
// 수신 측: 사용자 정의 메시지 수신
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint(":\(String(describing: userInfo.userId))님이 발송한 금지어 공지:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```

