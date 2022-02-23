## 효과

Tencent Cloud의 App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076)한 후 설치하여 음성 살롱 기능을 체험해볼 수 있습니다. Demo에는 음성 채팅, 마이크 켜기/끄기, 저지연 음성 인터랙션 등 음성 채팅 시나리오에서의 TRTC 관련 기능이 포함되어 있습니다.

<table>
     <tr>
         <th>방 주인의 마이크 위치 작업</th>  
         <th>청취자의 마이크 위치 작업</th>  
     </tr>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/849c3cff658d82b0fe0d3e7b1a490e13.png"/ style="max-height:700px;"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/25cc9b7695cc208c946b50710e842e41.png"/  style="max-height:700px;"></td>
</tr>
</table>



빠른 음성 살롱 액세스 기능이 필요한 경우, Tencent Cloud에서 제공하는 App를 기반으로 설정을 적합하게 수정하거나 TUIChatSalon 컴포넌트을 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:DemoUI)

## App UI 인터페이스 재사용

[](id:ui.step1)

### 1단계: 신규 애플리케이션 생성

1. TRTC 멀티미디어 콘솔에 로그인한 후, **개발 지원** > **[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. 애플리케이션 이름(예: `TestChatSalon`)을 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.



[](id:ui.step2)

### 2단계: App 소스 코드 다운로드
[TUIChatSalon](https://github.com/tencentyun/TUIChatSalon)를 클릭하여 이동하거나, 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:ui.step3)
### 3단계: App 프로그램 파일 설정

1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `TUIChatSalon/Debug/GenerateTestUserSig.swift` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.swift` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)

### 4단계: App 실행

Xcode(11.0 및 이후 버전)를 사용하여 소스 코드 프로젝트 `TUIChatSalon/TUIChatSalonApp.xcworkspace`를 열고 **실행**을 클릭하여 이 App에 대한 디버깅을 시작합니다.

[](id:ui.step5)

### 5단계: App 소스 코드 수정

소스 코드의 `Source` 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 관련 코드 및 로직입니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더                      | 기능 설명                             |
| --------------------------------- | ------------------------------------ |
| TRTCChatSalonEnteryControl.swift  |이 파일에는 모든 ViewController를 초기화하는 방법이 포함되어 있습니다. 해당 인스턴스를 통해 신속하게 ViewController 객체를 획득할 수 있습니다.|
| TRTCCreateChatSalonViewController | 방 생성 페이지 로직                   |
| TRTCChatSalonViewController       | 방 주인과 청취자의 인터페이스를 포함하는 메인 방 페이지 |

## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A

1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. **방 생성**을 클릭합니다.
3. 방의 제목을 입력하고 **채팅 시작**을 클릭합니다.

### 사용자 B
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 사용자 A가 생성한 방 번호를 입력한 후 **방 입장**을 클릭합니다.


>! 방 번호는 사용자 A의 방 상단에서 확인할 수 있습니다.


[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUIChatSalon)의 `Source` 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TRTCChatSalon이 포함되어 있습니다. `TRTCChatSalon.h` 파일에서 해당 컴포넌트이 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)

[](id:model.step1)

### 1단계: SDK 통합

음성 살롱 컴포넌트인 TRTCChatSalon은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

- **방법1: cocoapods 라이브러리를 통한 종속**
<dx-codeblock>
::: swift
pod 'TXIMSDK_iOS'
pod ’TXLiteAVSDK_TRTC’
:::
</dx-codeblock>
>?두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK)의 GitHub 메인 페이지에서 획득할 수 있습니다.
- **방법2: 로컬을 통한 종속**
cocoapods 라이브러리 액세스가 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참고하여 프로젝트에 통합할 수 있습니다.
<table>
<tr><th>SDK</th><th>다운로드 페이지</th><th>통합 가이드</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드 문서</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">통합 가이드 문서</a></td>
</tr></table>

[](id:model.step2)
### 2단계: 권한 설정
`info.plist` 파일에 `Privacy > Camera Usage Description`, `Privacy > Microphone Usage Description`을 추가해 마이크 권한을 신청해야 합니다.

[](id:model.step3)
### 3단계: TUIChatSalon 컴포넌트 가져오기
**cocoapods를 통해 컴포넌트 가져오기**의 구체적인 작업은 다음과 같습니다.
1. 프로젝트 디렉터리의 `Source`, `Resources`, `TXAppBasic` 폴더 및 `TUIChatSalon.podspec` 파일을 프로젝트 디렉터리에 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod ’TXLiteAVSDK_TRTC’
pod 'TUIChatSalon', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### 4단계: 컴포넌트 생성 및 로그인
1. TRTCChatSalon의 `sharedInstance` 유형 방법을 호출해 TRTCChatSalon 인스턴스 객체를 생성합니다.
2. `setDelegate` 방법을 호출해 컴포넌트의 이벤트 콜백 공지를 등록합니다.
3. `login` 방법을 호출해 컴포넌트에 로그인하고, 다음 표를 참고해 관련 매개변수를 입력합니다.
<table>    
<tr><th>매개변수 이름</th><th>역할</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다. 사업체의 실제 계정 시스템에 맞게 설정할 것을 권장합니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
</tr></tr>
<tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr></table>
<dx-codeblock>
::: Swift Swift
// Swift 예시
// 코드에서 서비스 로직을 담당하는 유형
class YourController {
    // 속성을 계산해 단일 항목 객체 획득
    var chatSalon: TRTCChatSalon {
        return TRTCChatSalon.shared()
    }
    

    // 기타 코드 로직
    ......

}
// chatSalon 프록시 설정
self.chatSalon.setDelegate(delegate: self)

// 호출 방법은 다음과 같습니다. 클로저 내에서 weak self를 사용해 순환 참고를 방지하시기 바랍니다. 다음은 weak self를 생략한 예시 코드입니다.
self.chatSalon.login(sdkAppID: sdkAppID, userID: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // 콜백 서비스 로직        
}
:::
</dx-codeblock>

[](id:model.step5)

### 5단계: 방 주인 방송 시작

1. 방 주인은 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 방 주인이 `createRoom`을 호출해 새로운 음성 살롱을 생성합니다. 방 ID, 마이크를 켤 때 방 주인 확인 필요 여부, 방 유형 등 방 속성 정보를 전송합니다.
3. 방 주인은 사용자가 입장할 때 `onAnchorEnterSeat` 이벤트 알림을 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)
<dx-codeblock>
::: Swift Swift
// 1. 방 주인 닉네임 및 프로필 사진 설정
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 결과 콜백           
}


// 2. 방 주인 방 생성
let param = ChatSalonParam.init()
param.roomName = "방 이름"
param.needRequest = true // 청취자가 마이크를 켤 때 방 주인 동의 필요 여부
param.coverUrl = "썸네일 URL"
param.seatInfoList = []
self.chatSalon.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // 3. 방 생성 후 자리 점유 시작
    self.chatSalon.enterSeat { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 방 주인 자리 점유 성공
        } else {
            // 방 주인 자리 점유 실패
        }
    }
}

// 4. 자리를 점유한 후 onAnchorEnterSeat 이벤트 공지 수신
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
}
:::
</dx-codeblock>


[](id:model.step6)

### 6단계: 청취자 시청

1. 청취자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 청취자가 서비스 백엔드에서 최신 음성 살롱 방 리스트를 가져옵니다.
>?App의 음성 살롱 리스트는 참고용입니다. 음성 살롱 리스트의 서비스 로직은 매우 다양하여 Tencent Cloud에서는 현재 음성 살롱 리스트 관리 서비스를 제공하지 않습니다. 음성 살롱 리스트는 직접 관리하시기 바랍니다.
3. 청취자가 `getRoomInfoList`를 호출해 방 세부 정보를 가져옵니다. 해당 정보는 방 주인이 `createRoom`을 호출해 음성 살롱 생성 시 설정한 간단한 설명 정보입니다.
>!음성 살롱 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomInfoList` 호출 관련 단계는 건너뛸 수 있습니다.
4. 청취자가 음성 살롱 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
5. 방 입장 후 컴포넌트의 `onRoomInfoChange` 방 속성 변경 이벤트 알림을 수신합니다. 이 때 UI에 방 이름 표시, 마이크를 켤 때 방 주인에게 동의 요청 필요 여부 기록 등 방의 속성을 기록할 수 있으며 그에 해당하는 변경이 가능합니다.
6. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterSeat` 이벤트 알림도 수신합니다.

![](https://main.qcloudimg.com/raw/6fbabfa4e217022cf3d05677e4a45538.png)
<dx-codeblock>
::: Swift Swift
// 1. 청취자 닉네임 및 프로필 사진 설정
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 결과 콜백           
}

// 2. 서비스 백엔드로부터 획득하는 방 리스트가 roomList라고 가정할 경우
let roomList: [Int] = getRoomIDList() // 방 ID 리스트 함수 획득

// 3. getRoomInfoList 호출을 통해 방 세부 정보 획득
self.chatSalon.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [ChatSalonInfo]) in
    // 결과 획득, UI 새로고침 가능
}

// 4. roomId를 전송하여 방 입장
self.chatSalon.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 방 입장 결과 콜백
    if code == 0 {
       // 방 입장 성공
    }
}

// 5. 방 입장 완료 후 onRoomInfoChange 이벤트 알림 수신
func onRoomInfoChange(roomInfo: ChatSalonInfo) {
    // 방 이름 등 정보 새로고침 가능
}

// 6. onAnchorEnterSeat 이벤트 알림 수신
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // 마이크 켜기 이벤트 처리
}
:::
</dx-codeblock>

[](id:model.step7)

### 7단계: 마이크 켜기/끄기

<dx-tabs>
::: 방 주인

1. `pickSeat`로 청취자 userId를 전송하면 특정 사용자의 마이크를 켤 수 있으며, 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.
2. `kickSeat`로 해당하는 사용자의 userId를 전송하면 특정 사용자의 마이크를 끌 수 있으며, 방 안에 있는 모든 사용자가 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/0eb3dbe14b166a24252f0efb45a6b24f.png)

마이크 위치 작업 후의 이벤트 알림 순서는 다음과 같습니다. callback > onAnchorEnterSeat 등 독립 이벤트.

<dx-codeblock>
::: Swift Swift
// 1. 방 주인의 특정 사용자의 마이크 켜기
self.chatSalon.pickSeat(userID: "123") { (code, message) in
    // 2. callback 콜백 수신
}

// 3. 청취자가 호스트가 되어, 마이크 위치를 알림하면 청취자가 실제로 마이크 켜기에 성공했는지 판단
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // 마이크 켜기 이벤트 처리
}
:::
</dx-codeblock>

:::
::: 청취자

1. `enterSeat`로 마이크를 켤 수 있으며 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.
2. `leaveSeat`로 직접 마이크를 끄면 방 안에 있는 모든 사용자가 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)
마이크 위치 작업 후의 이벤트 알림 순서는 다음과 같습니다. callback > onAnchorEnterSeat 등 독립 이벤트.
<dx-codeblock>
::: Swift Swift
// 1. 청취자의 마이크 켜기 신청
self.chatSalon.enterSeat { (code, message) in
    // 2. callback 콜백 수신
}

// 3. 청취자가 호스트가 되어 마이크 위치를 알림하면, 본인 여부 및 해당하는 프로세스 진행 여부 판단
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // 마이크 켜기 이벤트 처리
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)

### 8단계: 초대 신호 사용

사용자 App이 상대방이 동의해야 다음 단계의 작업을 진행할 수 있는 비즈니스 프로세스인 경우, 초대 신호는 해당하는 지원을 제공할 수 있습니다.

<dx-tabs>
::: 청취자가 직접 마이크 켜기 신청

1. 청취자가 `sendInvitation`을 호출해 방 주인의 userId와 서비스 사용자 정의 명령어 등을 전송합니다. 이 때 함수는 inviteId를 반환하고 해당 inviteId를 기록합니다.
2. 방 주인이 `onReceiveNewInvitation` 이벤트 알림을 수신합니다. 이 때 UI에 방 주인의 동의 여부를 묻는 팝업 창을 띄울 수 있습니다.
3. 방 주인이 동의를 선택한 후 `acceptInvitation`을 호출하고 inviteId를 전송합니다.
4. 청취자가 `onInviteeAccepted` 이벤트 공지를 수신하고 `enterSeat`를 호출해 마이크를 켭니다.

![](https://main.qcloudimg.com/raw/71b657c495cb52317c4c32a919407b36.png)
<dx-codeblock>
::: Swift Swift
// 청취자 앵글
// 1. sendInvitation을 호출해 마이크 켜기 요청
let inviteId = self.chatSalon.sendInvitation(cmd: "ENTER_SEAT", userID: ownerUserId, content: "1") { (code, message) in
    // 발송 결과 콜백
}
// 2. 초대 동의 요청을 수신하면 정식으로 마이크 켜짐
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.enterSeat { (code, message) in
            // 마이크 켜기 결과 콜백
        }
    }
}

// 방 주인 앵글
// 1. 방 주인이 요청을 수신함
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. 방 주인이 청취자 요청에 동의
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
::: 방 주인이 청취자에게 마이크 켜기 요청

1. 방 주인이 `sendInvitation`을 호출해 청취자의 userId와 서비스 사용자 정의 명령어 등을 전송합니다. 이때 함수는 inviteId를 반환하고 해당 inviteId를 기록합니다.
2. 청취자가 `onReceiveNewInvitation` 이벤트 알림을 수신합니다. 이 때 UI에 청취자의 마이크 켜기 동의 여부를 묻는 팝업창을 띄울 수 있습니다.
3. 청취자가 동의를 선택한 후 `acceptInvitation`을 호출하고 inviteId를 전송합니다.
4. 방 주인이 `onInviteeAccepted` 이벤트 알림을 수신하고 `pickSeat`를 호출해 청취자의 마이크를 켭니다.

![](https://main.qcloudimg.com/raw/60025544abae69e22de22a4b81bf6951.png)

<dx-codeblock>
::: Swift Swift
// 방 주인 앵글
// 1. 방 주인이 sendInvitation을 호출해 청취자에게 '123'마이크 켜기 요청
let inviteId = self.chatSalon.sendInvitation(cmd: "PICK_SEAT", userID: ownerUserId, content: "2") { (code, message) in
    // 발송 결과 콜백
}

// 2. 초대 동의 요청을 수신하면 정식으로 마이크 켜짐
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.pickSeat(userID: ) { (code, message) in
            // 마이크 켜기 결과 콜백
        }
    }
}

// 청취자 앵글
// 1. 청취자가 요청을 수신함
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. 청취자의 방 주인 요청 수락
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step9)

### 9단계: 문자 채팅 및 댓글 자막 메시지 구현

- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며 해당 방에 있는 모든 호스트와 청취자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
  IM의 백엔드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
  <dx-codeblock>
  ::: Swift Swift
  // 발신측: 텍스트 메시지 발송
  self.chatSalon.sendRoomTextMsg(message: message) { (code, message) in
        

}
// 수신측: 텍스트 메시지 수신
func onRecvRoomTextMsg(message: String, userInfo: ChatSalonUserInfo) {
    //수신한 message 정보 처리 방법        
}
:::
</dx-codeblock>

- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며 해당 방에 있는 모든 호스트와 청취자가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
  사용자 정의 메시지는 '좋아요' 메시지 발송과 같은 사용자 정의 신호 전송에 주로 사용됩니다.
  <dx-codeblock>
  ::: Swift Swift
  // 예시: 발신측: 사용자 정의 Cmd를 통해 댓글 자막과 '좋아요' 메시지 구분 가능
  // eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": '좋아요' 메시지
  self.chatSalon.sendRoomCustomMsg(cmd: 'CMD_DANMU', message: "hello world", callback: nil)
  self.chatSalon.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
  // 수신측: 사용자 정의 메시지 수신
  func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: ChatSalonUserInfo) {
    if cmd == "CMD_DANMU" {
        // 댓글 자막 메시지 수신
    }
    if cmd == "CMD_LIKE" {
        // '좋아요' 메시지 수신
    }
  }
  :::
  </dx-codeblock>
