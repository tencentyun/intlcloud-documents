비디오 ILVB 기능에 빠르게 액세스해야 하는 경우 Tencent Cloud에서 제공하는 Demo를 기반으로 직접 수정하거나 Tencent Cloud에서 제공하는 TRTCLiveRoom 컴포넌트로 사용자 정의 UI 인터페이스를 구현해도 됩니다.

[](id:DemoUI)

## Demo UI 인터페이스 재사용

[](id:ui.step1)

### 1단계: 신규 애플리케이션 생성

1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원] > [Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예:`TestLive`)을 입력한 후 [생성]을 클릭합니다.

>! 본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication(TRTC)](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging(IM)](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.



[](id:ui.step2)
### 2단계: SDK와 Demo 소스 코드 다운로드

1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### 3단계: Demo 프로그래밍 파일 설정

1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `/example/lib/debug/GenerateTestUserSig.dart` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.dart` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)

### 4단계: 컴파일 실행
>! Android는 실제 기기에서 실행해야 하며, 시뮬레이터 디버깅을 지원하지 않습니다.

1. 'flutter pub get'을 실행합니다.
2. 컴파일 실행 디버깅:
   <dx-tabs>
:::  Android\s
1. 'flutter run'을 실행합니다.
2. Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램을 열고 [실행]을 클릭합니다.
:::
::: iOS\s
1. XCode(11.0 버전 이상)를 사용해 소스 코드 디렉터리에 있는 '/ios 프로그램'을 엽니다.
2. Demo 프로그램을 컴파일 및 실행합니다.
:::
</dx-tabs>

[](id:ui.step5)

### 5단계: Demo 소스 코드 수정

소스 코드 TRTCLiveRoom 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더에는 인터페이스 코드가 포함되어 있습니다. 다음 표에는 2차 조정을 위한 각 파일 또는 폴더 및 해당하는 UI 인터페이스가 나열되어 있습니다.

| 파일 또는 폴더 | 기능 설명                             |
| ------------ | ------------------------------------ |
| base         | UI 기본 사용 유형.                    |
| list         | 리스트 페이지 및 방 생성 페이지.                 |
| room         | 호스트와 시청자의 인터페이스를 포함하는 메인 방 페이지. |

[](id:model)

## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TRTCFlutterScenesDemo)의 TRTCLiveRoom 폴더에는 ui 폴더와 model 폴더가 있으며, model 폴더에는 재사용 가능한 오픈 소스 컴포넌트인 TRTCLiveRoom이 포함되어 있습니다. `TRTCLiveRoom.dart` 파일에서 해당 컴포넌트가 제공하는 인터페이스 함수를 확인할 수 있으며, 해당 인터페이스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:model.step1)

### 1단계: SDK 통합

ILVB 컴포넌트 TRTCLiveRoom은 [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)와 [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)에 종속되며, `pubspec.yaml` 설정을 통해 자동으로 다운로드 및 업데이트할 수 있습니다.

프로젝트의 `pubspec.yaml`에 다음과 같이 종속성을 작성합니다.
```
dependencies:
  tencent_trtc_cloud: 최신 버전 넘버
  tencent_im_sdk_plugin: 최신 버전 넘버
```

[](id:model.step2)
### 2단계: 권한 및 난독화 규칙 설정
<dx-tabs>
::: iOS\s
'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
:::
:::  Android\s

1. '/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
2. 'xmlns:tools="http://schemas.android.com/tools"'를 manifest에 추가합니다.
3. 'tools:replace="android:label"'을 application에 추가합니다.

>? 이 단계를 수행하지 않으면 [Android Manifest merge failed 컴파일 실패](https://intl.cloud.tencent.com/document/product/647/39242) 문제가 발생합니다.


![이미지](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>


[](id:model.step3)

### 3단계: TRTCLiveRoom 컴포넌트 가져오기

다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.

```
lib/TRTCLiveRoom/model/
```

[](id:model.step4)

### 4단계: 컴포넌트 생성 및 로그인

1. `sharedInstance` 인터페이스를 호출하여 TRTCLiveRoom 컴포넌트의 인스턴스 객체를 생성할 수 있습니다.
2. `registerListener` 함수를 호출하여 컴포넌트의 이벤트 공지를 등록합니다.
3. `login` 함수를 호출해 컴포넌트에 로그인하고, 다음 표를 참고하여 핵심 매개변수를 입력합니다.
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
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
</tr>
<tr>
<td>useCDNFirst</td>
<td> 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자의 CDN을 통한 시청을 의미하며 요금이 저렴하지만, 딜레이가 많이 발생합니다. false는 일반 시청자의 저지연 시청을 의미하며 요금이 CDN과 마이크 연결 요금의 중간이지만, 딜레이가 1s 이내로 제어됩니다.</td>
</tr>
<tr>
<td>CDNPlayDomain</td>
<td> useCDNFirst를 true로 설정해야만 적용되며 CDN을 통해 시청하는 재생 도메인을 지정하는 데 사용합니다. 라이브 방송 콘솔에 로그인하여 [<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 관리</a>] 페이지에서 설정할 수 있습니다.</td>
</tr>
</table>

[](id:model.step5)
### 5단계: 호스트 방송 시작

1. 호스트는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 호스트는 방송 시작 전에 `startCameraPreview`를 호출하여 카메라 미리보기를 활성화할 수 있으며 인터페이스에 뷰티 필터 조절 버튼 호출을 설정하고 `getBeautyManager`를 통해 뷰티 필터를 설정할 수 있습니다.
>?엔터프라이즈 버전 이외의 SDK는 얼굴 변경과 스티커 효과 기능을 지원하지 않습니다.
3. 호스트는 뷰티 필터 효과 조정 후, `createRoom` 을 호출하여 새로운 라이브 룸을 생성할 수 있습니다.
4. 호스트가 `startPublish` 를 호출해 푸시 스트리밍을 시작합니다. CDN 을 통한 시청을 지원하려면 login 시 전송되는 `TRTCLiveRoomConfig` 매개변수에서 `useCDNFirst` 와 `CDNPlayDomain` 을 지정하고 `startPublish` 에서 라이브 방송 풀 스트림용 streamID를 지정하십시오.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

[](id:model.step6)
### 6단계: 시청자 시청

1. 시청자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출해 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 시청자는 서비스 백엔드로부터 최신 라이브 룸 리스트를 획득합니다.
>?Demo에 있는 라이브 룸 리스트는 참고용입니다. 라이브 룸 리스트의 서비스 로직은 매우 다양하며 현재 Tencent Cloud는 라이브 룸 리스트 관리 서비스를 제공하지 않습니다. 라이브 룸 리스트는 직접 관리하시기 바랍니다.
3. 시청자가 `getRoomInfos`를 호출해 방의 세부 정보를 가져옵니다. 해당 정보는 호스트가 `createRoom`을 호출하여 라이브 룸 생성 시 설정한 간단한 설명 정보입니다.
 >!라이브 룸 리스트에 포괄적인 정보가 충분히 포함되어 있다면 `getRoomInfos` 호출 관련 단계는 건너뛸 수 있습니다.
4. 시청자가 하나의 라이브 룸을 선택하고 `enterRoom`을 호출하여 방 번호를 전송하면 즉시 해당 방에 입장할 수 있습니다.
5. `startPlay`를 호출하고 호스트의 userId를 전송하여 재생을 시작합니다.
 - 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자가 직접 `startPlay`를 호출하고 호스트의 userId를 전송하여 즉시 재생을 시작할 수 있습니다.
 - 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자는 방 입장 후 `onAnchorEnter`의 이벤트 콜백을 수신하게 됩니다. 해당 콜백에 호스트의 userId 정보가 포함되어 있으므로 `startPlay`를 호출하면 즉시 재생됩니다. 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

[](id:model.step7)
### 7단계: 시청자와 호스트 마이크 연결 ON/OFF

1. 시청자가 `requestJoinAnchor`를 호출하여 호스트에게 마이크 연결을 요청합니다.
2. 호스트가 `TRTCLiveRoomDelegate#onRequestJoinAnchor`(시청자의 마이크 연결 요청) 이벤트 공지를 수신합니다.
3. 호스트가 `responseJoinAnchor`를 호출하여 시청자의 마이크 연결 요청에 대한 수락 여부를 결정합니다.
4. 시청자는 호스트단 처리 결과를 전달하는 'onAnchorAccepted' 이벤트 알림을 받게 됩니다.
5. 호스트가 마이크 연결 요청을 수락하면 시청자는 `startCameraPreview`를 호출하여 로컬 카메라를 활성화하고 `startPublish`를 호출하여 시청자 푸시 스트리밍을 실행할 수 있습니다.
6. 호스트는 시청자 푸시 스트림 실행 공지 후 `TRTCLiveRoomDelegate#onAnchorEnter`(다른 채널의 멀티미디어 스트림 도착) 공지를 수신하며 해당 공지에는 시청자의 userId가 포함되어 있습니다.
7. 호스트가 `startPlay`를 호출하면 마이크가 연결된 시청자의 비디오 화면을 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)


