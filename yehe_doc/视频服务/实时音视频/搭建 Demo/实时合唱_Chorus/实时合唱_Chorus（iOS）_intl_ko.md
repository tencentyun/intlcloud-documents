## 효과
Tencent Cloud의 App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 2인 초저지연 합창, 선물하기, 문자 채팅 등 TRTC의 Chorus 기능을 사용해 볼 수 있습니다. 
<table>
     <tr>
         <th style="text-align:center">방 주인의 마이크 위치 작업</th>  
         <th style="text-align:center">청취자의 마이크 위치 작업</th>  
     </tr>
<tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
</tr>
</table>


빠른 Chorus 액세스 기능이 필요한 경우, Tencent Cloud에서 제공하는 App를 기반으로 설정을 적합하게 수정하거나 TUIChorus 컴포넌트을 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
[](id:DemoUI)
## App UI 인터페이스 재사용
[](id:ui.step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, **개발 지원**>**[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. 애플리케이션 이름, 예시 `TestChorus` 를 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?본 기능은 기본 PAAS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.


[](id:ui.step2)
### 2단계: App 소스 코드 다운로드
[TUIChorus](https://github.com/tencentyun/TUIChorus)를 클릭하여 이동하거나, 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:ui.step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `TUIChorus/Debug/GenerateTestUserSig.swift` 파일을 찾아 엽니다.
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
Xcode(11.0 및 이후 버전)를 사용하여 소스 코드 프로젝트 `TUIChorus/TUIChorusApp.xcworkspace`를 열고 **실행**을 클릭하면 즉시 해당 App이 디버깅됩니다.

[](id:ui.step5)
### 5단계: App 소스 코드 수정
소스 코드의 `Source` 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 관련 코드 및 로직입니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| TRTCChorusEnteryControl.swift|이 파일에는 모든 ViewController를 초기화하는 방법이 포함되어 있습니다. 해당 인스턴스를 통해 신속하게 ViewController 객체를 획득할 수 있습니다.|
| TRTCCreateChorusViewController | Chorus 페이지 로직 생성. |
| TRTCChorusViewController       | 방 주인과 시청자의 인터페이스를 포함하는 메인 방 페이지. |

모든 `TRTC'XXXX'ViewController` 폴더에는 `ViewController`, `RootView`, `ViewModel`이 포함되어 있으며, 각 파일의 역할은 다음과 같습니다.

| 파일 | 기능 설명 |
|:-------:|:--------|
| ViewController.swift | 페이지 컨트롤러. 페이지 라우팅 작업, RootView 및 ViewModel의 바인딩 작업을 담당합니다. |
| RootView.swift | 뷰. 모든 뷰 레이아웃. |
| ViewModel.swift | 뷰 컨트롤러. 뷰 인터랙티브에 응답하며, 뷰 응답 상태를 반환합니다. |

## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.
### 사용자 A

1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. **방 생성**을 클릭합니다.
2. 방 주제를 입력하고, **같이 노래하기**를 클릭합니다.

### 사용자 B
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 사용자 A가 생성한 방 번호를 입력한 후 **방 입장**을 클릭합니다.<br>

>! 방 번호는 사용자 A의 방 상단에서 확인할 수 있습니다.

[](id:model)
## 사용자 정의 UI 인터페이스 구현
[소스 코드](https://github.com/tencentyun/TUIChorus)의 `Source` 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TRTCChorusRoom이 포함되어 있습니다. `TRTCChorusRoom.h` 파일에서 해당 컴포넌트가 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png">

[](id:model.step1)
### 1단계: SDK 통합
Chorus 컴포넌트인 TRTCChorusRoom은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 두 개의 SDK를 프로젝트에 통합할 수 있습니다.

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
info.plist 파일에 `Privacy > Microphone Usage Description`을 추가해 마이크 권한을 신청해야 합니다.

[](id:model.step3)
### 3단계: TUIChorus 컴포넌트 가져오기
**cocoapods를 통해 컴포넌트 가져오기**의 구체적인 작업은 다음과 같습니다.
1. 프로젝트 디렉터리의 `Source`, `Resources`, `TXAppBasic` 폴더 및 `TUIChorus.podspec` 파일을 프로젝트 디렉터리에 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod ’TXLiteAVSDK_TRTC’
pod 'TUIChorus', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)

### 4단계: 컴포넌트 생성 및 로그인
1. TRTCChorusRoom의 `sharedInstance`와 같은 메소드로 TRTCChorusRoom 프로토콜을 준수하는 인스턴스 객체를 생성할 수 있고, `shared`와 같은 메소드 호출로 TRTCChorusRoom 인스턴스 객체를 불러와 직접 사용할 수도 있습니다. 두 메소드는 TRTCChorusRoom 인터페이스를 사용하는 데에 있어 아무런 차이가 없습니다.
2. `setDelegate` 함수를 호출하여 컴포넌트의 이벤트 콜백 알림을 등록합니다.
3. `login` 함수를 호출해 컴포넌트에 로그인하고, 다음 표를 참조해 핵심 매개변수를 입력합니다.
<table>    
<tr><th>매개변수 이름</th><th>역할</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다. 사업체의 실제 계정 시스템에 맞게 설정할 것을 권장합니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
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
    var chorusRoom: TRTCChorusRoom {
        return TRTCChorusRoom.shared()
    }
    
    // 기타 코드 로직
    ......
}
// Chorus 프록시 설정
self.chorusRoom.setDelegate(delegate: chorusRoomDelegate)

// 호출 방법은 다음과 같습니다. 클로저 내에서 weak self를 사용해 순환 참고를 방지하시기 바랍니다. 다음은 weak self를 생략한 예시 코드입니다.
self.chorusRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // 콜백 서비스 로직        
}
:::
</dx-codeblock>

[](id:model.step5)
### 5단계: 방 주인 방 생성
1. 방 주인은 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 방 주인이 `createRoom`을 호출하여 새로운 Chorus 방을 생성합니다. 이 때, 방 ID, 마이크 연결 시 방 주인 확인 필요 여부 등 방 속성 정보를 전송합니다.
3. 방 주인이 방 생성 후 자동으로 `enterSeat`을 호출하여 메인 보컬 1번 자리에 입장합니다.
4. 방 주인이 컴포넌트의 `onSeatListChange` 마이크 위치 리스트 변경 이벤트 알림을 수신합니다. 이때 마이크 위치 리스트의 변경 내용을 UI 인터페이스에 새로고침할 수 있습니다.
5. 방 주인은 마이크 위치 리스트에 사용자가 입장할 때 `onAnchorEnterSeat` 이벤트 알림 또한 수신하며, 이 때 자동으로 마이크 수집이 활성화됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/7346adee3042426ca4c9f72777cebd2d.png)

