[](id:que1)
###  라이브 방송, ILVB, TRTC, 릴레이 라이브 방송에는 어떤 차이와 관계가 있습니까?
- 라이브 방송(키워드: 일 대 다수, RTMP/HLS/HTTP-FLV，CDN）
 라이브 방송은 푸시 스트리밍, 재생, 라이브 방송 클라우드 서비스로 나뉘며, 클라우드 서비스는 CDN을 사용해 라이브 방송 스트리밍을 배포합니다. 푸시 스트리밍은 범용 표준 프로토콜 RTMP를 사용해 CDN을 거쳐 배포한 후 재생 시 일반적으로 RTMP, HTTP-FLV 또는 HLS(H5 지원) 등의 방식을 선택하여 시청할 수 있습니다.
- ILVB(키워드: 마이크 연결, PK)
 ILVB는 일종의 비즈니스 형태로, 호스트와 시청자 사이에서 인터랙션 마이크를 연결하고, 호스트와 호스트 사이에서 인터랙션 PK를 진행하는 일종의 라이브 방송 형태입니다.
- TRTC(키워드: 다중 사용자 인터랙션, UDP 사유 프로토콜, 저지연)
 TRTC(Real-Time Communication, TRTC)의 주요 응용 시나리오는 멀티미디어 인터랙션과 저딜레이 라이브 방송이며, UDP 기반의 사유 프로토콜을 사용하여 딜레이가 100ms까지 낮아집니다. 전형적인 시나리오로는 QQ 전화, VooV Meeting, 대규모 수업 등이 있습니다. Tencent Cloud TRTC는 전 플랫폼을 커버하며 iOS/Android/Windows 이외에 미니프로그램, WebRTC 통신을 지원하고 클라우드 혼합 스트리밍 방식을 통해 릴레이 라이브 방송 화면을 CDN으로 전달합니다.
- 릴레이 라이브 방송(키워드: 클라우드 혼합 스트리밍, RTC 릴레이 공유，CDN)
 릴레이 라이브 방송은 저지연 마이크 연결 방 안의 여러 채널의 푸시 스트리밍 화면을 복사하여 클라우드에서 화면을 한 채널로 통합하고, 혼합 스트리밍 후의 화면을 라이브 방송 CDN으로 푸시 스트리밍하여 배포 재생하는 기술입니다. 


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
 - 6.7 및 이전 버전: `/sdcard/log/tencent/liteav`
 - 6.8 이후 버전: `/sdcard/Android/data/패키지명/files/log/tencent/liteav/`
- Windows: `%appdata%/tencent/liteav/log`
- 웹: 브라우저 콘솔을 열거나 vConsole을 사용하여 SDK 출력 정보를 기록합니다.
- 미니프로그램: &lt;live-pusher&gt;와 &lt;live-player&gt; 태그의 debug Attribute를 활성화하고 vConsole을 사용하여 출력 정보를 기록합니다.

>?
>- .xlog 파일을 조회하려면 복호화 툴을 다운로드해야 합니다. python 2.7 환경에서 툴을 xlog 파일과 동일한 디렉터리에 넣고 `python decode_mars_log_file.py`를 사용하여 실행하면 됩니다.
>- 로그 복호화 툴 다운로드 주소는 `dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`입니다.


[](id:que6)
###  10006 error가 발생합니다. 어떻게 처리해야 합니까?
"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it" 오류가 발생하는 경우 TRTC 애플리케이션의 서버 상태가 사용 가능한 상태인지 확인합니다.
**TRTC 콘솔**>**[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**에 로그인하여 생성한 애플리케이션을 선택한 후 **애플리케이션 정보**를 클릭하면 애플리케이션 정보 화면에서 서버 상태를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/57e63830a368520c5e81e8e4b43d09b7.png)

[](id:que7)
###  방 입장 시 에러 코드-100018이 출력되는 이유는 무엇입니까?
UserSig 인증 실패 때문이며 다음과 같은 경우에 나타납니다.
- 매개변수 SDKAppID의 전송이 부정확한 경우. TRTC 콘솔에 로그인하여 **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**를 선택해 해당 SDKAppID를 조회할 수 있습니다.
- 매개변수 UserID에 상응하는 인증 서명 UserSig의 전송이 부정확한 경우. TRTC 콘솔에 로그인하여 **개발 지원**>**[UserSig 생성&검증](https://console.cloud.tencent.com/trtc/usersigtool)**을 선택해 UserSig를 인증합니다.


[](id:que8)
### 크로스 룸 마이크 연결(호스트 PK)은 어떻게 해야 합니까?
connectOtherRoom 인터페이스를 사용할 수 있습니다. 호스트는 connectOtherRoom()을 호출한 후 onConnectOtherRoom 콜백을 통해 크로스 룸 PK 결과를 획득할 수 있습니다. 호스트 1이 속한 방 안에 있는 모든 사람은 onUserEnter 콜백을 통해 호스트 2가 방에 입장했다는 공지를 확인할 수 있습니다. 호스트 2가 속한 방의 모든 사람도 onUserEnter 콜백을 통해 호스트 1의 방 입장 공지를 확인합니다.

[](id:que9)
###  디바이스 카메라 또는 마이크의 점용이 확인되는 등 이상 현상이 나타나는 이유는 무엇입니까?
exitRoom() 인터페이스를 호출하면 방 나가기 관련 로직이 실행됩니다. 예를 들어 멀티미디어 디바이스 리소스 및 코덱 리소스 릴리스 등의 하드웨어 디바이스의 릴리스는 비동기화 작업이며, SDK는 리소스 릴리스 완료 후 TRTCCloudListener의 onExitRoom() 콜백을 통해 어퍼 클래스에 알립니다. enterRoom()을 다시 호출하거나 기타 멀티미디어 SDK로 전환하려면, onExitRoom()의 콜백 이후 다시 관련 작업을 진행할 수 있습니다.

[](id:que10)
###  방 나가기 인터페이스 exitRoom()을 반드시 호출해야 합니까?
방 입장 성공 여부에 상관없이 enterRoom은 exitRoom과 함께 사용되어야 합니다. exitRoom 호출 전 다시 enterRoom 함수를 호출하면 예상치 못한 오류가 발생할 수 있습니다.

[](id:que11)
###  TRTC 비디오 화면에 검은 띠가 나타났습니다. 어떻게 제거합니까?
TRTCVideoFillMode_Fill(채우기)을 설정하면 됩니다. TRTC 비디오 렌더링 모드는 채우기와 적용으로 나뉘며, 로컬 렌더링 화면은 setLocalViewFillMode()를 통해 설정할 수 있습니다. 원격 렌더링 화면은 setRemoteViewFillMode를 통해 설정할 수 있습니다.
- TRTCVideoFillMode_Fill: 이미지 전체 화면. 윈도우를 초과한 비디오 부분이 잘려 나가 화면이 완전히 표시되지 않을 수 있습니다.
- TRTCVideoFillMode_Fit: 이미지 긴 변 전체 화면. 짧은 변 부분이 검은색으로 채워지며 화면은 완전히 표시됩니다.

[](id:que12)
###  TRTC에서 로컬 화면과 원격 화면의 좌우가 상반됩니까?
로컬 기본 캡처 화면은 이미지입니다. 앱에서 [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) 인터페이스를 통해 설정할 수 있으며, 해당 인터페이스는 로컬 카메라 미리보기 화면의 이미지 모드만을 변경합니다. 또한 setVideoEncoderMirror 인터페이스를 통해 인코더에서 출력된 화면 이미지 모드를 설정할 수 있으며, 해당 인터페이스는 로컬 카메라의 미리보기 화면은 변경하지 않습니다. 단, 사용자가 보게 되는 (및 서버 녹화) 화면 효과는 변경합니다. 웹에서는 [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) 인터페이스를 통해 mirror 매개변수를 수정하여 설정할 수 있습니다. 


[](id:que13)
###  TRTC에서 비디오 코딩 출력 방향을 설정했는데 적용되지 않은 이유는 무엇입니까?
setGSensorMode()를 TRTCGSensorMode_Disable로 설정하고 중력 센서를 차단해야 합니다. 그렇지 않으면 setVideoEncoderRotation 호출 후 원격 사용자가 보게 되는 화면이 변하지 않습니다.

[](id:que14)
###   TRTC의 통화와 동시에 VOD 플레이어 TXVodPlayer를 사용하여 재생했는데 소리가 작은 이유는 무엇입니까?
setSystemVolumeType 인터페이스를 통해 통화 시 사용하는 시스템 음량 유형을 설정합니다. 미디어 음량 모드 TRTCSystemVolumeTypeMedia로 설정하면 해결됩니다.

[](id:que15)
###  TRTC에 정상적인 업스트림 데이터가 있는데 릴레이 풀 스트리밍에 실패하며 화면이 보이지 않는 이유는 무엇입니까?	
**[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**>**기능 설정**에서 자동 릴레이 푸시 스트리밍을 활성화했는지 확인합니다.


[](id:que16)
###  릴레이 녹화된 시나리오에서 생성된 녹화 파일의 포맷은 어떻게 됩니까?	
[TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 설정한 녹화 파일 포맷을 기준으로 합니다.

[](id:que17)
###  미디어 음량과 통화 음량은 어떻게 선택합니까?
setSystemVolumeType 인터페이스를 통해 통화 음량 및 미디어 음량을 선택할 수 있습니다.
- TRTCAudioVolumeTypeAuto: 기본 유형, 마이크 연결 통화 음량, 마이크 꺼짐 미디어 음량.
- TRTCAudioVolumeTypeVOIP: 통화 음량 사용
- TRTCAudioVolumeTypeMedia: 미디어 음량 사용

[](id:que18)
###  카메라 작동에 성공했는지 어떻게 판단합니까?
onCameraDidReady 콜백을 통해 콜백이 수신되면 카메라 준비가 완료되었다는 것을 의미합니다.

[](id:que19)
###  마이크 작동에 성공했는지 어떻게 판단합니까?
onMicDidReady 콜백을 통해 콜백이 수신되면 마이크 준비가 완료되었다는 것을 의미합니다.

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
1. **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**>**기능 설정**에서 **자동 릴레이 푸시 스트리밍**을 활성화하고 **클라우드 녹화 실행**을 비활성화합니다.
2. 사용자는 방에 입장한 후 스트리밍 ID에 따라 규칙을 생성하고 userid에 상응하는 streamid를 산출합니다.
3. LVB의 [녹화 작업 생성 API](https://intl.cloud.tencent.com/document/product/267/37309)를 사용하여 streamid에 대한 녹화 작업을 실행합니다.
 - DomainName은 `[bizid].livepush.myqcloud.com`입니다.
 - AppName은 `trtc_[sdkappid]`입니다.
 - StreamName은 `streamid`입니다.
4. 녹화 작업 완료 후 LVB는 파일을 VOD에 입력하며 [녹화 콜백 이벤트 공지](https://intl.cloud.tencent.com/document/product/267/38080)를 통과합니다.

[](id:que26)
###  TRTC에서 생성된 UserSig가 정확한지 어떻게 인증합니까? 방 입장 시 -3319, -3320 오류가 보고되었는데 어떻게 해결합니까?	
TRTC 콘솔에 로그인하여 **개발 지원**>**[UserSig 생성&검증](https://console.cloud.tencent.com/trtc/usersigtool)**을 선택해 UserSig를 인증합니다.

[](id:que27)
###  TRTC에서 통화 시간과 사용량은 어떻게 확인합니까?	
TRTC 콘솔의 **[사용량 통계](https://console.cloud.tencent.com/trtc/statistics)** 페이지에서 확인할 수 있습니다.

[](id:que28)
### TRTC에서 어떻게 사용자 리스트를 점검하여 라이브 룸 시청자 수에 대한 통계를 진행합니까?	
개발자 프로젝트에 통합 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)이 있을 경우 IM 그룹 인원수 통계 인터페이스를 통해 통계를 낼 수 있습니다. 그러나 이 방법은 정확도가 떨어지므로 접속자 수에 대한 개발자의 요구 사항이 높지 않을 경우 사용하는 것이 좋습니다.
개발자가 접속자 수에 대한 정확한 통계를 원할 경우 자체적으로 통계 로직을 실행하는 것을 권장합니다.
1. 시청자 수 증가(Client -> Server) 신규 시청자가 들어왔을 경우 방의 시청자 수가 +1 되어야 한다는 의미로 앱의 시청자 측에서는 방 입장 시 Server에 누적 요청을 1회 발송합니다.
2. 시청자 수 감소(Client -> Server) 시청자가 방에서 나갔을 경우 방의 시청자 수가 -1 되어야 한다는 의미로 앱의 시청자 측에서는 방에서 나갈 시 Server에 차감 요청을 1회 발송합니다.

[](id:que29)
###  방 입장 시 -100013 오류 코드가 보고되며, ERR_SERVER_INFO_SERVICE_SUSPENDED라는 오류 메시지가 뜨는데 이유가 무엇입니까?	
해당 오류는 서비스를 이용할 수 없을 경우 나타납니다. 다음 내용을 확인해 보십시오.
- 패키지의 남은 분 수가 0보다 큽니까?
- Tencent Cloud 계정이 연체되었습니까?

[](id:que30)
###  TRTC는 어떻게 네트워크 상태를 모니터링하여 신호 강약 표시 기능을 나타냅니까? 	
onNetworkQuality()를 사용하여 현재 네트워크의 업스트림과 다운스트림 품질을 리슨할 수 있습니다. [공식 Demo](https://github.com/tencentyun/TRTCSDK)를 참고하여 신호 강도 기능을 실행하십시오.

[](id:que31)
###  TRTC에서 사용하고 있는 것이 신규 mcu 혼합 스트리밍인지 아니면 기존 클라우드 혼합 스트리밍인지 어떻게 알 수 있습니까?
다음 조건을 만족하며 클라이언트 로그에 mcumix = 1이라고 출력되면 사용 스트리밍은 신규 mcu 혼합 스트리밍입니다.
- 2020년 01월 09일 및 이후 생성된 애플리케이션
- TRTC SDK 6.9 이후 버전

[](id:que32)
###  TRTC에서 혼합 스트리밍 인터페이스 호출에 실패할 경우 어떻게 해결합니까?
1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 **자동 릴레이 푸시 스트리밍**을 활성화해야 합니다.
2. onSetMixTranscodingConfig() 인터페이스를 리슨하고 리턴된 오류 정보에 따라 수정합니다.
3. SDK 인터페이스를 통해 릴레이 스트리밍 ID를 사용자 정의하면 기존 클라우드 혼합 스트리밍 방식은 혼합 스트리밍에 실패합니다.
4. onSetMixTranscodingConfig() 리턴에 성공하나 릴레이 CDN 풀 스트리밍이 되지 않는다면 재생 도메인을 설정하지 않았기 때문입니다. 재생 도메인 관련 설정을 확인해 보십시오.

[](id:que33)
###  TRTC에서 클라운드 녹화를 실행했으나 녹화 파일이 생성되지 않은 경우 어떻게 해결합니까?
1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 **자동 릴레이 푸시 스트리밍**과 **클라우드 녹화 실행**을 활성화합니다.
2. TRTC 방에서 사용자 멀티미디어 데이터가 정상적으로 업스트림되어야 녹화가 시작됩니다.
3. 릴레이 CDN 풀 스트리밍이 정상이어야 녹화 파일이 생성됩니다.
4. 시작할 때 오디오만 있다가 도중에 비디오로 전환되었을 경우 녹화 템플릿이 달라 비디오 시간대의 녹화 파일만이 생성되었거나 오디오 시간대의 녹화 파일만 생성되었을 수 있습니다.

[](id:que34)
###  TRTC에 랙이 발생하면 어떻게 해결해야 합니까?
TRTC 콘솔의 **[모니터링 대시보드](https://console.cloud.tencent.com/trtc/monitor)** 페이지에서 ​해당 RoomID, UserID를 통해 통화 품질을 확인할 수 있습니다.
- 수신자 시점에서 발신자와 수신자의 상황을 확인합니다.
- 발신자와 수신자의 패킷 손실률이 높은지 확인합니다. 패킷 손실률이 너무 높은 경우 일반적으로 네트워크가 불안정하여 랙이 발생합니다.
- 프레임 레이트와 CPU 이용률을 확인합니다. 프레임 레이트가 낮거나 CPU 이용률이 너무 높은 경우 랙 현상이 발생합니다.

[](id:que35)
###  TRTC 화질이 좋지 않습니다. 흐릿하고 모자이크 현상 등이 발생합니다. 어떻게 해결해야 합니까?
- 해상도는 주로 비트 레이트와 관련이 있습니다. SDK 비트 레이트가 낮게 설정되어 있는지 확인하십시오. 해상도가 높은데 비트 레이트가 낮은 경우 모자이크 현상이 쉽게 나타날 수 있습니다.
- TRTC는 클라우드 QOS 트래픽 제어 정책을 통해 네트워크 상태에 따라 비트 레이트와 해상도를 동적으로 조정합니다. 네트워크 상태가 좋지 않은 경우 비트 레이트가 낮아져 해상도가 떨어질 수 있습니다.
- 방 입장 시 사용한 VideoCall 모드가 Live 모드인지 확인합니다. 통화 VideoCall 모드는 저지연와 원활한 통화에 중점을 두므로 네트워크가 약한 경우 화질을 포기하고 원활한 통화 상태를 확보합니다. 화질이 더 중요한 경우 Live 모드 사용을 권장합니다.


[](id:que36)
###  게스트 초대 연결 시 게스트에게 방 번호는 어떻게 알립니까?
사용자 정의 메시지를 통해 게스트에게 방 번호를 공지하고, 메시지를 리졸브하여 roomid를 획득합니다. 자세한 내용은 [사용자 정의 메시지 생성](https://intl.cloud.tencent.com/document/product/1047/34322), [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391)를 참고하십시오.

[](id:que37)
###  2인 이상 방에 입장한 후 녹음을 시작할 수 있습니까?
가능합니다. 혼합 스트리밍 녹음 후의 오디오 데이터를 획득하고자 할 경우 [클라우드 혼합 스트리밍 실행](https://intl.cloud.tencent.com/document/product/647/34618) 후 출력 스트리밍 ID를 만들어 라이브 방송 인터페이스 [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/37309)을 호출할 수 있습니다.

 [](id:que38)
### Windows에서 공유된 애플리케이션의 재생 소리를 어떻게 캡처합니까?
[startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) 인터페이스를 호출하여 시스템 음량 수집을 활성화할 수 있습니다.

[](id:que39)
### Windows 회의 모드에서 호스트가 시청자에게 멀티미디어 연결 기능을 시작하려면 어떻게 해야 합니까?
다른 클라우드 서비스와 연결이 필요한 경우 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/33996)에서 연결을 요청해야 합니다.

호출의 대략적인 로직은 다음과 같습니다. A가 B에게 사용자 정의 메시지 X를 발송하고 호출 페이지 알람을 설정하면 X 출력 효과를 자체적으로 처리하고 B는 X를 받은 후 호출된 페이지를 호출합니다. B가 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)을 클릭하여 방에 입장하고 사용자 정의 정보 X1을 A에게 발송하면 A가 X1(출력 여부 자체 결정)을 수신하고 동시에 enterRoom을 호출하여 방으로 들어가고 IM으로 사용자 정의 정보를 발송합니다.

[](id:que40)
### 시청자가 어떻게 방 안에 있는 연결 화면을 볼 수 있나요?
시청자가 라이브 방송 모드를 사용하는 경우, 방 안으로 들어가 TRTCCloudDelegate의 [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) 콜백을 통해 호스트의 userid(마이크 연결한 사람도 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)으로 방에 들어갈 수 있으며, 시청자에게는 해당 사용자가 호스트가 됨)를 알 수 있습니다. 그리고 시청자는 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9)를 호출해 호스트의 비디오 화면을 볼 수 있습니다.
자세한 작업 방법은 [라이브 방송 모드 실행(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)을 참고하십시오.

