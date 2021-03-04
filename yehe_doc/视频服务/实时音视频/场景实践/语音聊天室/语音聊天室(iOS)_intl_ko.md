## 효과
Tencent Cloud의 Demo를 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 음성 채팅방 기능을 체험해볼 수 있습니다. Demo에는 마이크 위치 관리, 저딜레이 음성 인터랙션, 문자 채팅 등 음성 채팅 시나리오에서의 TRTC 관련 기능이 포함되어 있습니다.











신속한 음성 채팅방 기능이 필요할 경우, Tencent Cloud의 Demo를 기반으로 직접 수정 및 모델링을 진행하거나 TRTCVoiceRoom 모듈을 사용하여 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

<span id="DemoUI"> </span>
## Demo UI 인터페이스 재사용

<span id="ui.step1"></span>
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인하여 [개발 보조]>[빠른 Demo 활성화](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestVoiceRoom`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

>?해당 기능은 Tencent Cloud의 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [IM](https://intl.cloud.tencent.com/document/product/1047) 두 가지 서비스 기반의 PAAS 서비스를 이용합니다. TRTC가 활성화되면 인스턴트 메시징 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [IM 가격 설명](https://intl.cloud.tencent.com/document/product/1047/34350)을 참조하십시오.



<span id="ui.step2"></span>
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 커서를 해당하는 부분으로 이동한 후, [Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)를 클릭하여 Github(또는 [ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip) 클릭)로 이동하여 SDK와 Demo 소스 코드를 다운로드합니다.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

<span id="ui.step3"></span>
### 3단계: Demo 프로젝트 파일 설정
1. [2단계](#ui.step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.h` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 방법입니다. 여기에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 지향의 인터페이스를 제공합니다. UserSig가 필요한 경우 귀하의 App이 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

<span id="ui.step4"></span>
### 4단계: Demo 실행
Xcode(11.0 버전 이상)를 사용하여 오픈 소스 프로그램인 `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`를 열고 [실행]을 클릭하면 해당 Demo가 디버깅됩니다.

<span id="ui.step5"></span>
### 5단계: Demo 소스 코드 수정
소스 코드의 TRTCVoiceRoomDemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 관련 코드 및 로직입니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
|TRTCVoiceRoomEnteryController|해당 파일에는 모든 ViewController의 기본 설정 획득 방법이 포함되어 있으며, 해당 인스턴스를 통해 신속하게 ViewController 객체를 획득할 수 있습니다.|
| NetworkRoomManager | 서비스 백그라운드 인터랙티브 관련 | 
| TRTCCreateVoiceRoomViewController | 음성 채팅방 페이지 생성 로직 | 
| TRTCVoiceRoomListViewController | 리스트 페이지 로직 | 
| TRTCVoiceRoomViewController | 메인 방 페이지. 호스트와 시청자 두 가지 인터페이스 포함 | 

각 `TRTC'XXXX'ViewController` 폴더에는 `ViewController`, `RootView`, `ViewModel`이 포함되어 있으며, 해당 파일의 역할은 다음과 같습니다.

| 파일 이름 | 기능 설명 |
|:-------:|:--------|
| ViewController | 페이지 컨트롤러. 페이지 라우팅 작업과 RootView 및 ViweModel의 바인딩 작업 담당 | 
| RootView | 이미지 보기, 모든 이미지 레이아웃 | 
| ViewModel | 이미지 보기 컨트롤러. 이미지 보기 인터랙션에 응답하며, 이미지 보기 응답 상태 반환 | 

<span id="model"> </span>
## 사용자 정의 UI 인터페이스 구현
[소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo)의 TRTCVoiceRoomDemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 모듈인 TRTCVoiceRoom이 포함되어 있습니다. `TRTCVoiceRoom.swift` 파일에서 해당 모듈에서 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


<span id="model.step1"> </span>
### 1단계: SDK 통합
음성 채팅 모듈인 TRTCVoiceRoom은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: cocoapods 웨어하우스를 통한 종속 **
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?해당 두 SDK 제품의 최신 버전은 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK) Github 메인 페이지에서 다운로드할 수 있습니다.

