
<h3 id="UserSig">UserSig란 무엇인가요?</h3>

UserSig란 Tencent Cloud가 설계한 일종의 보안 서명으로, 악성 해커가 귀하의 클라우드 서비스 사용권을 도용하는 것을 방지합니다.
현재 Tencent Real-Time Communication(TRTC), Instant Messaging(IM), Mobile Live Video Broadcastng(MLVB) 등의 서비스는 모두 이 보안 메커니즘을 사용하고 있으며, 이러한 서비스를 사용하려면 해당 SDK의 초기화 또는 로그인 함수에 SDKAppID, UserID, UserSig의 주요 정보를 제공해야 합니다.
이 중, SDKAppID는 귀하의 애플리케이션 식별에 사용되고, UserID는 귀사의 사용자 식별에 사용됩니다. UserSig는 이 둘을 기반으로 보안 서명을 계산합니다. UserSig는 **HMAC SHA256** 암호화 알고리즘으로 계산됩니다. 해커가 UserSig를 위조하지 못하는 이상 귀하의 클라우드 서비스 트래픽을 도용할 수 없습니다.
UserSig의 계산 원리는 다음 이미지와 같으며, 그 본질은 SDKAppID, UserID, ExpireTime 등 주요 정보에 대해 해시 암호화를 1회 진행하는 것입니다.
```Cpp
//UserSig 계산 공식, 여기서 secretkey는 usersig 계산용 암호화 키

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```
>?
>- 'currtime'은 현재 시스템 시간이고 'expire'는 서명 만료 시간입니다.
>- UserSig의 구체적인 계산 및 획득 방법은 [UserSig 세부 정보](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.

[](id:que2)
### TRTC는 동시에 최대 몇 개의 방을 생성할 수 있습니까?
동시에 4294967294개의 방이 존재할 수 있으며, 누적 방 수량에는 제한이 없습니다.


[](id:que3)
### TRTC는 대략 어느 정도 딜레이됩니까?
글로벌 end to end로 평균 300ms 미만으로 딜레이됩니다.


[](id:que4)
### TRTC의 PC 액세스에 화면 공유 기능을 지원합니까?
지원합니다. 다음 문서를 참고하십시오.
- [화면 공유(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [화면 공유(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [화면 공유(Web)](https://intl.cloud.tencent.com/document/product/647/35163)

화면 공유 인터페이스에 대한 자세한 내용은 [Windows(C++) API](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오. 또한, [Electron 인터페이스](https://intl.cloud.tencent.com/document/product/647/35141)를 사용할 수도 있습니다.


[](id:que5)
### TRTC에서 지원하는 플랫폼에는 어떤 것이 있습니까?
iOS, Android, Windows(C++), Windows(C#), Mac, Web, Electron 등의 플랫폼을 지원합니다. 자세한 내용은 [플랫폼 지원](https://intl.cloud.tencent.com/document/product/647/35078)을 참고하십시오.


[](id:que6)
### TRTC는 최대 몇 명의 동시 통화를 지원합니까?
- 통화 모드에서는 단일 방에 최대 300명까지 동시 접속이 가능하며 최대 50명까지 동시에 카메라 또는 마이크를 활성화할 수 있습니다.
- 라이브 방송 모드에서는 한 방에 10만 명 이상이 시청자 자격으로 접속하여 시청할 수 있으며, 최대 50명까지 호스트 자격으로 카메라 또는 마이크를 활성화할 수 있습니다.


[](id:que7)
### TRTC는 라이브 방송 시나리오 애플리케이션을 어떻게 실행합니까?
TRTC는 온라인 라이브 방송 시나리오 전용으로 10만 명 참여 시의 ILVB 저지연 솔루션을 출시했으며, 이를 통해 호스트와 마이크가 연결된 호스트의 최저 딜레이 시간은 200ms 이내, 일반 시청자의 딜레이 시간은 1s 이내로 보장합니다. 또한 약한 네트워크 보완 기술을 통해 복잡한 모바일 네트워크 환경에 대응합니다.
자세한 작업 가이드는 [라이브 방송 모드 실행](https://intl.cloud.tencent.com/document/product/647/35107)을 참고하십시오.



[](id:que8)
### TRTC 라이브 방송은 어떤 역할을 지원하며, 어떤 차이가 있습니까?
라이브 방송 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)는 TRTCRoleAnchor(호스트)와 TRTCRoleAudience(시청자)이라는 두 가지 역할을 지원합니다. 호스트 역할은 멀티미디어 데이터를 동시에 업스트림, 다운스트림할 수 있으며, 시청자 역할은 다른 사람의 데이터를 다운스트림 재생만 할 수 있습니다. switchRole() 호출을 통해 역할을 교체할 수 있습니다.


[](id:que9)
### TRTC 방에서 강제 퇴장, 발언 금지, 음소거 기능을 지원합니까?  
지원합니다.
- 간단한 작업 명령인 경우 TRTC의 사용자 정의 명령 인터페이스 sendCustomCmdMsg를 사용해 개발자가 해당 제어 명령을 사용자 정의할 수 있으며, 제어 명령을 수신하는 통화 상대방이 해당 작업을 실행하면 됩니다. 예를 들어 강제 퇴장의 경우 강제 퇴장 명령을 정의하면 되며, 해당 명령을 수신한 사용자는 스스로 방을 퇴장하게 됩니다.
- 더 완벽한 작업 로직이 필요한 경우 개발자가 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 통해 관련 로직을 실현하는 것이 좋습니다. TRTC의 방과 IM 그룹을 매핑하고 IM 그룹에서 사용자 정의 정보를 수신/발신해 해당 작업을 구현하십시오.


[](id:que10)
### TRTC 멀티미디어 스트리밍은 CDN 풀 스트리밍 시청을 지원합니까? 
지원합니다. 자세한 내용은 [CDN 라이브 방송 시청 실행](https://intl.cloud.tencent.com/document/product/647/35242)을 참고하십시오.


[](id:que11)
###  iOS에서 Swift 통합이 지원됩니까?
지원합니다. Third Party 라이브러리 통합 지원 프로세스에 따라 SDK를 통합하면 됩니다. [Demo 실행(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)을 참고하십시오.


[](id:que12)
### Web SDK는 어떤 브라우저를 지원합니까?  
현재 데스크톱 버전 Chrome 브라우저, 데스크톱 버전 Safari 브라우저, 모바일 버전 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예시: Android 시스템 브라우저)의 지원 상황은 완전하지 못할 수 있습니다. 자세한 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/41664)을 참고하십시오.
브라우저에서 [WebRTC 기능 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC 기능을 완벽하게 지원하는지 테스트할 수 있습니다.


[](id:que13)
### Web SDK 로그에서 보고하는 NotFoundError, NotAllowedError, NotReadableError, OverConstrainedError, AbortError 오류 메시지는 각각 어떤 오류입니까?


| 오류 이름 | 설명 | 해결 방법 |
|---------|---------|---------|
| NotFoundError  | 요청에 맞는 매개변수의 미디어 유형(오디오, 비디오, 화면 공유 등)을 찾을 수 없는 경우입니다. <br>예를 들어, PC에 카메라가 없는데 브라우저에 비디오 스트림을 요청하는 경우, 오류 메세지를 보고합니다.   | 통화 전 사용자에게 통화에 필요한 카메라 또는 마이크 등의 디바이스가 있는지 확인을 요청하고, 카메라가 없고 음성 통화만 필요한 경우, [TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)에서 마이크만 사용하는 방법을 확인하십시오. |
| NotAllowedError | 사용자가 현재 브라우저 인스턴스의 오디오, 비디오, 화면 공유 액세스 요청을 거절한 상태입니다.   | 사용자에게 카메라/마이크의 액세스 권한 요청을 거절하면 멀티미디어 통화를 사용할 수 없다고 안내하십시오.       |
| NotReadableError  | 사용자가 상응하는 디바이스의 권한을 허용하였으나 운영 체제의 일부 하드웨어, 브라우저 또는 웹 페이지 레이어로 인해 오류가 발생해 디바이스가 액세스할 수 없는 상태입니다.  | 브라우저 오류 메시지에 따라 처리하고, 사용자에게 “일시적으로 카메라/마이크에 액세스할 수 없습니다. 현재 다른 애플리케이션에서 카메라/마이크에 액세스 요청을 하지 않았는지 확인한 후 다시 시도해 주십시오.”라고 안내하십시오.|
| OverConstrainedError|   cameraId/microphoneId 매개변수 값이 유효하지 않습니다. | cameraId/microphoneId 전송 값이 정확하고 유효한지 확인하십시오.|
| AbortError  | 알 수 없는 문제로 인해 디바이스를 사용할 수 없는 상태입니다.| - |


자세한 내용은 [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)를 참고하십시오.


[](id:que14)
### Web SDK가 정상적으로 디바이스(카메라/마이크) 리스트를 획득했는지 어떻게 알 수 있습니까?
1. 브라우저가 정상적으로 디바이스를 사용할 수 있는지 확인합니다.
페이지에서 직접 콘솔을 열어 `navigator.mediaDevices.enumerateDevices()`를 입력해 디바이스 리스트를 획득할 수 있는지 확인합니다.
 - 정상적으로 디바이스를 획득한 경우 Promise가 리턴되며, 안에 MediaDeviceInfo 객체 디지털 그룹이 나타납니다. 디지털 그룹 안의 모든 객체는 각각 사용 가능한 미디어 디바이스가 있습니다.
 - 열거에 실패한 경우 Promise가 rejected를 리턴하며, 이는 브라우저가 식별할 수 있는 디바이스가 없음을 의미하므로 브라우저 또는 디바이스를 점검해야 합니다.
2. 디바이스 리스트를 획득한 경우 `navigator.mediaDevices.getUserMedia({ audio: true, video: true })`를 입력하여 MediaStream 객체가 정상적으로 리턴되는지 확인합니다. 정상적으로 리턴되지 않으면 브라우저가 데이터를 획득할 수 없는 상태이므로 브라우저 설정을 점검해야 합니다.

[](id:que17)
###  라이브 방송, ILVB, TRTC, 릴레이 라이브 방송에는 어떤 차이와 관계가 있습니까?
- **라이브 방송**(키워드: 1대 다수, RTMP/HLS/HTTP-FLV, CDN)
 라이브 방송은 푸시 스트리밍, 재생, 라이브 방송 클라우드 서비스로 나뉘며, 클라우드 서비스는 CDN을 사용해 라이브 방송 스트리밍을 배포합니다. 푸시 스트리밍은 범용 표준 프로토콜 RTMP를 사용해 CDN을 거쳐 배포한 후 재생 시 일반적으로 RTMP, HTTP-FLV 또는 HLS(H5 지원) 등의 방식을 선택하여 시청할 수 있습니다.
- **ILVB**(키워드: 마이크 연결, PK)
 ILVB는 일종의 비즈니스 형태로, 호스트와 시청자 사이의 인터랙션 마이크를 연결하고, 호스트와 호스트 사이에서 인터랙션 PK를 진행하는 일종의 라이브 방송 형태입니다.
- **TRTC**(키워드: 다중 사용자 인터랙션, UDP, 사유 프로토콜, 저지연)
 Tencent Real-Time Communication(TRTC)의 주요 응용 시나리오는 멀티미디어 인터랙션과 저지연 라이브 방송이며, UDP 기반의 사유 프로토콜을 사용하여 딜레이가 100ms까지 낮아집니다. 전형적인 시나리오로는 QQ 전화, VooV Meeting, 대규모 수업 등이 있습니다. Tencent Cloud TRTC는 전 플랫폼을 커버하며 iOS/Android/Windows 이외에 WebRTC 통신을 지원하고 클라우드 혼합 스트리밍 방식을 통해 릴레이 라이브 방송 화면을 CDN으로 전달합니다.
- **릴레이 라이브 방송**(키워드: 클라우드 혼합 스트리밍, RTC 릴레이 공유, CDN)
 릴레이 라이브 방송은 저지연 마이크 연결 방 안의 여러 채널의 푸시 스트리밍 화면을 복사하여 클라우드에서 화면을 한 채널로 통합하고, 혼합 스트리밍 후의 화면을 라이브 방송 CDN으로 푸시 스트리밍하여 배포 재생하는 기술입니다. 

[](id:que18)
### TRTC에서 통화 시간과 사용량은 어떻게 확인합니까?  
TRTC 콘솔의 [[사용량 통계](https://console.cloud.tencent.com/trtc/statistics)] 페이지에서 확인할 수 있습니다.

[](id:que19)
### TRTC에 랙이 발생하면 어떻게 해결해야 합니까?
TRTC 콘솔의 [[모니터링 대시보드](https://console.cloud.tencent.com/trtc/monitor)] 페이지에서 ​해당 RoomID, UserID를 통해 통화 품질을 확인할 수 있습니다.
- 수신자 시점에서 발신자와 수신자의 상황을 확인합니다.
- 발신자와 수신자의 패킷 손실률이 높은지 확인합니다. 패킷 손실률이 너무 높은 경우 일반적으로 네트워크가 불안정하여 랙이 발생합니다.
- 프레임 레이트와 CPU 이용률을 확인합니다. 프레임 레이트가 낮거나 CPU 이용률이 너무 높은 경우 랙 현상이 발생합니다.


[](id:que20)
### TRTC 화질이 좋지 않습니다. 흐릿하고 모자이크 현상 등이 발생합니다. 어떻게 해결해야 합니까?
- 해상도는 주로 비트 레이트와 관련이 있습니다. SDK 비트 레이트가 낮게 설정되어 있는지 확인하십시오. 해상도가 높은데 비트 레이트가 낮은 경우 모자이크 현상이 쉽게 나타날 수 있습니다.
- TRTC는 클라우드 QOS 트래픽 제어 정책을 통해 네트워크 상태에 따라 비트 레이트와 해상도를 동적으로 조정합니다. 네트워크 상태가 좋지 않은 경우 비트 레이트가 낮아져 해상도가 떨어질 수 있습니다.
- 방 입장 시 사용한 VideoCall 모드가 Live 모드인지 확인합니다. 통화 VideoCall 모드는 저지연성과 원활한 통화에 중점을 두므로 네트워크가 약한 경우 화질을 포기하고 원활한 통화 상태를 확보합니다. 화질이 더 중요한 경우 Live 모드 사용을 권장합니다.

[](id:que21)
### SDK 최신 버전 번호는 어떻게 조회합니까?
- 자동 로딩 방식을 사용하는 경우, `latest.release`가 최신 버전과 매칭되어 자동 로딩되므로 버전 번호를 수정하지 않아도 됩니다. 자세한 방법은 [SDK 1분 통합](https://intl.cloud.tencent.com/document/product/647/35092)을 참고하십시오.
- 현재 SDK 최신 버전 번호는 릴리스 노트를 통해 조회 가능합니다. 자세한 내용은 다음을 참고하십시오.
  - iOS & Android는 [릴리스 노트(App)](https://intl.cloud.tencent.com/document/product/647/39426)를 참고하십시오.
  - Web은 [릴리스 노트(Web)](https://intl.cloud.tencent.com/document/product/647/39779)를 참고하십시오.
  - Electron은 [릴리스 노트(Electron)](https://intl.cloud.tencent.com/document/product/647/38702)를 참고하십시오.