예시 코드:
<dx-codeblock>
::: swift
// 1. 방 주인 닉네임 및 프로필 사진 설정
self.chorusRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 결과 콜백           
}

// 2. 방 주인 방 생성
let param = RoomParam.init()
param.roomName = "방 이름"
param.needRequest = true // 청취자가 마이크를 켤 때 방 주인 동의 필요 여부
param.coverUrl = "썸네일 URL"
param.seatCount = 2 // 방의 자리 수. 예시에서는 메인 보컬과 서브 보컬 총 2개 설정.
param.seatInfoList = []

for _ in 0..< param.seatCount {
    let seatInfo = SeatInfo.init()
    param.seatInfoList.append(seatInfo)
}

self.chorusRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // 생성 성공
    
    // 3. 마이크 켜기
    self.chorusRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 방 주인 자리 점유 성공
        } else {
            // 방 주인 자리 점유 실패
        }
    }
} 

// 4. 마이크 켜짐 후 onSeatListChange 이벤트 알림 수신
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // 마이크 위치 리스트 새로고침
}

// 5. onAnchorEnterSeat 이벤트 알림 수신
func onAnchorEnterSeat(index: Int, user: UserInfo) {
  // 방 주인 마이크 연결 이벤트 처리
}

:::
</dx-codeblock>

