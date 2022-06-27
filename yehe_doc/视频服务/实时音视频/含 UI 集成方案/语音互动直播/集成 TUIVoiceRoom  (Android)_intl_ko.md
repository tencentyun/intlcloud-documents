## 컴포넌트 개요

TUIVoiceRoom은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 App에서 ‘그룹 오디오 채팅’ 시나리오를 지원하도록 할 수 있습니다. [iOS](https://intl.cloud.tencent.com/document/product/647/37287) 플랫폼도 지원합니다. 기본 기능은 다음과 같습니다.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/064229b8d27147985311825f21dd27c2.png"></td>
</tr>
</tbody></table>


## 컴포넌트 통합

### 1단계: TUIVoiceRoom 컴포넌트 다운로드 및 가져오기
[Github](https://github.com/tencentyun/TUIVoiceRoom)로 이동하여 코드를 복제하거나 다운로드하고 Android/Source 디렉터리를 프로젝트에 복사하고 다음 가져오기 작업을 완료합니다.
- 아래와 같이 `setting.gradle`에서 가져오기를 완료합니다.
```
include ':Source'
```
- app의 build.gradle 파일에 Source에 대한 종속성을 추가합니다.
```
api project(':Source')
```
- 루트 디렉터리의 `build.gradle` 파일에 `TRTC SDK` 및 `IM SDK`에 대한 종속성을 추가합니다.
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### 2단계: 권한 요청 및 난독화 규칙 구성
AndroidManifest.xml에서 App 권한을 설정합니다. SDK에는 다음 권한이 필요합니다(Android 6.0 이상에서는 런타임 시 마이크 액세스를 요청해야 함).

```
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

proguard-rules.pro 파일에서 SDK 관련 유형을 비난독화 리스트에 추가합니다.

```
-keep class com.tencent.** { *; }
```

### 3단계: 컴포넌트 초기화 및 로그인
```java
    // 1. 초기화，
    TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
    mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    );
		  // 2. 로그인，
    mTRTCVoiceRoom.login(SDKAppID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            //로그인 성공
            }
        }
    });
```

**매개변수 설명:**
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 현재 사용자의 ID로, 문자(a-z 및 A-Z), 숫자(0-9), 하이픈(-) 및 언더바(\_)만 포함할 수 있는 문자열입니다. 사용자 계정 시스템과 일관성을 유지하는 것이 좋습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [데모 프로젝트](https://github.com/tencentyun/TUIVoiceRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.

### 4단계: 음성 채팅방 구현
1. **방 주인은 [TRTCVoiceRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37339)을 통해 음성 대화방 생성**
```java
// 1.방주인은 API를 호출하여 방 생성
int roomId = 12345; //방 id
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "방 이름";
roomParam.needRequest = false; // 마이크 연결 시 방주인 확인 필요 여부
roomParam.seatCount = 7; // 방의 자리 수, 총 7개로 설정하고 방주인이 한 개를 점유한 후 시청자가 남은 6개 자리 점유
roomParam.coverUrl = "방 표지 이미지의 URL";
mTRTCVoiceRoom.createRoom(roomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
				//생성 성공
        }
    }
});
```
2. **청취자는 [TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37339)을 통해 오디오 대화방에 입장**
```java
// 1.청취자가 API를 호출하여 방에 입장
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            //방 들어가기
            }
        }
});
```
3. **청취자는 [TRTCVoiceRoom#enterSeat](https://intl.cloud.tencent.com/document/product/647/37339)를 통해 마이크 켬**
```java
// 1: 청취자가 마이크를 켜기 위해 API 호출
int seatIndex = 2; // 좌석 index
mTRTCVoiceRoom.enterSeat(seatIndex, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        //작업 완료
        }
    }
});

// 2.onSeatListChange 콜백 수신, 마이크 위치 리스트 새로고침
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}
```
4. **방 주인이 [TRTCVoiceRoom#pickSeat](https://intl.cloud.tencent.com/document/product/647/37339)를 통해 청취자 마이크 활성화**
```java
// 1: 방 주인이 청취자를 초대
int seatIndex = 2; //좌석 index
String userId = "123"; //발언할 사용자의 id
mTRTCVoiceRoom.pickSeat(1, userId, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
				//작업 완료
        }
    }
});

// 2.onSeatListChange 콜백 수신, 마이크 위치 리스트 새로고침
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}
```
5. **청취자는 [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/37339)을 통해 발언 요청**
```java
// 청취자 앵글
// 1.청취자가 API를 호출하여 말하기 요청
String seatIndex = "1"; //좌석 index
String userId = "123"; //사용자 id
String inviteId = mTRTCVoiceRoom.sendInvitation("takeSeat", userId, seatIndex, null);

// 2.초대가 수락된 후 사용자를 자리에 앉힘
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(index, null);
    }
}

// 방 주인 앵글
// 1.방 주인이 요청을 수신함
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("takeSeat")) {
        // 2.방 주인이 청취자 요청에 동의
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
6. **방 주인은 [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/37339)을 통해 청취자 초대**
```java
// 방 주인 앵글
// 1.방 주인은 API를 호출하여 청취자에게 발언 요청
String seatIndex = "1"; //좌석 index
String userId = "123"; //사용자 id
String inviteId = mTRTCVoiceRoom.sendInvitation("pickSeat", userId, seatIndex, null);

// 2.초대가 수락된 후 사용자를 자리에 앉힘
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(index, null);
    }
}

// 청취자 앵글
// 1.청취자가 요청을 수신함
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("pickSeat")) {
        // 2.청취자의 방 주인 요청 수락
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
7. **[TRTCVoiceRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37339)를 통한 문자 채팅 구현**
```java
// 발신측: 텍스트 메시지 발송
mTRTCVoiceRoom.sendRoomTextMsg("Hello Word!", null);
// 수신측: 텍스트 메시지 수신
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
  @Override
  public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
      Log.d(TAG, userInfo.userName + "님이 발송한 메시지:" + message);
  }
});
```
8. **[TRTCVoiceRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37339)를 통한 화면 댓글 구현**
```java
// 발신 측: 사용자 정의 Cmd를 통해 댓글 자막과 '좋아요' 메시지 구분 가능
// eg: "CMD_DANMU": 댓글 자막 메시지, "CMD_LIKE": '좋아요' 메시지
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 수신측: 사용자 정의 메시지 수신
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 댓글 자막 메시지 수신
            Log.d(TAG, userInfo.userName + "님이 발송한 댓글 자막 메시지:" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // '좋아요' 메시지 수신
            Log.d(TAG, userInfo.userName + "좋아요를 눌렀습니다!");
        }
    }
});
```

## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 보내주시기 바랍니다.
