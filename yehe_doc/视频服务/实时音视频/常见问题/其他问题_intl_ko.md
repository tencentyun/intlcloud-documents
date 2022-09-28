[](id:que1)
###  라이브 스트리밍, 인터랙티브 라이브 스트리밍, TRTC 및 릴레이 라이브 스트리밍은 어떻게 다르고 서로 관련이 있습니까?
- **라이브 방송**(키워드: 1대 다수, RTMP/HLS/HTTP-FLV, CDN)
 라이브 스트리밍은 푸시 엔드, 재생 엔드 및 클라우드 라이브 스트리밍 서비스로 구성됩니다. 스트림은 범용 프로토콜 RTMP를 통해 푸시되고 CDN을 통해 배포되며 RTMP, HTTP-FLV 또는 HLS(H5용)를 포함한 프로토콜을 통해 볼 수 있습니다.
- **인터랙티브 라이브 스트리밍**(키워드: 마이크 연결, PK)
 인터랙티브 라이브 스트리밍에서 시청자는 호스트와 공동 호스트를 할 수 있고 다른 방의 호스트는 서로 경쟁할 수 있습니다.
- **TRTC**(키워드: 다중 사용자 인터랙션, UDP 기반 독점 프로토콜, 저지연)
 TRTC(Real-Time Communication)의 주요 기능은 오디오/비디오 상호작용 및 저지연 라이브 스트리밍입니다. UDP 기반 독점 프로토콜을 사용하며 대기 시간을 100ms만큼 낮게 유지할 수 있습니다. 일반적인 응용 프로그램에는 QQ 통화, VooV Meeting 및 온라인 그룹 수업이 포함됩니다. TRTC는 iOS/Android/Windows를 포함한 주류 플랫폼을 위한 솔루션을 제공하고 WebRTC와의 통신을 허용하며 클라우드에서 스트림을 혼합하고 CDN으로 중계하는 것을 지원합니다.
- **릴레이 라이브 방송**(키워드: 클라우드 혼합 스트리밍, RTC 릴레이 공유, CDN)
 중계된 라이브 스트리밍 기술은 지연 시간이 짧은 공동 호스트 룸에서 여러 스트림을 복제하고 배포 및 재생을 위해 라이브 스트리밍 CDN으로 푸시하기 전에 클라우드에서 하나의 스트림으로 혼합합니다. 

[](id:que2)

###  2대의 디바이스에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇입니까?
2대의 디바이스가 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 디바이스에서 동시에 사용할 수 없습니다.

[](id:que3)
###  CDN을 사용하여 라이브 방송 시청 시 방 안에 1명만 있을 경우 화면이 멈추고 흐릿해지는 이유는 무엇입니까?
`enterRoom`의 TRTCAppScene 매개변수를 **TRTCAppSceneLIVE**로 지정합니다.
VideoCall 모드는 영상 통화에 최적화되어 있어 방에 1명의 사용자만 있을 경우 화면이 사용자의 네트워크 트래픽을 절약하기 위해 낮은 비트 레이트와 프레임 레이트를 유지하기 때문에 화면이 멈추고 흐릿한 것처럼 느껴질 수 있습니다.

[](id:que4)
###  온라인 방에 입장할 수 없는 이유는 무엇입니까?

