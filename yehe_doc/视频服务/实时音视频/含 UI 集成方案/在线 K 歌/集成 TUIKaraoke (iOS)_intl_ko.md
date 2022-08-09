## 컴포넌트 개요

TUIKaraoke는 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합하고 몇 줄의 코드 작성만으로 애플리케이션에 온라인 노래방 시나리오를 추가하고 노래방, 좌석 관리, 선물 주고받기, 문자 채팅과 같은 TRTC 기능을 체험해 볼 수 있습니다. Android 플랫폼도 지원합니다. 기본 기능은 다음과 같습니다.

>?TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 내역은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/c17771587a0803db28047796fcd0df11.png)

## 컴포넌트 통합
### 1단계: TUIKaraoke 컴포넌트 다운로드 및 가져오기

[Github](https://github.com/tencentyun/TUIKaraoke)로 이동하여 코드를 복제하거나 다운로드하고 iOS 디렉터리의 `Source`, `Resources` 및 `TXAppBasic` 폴더와 `TUIKaraoke.podspec` 파일을 프로젝트에 복사하여 다음 가져오기 작업을 완료합니다.

- `Podfile`에 다음 가져오기 명령을 추가합니다.
```
pod 'TUIKaraoke', :path => "./", :subspecs => ["TRTC"]
pod ’TXLiteAVSDK_TRTC’
pod 'TXAppBasic', :path => "TXAppBasic/"
```
- 터미널을 열고 `Podfile` 디렉터리에서 다음 설치 명령을 실행합니다.
```
pod install
```

### 2단계: 권한 설정
프로젝트의 info.plist 파일에서 App에 대한 권한 요청을 구성합니다. SDK에는 다음 권한이 필요합니다(iOS에서는 런타임 시 마이크 액세스를 요청해야 함).
```
 <key>NSMicrophoneUsageDescription</key>
    <string>Karaoke는 마이크에 액세스 필요</string>
```


### 3단계: 컴포넌트 초기화 및 로그인
관련 API에 대한 자세한 내용은 [TRTCKaraoke(iOS)](https://intl.cloud.tencent.com/document/product/647/41942)를 참고하십시오.
```swift
  // 1. 초기화
  let karaokeRoom = TRTCKaraokeRoom.shared()
  karaokeRoom.setDelegate(delegate: self)
  // 2. 로그인
  karaokeRoom.login(SDKAppID: Int32(SDKAppID), UserId: UserId, UserSig: ProfileManager.shared.curUserSig()) { code, message in
		if code == 0 {
			//로그인 성공
		}
  }
```
**매개변수 설명**:
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 문자열이며 최대 32바이트의 문자와 숫자를 포함할 수 있는 현재 사용자 ID입니다(특수 기호는 지원되지 않음). 실제 계정 시스템에 따라 사용자 정의할 수 있습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 UserSig를 온라인으로 직접 생성하거나 [TUIKaraoke 데모 프로젝트](https://github.com/tencentyun/TUICalling/blob/main/Android/App/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://cloud.tencent.com/document/product/647/17275)를 참고하십시오.


### 4단계: 온라인 노래방 시나리오 구현
1. **앵커는 [TUIKaraoke.createRoom](https://intl.cloud.tencent.com/document/product/647/41942)을 통해 방을 생성합니다.**
```swift
int roomId = "방 ID";
let param = RoomParam.init()
param.roomName = "방 이름";
param.needRequest = false; // 마이크 연결 시 방 주인 확인 필요 여부
param.seatCount = 8;       // 방의 좌석 수. 8개로 설정
param.coverUrl = "방 커버 이미지의 URL";

karaokeRoom.createRoom(roomID: Int32(roomInfo.roomID), roomParam: param) { [weak self] (code, message) in
	guard let `self` = self else { return }
	if code == 0 {
        //방 생성 성공
	}
}
```
2. **청취자는 [TUIKaraoke.enterRoom](https://intl.cloud.tencent.com/document/product/647/41942)을 통해 방에 들어갑니다**.
```swift
karaokeRoom.enterRoom(roomID: roomInfo.roomID) { [weak self] (code, message) in
	guard let `self` = self else { return }
	if code == 0 {
		//방 들어가기 성공
	}
}
```
3. **청취자는 [TUIKaraoke.enterSeat](https://intl.cloud.tencent.com/document/product/647/41942)를 통해 마이크를 켭니다**.
```swift
// 1. 청취자가 마이크를 켜기 위해 API 호출
int seatIndex = 1; 
karaokeRoom.enterSeat(seatIndex: seatIndex) { [weak self] (code, message) in
	guard let `self` = self else { return }
	if code == 0 {
		//마이크 활성화 성공
	}
}
// 2. 청취자는 onSeatListChange 콜백을 수신하고 좌석 목록을 새로고침함
func onSeatListChange(seatInfoList: [SeatInfo]) {
}
```

>? [TRTCKaraoke(iOS)](https://intl.cloud.tencent.com/document/product/647/41942) 또는 [TUIKaraoke 데모 프로젝트](https://github.com/tencentyun/TUIKaraoke/)를 참고하여 다른 좌석 관리 작업을 구현할 수 있습니다.

4. **노래를 재생하고 노래방 시나리오를 체험합니다**
음악 ID와 URL을 가져와 비즈니스에 따라 노래를 재생할 수 있습니다. 자세한 내용은 [TUIKaraoke 음악 재생 인터페이스](https://intl.cloud.tencent.com/document/product/647/41942#.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E6.8E.A5.E5.8F.A32)를 참고하십시오.
```swift
//음악 재생
karaokeRoom.startPlayMusic(musicID: musicID, originalUrl: muscicLocalPath, accompanyUrl: accompanyLocalPath);
//음악 중지
karaokeRoom.stopPlayMusic();
```

이전 단계를 완료한 후 기본 노래방 기능을 구현할 수 있습니다. 비즈니스에 채팅 및 선물 제공과 같은 더 많은 기능이 필요한 경우 다음 기능을 통합할 수 있습니다.

### 6단계: 문자 채팅 기능 추가(옵션)
앵커와 청취자 간의 텍스트 채팅 기능을 원하시면 다음과 같이 메시지 송수신을 구현하십시오.
관련 API에 대한 자세한 내용은 [TRTCKaraokeRoom.sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/41942#sendroomtextmsg)를 참고하십시오.
```swift
// 발신측: 텍스트 메시지 발송
karaokeRoom.sendRoomTextMsg(message: message) { [weak self] (code, message) in
	if code == 0 {
		//전송 성공
	}
}
// 수신측: 텍스트 메시지 수신
karaokeRoom.setDelegate(delegate: self)
func onRecvRoomTextMsg(message: String, userInfo: UserInfo) {
	debugPrint(userInfo.userName + "님이 발송한 메시지:" + message)
}
```

### 7단계: 선물하기 기능 추가(옵션)
선물 주고받기, 표시하기를 다음과 같이 구현할 수 있습니다.
```swift
// 발신측: "IMCMD_GIFT"를 사용자 지정하여 선물 메시지를 구분합니다.
karaokeRoom.sendRoomCustomMsg(cmd: kSendGiftCmd, message: message) { code, msg in
	if (code == 0) {
		//전송 성공
	}
}

// 수신측: 선물 메시지 수신
karaokeRoom.setDelegate(delegate: self)
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: UserInfo) {
	if cmd == kSendGiftCmd {
		debugPrint(userInfo.userName + "님이 보낸" + "선물을 받았습니다." + message)
	}
}
```

## FAQ

### TUIKaraoke 컴포넌트는 음성 변경, 톤 변경 및 리버브와 같은 음향 효과 기능을 지원합니까?
지원합니다. 자세한 내용은 [TUIKaraoke 데모 프로젝트](https://github.com/tencentyun/TUIKaraoke/blob/main/iOS/Source/ui/TRTCKTVViewController/SubViews/TRTCKaraokeSoundEffectAlert.swift)를 참고하십시오.

? 요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의하십시오.