[](id:model.step6)
### 6단계: 청취자 시청
1. 청취자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 청취자는 서비스 백엔드로부터 최신 Chorus 방 목록을 가져옵니다.
>?App에 있는 Chorus 방 리스트는 참고용입니다. Chorus 방 리스트의 서비스 로직은 매우 다양하며 현재 Tencent Cloud는 Chorus 방 리스트 관리 서비스를 제공하지 않습니다. Chorus 방 리스트는 직접 관리하시기 바랍니다.
3. 청취자가 `getRoomInfoList`를 호출해 방 세부 정보를 가져옵니다. 해당 정보는 방 주인이 `createRoom`을 호출해 Chorus 방 생성 시 설정한 간단한 설명 정보입니다.
>!Chorus 방 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomInfoList` 호출 관련 단계는 건너뛸 수 있습니다.
4. 청취자가 하나의 Chorus 방을 선택하고 `enterRoom`을 호출하여 방 번호를 전송하면 즉시 해당 방에 입장할 수 있습니다.
5. 방 입장 후 컴포넌트의 `onRoomInfoChange` 방 속성 변경 이벤트 알림을 수신합니다. 이 때 UI에 방 이름 표시, 마이크를 켤 때 방 주인에게 동의 요청 필요 여부 기록 등 방의 속성을 기록할 수 있으며 그에 해당하는 변경이 가능합니다.
6. 방 입장 후 컴포넌트의 `onSeatListChange` 마이크 위치 리스트 변경 이벤트 알림을 수신합니다. 이때 마이크 위치 리스트의 변경 내용을 UI 인터페이스에 새로고침할 수 있습니다.
7. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterSeat` 이벤트 알림도 수신합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/f225633062cf83d749ae8137cbb26fe1.png)
<dx-codeblock>
::: Swift Swift
// 1. 청취자 닉네임 및 프로필 사진 설정
self.chorusRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 결과 콜백           
}

// 2. 서비스 백엔드로부터 획득하는 방 리스트가 roomList라고 가정할 경우
let roomList: [Int] = getRoomIDList() // 방 ID 리스트 함수 획득

// 3. getRoomInfoList 호출을 통해 방 세부 정보 획득
self.chorusRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [RoomInfo]) in
    // 결과 획득, UI 새로고침 가능
}

// 4. Chorus 선택 후 roomId를 전송하여 방 입장
self.chorusRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 방 입장 결과 콜백
    if code == 0 {
       // 방 입장 성공
    }
}

// 5. 방 입장 완료 후 onRoomInfoChange 이벤트 알림 수신
func onRoomInfoChange(roomInfo: RoomInfo) {
    // 방 이름 등 정보 새로고침 가능
}

// 6. 방 입장 완료 후 onSeatListChange 이벤트 알림 수신
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // 마이크 위치 리스트 새로 고침
}

// 7. onAnchorEnterSeat 이벤트 알림 수신
func onAnchorEnterSeat(index: Int, user: UserInfo) {
    // 마이크 켜기 이벤트 처리
}
:::
</dx-codeblock>