방 권한 제어를 활성화했기 때문입니다. 방 권한 제어 활성화 후 SDKAppID의 방은 TRTCParamEnc에서 privateMapKey를 설정해야 입장할 수 있습니다. 온라인 비즈니스를 운영하고 있으며 온라인 버전에 privateMapKey 관련 로직을 추가하지 않았을 경우 해당 기능을 활성화하지 마십시오. 자세한 내용은 [방 입장 권한 보호](https://intl.cloud.tencent.com/document/product/647/35157)를 참고하십시오.

[](id:que5)
###  TRTC 로그는 어떻게 조회합니까?
TRTC의 로그는 기본적으로 압축 암호화하여 .xlog라는 접미사가 붙어 있습니다. 로그 암호화 여부는 setLogCompressEnabled를 통해 제어할 수 있으며, 생성된 파일명에 C(compressed)가 포함되어 있으면 암호화 압축한 것이고, R(raw)이 포함되어 있으면 플레인 텍스트입니다.

- iOS 및 Mac: `sandbox의 Documents/log`
- Android:
	- 6.7 이하 버전: `/sdcard/log/tencent/liteav`.
	- 6.8-8.5 버전: `/sdcard/Android/data/패키지명/files/log/tencent/liteav/`.
	- 8.5 이후 버전: `/sdcard/Android/data/패키지명/files/log/liteav/`
- Windows:
	- 8.8 이전 버전: `%appdata%/tencent/liteav/log`
	- 8.8 또는 8.8 이후 버전: `%appdata%/liteav/log`
- Web: 브라우저 콘솔을 열거나 vConsole을 사용하여 SDK 출력 정보를 기록합니다.

  

>?
>- .xlog 파일을 조회하려면 복호화 툴을 다운로드해야 합니다. python 2.7 환경에서 툴을 xlog 파일과 동일한 디렉터리에 넣고 `python decode_mars_log_file.py`를 사용하여 실행하면 됩니다.
>- 로그 복호화 툴 다운로드 주소는 `dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`입니다.


[](id:que6)
###  10006 error가 발생합니다. 어떻게 처리해야 합니까?
"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it" 오류가 발생하는 경우 TRTC 애플리케이션의 서버 상태가 사용 가능한 상태인지 확인합니다.
**TRTC 콘솔** > **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**에 로그인하여 생성한 애플리케이션을 선택한 후 **애플리케이션 정보**를 클릭하면 애플리케이션 정보 화면에서 서버 상태를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/57e63830a368520c5e81e8e4b43d09b7.png)