[](id:model.step8)

### 8단계: 호스트 간의 PK

1. 호스트 A가 `requestRoomPK`를 호출하여 호스트 B에게 PK 요청을 발송합니다.
2. 호스트 B가 `TRTCLiveRoomDelegate onRequestRoomPK` 콜백 공지를 수신합니다.
3. 호스트 B는 `responseRoomPK`를 호출하여 호스트 A의 PK 요청에 대한 수락 여부를 결정합니다.
4. 호스트 B가 호스트 A의 요청을 수락한 후 `TRTCLiveRoomDelegate onAnchorEnter` 공지를 기다렸다가 `startPlay`를 호출하여 호스트 A를 표시합니다.
5. 호스트 A가 PK 요청 수락 여부에 대한`onRoomPKAccepted` 콜백 공지를 수신합니다. 
6. 호스트 A의 요청이 수락되면 `TRTCLiveRoomDelegate onAnchorEnter` 공지를 기다렸다가 `startPlay`를 호출하여 호스트 B를 표시합니다.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

[](id:model.step9)
### 9단계: 문자 채팅 및 댓글 자막 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
  IM의 백엔드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.
<dx-codeblock>
::: dart dart
// 발신 측: 텍스트 메시지 발송
trtcLiveCloud.sendRoomTextMsg("Hello Word!");
  

// 수신 측: 텍스트 메시지 수신
onListenerFunc(type, params) async {
  switch (type) {
    case TRTCLiveRoomDelegate.onRecvRoomTextMsg:
          //그룹 텍스트 메시지를 수신하여 텍스트 채팅방으로 사용 가능
      break;
  }
}
:::
</dx-codeblock>
- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
  사용자 정의 메시지는 '좋아요' 메시지 발송과 같은 사용자 정의 신호 전송에 주로 사용됩니다.
