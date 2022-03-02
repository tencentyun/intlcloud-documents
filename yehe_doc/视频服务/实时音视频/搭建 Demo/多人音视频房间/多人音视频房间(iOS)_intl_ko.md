## 효과
App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 그룹 음성/영상 통화, 화면 공유, 뷰티 필터, 저지연 영상 통화 등 TRTC 기능 효과를 경험해 볼 수 있습니다.

## 솔루션 장점
- 초저지연 음성 및 영상 통화, 화면 공유, 뷰티필터, 등과 같은 기능을 통합하여 다중 사용자 멀티미디어 방의 공통 기능을 다룹니다.
- 수요의 2차 개발에 따라 사용자 정의 UI 인터페이스 및 레이아웃을 빠르게 실현할 수 있으며 비즈니스가 빠르게 런칭 되도록 도울 수 있습니다.
- TRTC 및 IM 기본 SDK를 캡슐화하여 기본 로직 제어를 구현하며, 편리한 호출을 위한 인터페이스를 제공합니다.

## 연결 가이드
그룹 멀티미디어 룸 기능에 빠르게 액세스하려면 당사에서 제공하는 App을 기반으로 직접 수정 및 조정하거나 App의 Module을 사용하여 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:ui_step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, **개발 지원** > [Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예: `TestTUIRoom`)을 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

[](id:ui_step2)
### 2단계: App 소스 코드 다운로드
[TUIRoom](https://github.com/tencentyun/TUIRoom)을 클릭하여 이동하거나, 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:ui_step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2 `Example/Debug/GenerateTestUserSig.swift` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.swift` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png" width="750" height="395"/>

4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>?
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui_step4)
### 4단계: 프로젝트 실행
Xcode(11.0 및 이후 버전)를 사용하여 소스 코드 프로젝트 `Example/DemoApp.xcworkspace`를 열고 **실행**을 클릭하면 즉시 해당 App이 디버깅됩니다.

[](id:ui_step5)
### 5단계: 프로젝트 소스 코드 수정
소스 코드의 `Source`에는 UI 폴더가 포함되어 있습니다. 이 폴더는 모두 UI 관련 코드입니다. 다음 표에는 각 폴더에 해당하는 UI 인터페이스가 나열되어 있으므로 2차 조정이 가능합니다.

| 폴더 | 기능 설명 |
|:-------:|:--------|
| TUIRoomEnter | TUIRoom 게이트 관련 구현 코드. TUIRoomEntranceViewController 클래스는 Pods에 의해 노출되는 공개 클래스입니다. |
| TUIRoomMain | TUIRoom의 메인 인터페이스와 관련된 UI 구현 코드. 이 클래스는 Pods의 프라이빗 클래스입니다. |
| TUIRoomMemberList | 참석자 목록 인터페이스와 관련된 UI 구현 코드. 이 클래스는 Pods의 프라이빗 클래스입니다. |
| TUIRoomSet | 인터페이스 관련 UI 구현 코드 설정. 이 클래스는 Pods의 프라이빗 클래스입니다. |

## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.
### 게이트 인터페이스
이미지와 같이 **방 생성** 또는 **방 추가**를 선택하세요.


### 방 페이지 생성
사용자 A 생성, 방 번호는 기본적으로 생성됩니다. **방 생성**을 클릭하여 메인 페이지로 들어갑니다.


### 방 추가 페이지
사용자 B는 사용자 A의 방 번호를 입력하고 **방 추가**를 클릭하여 메인 페이지로 들어갑니다.



### 메인 페이지(사용자 A)
<img src="https://qcloudimg.tencent-cloud.cn/raw/eebab2b82db719000f0dc376070a25e7.png" width=300px>


### 마이크 목록
마이크 목록은 현재 방에 있는 참석자를 표시할 수 있으며, 상대방이 카메라와 마이크를 켜면 상대방의 사진을 보고 상대방의 음성을 들을 수 있습니다.

### 상단 컨트롤 바
헤드셋 전환, 전후방 카메라 전환, 룸 정보, 퇴실 기능을 구현합니다.

### 하단 툴바
마이크/카메라, 뷰티 필터, 참석자 목록, 설정 등의 셀프 제어 기능이 있습니다.

### 뷰티 필터
라이브 방송 중에 화면에 뷰티 필터와 특수 효과를 표시할 수 있습니다.



### 설정 창
멀티미디어 관련 매개변수를 설정할 수 있으며 **화면 공유**를 활성화할 수 있습니다.



### 방 퇴장
- **호스트**: 방 해산, 즉, 모든 사람이 방에서 나옵니다.
- **비호스트**: 혼자 방에서 퇴장합니다.

## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUIRoom)의 `Source` 폴더에는 UI 폴더와 Presenter 폴더가 포함되어 있으며, Presenter 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TUIRoomCore이 포함되어 있습니다. `TUIRoomCore.h` 파일에서 해당 컴포넌트가 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![#600px](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:ui_step1)
### 1단계: SDK 통합
다중 사용자 멀티미디어 비디오 컴포넌트 TUIRoom은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