**방법2: 로컬을 통한 종속**
cocoapods 웨어하우스 연결이 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참조하여 프로젝트에 통합할 수 있습니다.

| SDK | 다운로드 페이지 | 통합 가이드 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### 2단계: 권한 설정
info.plist 파일에 Privacy > Camera Usage Description, Privacy > Microphone Usage Description을 추가하여 카메라와 마이크 권한을 요청해야 합니다.

<span id="model.step3"> </span>
### 3단계: TRTCVoiceRoom 모듈 가져오기
`iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo/model` 디렉터리의 모든 파일을 프로젝트에 붙여넣습니다.

<span id="model.step4"> </span>
### 4단계: 모듈 생성 및 로그인
1. TRTCVoiceRoomImp의 `sharedInstance` 클래스를 호출하는 방법으로 TRTCVoiceRoom 프로토콜을 준수하는 인스턴스 객체를 생성할 수 있습니다. 또는 `shared` 클래스를 호출하는 방법으로 TRTCVoiceRoomImp 인스턴스 객체를 불러와 직접 사용할 수 있으며, 두 방법은 TRTCVoiceRoom 인터페이스 사용 상에 어떠한 차이점도 없습니다.
2. `setDelegate` 함수를 호출하여 모듈의 이벤트 콜백 알림을 등록합니다.
3. `login` 함수를 호출해 모듈에 로그인하고, 다음 표를 참고하여 관련 매개변수를 입력합니다.
<table>    
<tr>
<th>매개변수 이름</th>
<th>작용</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr>
<tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr>
</tr>
<tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr>
</table>

```Swift
// Swift 예시
// 코드에서 서비스 로직을 담당하는 클래스
class YourController {
    // 속성을 계산해 단일 항목 객체 획득
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // 기타 코드 로직
    ......
}
// voiceroom 프록시 설정
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// 호출 방법은 다음과 같습니다.클로저 내에서 weak self를 사용해 순환 참조를 방지하시기 바랍니다. (다음은 weak self를 생략한 예시 코드입니다.)
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // 콜백 서비스 로직        
}
```

<span id="model.step5"> </span>
### 5단계: 호스트의 방송 시작
1. 호스트는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트가 `createRoom`을 호출하여 새로운 음성 채팅방을 생성합니다. 이때 방 ID, 마이크 연결 시 방장 확인 필요 여부, 마이크 위치 개수 등 방 속성 정보를 전송합니다.
3. 호스트가 방 생성 후 `enterSeat`을 호출하여 자리에 입장합니다.
4. 호스트가 모듈의 `onSeatListChange` 마이크 위치 리스트 변경 이벤트 알림을 수신합니다. 이때 마이크 위치 리스트의 변경 내용을 UI 인터페이스에 새로고침할 수 있습니다.
5. 호스트는 마이크 위치 리스트에 사용자가 입장할 때 `onAnchorEnterSeat` 이벤트 알림 또한 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

예시 코드:

```swift
// 1. 호스트 닉네임 및 프로필 사진 설정
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 결과 콜백           
}

// 2. 호스트 방 생성
let param = VoiceRoomParam.init()
param.roomName = "방 이름"
param.needRequest = true // 시청자 마이크 연결 시 호스트 동의 필요 여부
param.coverUrl = "썸네일 URL"
param.seatCount = 7 // 방 자리 개수. 여기에서는 총 7개로 설정하며, 방장이 한 자리를 점유한 후 시청자가 남은 6개 자리를 점유합니다.
param.seatInfoList = []
for _ in 0..<param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}
self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // 방 생성 성공 후 자리 점유
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 방장 자리 점유 성공
        } else {
            // 방장 자리 점유 실패
        }

    }
}

// 4. 자리를 점유한 후 onSeatListChange 이벤트 알림 수신
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 마이크 위치 리스트 새로고침
}
// 5. onAnchorEnterSeat 이벤트 알림 수신
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // 호스트 마이크 연결 이벤트 처리
}
```

