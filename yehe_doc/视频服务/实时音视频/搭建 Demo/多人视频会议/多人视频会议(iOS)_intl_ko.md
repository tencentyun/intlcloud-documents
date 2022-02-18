## 효과
App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 화면 공유, 뷰티 필터, 저지연 회의 등 TRTC 그룹 화상 회의 시나리오 관련 기능을 체험해 볼 수 있습니다.




빠른 그룹 화상 회의 기능이 필요한 경우, Tencent Cloud에서 제공하는 App을 기반으로 설정을 적절히 수정하거나, TUIMeeting 컴포넌트를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

## App UI 인터페이스 재사용
[](id:ui_step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, **개발 지원>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. 애플리케이션 이름(예: `TestMeetingRoom`)을 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

[](id:ui_step2)
### 2단계: App 소스 코드 다운로드
[TUIMeeting](https://github.com/tencentyun/TUIMeeting)을 클릭하여 Clone하거나 소스 코드를 다운로드합니다.

[](id:ui_step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `TUIMeeting/Debug/GenerateTestUserSig.swift` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.swift` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.


>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui_step4)
### 4단계: 프로젝트 실행
Xcode(11.0 및 이후 버전)를 사용하여 소스 코드 프로젝트 `TUIMeeting/TUIMeetingApp.xcworkspace`를 열고 **실행**을 클릭하여 이 App에 대한 디버깅을 시작합니다.

[](id:ui_step5)
### 5단계: 프로젝트 소스 코드 수정
소스 코드 `Source`에는 Source 폴더와 model 폴더가 포함되어 있으며, ui 폴더에는 인터페이스 코드가 포함되어 있습니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| TRTCMeetingNewViewController.swift | 화상 회의 생성 인터페이스 UI 구현 코드, Pods에 노출되는 퍼블릭 클래스. |
| SegmentVC | 인터페이스 설정 관련 UI 구현 코드. |
| TRTCBroadcastExtensionLauncher.swift | 녹화 팝업창 관련 UI 구현 코드, Pods 프라이빗 클래스. |
| TRTCMeetingMainViewController.swift | 회의방 UI 구현 코드, Pods 프라이빗 클래스. |
| TRTCMeetingMemberViewController.swift | 참석자 리스트 인터페이스 UI 구현 코드, Pods 프라이빗 클래스. |
| TRTCMeetingMoreViewController.swift | 인터페이스 설정 관련 UI 구현 코드, Pods에 노출되는 퍼블릭 클래스. |


## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 회의 번호를 입력하고 **회의 입장**을 클릭합니다.
3. 방의 제목을 입력하고 **채팅 시작**을 클릭합니다.

### 사용자 B
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 사용자 A가 생성한 회의 번호를 입력한 후 *회의 입장**을 클릭합니다.

[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUIMeeting)의 `Source` 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TRTCMeeting이 포함되어 있습니다. `TRTCMeeting.h` 파일에서 해당 컴포넌트가 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


[](id:model.step1)
### 1단계: SDK 통합
그룹 화상 회의 컴포넌트 TUIMeeting은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: cocoapods 라이브러리를 통한 종속**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod ’TXLiteAVSDK_TRTC’
:::
</dx-codeblock>

>? 두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 Github 메인 페이지에서 획득할 수 있습니다.

**방법2: 로컬을 통한 종속**
cocoapods 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참고하여 프로젝트에 통합할 수 있습니다.

| SDK | 다운로드 페이지 | 통합 가이드 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### 2단계: 권한 설정
info.plist 파일에 `Privacy > Camera Usage Description`, `Privacy > Microphone Usage Description`을 추가하고 카메라 및 마이크 권한을 신청해야 합니다.

[](id:model.step3)
### 3단계: TUIMeeting 컴포넌트 가져오기
**cocoapods를 통해 컴포넌트 가져오기**의 구체적인 작업 단계는 다음과 같습니다.
1. 프로젝트 디렉터리의 `Source`, `Resources`, `TCBeautyKit`, `TXAppBasic` 폴더 및 `TUIMeeting.podspec` 파일을 프로젝트 디렉터리에 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
```swift
 pod 'TXAppBasic', :path => "TXAppBasic/"
 pod 'TCBeautyKit', :path => "TCBeautyKit/"
 pod ’TXLiteAVSDK_TRTC’
 pod 'TUIMeeting', :path => "./", :subspecs => ["TRTC"] 
```

[](id:model.step4)
### 4단계: 컴포넌트 생성 및 로그인
1. `sharedInstance` 인터페이스를 호출하여 TRTCMeeting 컴포넌트의 인스턴스 객체를 생성합니다.
2. `setDelegate` 함수를 호출해 컴포넌트의 이벤트 공지를 등록합니다.
3. `login` 함수를 호출해 컴포넌트에 로그인하고, 다음 표를 참조해 핵심 매개변수를 입력합니다.
<table> 
<tr>
<th>매개변수 이름</th>
<th>역할</th>
</tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다. 사업체의 실제 계정 시스템에 맞게 설정할 것을 권장합니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
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
2. 호스트는 `setDelegate`로 이벤트를 호출합니다. `createMeeting`으로 새로운 회의 방을 생성할 수 있습니다.
3. 호스트는 `startCameraPreview`로 비디오 화면 수집을, `startMicrophone`으로 오디오 수집을 시작할 수 있습니다.
4. 호스트가 뷰티 필터 사용을 원할 경우 인터페이스에 뷰티 필터 조절 버튼 호출을 설정하고, `getBeautyManager`를 통해 뷰티 필터를 설정할 수 있습니다.
>? 엔터프라이즈 버전 이외의 SDK는 얼굴 변경 및 스티커 효과 기능을 지원하지 않습니다.

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```swift
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
### 6단계: 그룹 회의에 참석자 입장
1. 참석자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 참석자는 `enterMeeting`을 호출하고 회의방 번호를 전송하여 회의방에 입장할 수 있습니다.
3. 참석자는 `startCameraPreview`로 비디오 화면 수집을, `startMicrophone`으로 오디오 수집을 시작할 수 있습니다.
4. 다른 참석자가 카메라를 켜면 `onUserVideoAvailable` 이벤트가 수신됩니다. 이때 `startRemoteView`를 호출하고 userId를 전송하면 재생이 시작됩니다.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```swift
// 1. 참석자 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. enterMeeting 함수 구현
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("회의 입장 실패:" + msg!)
   }
}
```
```swift
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
1. `startScreenCapture`를 호출하여 인코딩 매개변수와 녹화 플로팅 창을 전송하면 화면 공유 기능을 구현할 수 있습니다. 자세한 정보는 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)를 참고하십시오.
2. 회의 중 다른 참석자들은 `onUserVideoAvailable` 이벤트 공지를 수신합니다.

>!화면 공유와 카메라 수집은 상호 충돌되는 작업입니다. 화면 공유 기능을 활성화하고 싶은 경우, 먼저 `stopCameraPreview`를 호출하여 카메라 수집을 비활성화해야 합니다.

```swift
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
### 8단계: 텍스트 채팅 및 음소거 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
IM의 백엔드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
```swift
// 발신측: 텍스트 메시지 발송
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}

// 수신측: 텍스트 메시지 수신
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint(":\(String(describing: userInfo.userId))님이 발송한 메시지\(String(describing: message))")
}
```
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 호스트와 시청자 모두가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
사용자 정의 메시지는 주로 음소거 등과 같은 사용자 정의 신호 전송에 사용됩니다.
```swift
// 발신 측: 사용자 정의 Cmd로 음소거 알림 구분
// eg:"CMD_MUTE_AUDIO"는 음소거 알림을 의미함
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}

// 수신측: 사용자 정의 메시지 수신
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint(":\(String(describing: userInfo.userId))님이 발송한 음소거 알림:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```