[](id:model.step7)
### 7단계: 마이크 위치 관리
<dx-tabs>
::: 방 주인
1. `pickSeat`로 해당 마이크 위치와 청취자 userId를 전송하면 마이크를 연결할 사용자를 지정할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.
2. `kickSeat`로 해당 마이크 위치를 전송하면 합창이 끝난 후 마이크 연결을 강제 해제할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.
3. `closeSeat`로 해당 마이크 위치를 전송하면 해당 마이크 위치를 차단/해제할 수 있으며, 차단된 청취자는 마이크를 연결할 수 없습니다. 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onSeatClose` 이벤트 알림을 수신합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bbb72bdc50cfd1b5d4b567239b035d32.png)
:::
::: 청취자
1. `enterSeat`로 해당 마이크 위치를 전송하면 마이크를 연결할 수 있으며, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.
2. `leaveSeat` 합창 종료 후 시청자는 마이크 끄기를 신청할 수 있으며, 직접 마이크 연결을 해제하면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/9747219d17f955530c5e502745008dce.png)

마이크 위치 작업 후의 이벤트 공지 순서는 다음과 같습니다: callback > onSeatListChange > onAnchorEnterSeat 등 독립 이벤트.

<dx-codeblock>
::: swift
// case1: 방 주인이 1번 마이크 자리에 사용자 배치
self.chorusRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 결과 콜백
}

// 3. onSeatListChange 콜백 수신, 마이크 위치 리스트 새로고침
func onSeatListChange(seatInfoList: [ChorusRoomSeatInfo]) {
    // 새로 고친 마이크 위치 리스트
}

// 4. 청취자 마이크 연결의 실제 성공 여부를 판단할 수 있는 단일 마이크 위치 변경 알림
func onAnchorEnterSeat(index: Int, user: ChorusRoomSeatInfo) {
    // 마이크 켜기 이벤트 처리
}
:::
</dx-codeblock>

<dx-codeblock>
::: swift
// case2: 청취자가 직접 보조 마이크 자리 사용
chorusRoom.enterSeat(seatIndex: 1) { (code, message) in
    // 마이크 켜기 결과 콜백
}

// 3. onSeatListChange 콜백 수신, 마이크 위치 리스트 새로고침
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // 새로 고친 마이크 위치 리스트
}

// 4. 사용자 본인 여부와 해당하는 프로세스 진행 여부를 판단할 수 있는 단일 마이크 위치 변경 알림
func onAnchorEnterSeat(index: Int, user: UserInfo) {
    // 마이크 켜기 이벤트 처리
}
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:model.step8)
### 8단계: 초대 신호 사용
[마이크 위치 관리](#model.step7)에서 청취자의 마이크 연결 및 해제, 방 주인의 마이크 연결 사용자 지정은 상대방의 동의가 없어도 작업할 수 있습니다.
사용자 App이 상대방이 동의해야 다음 단계의 작업을 진행할 수 있는 비즈니스 프로세스인 경우, 초대 신호는 해당하는 지원을 제공할 수 있습니다.
<dx-tabs>
::: 청취자가 직접 마이크 켜기 신청
1. 청취자가 `sendInvitation`을 호출해 방 주인의 userId와 서비스 사용자 정의 명령어 등을 전송합니다. 이 때 함수는 inviteId를 반환하고 해당 inviteId를 기록합니다.
2. 방 주인이 `onReceiveNewInvitation` 이벤트 알림을 수신합니다. 이 때 UI에 방 주인의 동의 여부를 묻는 팝업 창을 띄울 수 있습니다.
3. 방 주인이 동의를 선택한 후 `acceptInvitation`을 호출하고 inviteId를 전송합니다.
4. 청취자가 `onInviteeAccepted` 이벤트 알림을 수신하고 `enterSeat`를 호출해 마이크를 켭니다.

![](https://qcloudimg.tencent-cloud.cn/raw/1b37fa84f59c81dc89bf50ce4e30551f.png)

<dx-codeblock>
::: Swift Swift
// 청취자 앵글
// 1. sendInvitation을 호출하여 1번 마이크 위치 연결 요청
let inviteId = self.chorusRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 발송 결과 콜백
}
// 2. 초대 동의 요청을 수신하면 정식으로 마이크 켜짐
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chorusRoom.enterSeat(seatIndex: ) { (code, message) in
            // 마이크 켜기 결과 콜백
        }
    }
}

// 방 주인 앵글
// 1. 방 주인이 요청을 수신함
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. 방 주인이 청취자 요청에 동의
        self.chorusRoom.acceptInvitation(identifier: identifier, callback: nil)
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

![](https://qcloudimg.tencent-cloud.cn/raw/3a8b31dac680c70d1adac92287e645dd.png)


<dx-codeblock>
::: Swift Swift
// 방 주인 앵글
// 1. 방 주인이 sendInvitation을 호출해 청취자에게 '123' 서브 보컬 마이크 자리 사용 요청
let inviteId = self.chorusRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 발송 결과 콜백
}

// 2. 초대 동의 요청을 수신하면 정식으로 마이크 켜짐
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chorusRoom.pickSeat(seatIndex: ) { (code, message) in
            // 마이크 켜기 결과 콜백
        }
    }
}

// 청취자 앵글
// 1. 청취자가 요청을 수신함
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. 청취자의 방 주인 요청 수락
        self.chorusRoom.acceptInvitation(identifier: identifier, callback: nil)
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
  self.chorusRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// 수신측: 텍스트 메시지 수신
func onRecvRoomTextMsg(message: String, userInfo: UserInfo) {
    //수신한 message 정보 처리 방법        
}
:::
</dx-codeblock>
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며 해당 방에 있는 서브 보컬과 시청자 모두가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
 사용자 정의 메시지는 '좋아요' 메시지 발송과 같은 사용자 정의 신호 전송에 주로 사용됩니다.
  <dx-codeblock>
  ::: Swift Swift
  // 예시: 발신측: 사용자 정의 Cmd를 통해 댓글 자막과 '좋아요' 메시지 구분 가능
  // eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": '좋아요' 메시지
  self.chorusRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
  self.chorusRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
  // 수신측: 사용자 정의 메시지 수신
  func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: UserInfo) {
    if cmd == "CMD_DANMU" {
        // 댓글 자막 메시지 수신
    }
    if cmd == "CMD_LIKE" {
        // '좋아요' 메시지 수신
    }
  }
  :::
  </dx-codeblock>

