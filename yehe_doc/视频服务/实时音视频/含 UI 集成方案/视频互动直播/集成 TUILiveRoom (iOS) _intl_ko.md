## 컴포넌트 개요

TUILiveRoom은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 App이 ‘인터랙티브 비디오 라이브 스트리밍’ 시나리오를 추가할 수 있습니다. [Android](https://intl.cloud.tencent.com/document/product/647/36061) 및 [Flutter](https://intl.cloud.tencent.com/document/product/647/41944) 플랫폼도 지원합니다. 기본 기능은 다음과 같습니다.

<table>
<tr>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/34337da1f6427b9a834f6562eba5c663.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/52eb1656b5a892e6da65f49a1d503735.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/70c9e1e7290592f8c7892b236fb1061e.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/ed8c3666aa03951c6d0d9cfe2dccc495.jpg"/></td>
</tr>
</table>



## 컴포넌트 통합

### 1단계: TUILiveRoom 컴포넌트 다운로드 및 가져오기
xcode 프로젝트의 `Podfile`과 동일한 수준에 `TUILiveRoom` 폴더를 만들고 [GitHub 리포지토리의 iOS 디렉터리](https://github.com/One-time/TUILiveRoom/tree/main/iOS)에서 [TXAppBasic](https://github.com/One-time/TUILiveRoom/tree/main/iOS/TXAppBasic), [TCBeautyKit](https://github.com/One-time/TUILiveRoom/tree/main/iOS/TCBeautyKit), [Resources](https://github.com/One-time/TUILiveRoom/tree/main/iOS/Resources), [Source](https://github.com/One-time/TUILiveRoom/tree/main/iOS/Source) 및 [TUILiveRoom.podspec](https://github.com/One-time/TUILiveRoom/blob/main/iOS/TUILiveRoom.podspec) 파일을 폴더로 복사하고 다음 가져오기 작업을 완료합니다.
- 프로젝트의 Podfile을 열고 다음과 같이 TUILiveRoom.podspec을 가져옵니다.
```
# :path => "TXAppBasic.podspec 디렉터리의 상대 경로를 가리킵니다."
pod 'TXAppBasic', :path => "TUILiveRoom/TXAppBasic/"

# :path => "TCBeautyKit.podspec 디렉터리의 상대 경로를 가리킵니다."
pod 'TCBeautyKit', :path => "TUILiveRoom/TCBeautyKit/"

# :path => "TUILiveRoom.podspec 디렉터리의 상대 경로를 가리킵니다."
pod 'TUILiveRoom', :path => "TUILiveRoom/", :subspecs => ["TRTC"]
```
- 터미널을 열고 Podfile 디렉터리로 들어가 `pod install`을 실행합니다.
```
pod install
```

### 2단계: 권한 요청 및 난독화 규칙 구성
info.plist 파일에 `Privacy > Microphone Usage Description`(마이크 접근 요청)과 `Privacy > Camera Usage Description`(카메라 접근 요청)을 순서대로 추가하십시오.

```plist
<key>NSMicrophoneUsageDescription</key>
<string>LiveRoom은 오디오가 포함된 비디오를 촬영하려면 마이크에 액세스해야 합니다.</string>
<key>NSCameraUsageDescription</key>
<string>LiveRoom은 이미지가 포함된 비디오를 촬영하려면 카메라에 액세스해야 합니다.</string>
```

### 3단계: 컴포넌트 초기화 및 로그인
```Swift
 let mTRTCLiveRoom = TRTCLiveRoom()
 //useCDNFirst: true는 일반 시청자의 CDN을 통한 시청을, false는 일반 시청자의 저지연 시청을 의미
 //CDNPlayDomain: CDN 라이브 스트리밍을 위한 재생 도메인 이름
 let config = TRTCLiveRoomConfig(useCDNFirst: useCDNFirst, cdnPlayDomain: yourCDNPlayDomain)
 mTRTCLiveRoom.login(SDKAPPID, userID, userSig, config) { (code, error) in
   if code == 0 {
     //로그인 성공
   }
}
```
**매개변수 설명:**
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 현재 사용자의 ID로, 문자(a-z 및 A-Z), 숫자(0-9), 하이픈(-) 및 언더바(\_)만 포함할 수 있는 문자열입니다. 사용자 계정 시스템과 일관성을 유지하는 것이 좋습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [데모 프로젝트](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.

### 4단계: 인터랙티브 비디오 라이브 룸 구현
1. **앵커가 [TRTCLiveRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37332)을 통해 스트리밍을 시작합니다.**
```Swift
// 1. 사용자 이름과 프로필 사진을 앵커로 설정
 mTRTCLiveRoom.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

 // 2. 스트리밍 전에 카메라 미리보기를 활성화하고 뷰티 필터를 설정
 let view = UIView()
 parentView.add(view)
 mTRTCLiveRoom.startCameraPreview(frontCamera: true, view: view, callback: nil)
 mTRTCLiveRoom.getBeautyManager().setBeautyStyle(.nature)
 mTRTCLiveRoom.getBeautyManager().setBeautyLevel(6)

 // 3. 방 생성
 let param = TRTCCreateRoomParam(roomName: "테스트 룸", coverUrl: "")
 mTRTCLiveRoom.createRoom(roomID: 123456789, roomParam: param) { [weak self] (code, error) in
  if code == 0 {
    // 4. 스트리밍을 시작하고 스트림을 CDN에 게시
    self?.mTRTCLiveRoom.startPublish(streamID: mSelfUserId + "_stream", callback: nil)
  }
}
```
2. **시청자는 [TRTCLiveRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37332)을 통해 시청합니다.**
```Swift
// 1. 백엔드에서 방 목록을 가져옵니다. 이를 roomList라고 가정함.
 var roomList: [UInt32] = GetRoomList()

 // 2. getRoomInfos를 호출하여 방의 세부 정보 가져오기
 mTRTCLiveRoom.getRoomInfos(roomIDs: roomList, callback: { (code, msg, list) in
    if code == 0 {
      // 방 정보를 얻은 후 앵커 목록 페이지에 앵커의 닉네임, 프로필 사진 및 기타 정보 표시
    }
 })

 // 3. roomid를 선택하고 방에 입장
 mTRTCLiveRoom.enterRoom(roomID: roomID, callback: callback)

 // 4. 앵커 진입 알림 수신 후 재생 시작
 public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
   // 5. 앵커의 동영상 재생
   mTRTCLiveRoom.startPlay(userID: userID, view: renderView, callback: nil) 
 }
```
3. **[TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37332)를 통해 관객과 앵커가 함께 공동 앵커링합니다.**
```Swift
// 시청자 측:
  // 1. 시청자가 공동 앵커링 요청 발송
  mTRTCLiveRoom.requestJoinAnchor(reason: mSelfUserId + "공동 앵커 요청", responseCallback: { [weak self] (agreed, reason) in 
      // 4. 앵커가 요청 수락
       if agreed {
        // 5. 시청자가 카메라를 켜고 스트림 푸시 시작
        self?.mTRTCLiveRoom.startCameraPreview(frontCamera: true, view: localView, callback: nil)
        self?.mTRTCLiveRoom.startPublish(streamID: streamID, callback: nil)
       }        
  }, callback: callback)

  // 앵커측:
  // 2. 앵커가 공동 앵커 요청을 수신
  public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double) {
    // 3. 앵커가 공동 앵커 요청을 수락
    mTRTCLiveRoom.responseJoinAnchor(userID: userID, agree: true, reason: "공동앵커로 합의")
  }

  // 6. 앵커는 공동 앵커 관객이 마이크를 켰다는 알림 수신
  public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
    // 7. 앵커가 청중의 비디오 재생
    mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: nil)
  }
```
4. **앵커는 [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37332)를 통해 PK합니다.**
```Swift
// 앵커 A:
// 12345번 방 생성
mTRTCLiveRoom.createRoom(roomID: 12345, roomParam: param, callback: nil)

// 1. 앵커 B에 PK 요청 보내기
mTRTCLiveRoom.requestRoomPK(roomID: 54321, userID: "B", responseCallback: { (agree, reason) in
  // 5. 앵커 B가 요청을 수락했는지 여부에 대한 콜백 수신
  if agree {
  }       
}, callback: callback)

// 앵커 A는 앵커 B의 항목에 대한 콜백 수신
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
  // 6. 앵커 B 진입 알림을 받은 앵커 A는 앵커 B의 비디오 재생
  mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}

// 앵커 B:
// 54321 방 생성
mTRTCLiveRoom.createRoom(roomID: 54321, roomParam: param, callback: nil)

// 2. 앵커 A의 요청 수신
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) {
  // 3. 앵커 A의 요청 수락
  mTRTCLiveRoom.responseRoomPK(userID: userID, agree: true, reason: reason)
}

public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
  // 4. 앵커 A 진입 알림 수신 및 앵커 A 비디오 재생
  mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}
```
5. **[TRTCLiveRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37332)를 통해 문자 채팅을 구현합니다.**
```Swift
// 발신측: 텍스트 메시지 발송
mTRTCLiveRoom.sendRoomTextMsg(message: "Hello Word!", callback: callback)
// 수신측: 텍스트 메시지 수신
mTRTCLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo) {
  debugPrint("\(user.userName)님이 발송한 텍스트 메시지:\(message)")
}
```
6. **[TRTCLiveRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37332)를 통해 화면 댓글을 구현합니다.**
```Swift
// 발신 측: 사용자 정의 Cmd를 통해 댓글 자막과 '좋아요' 메시지 구분 가능
// eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": '좋아요' 메시지
mTRTCLiveRoom.sendRoomCustomMsg(command: "CMD_DANMU", message: "Hello world", callback: nil)
mTRTCLiveRoom.sendRoomCustomMsg(command: "CMD_LIKE", message: "", callback: nil)
// 수신측: 사용자 정의 메시지 수신
mTRTCLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo) {
  if "CMD_DANMU" == command {
    // 댓글 자막 메시지 수신
    debugPrint("\(user.userName)님이 발송한 댓글 자막 메시지:\(message)")
  } else if "CMD_LIKE" == command {
    // '좋아요' 메시지 수신
    debugPrint("\(user.userName)님이 좋아합니다.")
  }
}
```


## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 문의하십시오.