<span id="model.step6"> </span>
### 6단계: 시청자 시청
1. 시청자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 시청자 측에서 서비스 백그라운드로부터 최신 음성 채팅방 리스트를 가져옵니다.
 >?Demo의 음성 채팅방 리스트는 참고용입니다. 음성 채팅방 리스트 로직은 매우 다양하여 Tencent Cloud에서는 현재 음성 채팅방 리스트 관리 서비스를 제공하지 않으며, 음성 채팅방 리스트는 직접 관리하시기 바랍니다.
3. 시청자가 `getRoomInfoList`를 호출해 방 세부 정보를 가져옵니다. 해당 정보는 호스트가 `createRoom`을 호출하여 음성 채팅방 생성 시 설정한 간단한 설명 정보입니다.
 >!음성 채팅방 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomInfoList` 호출 관련 단계는 건너뛸 수 있습니다.
4. 시청자가 음성 채팅방 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
5. 방 입장 후 모듈의 `onRoomInfoChange` 방 속성 변경 이벤트 알림을 수신하며, 이때 UI에 방 이름 표시, 마이크 연결 시 호스트에게 동의를 요청해야 하는지 여부 등 방 속성을 기록할 수 있으며, 상응하게 변경합니다.
6. 방 입장 후 모듈의 `onSeatListChange` 마이크 위치 리스트 변경 이벤트 알림을 수신합니다. 이때 마이크 위치 리스트의 변경 내용을 UI 인터페이스에 새로고침할 수 있습니다.
7. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterSeat` 이벤트 알림 또한 수신합니다.


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)

```Swift
// 1. 시청자 닉네임 및 프로필 사진 설정
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 결과 콜백           
}

// 2. 서비스 백그라운드로부터 획득하는 방 리스트가 roomList라고 가정할 경우,
let roomList: [Int] = getRoomIDList() // 방 ID 리스트 획득 함수

// 3. getRoomInfoList 호출을 통해 방 세부 정보 획득
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    // 결과 획득, 이때 UI 새로고침
}

// 4. 음성 채팅방 선택 후 roomid를 전달하여 방 입장
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 방 입장 결과 콜백
    if code == 0 {
       // 방 입장 성공
    }
}

// 5. 방 입장 완료 후 onRoomInfoChange 이벤트 알림 수신
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // 방 이름 등 정보 새로고침 가능
}

// 6. 방 입장 완료 후 onSeatListChange 이벤트 알림 수신
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 마이크 위치 리스트 새로고침
}

// 7. onAnchorEnterSeat 이벤트 알림 수신
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // 마이크 연결 이벤트 처리
}

```

<span id="model.step7"> </span>
### 7단계: 마이크 위치 관리
호스트:
1. `pickSeat`에 해당하는 마이크 위치와 시청자 userId를 전달하면 마이크를 연결할 사용자를 지정할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.
2. `kickSeat`에 해당하는 마이크 위치를 전달하면 마이크 연결을 강제 해제할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.
3. `muteSeat`에 해당하는 마이크 위치를 전달하면 해당 마이크 위치를 음소거/음소거 해제할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onSeatMute` 이벤트 알림을 수신합니다.
4. `closeSeat`에 해당하는 마이크 위치를 전달하면 해당 마이크 위치를 차단/차단 해제할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onSeatClose` 이벤트 알림을 수신합니다.
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)

시청자:
1. `enterSeat`에 해당하는 마이크 위치를 전달하면 마이크를 연결할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.
2. `leaveSeat`로 직접 마이크 연결을 해제하면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

마이크 위치 작업 후의 이벤트 알림 순서는 다음과 같습니다.
callback > onSeatListChange > onAnchorEnterSeat 등 독립 이벤트

```Swift
// case1: 호스트가 1번 마이크 위치를 지정 연결
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 결과 콜백
}

// 3. onSeatListChange 콜백 수신, 마이크 위치 리스트 새로고침
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 새로고침된 마이크 위치 리스트
}

// 4. 단일 마이크 위치 변경 발생 시 알림, 여기에서 시청자가 실제로 마이크 연결에 성공했는지 여부 판단
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // 마이크 연결 이벤트 처리
}
```