[](id:que7)
###  방 입장 시 에러 코드-100018이 출력되는 이유는 무엇입니까?
UserSig 검사 실패 때문이며 다음과 같은 경우에 나타납니다.
- 매개변수 SDKAppID의 전송이 부정확한 경우. TRTC 콘솔에 로그인하여 **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**를 선택해 해당 SDKAppID를 조회할 수 있습니다.
- 매개변수 UserID에 상응하는 인증 서명 UserSig의 전송이 부정확한 경우. TRTC 콘솔에 로그인하여 **개발 지원** > **[UserSig 생성&검사](https://console.cloud.tencent.com/trtc/usersigtool)**를 선택해 UserSig를 검사합니다.


[](id:que8)
###  크로스 룸 마이크 연결(호스트 PK)은 어떻게 해야 합니까?
connectOtherRoom 인터페이스를 사용할 수 있습니다. 호스트는 connectOtherRoom()을 호출한 후 onConnectOtherRoom 콜백을 통해 크로스 룸 PK 결과를 획득할 수 있습니다. 호스트 1이 속한 방 안에 있는 모든 사람은 onUserEnter 콜백을 통해 호스트 2가 방에 입장했다는 공지를 확인할 수 있습니다. 호스트 2가 속한 방의 모든 사람도 onUserEnter 콜백을 통해 호스트 1의 방 입장 공지를 확인합니다.

[](id:que10)
###  방 나가기 인터페이스 exitRoom()을 반드시 호출해야 합니까?
방 입장 성공 여부에 상관없이 enterRoom은 exitRoom과 함께 사용되어야 합니다. exitRoom 호출 전 다시 enterRoom 함수를 호출하면 예상치 못한 오류가 발생할 수 있습니다.


[](id:que16)
###  릴레이 녹화된 시나리오에서 생성된 녹화 파일의 포맷은 어떻게 됩니까?  
[TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 설정한 녹화 파일 포맷을 기준으로 합니다.


[](id:que20)
###  멀티미디어 통화가 푸시 스트리밍에 성공했는지 어떻게 판단합니까?
onSendFirstLocalVideoFrame 콜백을 통해 enterRoom 및 startLocalPreview 성공 후 카메라 캡처를 시작하며, 캡처한 화면에 대한 코딩을 진행합니다. SDK에서는 클라우드에 첫 번째 프레임 비디오 데이터 발송 성공 후 해당 콜백 이벤트를 제거합니다.

[](id:que21)
###  음성 통화가 푸시 스트리밍에 성공했는지 어떻게 판단합니까?
onSendFirstLocalAudioFrame 콜백을 통해 enterRoom및 startLocalPreview 성공 후 마이크 캡처를 시작하며, 캡처한 음성에 대한 코딩을 진행합니다. SDK에서는 클라우드에 첫 번째 프레임 음성 데이터 발송 성공 후 해당 콜백 이벤트를 제거합니다.

[](id:que22)
###  모든 UserID를 조회할 수 있습니까?
모든 UserID 통계를 지원하지 않고 있습니다. 클라이언트에서 사용자 계정 등록 성공 후 사용자 정보는 SQL에 기록되어 관리 및 조회할 수 있습니다.


[](id:que23)
###  동일 UserID로 동시에 여러 개 방에 들어갈 수 있습니까?
TRTC에서는 2개의 동일한 userID로 동시에 방에 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.

[](id:que24)
###  setAudioRoute를 호출하여 음성 라우팅(헤드폰/스피커)을 설정했는데 적용되지 않는 이유는 무엇입니까? 
통화 음량 모드에서만 헤드폰/스피커를 전환할 수 있습니다. 즉, 2명 이상의 사용자가 마이크를 연결한 경우 호출해야 적용됩니다.


[](id:que25)
###  TRTC는 Tencent Cloud 콘솔에서만 자동 녹화를 활성화할 수 있습니까? 수동 녹화 활성화는 어떻게 합니까?
TRTC는 수동 녹화를 지원합니다. 구체적인 작업 방법은 다음과 같습니다.
1. **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)** > **기능 설정**에서 **자동 릴레이 푸시 스트리밍**을 활성화하고 **클라우드 녹화 실행**을 비활성화합니다.
2. 사용자는 방에 입장한 후 스트리밍 ID에 따라 규칙을 생성하고 userid에 상응하는 streamid를 산출합니다.
3. CSS의 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 사용하여 streamid에 대한 녹화 작업을 실행합니다.
 - DomainName은 `[bizid].livepush.myqcloud.com`입니다.
 - AppName은 `trtc_[sdkappid]`입니다.
 - StreamName은 `streamid`입니다.
4. 녹화 작업 완료 후 CSS는 파일을 VOD에 입력하며 [녹화 콜백 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38080)을 통과합니다.

[](id:que26)
###  TRTC에서 생성된 UserSig가 정확한지 어떻게 검사합니까? 방 입장 시 -3319, -3320 오류가 보고되었는데 어떻게 해결합니까? 
TRTC 콘솔에 로그인하여 **개발 지원>[UserSig 생성&검사](https://console.cloud.tencent.com/trtc/usersigtool)**를 선택해 UserSig를 검사합니다.

[](id:que27)
###  TRTC에서 통화 시간과 사용량은 어떻게 확인합니까? 
TRTC 콘솔의 **[사용량 통계](https://console.cloud.tencent.com/trtc/statistics)** 페이지에서 확인할 수 있습니다.

[](id:que28)
###  TRTC에서 어떻게 사용자 리스트를 점검하여 라이브 룸 시청자 수에 대한 통계를 진행합니까?  
개발자 프로젝트에 통합 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)이 있을 경우 IM 그룹 인원수 통계 인터페이스를 통해 통계를 낼 수 있습니다. 그러나 이 방법은 정확도가 떨어지므로 접속자 수에 대한 개발자의 요구 사항이 높지 않을 경우 사용하는 것이 좋습니다.
개발자가 접속자 수에 대한 정확한 통계를 원할 경우 자체적으로 통계 로직을 실행하는 것을 권장합니다.
1. 시청자 수 증가(Client -> Server) 신규 시청자가 들어왔을 경우 방의 시청자 수가 +1 되어야 한다는 의미로 앱의 시청자 측에서는 방 입장 시 Server에 누적 요청을 1회 발송합니다.
2. 시청자 수 감소(Client -> Server) 시청자가 방에서 나갔을 경우 방의 시청자 수가 -1 되어야 한다는 의미로 앱의 시청자 측에서는 방에서 나갈 시 Server에 차감 요청을 1회 발송합니다.

[](id:que29)
###  방 입장 시 -100013 오류 코드가 보고되며, ERR_SERVER_INFO_SERVICE_SUSPENDED라는 오류 메시지가 뜨는데 이유가 무엇입니까?  
해당 오류는 서비스를 이용할 수 없을 경우 나타납니다. 다음 내용을 확인해 보십시오.
- 패키지의 남은 분 수가 0보다 큽니까?
- Tencent Cloud 계정이 연체되었습니까?

[](id:que33)
###  TRTC에서 클라운드 녹화를 실행했으나 녹화 파일이 생성되지 않은 경우 어떻게 해결합니까?
1.  [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 **자동 릴레이 푸시 스트리밍**과 **클라우드 녹화 실행**을 활성화합니다.
2. TRTC 방에서 사용자 멀티미디어 데이터가 정상적으로 업스트림되어야 녹화가 시작됩니다.
3. 릴레이 CDN 풀 스트리밍이 정상이어야 녹화 파일이 생성됩니다.
4. 시작할 때 오디오만 있다가 도중에 비디오로 전환되었을 경우 녹화 템플릿이 달라 비디오 시간대의 녹화 파일만이 생성되었거나 오디오 시간대의 녹화 파일만 생성되었을 수 있습니다.

[](id:que36)
###  게스트 초대 연결 시 게스트에게 방 번호는 어떻게 알립니까?
사용자 정의 메시지를 통해 게스트에게 방 번호를 공지하고, 메시지를 리졸브하여 roomid를 획득합니다. 자세한 내용은 [Creating a custom message](https://intl.cloud.tencent.com/document/product/1047/34322), [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391)를 참고하십시오.

[](id:que37)
###  2인 이상 방에 입장한 후 녹음을 시작할 수 있습니까?
가능합니다. 혼합 스트리밍 녹음 후의 오디오 데이터를 획득하고자 할 경우 [혼합 스트림 실행](https://intl.cloud.tencent.com/document/product/647/34618) 후 출력 스트리밍 ID를 만들어 라이브 방송 인터페이스 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 호출할 수 있습니다.

 [](id:que38)
###  Windows에서 공유된 애플리케이션의 재생 오디오를 어떻게 수집합니까?
[startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) 인터페이스를 호출하여 시스템 오디오 수집을 활성화할 수 있습니다.

[](id:que39)
### Windows 회의 모드에서 호스트가 시청자에게 멀티미디어 연결 기능을 시작하려면 어떻게 해야 합니까?
다른 클라우드 서비스와 연결이 필요한 경우 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/33996)에서 연결을 요청해야 합니다.

호출의 대략적인 로직은 다음과 같습니다. A가 B에게 사용자 정의 메시지 X를 발송하고 호출 페이지 알람을 설정하면 X 출력 효과를 자체적으로 처리하고 B는 X를 받은 후 호출된 페이지를 호출합니다. B가 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)을 클릭하여 방에 입장하고 사용자 정의 정보 X1을 A에게 발송하면 A가 X1(출력 여부 자체 결정)을 수신하고 동시에 enterRoom을 호출하여 방으로 들어가고 IM으로 사용자 정의 정보를 발송합니다.

[](id:que40)
###  시청자가 어떻게 방 안에 있는 연결 화면을 볼 수 있습니까?
시청자가 라이브 방송 모드를 사용하는 경우, 방 안으로 들어가 TRTCCloudDelegate의 onUserVideoAvailable 콜백을 통해 호스트의 userid(마이크 연결한 사람도 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)으로 방에 들어갈 수 있으며, 시청자에게는 해당 사용자가 호스트가 됨)를 알 수 있습니다. 그리고 시청자는 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9)를 호출해 호스트의 비디오 화면을 볼 수 있습니다.
자세한 작업 방법은 [라이브 방송 모드 실행(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)을 참고하십시오.

[](id:que41)
### TRTC에 Linux SDK가 있습니까?
Linux SDK는 현재 지원하지 않습니다. 서비스 관련 문의사항은 colleenyu@tencent.com으로 연락주시기 바랍니다.

[](id:que42)
### TRTC는 영상 통화 또는 인터랙션 라이브 스트리밍 중 화면 공유를 지원합니까?
지원합니다. 영상 통화 또는 인터랙티브 라이브 스트리밍 중에 카메라에서 캡처한 비디오가 기본 스트림으로 게시됩니다. 화면을 하위 스트림으로 게시할 수도 있습니다. 공유 화면에는 영상 통화 또는 인터랙티브 라이브 스트리밍 창이 포함됩니다.