- **방법1: cocoapods 라이브러리를 통한 종속**
```
 pod 'TXIMSDK_iOS'
 pod ’TXLiteAVSDK_TRTC’
```
>? 두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 Github 메인 페이지에서 획득할 수 있습니다.
- **방법2: 로컬을 통한 종속**
cocoapods 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참고하여 프로젝트에 통합할 수 있습니다.
<table>
<thead><tr><th>SDK</th><th>다운로드 페이지</th><th>통합 가이드</th></tr></thead>
<tbody><tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드 문서</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">통합 가이드 문서</a></td>
</tr>
</tbody></table>

[](id:model_step2)
### 2단계: 권한 설정
`info.plist` 파일에 `Privacy > Camera Usage Description` 및 `Privacy > Microphone Usage Description`을 추가하고 카메라 및 마이크 권한을 신청해야 합니다.

[](id:model_step3)
### 3단계: TUIRoom 컴포넌트 가져오기
**cocoapods를 통해 컴포넌트 가져오기**의 구체적인 작업 단계는 다음과 같습니다.
1. 프로젝트 디렉터리의 `Source`, `Resources`, `TCBeautyKit`, `TXAppBasic` 폴더 및 `TUIRoom.podspec` 파일을 프로젝트 디렉터리에 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
```swift
# 로컬 종속 라이브러리
def local
  pod 'TXAppBasic', :path => "../../TXAppBasic/"
  pod 'TCBeautyKit', :path => "../../TCBeautyKit/"
  pod 'TXLiteAVSDK_TRTC',:path => "../../../SDK/"
end

def pod_local(type)
  loadLocalPod('TUIRoom', type)
end

def loadLocalPod(name, type)
    pod "#{name}/#{type}", :path => "../"
end

target 'DemoApp' do
  local
  pod_local('TRTC')
end
```

[](id:model_step4)
### 4단계: 컴포넌트 생성 및 로그인
1.  TUICore에서 TUILogin을 호출하여 로그인합니다. 다음 예를 참고하십시오.
```swift
TUILogin.initWithSdkAppID(Int32(SDKAPPID))
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)
TUILogin.login(userID, userSig: userSig, succ: {
    debugPrint("login success") 
}, fail: { (code, errorDes) in
   debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```
2. 로그인에 성공하면 TUIRoomCore를 호출하여 방을 생성합니다.
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    } else {
    }
})
```
4. 생성이 완료되면 메인 페이지로 이동합니다.
```swift
let vc = TUIRoomMainViewController(roomId: roomId, isVideoOn: openCameraSwitch.isOn, isAudioOn: openMicSwitch.isOn)
TUIRoomCore.shareInstance().setDelegate(vc)
navigationController?.pushViewController(vc, animated: true)
```
![#600px](https://qcloudimg.tencent-cloud.cn/raw/8c3391905188089fecd17e23477d34ea.png)

[](id:model_step5)
### 5단계: 참석자 방 입장
1. 참석자는 TUICore에서 TUILogin을 호출하여 로그인합니다. 다음 예를 참고하십시오.
```swift
TUILogin.initWithSdkAppID(Int32(SDKAPPID))
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)
TUILogin.login(userID, userSig: userSig, succ: {
    debugPrint("login success") 
}, fail: { (code, errorDes) in
   debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```
2. 로그인에 성공 후 TUIRoomCrre를 호출하여 방에 들어갈 수 있습니다.
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
	    debugPrint("enter room success") 
	} else {
	}
})
```
4. 성공적으로 입장한 후, 다시 메인 페이지로 입장합니다.
```swift
let vc = TUIRoomMainViewController(roomId: roomId, isVideoOn: openCameraSwitch.isOn, isAudioOn: openMicSwitch.isOn)
TUIRoomCore.shareInstance().setDelegate(vc)
navigationController?.pushViewController(vc, animated: true)
```
![#600px](https://qcloudimg.tencent-cloud.cn/raw/ffbda4de381ea198bf808de7d823ab59.png)

[](id:model_step6)
### 6단계: 화면 공유
1. TUIRoomCore의 'startScreenCapture'를 호출하여 공유합니다.
2. 방의 다른 참석자는 'onRemoteUserScreenVideoAvailable'의 이벤트 알림을 받게 됩니다.

```swift
// 버튼을 클릭하여 화면 공유 활성화
if #available(iOS 12.0, *) {
    // 화면 공유
    let params = TRTCVideoEncParam()
    params.videoResolution = TRTCVideoResolution._1280_720
    params.resMode = TRTCVideoResolutionMode.portrait
    params.videoFps = 10
    params.enableAdjustRes = false
    params.videoBitrate = 1500
    TUIRoomCore.shareInstance().startScreenCapture(params)
    TUIRoomBroadcastExtensionLauncher.launch()
} else {
    view.window?.makeToast(.versionLowToastText)
}    
```

[](id:step)
### 7단계: 방 퇴장
- **호스트**는 destoryRoom 인터페이스를 호출하여 방을 삭제하고, IM 그룹 채팅을 종료하고, TRTC 방에서 퇴장합니다. 참석자는 그룹 삭제 및 TRTC 방 퇴장을 알리는 onDestroyRoom 콜백 메시지를 받게 됩니다.
- **참석자**가 leaveRoom 인터페이스를 호출하여 방을 삭제하고, IM 그룹 채팅을 종료하고 TRTC 방에서 퇴장합니다. 다른 참석자는 onRemoteUserLeave 콜백을 수신하고 참석자는 방을 나갔음을 알립니다.

```swift
if isHomeowner {
    TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
} else {
    TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
 }
```
