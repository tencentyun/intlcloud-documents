## 효과

>! 본 프로젝트에서는 현재 Flutter 2.0을 지원하지 않습니다. Flutter 2.0 버전을 사용하시는 경우 버전을 다운그레이드하시기 바랍니다.

Tencent Cloud의 Demo를 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 후 설치하여 음성 살롱 기능을 체험해볼 수 있습니다. Demo에는 음성 채팅, 마이크 켜기/끄기, 저딜레이 음성 인터랙션 등 음성 채팅 시나리오에서의 TRTC 관련 기능이 포함되어 있습니다.


신속한 음성 살롱 기능이 필요할 경우, Tencent Cloud에서 제공하는 Demo를 기반으로 설정을 적합하게 수정하거나 TRTCChatSalon 모듈을 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:DemoUI)

## Demo UI 인터페이스 재사용

[](id:ui.step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예: `TestChatSalon`)을 입력한 후 [생성]을 클릭합니다.

>! 본 기능은 기본 PaaS 서비스인 Tencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [인스턴트 메시지 IM](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. 인스턴트 메시지 IM은 부가 서비스이며, 자세한 과금 규정은 [인스턴트 메시지 IM 요금 가이드](https://intl.cloud.tencent.com/document/product/1047/34350)를 참조하십시오.



[](id:ui.step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:ui.step3)
### 3단계: Demo 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `/example/lib/debug/GenerateTestUserSig.dart` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.dart` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.


>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 지향의 인터페이스를 제공합니다. UserSig가 필요한 경우 App에서 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

[](id:ui.step4)
### 4단계: 컴파일 실행

>! Android는 실제 기기에서 실행해야 하며, 시뮬레이터 디버깅을 지원하지 않습니다.

1. 'flutter pub get'을 실행합니다.
2. 컴파일 실행 디버깅:
  ####  Android\s
    1. 'flutter run'을 실행합니다.
    2. Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램을 열고 [실행]을 클릭합니다.
  ####  iOS\s
    1. XCode(11.0 버전 이상)를 사용해 소스 코드 디렉터리에 있는 '/ios 프로그램'을 엽니다.
    2. Demo 프로그램을 컴파일 및 실행합니다.

[](id:ui.step5)
### 5단계: Demo 소스 코드 수정
소스 코드 trtcchatsalondemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더의 모든 파일은 인터페이스 관련 코드입니다. 다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명                             |
| ------------ | ------------------------------------ |
| base         | UI로 사용하는 기본 유형                    |
| list         | 리스트 페이지 및 방 생성 페이지                 |
| room         | 호스트와 시청자의 인터페이스를 포함하는 메인 방 페이지
| widget       | 범용 컨트롤러                           |

[](id:model)
## 사용자 정의 UI 인터페이스 구현
[소스 코드](https://github.com/c1avie/TRTCChatSalon)의 trtcchatsalondemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 모듈인 TRTCChatSalon이 포함되어 있습니다. `TRTCChatSalon.dart` 파일에서 해당 모듈이 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png)

[](id:model.step1)
### 1단계: SDK 통합
음성 살롱 모듈 trtcchatsalondemo는 [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)와 [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)에 종속되며, `pubspec.yaml` 설정을 통해 자동으로 다운로드 및 업데이트할 수 있습니다.

프로젝트의 `pubspec.yaml`에 다음과 같이 종속성을 작성합니다.
```
dependencies:
  tencent_trtc_cloud: 최신 버전 넘버
  tencent_im_sdk_plugin: 최신 버전 넘버
```

[](id:model.step2)

### 2단계: 권한 및 난독화 규칙 설정
#### iOS
'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
#### Android
1. '/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
2. 'xmlns:tools="http://schemas.android.com/tools"'를 manifest에 추가합니다.
3. 'tools:replace="android:label"'을 application에 추가합니다.
>? 이 단계를 수행하지 않으면 [Android Manifest merge failed 컴파일 실패](https://intl.cloud.tencent.com/document/product/647/39242) 문제가 발생합니다.

![이미지](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)


[](id:model.step3)
### 3단계: TRTCChatSalon 모듈 가져오기
다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
```
lib/TRTCChatSalonDemo/model/
```

<span id="model.step4"></span>
### 4단계: 모듈 생성 및 로그인
1. `sharedInstance` 인터페이스를 호출하여 TRTCChatSalon 모듈의 인스턴스 객체를 생성합니다.
2. `registerListener` 함수를 호출하여 모듈의 이벤트 공지를 등록합니다.
3. `login` 함수를 호출해 모듈에 로그인하고, 다음 표를 참고하여 핵심 매개변수를 입력합니다.
<table>
<tr>
<th>매개변수 이름</th>
<th>역할</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr>
<tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr>
</table>

```
TRTCChatSalon trtcVoiceRoom = await TRTCChatSalon.sharedInstance();
trtcVoiceRoom.registerListener(onVoiceListener);
ActionCallback resValue = await trtcVoiceRoom.login(
    GenerateTestUserSig.sdkAppId,
    userId,
    GenerateTestUserSig.genTestSig(userId),
);
if (resValue.code == 0) {
    //로그인 성공
}
```

[](id:model.step5)

### 5단계: 호스트의 방송 시작

1. 호스트는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트가 `createRoom`을 호출하여 새로운 음성 살롱을 생성합니다. 이때 방 ID, 방 이름 등 방 속성 정보를 전송합니다.
3. 호스트는 사용자가 입장할 때 `TRTCChatSalonDelegate.onAnchorEnterSeat` 이벤트 공지를 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)

```
// 1. 호스트 닉네임 및 프로필 사진 설정
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. 호스트가 createRoom을 호출하여 방 생성
ActionCallback resp = await trtcVoiceRoom.createRoom(
    roomId,
    RoomParam(
    coverUrl: '방 썸네일 이미지 URL 주소',
    roomName: '방 이름',
    ),
);
if (resp.code == 0) {
   //자리 점유 성공
}

// 4. 자리를 점유한 후 TRTCChatSalonDelegate.onAudienceEnter 이벤트 공지 수신
onVoiceListener(type, param) async {
    switch (type) {
        case TRTCChatSalonDelegate.onAudienceEnter:
            //시청자 방 입장
            break;
    }
}
```

[](id:model.step6)

### 6단계: 시청자 시청

1. 시청자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 시청자가 서비스 백그라운드에서 최신 음성 살롱 방 리스트를 가져옵니다.
 >?Demo의 음성 살롱 리스트는 참고용입니다. 음성 살롱 리스트의 서비스 로직은 매우 다양하여 Tencent Cloud에서는 현재 음성 살롱 리스트 관리 서비스를 제공하지 않으며, 음성 살롱 리스트는 직접 관리하시기 바랍니다.
3. 시청자가 `getRoomList`를 호출해 방 세부 정보를 가져옵니다. 해당 정보는 호스트가 `createRoom`을 호출하여 음성 살롱 생성 시 설정한 간단한 설명 정보입니다.
>!음성 살롱 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomList` 호출 관련 단계는 건너뛰고 방 번호를 전달하여 해당 방으로 입장할 수 있습니다.
4. 방 입장 후, 모듈의 시청자 방 입장/퇴장 공지인 `TRTCChatSalonDelegate.onAudienceEnter`와 `TRTCChatSalonDelegate.onAudienceExit`를 수신하게 됩니다. 이벤트 콜백을 수신한 후 변경 사항을 UI 인터페이스에 새로 고침할 수 있습니다.
5. 방 입장 후 마이크 위치 리스트에 호스트 입장 `TRTCChatSalonDelegate.onAnchorEnterMic` 및 `TRTCChatSalonDelegate.onAnchorLeaveMic` 이벤트 공지도 수신합니다.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)
```
// 1. 시청자 닉네임 및 프로필 사진 설정
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url");

// 2. 서비스 백그라운드에서 획득한 방 리스트가 roomList라고 가정할 경우
List<Integer> roomList = GetRoomList();

// 3. getRoomInfoList 호출을 통해 방 세부 정보 획득
RoomInfoCallback resp = await trtcVoiceRoom.getRoomInfoList(roomList);
if (resp.code == 0) {
    //이때 사용자의 UI 방 리스트 새로고침 가능
} 

// 4. roomid를 전달하여 방 입장
ActionCallback enterRoomResp =
          await trtcVoiceRoom.enterRoom(_currentRoomId);
if (enterRoomResp.code == 0) {
    //방 입장 성공
}
// 5. 방 입장 완료 후 이벤트 처리 공지 수신
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAudienceEnter:
            //시청자 방 입장
        break;
      case TRTCChatSalonDelegate.onAudienceExit:
            //시청자 방 퇴장
        break;
      case TRTCChatSalonDelegate.onAnchorLeaveMic:
          //호스트 방 퇴장
        break;
      case TRTCChatSalonDelegate.onAnchorEnterMic:
          //호스트 방 입장
        break;
    }
}
```

[](id:model.step7)
### 7단계: 마이크 켜기/끄기
#### 호스트 측
1. `leaveMic`로 직접 마이크를 끄면 방 안에 있는 모든 사용자가 `onAnchorLeaveMic` 이벤트 공지를 수신합니다.
2. `kickMic`에 해당하는 사용자의 userId를 전달하면 특정 사용자의 마이크를 끌 수 있으며, 방 안에 있는 모든 사용자가 `onAnchorLeaveMic` 이벤트 공지를 수신합니다.

![](https://main.qcloudimg.com/raw/b47e4ce248aa71f9a68f28f57c699db6.png)
```
// 1. 호스트가 직접 마이크 끄기
trtcVoiceRoom.leaveMic();

//2. 특정 사용자 마이크 끄기
trtcVoiceRoom.kickMic(userId);
```
#### 시청자 측
1. `enterMic`로 마이크를 켤 수 있으며 방 안에 있는 모든 사용자가 `onAnchorEnterMic` 이벤트 공지를 수신합니다.
2. `leaveMic`로 직접 마이크를 끄면 방 안에 있는 모든 사용자가 `onAnchorLeaveMic` 이벤트 공지를 수신합니다.

![](https://main.qcloudimg.com/raw/8b68a5c714bf024c8598a52a7281c745.png)
```
// 1. 시청자가 직접 마이크 켜기
trtcVoiceRoom.enterMic();

// 2. 직접 마이크 끄기
trtcVoiceRoom.leaveMic();
```


[](id:model.step8)

### 8단계: 손 들기로 마이크 켜기 신호 사용 요청

사용자 App이 상대방이 동의해야 다음 단계의 작업을 진행할 수 있는 비즈니스 프로세스인 경우, 초대 신호는 해당하는 지원을 제공할 수 있습니다.

#### 시청자가 직접 마이크 켜기 신청

1. 시청자가 `raiseHand`를 호출하여 손 들기를 신청합니다.
2. 호스트가 `onRaiseHand` 이벤트 공지를 수신하고, 이때 UI가 호스트의 동의 여부를 묻는 팝업창을 팝업할 수 있습니다.
3. 호스트가 동의를 선택하면 `agreeToSpeak`을 호출하고 userId를 전달합니다.
4. 시청자는 `onAgreeToSpeak` 이벤트 공지를 수신하고, `enterMic`를 호출하여 마이크를 켭니다.

![](https://main.qcloudimg.com/raw/72e4ddc8e1d13b47c6713355145c297e.png)
```
// 시청자 측 앵글
// 1. sendInvitation를 호출하여 마이크 켜기 요청
trtcVoiceRoom.raiseHand();

// 2. 초대 동의 요청을 수신하면 정식으로 마이크 켜짐
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRaiseHand:
           trtcVoiceRoom.enterMic();
        break;
    }
}

// 호스트 측 앵글
// 1. 호스트가 요청 수신
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAgreeToSpeak:
           trtcVoiceRoom.agreeToSpeak();
        break;
    }
}
```

[](id:model.step9)

### 9단계: 문자 채팅 및 댓글 자막 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
IM의 백그라운드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
```
// 발신 측: 텍스트 메시지 발송
trtcVoiceRoom.sendRoomTextMsg("Hello Word!");
// 수신 측: 텍스트 메시지 수신
onVoiceListener(type, param) async {
  switch (type) {
    case TRTCChatSalonDelegate.onRecvRoomTextMsg:
          //그룹 텍스트 메시지를 수신하여 텍스트 채팅방으로 사용 가능
      break;
  }
}
```
