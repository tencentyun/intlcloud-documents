## 컴포넌트 개요
TUIKaraoke는 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합하고 몇 줄의 코드 작성만으로 애플리케이션에 온라인 노래방 시나리오를 추가하여 노래방, 좌석 관리, 선물 주고받기, 문자 채팅과 같은 TRTC 기능을 체험해 볼 수 있습니다. iOS 플랫폼도 지원합니다. 기본 기능은 다음과 같습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/c17771587a0803db28047796fcd0df11.png)

## 컴포넌트 통합
### 1단계: TUIKaraoke 컴포넌트 다운로드 및 가져오기

[GitHub](https://github.com/tencentyun/TUIKaraoke)으로 이동하여 코드를 복제 또는 다운로드하고 Android 디렉터리의 Source 및 Debug 디렉터리를 프로젝트에 복사하고 다음 가져오기 작업을 완료합니다.
- 아래와 같이 `setting.gradle`에서 가져오기를 완료합니다.
```
include ':Source'
include ':Debug'
```
- app의 build.gradle 파일에 TUIKaraoke에 대한 종속성을 추가합니다.
```
api project(':Source')
```
- 루트 디렉터리의 `build.gradle` 파일에 `TRTC SDK` 및 `IM SDK`에 대한 종속성을 추가합니다.
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTCl:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### 2단계: 권한 요청 및 난독화 규칙 구성

AndroidManifest.xml에서 App에 대한 권한 요청을 구성합니다. SDK에는 다음 권한이 필요합니다(Android 6.0 이상에서는 런타임 시 마이크 액세스 및 저장소 읽기 권한을 요청해야 함).

```
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // 사용 사례: 이 권한은 플로팅 창에 필요;
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // 사용 사례: 블루투스 헤드셋 사용 시 이 권한이 필요함;
```

proguard-rules.pro 파일에서 SDK 클래스를 난독화 금지 목록에 추가합니다.
```
-keep class com.tencent.** { *; }
```

### 3단계: 컴포넌트 초기화 및 로그인 
관련 API에 대한 자세한 내용은 [TUIKaraoke](https://intl.cloud.tencent.com/document/product/647/41943)를 참고하십시오.

```java
  // 1. 초기화
  TRTCKaraokeRoom mTRTCKaraokeRoom = TRTCKaraokeRoom.sharedInstance(this);
  mTRTCKaraokeRoom.setDelegate(this);
  // 2. 로그인
  mTRTCKaraokeRoom.login(SDKAppID, UserID, UserSig, new TRTCKaraokeRoomCallback.ActionCallback() {
      @Override
      public void onCallback(int code, String msg) {
          if (code == 0) {
          //로그인 성공
          }
      }
  });
```
**매개변수 설명**:
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [TRTC 애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 문자열이며 최대 32바이트의 문자와 숫자를 포함할 수 있는 현재 사용자 ID입니다(특수 기호는 지원되지 않음). 실제 계정 시스템에 따라 사용자 정의할 수 있습니다.
- **userSig**: SDKAppID, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [TUIKaraoke 데모 프로젝트](https://github.com/tencentyun/TUICalling/blob/main/Android/App/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.

### 4단계: 온라인 노래방 시나리오 구현
1. **앵커는 [TUIKaraoke.createRoom](https://intl.cloud.tencent.com/document/product/647/41943)을 통해 방을 만듭니다**.
```java
int roomId = "방 ID";
TRTCKaraokeRoomDef.RoomParam roomParam = new TRTCKaraokeRoomDef.RoomParam();
roomParam.roomName = "방 이름";
roomParam.needRequest = false; // 마이크 연결 시 방 주인 확인 필요 여부
roomParam.seatCount = 8;       // 방의 좌석 수. 8개로 설정
roomParam.coverUrl = "방 표지 이미지의 URL";
mTRTCKaraokeRoom.createRoom(roomId, roomParam, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
      if (code == 0) {
        //방 생성 성공
      }
    }
});
```
2. **청취자는 [TUIKaraoke.enterRoom](https://intl.cloud.tencent.com/document/product/647/41943)을 통해 방에 들어갑니다**.
```java
mTRTCKaraokeRoom.enterRoom(roomId, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        //방 들어가기 성공
        }
    }
});
```
3. **청취자는 [TUIKaraoke.enterSeat](https://intl.cloud.tencent.com/document/product/647/41943)를 통해 마이크를 켭니다**.
```java
// 1. 청취자가 마이크를 켜기 위해 API 호출
int seatIndex = 1;
mTRTCKaraokeRoom.enterSeat(seatIndex, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        //마이크 활성화 성공
        }
    }
});
// 2. 청취자는 onSeatListChange 콜백을 수신하고 좌석 목록을 새로고침함
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
}
```

>? [TRTCKaraoke(Android)](https://intl.cloud.tencent.com/document/product/647/41943) 또는 [TUIKaraoke 데모 프로젝트](https://github.com/tencentyun/TUIKaraoke/)를 참고하여 다른 좌석 관리 작업을 구현할 수 있습니다.

4. **노래를 재생하고 노래방 시나리오를 체험합니다.**
음악 ID와 URL을 가져와 비즈니스에 따라 노래를 재생할 수 있습니다. 자세한 내용은 [TUIKaraoke 음악 재생 API](https://intl.cloud.tencent.com/document/product/647/41943#.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E6.8E.A5.E5.8F.A32)를 참고하십시오.
```java
//음악 재생
mTRTCKaraokeRoom.startPlayMusic(musicID,url);
//음악 중지
mTRTCKaraokeRoom.stopPlayMusic();
```

이전 단계를 완료한 후 기본 노래방 기능을 구현할 수 있습니다. 비즈니스에 문자 채팅 및 선물하기 등 더 많은 기능이 필요한 경우 다음 기능을 통합할 수 있습니다.

### 5단계: 텍스트 채팅 기능 추가(옵션)
앵커와 청취자 간의 텍스트 채팅 기능을 원하시면 다음과 같이 메시지 송수신을 구현하십시오.
관련 API에 대한 자세한 내용은 [TRTCKaraokeRoom.sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/41943#sendroomtextmsg)를 참고하십시오.
```java
// 발신측: 텍스트 메시지 발송
mTRTCKaraokeRoom.sendRoomTextMsg("Hello Word!", new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //전송 성공
        }
    }
});
// 수신측: 텍스트 메시지 수신
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
  @Override
  public void onRecvRoomTextMsg(String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
      Log.d(TAG, userInfo.userName + "님이 발송한 메시지:" + message);
  }
});
```

### 6단계: 선물하기 기능 추가(옵션)
선물 주고받기 기능을 원하시면 다음과 같이 선물하기, 받기, 표시를 구현하십시오.
```java
// 발신측: 선물 메시지를 구별하기 위해 "CMD_GIFT"를 사용자 정의합니다.
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_GIFT",date, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //전송 성공
        }
    }
});

// 수신측: 선물 메시지 수신
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
        if ("CMD_GIFT".equals(cmd)) {
            // 선물 메시지 수신
            Log.d(TAG, userInfo.userName + "님이 보낸" + "선물을 받았습니다." + message);
        }
    }
});
```

## FAQ
### TUIKaraoke 컴포넌트는 음성 변경, 톤 변경 및 리버브와 같은 음향 효과 기능을 지원합니까?
지원합니다. 자세한 내용은 [TUIKaraoke 데모 프로젝트](https://github.com/tencentyun/TUIKaraoke/blob/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke/ui/audio/AudioEffectPanel.java)를 참고하십시오.

>? 요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의하십시오.