```Swift
// case2: 시청자가 직접 2번 마이크 위치로 마이크 연결
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // 마이크 연결 결과 콜백
}

// 3. onSeatListChange 콜백 수신, 마이크 위치 리스트 새로고침
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 새로고침된 마이크 위치 리스트
}

// 4. 단일 마이크 위치 변경 발생 시 알림, 여기에서 사용자 자신인지 여부와 상응하는 프로세스 진행 여부 판단
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // 마이크 연결 이벤트 처리
}
```

<span id="model.step8"> </span>
### 단계8: 초대 신호 사용
[마이크 관리](#model.step7)에서 시청자의 마이크 연결 및 해제, 호스트의 마이크 연결 사용자 지정은 모두 상대방의 동의가 있어야만 직접 작업할 수 있습니다.
귀하의 App에 상대방이 동의해야만 다음 작업을 진행할 수 있는 서비스 프로세스를 설정하고 싶은 경우 초대 신호를 사용해 해당 서비스를 제공할 수 있습니다.
시청자 마이크 연결에 신청 프로세스가 필요한 경우:
1. 시청자 측에서 `sendInvitation`을 호출하여 호스트의 userId와 서비스 사용자 정의 명령어 등을 전달하며, 이때 함수는 inviteId를 반환하고 해당 inviteId를 기록합니다.
2. 호스트가 `onReceiveNewInvitation` 이벤트 알림을 수신하고, 이때 UI에 호스트의 동의 여부를 묻는 팝업창을 팝업할 수 있습니다.
3. 호스트가 동의를 선택하면 `acceptInvitation`을 호출하고 inviteId를 전달합니다.
4. 시청자 측에서 `onInviteeAccepted` 이벤트 알림을 수신하고 `enterSeat`를 호출하여 마이크를 연결합니다.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```Swift
// 시청자 측 앵글
// 1. sendInvitation을 호출하여 1번 마이크 위치 연결 요청
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 발송 결과 콜백
}
// 4. 초대 동의 요청을 수신하면 정식으로 마이크 연결
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // 마이크 연결 결과 콜백
        }
    }
}

// 호스트 측 앵글
// 2 호스트가 요청 수신
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 3. 호스트가 시청자 요청에 동의
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

호스트가 초대를 발송해야만 마이크를 연결할 시청자를 지정할 수 있는 경우:
1. 호스트 측에서 `sendInvitation`을 호출하여 시청자의 userId와 서비스 사용자 정의 명령어 등을 전달하며, 이때 함수는 inviteId를 반환하고 해당 inviteId를 기록합니다.
2. 시청자가 `onReceiveNewInvitation` 이벤트 알림을 수신하고, 이때 UI에 시청자의 동의 여부를 묻는 팝업창을 팝업할 수 있습니다.
3. 시청자가 동의를 선택하면 `acceptInvitation`을 호출하고 inviteId를 전달합니다.
4. 호스트 측에서 `onInviteeAccepted` 이벤트 알림을 수신하고 `pickSeat`를 호출하여 지정 사용자의 마이크를 연결합니다.

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

```java
// 호스트 측 앵글
// 1. 호스트가 sendInvitation을 호출하여 시청자 123를 2번 마이크에 연결하도록 요청
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // 발송 결과 콜백
}

// 4. 초대 동의 요청을 수신하면 정식으로 마이크 연결
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // 마이크 연결 결과 콜백
        }
    }
}

// 시청자 측 앵글
// 2. 시청자가 요청 수신
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 3. 시청자가 호스트 요청에 동의
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

<span id="model.step9"> </span>
### 9단계: 문자 채팅 및 댓글 자막 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
IM의 백그라운드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.

```Swift
// 발신 측: 텍스트 메시지 발송
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}
// 수신 측: 텍스트 메시지 리슨
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    //수신한 message 처리 방법        
}
```
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
 사용자 정의 메시지는 좋아요 메시지 발송 등과 같은 사용자 정의 신호 전송에 주로 사용됩니다.
 
```swift
// 예시: 발신 측: 사용자 정의 Cmd를 통해 댓글 자막과 좋아요 메시지를 구분할 수 있습니다.
// eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": 좋아요 메시지
self.vocieRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// 수신 측: 사용자 정의 메시지 리슨
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // 댓글 자막 메시지 수신
    }
    if cmd == "CMD_LIKE" {
        // 좋아요 메시지 수신
    }
}
```


