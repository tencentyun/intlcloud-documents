[](id:que1)
### TRTC RoomID는 무엇입니까? 값의 범위는 어떻게 됩니까?
RoomID는 방을 고유하게 식별하며 범위는 1 - 4294967295입니다. 애플리케이션의 방 ID를 유지 관리하고 할당해야 합니다.

[](id:que2)
### TRTC에서 UserID는 무엇입니까? 값 범위는 무엇입니까? 
UserID는TRTC 애플리케이션에서 사용자를 고유하게 식별합니다. 영어 알파벳(대소문자 구분), 숫자, 언더바를 포함할 수 있으며 32바이트 이하가 바람직합니다.


[](id:que3)
### TRTC 방의 라이프사이클은 어떻게 됩니까?
- 방에 가장 먼저 입장하는 사용자는 방의 소유자지만, 방 소유자는 수동으로 방을 닫을 수 없습니다.
- **통화 모드**에서 TRTC는 모든 사용자가 방을 나갈 때 방을 닫습니다.
- **라이브 스트리밍 모드**에서 방을 나간 마지막 사용자가 앵커인 경우 TRTC는 즉시 방을 닫습니다. 사용자가 시청자인 경우 TRTC는 10분 후에 방을 닫습니다.
- 사용자는 예기치 않은 연결 해제가 발생한 후 90초 후에 방에서 퇴장됩니다. 모든 사용자의 연결이 끊어지면 90초 후에 방이 닫힙니다. **연결이 끊긴 후 대기 시간도 청구됩니다**.
- 사용자가 존재하지 않는 방에 입장을 시도하면 TRTC는 입력된 ID로 자동으로 방을 생성합니다.

[](id:que4)
### 사용자는 오디오/비디오 스트림을 구독할 수 없습니까? 
‘즉시 스트리밍’을 활성화하기 위해 TRTC는 기본적으로 방 입장 시 사용자에게 오디오/비디오 스트림을 구독합니다. setDefaultStreamRecvMode API를 호출하여 수동 구독 모드로 전환할 수 있습니다.

[](id:que5)
### TRTC에서 CDN으로 중계할 스트림 ID를 지정할 수 있나요?  
예. enterRoom의 TRTCParams를 통해 streamId를 지정하거나, startPublishing API를 호출하여 streamId를 전달할 수 있습니다.

[](id:que6)
### TRTC 라이브 방송은 어떤 역할을 지원하며, 어떤 차이가 있습니까?
라이브 스트리밍 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)는 TRTCRoleAnchor(앵커)와 TRTCRoleAudience(시청자)의 두 가지 역할을 지원합니다. 앵커는 오디오/비디오 데이터를 보내고 받을 수 있지만 시청자는 다른 사람의 데이터만 받고 재생할 수 있습니다. switchRole()을 호출하여 역할을 전환할 수 있습니다.

[](id:que7)
### TRTC의 역할(Role)은 무엇입니까? 
TRTC에서 역할(앵커 및 시청자)은 라이브 스트리밍 시나리오에서만 적용할 수 있습니다. 동시에 50명의 사용자에게 할당할 수 있는 앵커 역할(TRTCRoleAnchor)은 오디오/비디오를 보내고 받을 수 있습니다. 동시에 10만명의 사용자에게 할당할 수 있는 시청자 역할(TRTCRoleAudience)은 오디오/비디오만 수신할 수 있습니다.


[](id:que8)
### TRTC 회의실에서 지원되는 애플리케이션 시나리오는 무엇입니까?  
다음 애플리케이션 시나리오가 지원됩니다.
- TRTCAppSceneVideoCall: 화상 통화 시나리오는 일대일 화상 통화, 최대 300명까지 참여하는 화상 회의, 온라인 의료 상담, 화상 채팅 및 화상 인터뷰에 적합합니다.
- TRTCAppSceneLIVE: 인터랙션 비디오 스트리밍 시나리오는 대기 시간이 짧은 라이브 비디오 스트리밍, 최대 10만명의 참가자를 위한 인터랙션 교실, 라이브 비디오 경쟁, 비디오 데이트, 원격 교육 및 대규모 회의에 적합합니다.
- TRTCAppSceneAudioCall: 음성 통화 시나리오는 일대일 음성 통화, 최대 300명이 참여할 수 있는 음성 회의, 음성 채팅 및 온라인 늑대인간 플레이에 적합합니다.
- TRTCAppSceneVoiceChatRoom: 인터랙션 오디오 스트리밍 시나리오는 저지연 오디오 스트리밍, 라이브 오디오 공동 앵커링, 오디오 채팅방, 노래방 및 라디오에 적합합니다.


[](id:que9)
### TRTC에서 지원하는 플랫폼에는 어떤 것이 있습니까?
iOS, Android, Windows(C++), Unity, Mac, Web, Electron 등의 플랫폼을 지원합니다. 자세한 내용은 [플랫폼 지원](https://intl.cloud.tencent.com/document/product/647/35078)을 참고하십시오.

[](id:que10)
### TRTC 라이트 버전과 TRTC 프로 버전의 차이점은 무엇입니까? 
자세한 내용은 [버전 비교](https://intl.cloud.tencent.com/document/product/647/34615)를 참고하십시오.


[](id:que11)
### TRTC는 라이브 스트리밍 중 공동 앵커링을 지원합니까?
지원합니다. 운영 가이드를 참고하십시오.
- [라이브 방송 모드 실행(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35107)
- [라이브 방송 모드 실행(Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [라이브 방송 모드 실행(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [라이브 방송 모드 실행(Electron)](https://intl.cloud.tencent.com/document/product/647/36070)
- [라이브 스트리밍 모드 실행(Web)](https://intl.cloud.tencent.com/document/product/647/35110)


[](id:que12)
### TRTC는 동시에 최대 몇 개의 방을 생성할 수 있습니까?
동시에 4294967294개의 방이 존재할 수 있으며, 누적 방 수량에는 제한이 없습니다.

[](id:que13)
### 방은 어떻게 생성합니까?
방은 사용자가 방에 들어갈 때 TRTC에 의해 자동으로 생성됩니다. 따라서 수동으로 방을 만들 필요가 없습니다. ‘방 입장’을 위해 클라이언트 API를 호출하기만 하면 됩니다.
- [iOS & Mac > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- Windows（C++） > enterRoom
- [Windows（C#） > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afbb3a1e6f73f339d47368a7d620a995f)
- [Electron > enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)
- [Web > join](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)

[](id:que14)
### TRTC의 비디오 서버는 대역폭을 최대 얼마까지 지원합니까?
제한이 없습니다.


[](id:que15)
### TRTC는 프라이빗 배포를 지원합니까?
TRTC 프라이빗 배포는 현재 지원하지 않습니다. 서비스 사용 관련 문의사항은 colleenyu@tencent.com으로 연락주시기 바랍니다. 
프라이빗 클라이언트 제한 사항: 네이티브 SDK(iOS, Mac, Android 및 Windows), WebRTC는 지원되며, 미니프로그램은 지원되지 않습니다.

[](id:que16)
### TRTC에서 CDN으로 릴레이를 활성화하려면 도메인 이름을 ICP 비안 번호로 등록해야 합니까?
예, 관련 규정에 따라 재생 도메인을 등록해야 합니다.

[](id:que17)
### TRTC의 평균 지연 시간은 얼마입니까?
전 세계 TRTC의 평균 end to end 지연은 300ms 미만입니다.

[](id:que18)
### TRTC는 액티브 콜 기능을 지원합니까?
신호 채널을 사용하여 이 기능을 활성화할 수 있습니다. 예를 들어 [Instant Messaging](https://intl.cloud.tencent.com/product/im)의 사용자 정의 메시지 기능을 사용하여 활성 통화를 활성화할 수 있습니다. 자세한 내용은 [SDK](https://intl.cloud.tencent.com/document/product/647/34615) 소스 코드의 시나리오별 Demo를 참고하십시오.

[](id:que19)
### TRTC에서 일대일 영상통화를 할 때 블루투스 이어폰을 사용할 수 있나요?
예, 사용할 수 있습니다.

[](id:que21)
### TRTC는 PC에서 화면 공유를 지원합니까?
예, 지원합니다. 자세한 내용은 다음 문서를 참고하십시오.
- [실시간 화면 공유(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [실시간 화면 공유(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [실시간 화면 공유(Web)](https://intl.cloud.tencent.com/document/product/647/35163)

화면 공유 API에 대한 자세한 내용은 [Windows(C++) API](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오. 또한, [Electron API](https://intl.cloud.tencent.com/document/product/647/35141)를 사용할 수도 있습니다.

[](id:que23)
### TRTC에서 로컬 비디오 파일을 공유할 수 있습니까?

지원합니다. [사용자 정의 컬렉션 및 렌더링](https://intl.cloud.tencent.com/document/product/647/35158) 기능을 사용하여 이를 달성할 수 있습니다.

[](id:que24)
### 라이브 스트리밍 세션을 녹화하고 녹화 파일을 휴대폰에 로컬로 저장할 수 있습니까?
녹화 파일은 휴대폰에 직접 저장할 수 없습니다. 녹화 파일은 VOD로 저장됩니다. VOD에서 다운로드하여 휴대폰에 저장할 수 있습니다.


[](id:que25)
### TRTC는 오디오 전용 스트림을 지원합니까?
네, 그렇습니다.


[](id:que26)
### 같은 방에 하나 이상의 화면 공유 이미지가 있을 수 있습니까?
현재 한 방에 하나의 화면 공유 서브 스트림만 허용됩니다.

[](id:que27)
### 지정된 창을 공유할 때(SourceTypeWindow) 창 크기가 변경되면 비디오 스트림의 해상도도 그에 따라 변경됩니까?
기본적으로 SDK는 공유 창의 크기에 따라 인코딩 매개변수를 자동으로 조정합니다.
고정 해상도가 필요한 경우 setSubStreamEncoderParam API를 호출하여 화면 공유를 위한 인코딩 매개변수를 설정하거나 startScreenCapture API 호출 시 매개변수를 지정하십시오.


[](id:que28)
### TRTC는 1080P 비디오를 지원합니까?
예, 지원합니다. SDK의 비디오 인코딩 매개변수 setVideoEncoderParam을 통해 해상도를 설정할 수 있습니다.

[](id:que29)
### TRTC에서 데이터 캡처를 사용자 정의할 수 있습니까?
일부 플랫폼에서만 지원합니다. 자세한 내용은 [사용자 정의 컬렉션 및 렌더링](https://intl.cloud.tencent.com/document/product/647/35158)을 참고하십시오.

[](id:que30)
### TRTC와 LVB SDK 간의 통신이 가능합니까?
불가능합니다.

[](id:que31)
### TRTC는 MLVB와의 통신이 가능합니까? 
TRTC와 MLVB는 백엔드 아키텍처가 다르기 때문에 서로 통신할 수 없습니다. 그러나 TRTC에서 CDN으로 스트림을 릴레이할 수 있습니다.



[](id:que32)
### TRTC에서 서로 다른 방 입장 모드(AppScene)는 어떻게 다른가요?
TRTC에는 4가지 방 입장 모드가 있습니다. 통화 모드는 화상 통화(VideoCall) 및 음성 통화(·VoiceCall')이며, 라이브 스트리밍 모드는 인터랙션 비디오 라이브 스트리밍(Live) 및 인터랙션 오디오 라이브 스트리밍(VoiceChatRoom)입니다.
- 통화 모드의 TRTC는 단일 방에 최대 300명이 동시 접속할 수 있으며 최대 50명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.
- 라이브 스트리밍 모드는 각 방에서 최대 10만명의 동시 사용자를 지원하며 부드러운 마이크 온/오프가 가능합니다. 공동 앵커링 대기 시간은 300ms 미만으로 유지되고 시청 대기 시간은 1000ms 미만입니다. 라이브 스트리밍 모드는 대기 시간이 짧은 인터랙션 라이브 스트리밍, 최대 10만명의 참가자를 위한 인터랙션 강의실, 화상 소개팅, 온라인 교육, 원격 교육 및 초대형 회의와 같은 시나리오에 적합합니다.


[](id:que33)
### TRTC에서 화상 통화 중에 핸즈프리 모드를 사용할 수 있습니까?
예. 오디오 경로를 설정하여 핸즈프리 모드를 활성화할 수 있습니다. Native SDK에서 setAudioRoute API를 사용하여 경로를 전환합니다.

[](id:que34)
### TRTC는 볼륨 알림을 지원합니까?
지원합니다. enableAudioVolumeEvaluation API를 호출하여 볼륨 알림을 활성화할 수 있습니다.

[](id:que35)
### TRTC는 미러 이미지를 지원합니까? 
지원합니다. setLocalViewMirror API를 호출하여 로컬 카메라의 미리보기 이미지에 대한 미러링 모드를 설정하거나 setVideoEncoderMirror를 호출하여 인코딩된 이미지에 대한 미러링 모드를 설정할 수 있습니다.

[](id:que36)
### TRTC 통화의 오디오를 녹음하고 녹음 파일을 로컬에 저장할 수 있습니까? 
예. startAudioRecording을 호출하여 로컬 사용자, 원격 사용자 및 BGM을 포함한 모든 통화 오디오를 PCM, WAV 또는 AAC 형식의 단일 파일에 녹음할 수 있습니다.

[](id:que37)
### TRTC 통화의 비디오를 파일로 녹화할 수 있습니까?
TRTC는 로컬 서버에서 오디오/비디오 녹음을 지원합니다. 이 기능을 사용하려면 SDK 및 지침에 대한 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 하십시오. 
클라우드 녹화 기능을 사용하여 비디오를 녹화할 수도 있습니다.

[](id:que38)
### TRTC는 WeChat과 같은 플로팅 창 또는 큰 이미지와 작은 이미지 간의 창 전환을 지원합니까?
이러한 기능은 TRTC SDK가 제한을 설정하지 않는 UI 디자인의 일부입니다. 공식 Demo는 이미지 오버레이 및 그리드 레이아웃을 위한 샘플 코드를 제공하고 플로팅 창, 큰/작은 창 전환 및 창 드래그를 지원합니다. 자세한 내용은 [공식 Demo](https://github.com/tencentyun/TUICalling)를 참고하십시오.

[](id:que39)
### TRTC에서 음성 전용 통화를 하려면 어떻게 해야 하나요?
TRTC는 오디오와 비디오에 대해 별도의 채널을 사용하지 않습니다. startLocalPreview가 아닌 startLocalAudio만 호출하여 음성 전용 호출을 할 수 있습니다.

[](id:que40)
### CDN으로 릴레이를 활성화하고 TRTC에서 오디오 전용 통화를 녹음하려면 어떻게 합니까?
- TRTC SDK v6.9 이전 버전에서는 `json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}`을 생성하여 입장 시 TRTCParams.businessInfo에 전달해야 합니다. 1은 CDN으로의 중계, 2는 CDN으로 중계 및 녹음을 의미합니다.
- TRTC SDK 6.9 이상에서는 방 입장 시 scene 매개변수를 TRTCAppSceneAudioCall 또는 TRTCAppSceneVoiceChatRoom으로 설정하기만 하면 됩니다.

[](id:que41)
### 사용자를 퇴장시키거나, 사용자가 말하는 것을 금지하거나, TRTC 방에서 사용자를 음소거할 수 있습니까?  
예, 할 수 있습니다.
- 간단한 시그널링 작업을 통해 기능을 활성화하려면 TRTC의 사용자 정의 시그널링 API인 sendCustomCmdMsg를 사용하여 자신의 제어 시그널링을 정의하면 메시지를 수신한 사용자가 예상한 작업을 수행합니다. 예를 들어, 사용자를 퇴장시키려면 퇴장 신호를 정의하기만 하면 수신하는 사용자가 방을 나갈 것입니다.
- 보다 포괄적인 운영 로직을 구현하고 싶다면 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 이용하여 TRTC 룸을 IM 그룹에 매핑하고, 그룹의 사용자 정의 메시지 보내기/받기를 통해 기능을 활성화합니다.

[](id:que42)
### TRTC는 RTMP/FLV 스트림을 가져와서 재생할 수 있습니까?  
예. TRTC SDK에는 TXLivePlayer가 통합되어 있습니다. 더 많은 플레이어 기능이 필요한 경우 모든 기능을 갖춘 LiteAVSDK_Professional을 사용하는 것이 좋습니다.

[](id:que43)
### TRTC 통화에는 몇 명이 참여할 수 있나요?
- 통화 시나리오에서 각 방은 최대 300명의 동시 사용자를 수용할 수 있으며 최대 50명의 사용자가 동시에 카메라 또는 마이크를 켤 수 있습니다.
- 라이브 스트리밍 시나리오에서 각 방은 최대 10만명의 동시 사용자를 수용할 수 있으며, 그 중 최대 50명에게 앵커 역할을 할당하고 동시에 카메라 또는 마이크를 켤 수 있습니다.


[](id:que44)
### TRTC에서 라이브 스트리밍 세션을 시작하려면 어떻게 해야 하나요?
TRTC는 최대 10만명의 참가자가 공동 앵커링 대기 시간을 200ms 미만으로 유지하고 시청 대기 시간을 1s 미만으로 허용하는 대기 시간이 짧은 전용 인터랙션 라이브 스트리밍 솔루션을 제공합니다. 열악한 네트워크 조건에 탁월하게 적응하며 복잡한 모바일 네트워크 환경에 최적화되어 있습니다.
자세한 작업 가이드는 [라이브 방송 모드 실행(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35107)을 참고하십시오.

[](id:que45)
### TRTC의 사용자 정의 메시지 전송 API를 사용하여 채팅 및 화면 댓글과 같은 기능을 구현할 수 있나요?
아니요. 사용자 정의 메시지 전송은 단순하고 저주파 신호 시나리오를 위한 것입니다. 자세한 내용은 사용자 정의 메시지 보내기 [사용 제한](https://intl.cloud.tencent.com/document/product/647/35159)을 참고하십시오.

[](id:que46)
### TRTC에서 배경 음악을 반복할 수 있나요? 배경 음악의 재생 진행률을 조정할 수 있습니까?  
예. 재생 완료 콜백에서 재생 API를 다시 호출하여 배경 음악을 반복할 수 있습니다. TXAudioEffectManager의 seekMusicToPosInMS를 사용하여 재생 진행률을 설정할 수 있습니다.

>? 버전 7.3부터 TXAudioEffectManager의 setBGMPosition()이 seekMusicToPosInMS로 대체되었습니다.

[](id:que47)
### TRTC에서 콜백을 통해 사용자의 출입을 들을 수 있나요?onUserEnter/onUserExit를 사용할 수 있나요?
예. onRemoteUserEnterRoom/onRemoteUserLeaveRoom을 사용하여 사용자의 입/퇴장을 수신할 수 있지만 콜백은 데이터를 보낼 수 있는 사용자에 대해서만 트리거됩니다.
>?onUserEnter/onUserExit는 버전 6.8부터onRemoteUserEnterRoom/onRemoteUserLeaveRoom으로 대체되었습니다.

[](id:que48)
### TRTC에서 네트워크 연결 끊김 및 재연결을 어떻게 수신합니까?
다음 콜백을 통해 이벤트를 수신할 수 있습니다.
- onConnectionLost: SDK와 서버의 연결이 끊어졌습니다.
- onTryToReconnect: SDK가 서버에 다시 연결 중입니다.
- onConnectionRecovery: SDK가 서버에 다시 연결됩니다.

[](id:que49)
### TRTC SDK는 자동 재접속을 지원하나요?
SDK는 연결이 끊긴 후 자동으로 사용자를 다시 연결합니다. 30분 이내에 사용자를 다시 연결하지 못하면 방에서 사용자를 제거하고 -3301 오류를 반환합니다.   
다음 이미지는 Userid1이 방에 들어갈 때, SDK에서 연결을 끊고 방에 다시 들어갈 때 트리거되는 콜백을 보여줍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/893ec522169d27a7b9a0e2dc4b09c7d0.png)
**설명**:
- T1: 사용자가 'enterRoom' API를 호출하여 방에 입장합니다.
- T2: Userid1은 'onEnterRoom' 콜백을 수신하고 Userid2는 약 300ms(대기 시간) 후에 `onRemoteUserEnterRoom` 콜백을 수신합니다.
- T3: Userid1이 네트워크 문제로 연결이 끊겼고 SDK가 사용자에게 다시 연결을 시도합니다.
- T4: Userid1이 처음 8초 이내에 다시 연결되지 않으면 사용자는 'onConnectionLost' 콜백을 수신합니다.
- T5: 3초가 더 지나도 Userid1이 다시 연결되지 않으면 사용자는 `onTryToReconnect` 콜백을 수신합니다.
- T6: Userid1은 24초마다 onTryToReconnect 콜백을 수신합니다.
- T7: `onConnectionLost` 콜백 후 90s 후 Userid2가 `onRemoteUserLeaveRoom` 콜백을 수신합니다. 이는 Userid1이 오프라인 상태임을 나타냅니다.
- T8: 90s 중 어느 시점에서든 재접속이 성공하면 Userid1은 `onConnectionRecovery` 콜백을 수신합니다.


[](id:que50)
### 첫 번째 프레임 렌더링을 위한 콜백이 있습니까? 이미지 렌더링 또는 오디오 재생의 시작을 들을 수 있습니까?
예. onFirstVideoFrame/onFirstAudioFrame을 사용하여 이벤트를 수신할 수 있습니다.

[](id:que51)
### TRTC에서 동영상의 스크린샷 기능을 지원합니까?
현재 iOS/Android에서 snapshotVideo()를 호출하여 로컬 및 원격 비디오의 스크린샷 기능을 지원합니다.

[](id:que52)
### 블루투스 이어폰과 같은 주변기기를 TRTC에 연결하지 못하는 이유는 무엇인가요?
현재 TRTC는 주류 블루투스 이어폰 및 주변기기를 지원하지만 일부 장치의 경우 여전히 호환성 문제가 있습니다. 장치의 호환성을 테스트하려면 공식 Demo 및 QQ 음성/영상 통화를 사용하는 것이 좋습니다.

[](id:que53)
### TRTC 음성/영상 통화의 업스트림/다운스트림 비트레이트, 해상도, 패킷 손실률, 오디오 샘플 속도와 같은 정보는 어떻게 얻나요?
SDK의 onStatistics() API를 호출하여 통계를 얻을 수 있습니다.

[](id:que54)
### TRTC의 배경음악 API playBGM()이 온라인 음악을 지원하나요?
아니요. 현재 로컬 음악만 지원합니다. 온라인 음악 파일을 다운로드한 다음 playBGM()을 호출하여 재생할 수 있습니다.

[](id:que55)
### 로컬 오디오 캡처 볼륨이나 각 원격 사용자의 재생 볼륨을 설정할 수 있나요?
예. setAudioCaptureVolume()을 호출하여 SDK의 오디오 캡처 볼륨을 설정하고 setRemoteAudioVolume()을 호출하여 원격 사용자의 재생 볼륨을 설정할 수 있습니다.

[](id:que56)
### stopLocalPreview와 muteLocalVideo의 차이점은 무엇입니까?
- stopLocalPreview는 로컬 비디오 캡처를 중지하는 데 사용됩니다. 이 API를 호출하면 귀하와 다른 사용자 모두 귀하의 이미지를 볼 수 없습니다.
- muteLocalVideo는 로컬 비디오 이미지 전송을 중지하는 데 사용됩니다. 이 API를 호출하면 다른 사용자는 귀하의 이미지를 볼 수 없지만 여전히 자신의 이미지를 미리 볼 수 있습니다.

[](id:que57)
### stopLocalAudio와 muteLocalAudio의 차이점은 무엇입니까? 
- stopLocalAudio는 로컬 오디오의 캡처 및 전송을 비활성화하는 데 사용됩니다.
- muteLocalAudio가 호출되면 TRTC는 오디오/비디오 데이터 전송을 중지하지 않습니다. 매우 낮은 비트 레이트로 음소거된 데이터 패킷을 계속 보냅니다.

[](id:que58)
### TRTC SDK는 어떤 해상도를 지원합니까?
더 나은 화질을 위해 [화면 품질 설정](https://intl.cloud.tencent.com/document/product/647/35153)에 안내된 대로 해상도를 설정하는 것을 권장합니다.

[](id:que59)
### TRTC SDK에서 업스트림 비디오 비트 레이트, 해상도 및 프레임 속도를 설정하려면 어떻게 합니까? 
TRTCCloud의 setVideoEncoderParam() API를 호출하여 TRTCVideoEncParam에 videoResolution(해상도), videoFps(프레임 레이트), videoBitrate(비트 레이트)를 설정합니다.

[](id:que60)
### TRTC SDK에서 동영상을 회전하려면 어떻게 하나요?  
자세한 내용은 [비디오 화면 회전 및 축소와 확대](https://intl.cloud.tencent.com/document/product/647/35154)를 참고하십시오.

[](id:que61)
### 가로 모드에서 영상 통화를 하려면 어떻게 하나요? 
자세한 내용은 [가로 화면 영상 통화 구현](https://cloud.tencent.com/developer/article/1492095) 및 [비디오 화면 회전 및 축소와 확대](https://intl.cloud.tencent.com/document/product/647/35154)을 참고하십시오.

[](id:que62)
### 로컬 및 원격 비디오가 다른 경우 회전을 어떻게 일치시키나요?  
자세한 내용은 [비디오 화면 회전 및 축소와 확대](https://intl.cloud.tencent.com/document/product/647/35154)을 참고하십시오.


[](id:que63)
### TRTC에서 권장하는 이미지 품질 관련 설정(비트 레이트, 해상도, 프레임 레이트)은 무엇입니까?
자세한 내용은 [화면 품질 설정 > 권장 설정](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE)을 참고하십시오.

[](id:que64)
### TRTC에서 네트워크 속도를 테스트할 수 있나요? 어떻게 작업합니까?  
예, 할 수 있습니다. 자세한 내용은 [통화 전 네트워크 속도 테스트](https://intl.cloud.tencent.com/document/product/647/35156)를 참고하십시오.

[](id:que65)
### 승인된 사용자만 방에 들어갈 수 있도록 TRTC 방에 대한 액세스를 제어할 수 있습니까? 
예. 자세한 내용은 [고급 권한 제어 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 참고하십시오.

[](id:que66)
### TRTC는 RTMP/FLV 스트림을 가져와서 재생할 수 있습니까? 
예. 

[](id:que67)
### TRTC는 사용자 정의 렌더링을 위해 어떤 형식을 지원합니까? 
- iOS: i420, NV12 및 BGRA
- Android: I420 및 texture2d

[](id:que68)
### TRTC란 무엇인가요?
Tencent의 네트워크 및 오디오/비디오 기술에 대한 다년간의 경험을 활용하여 Tencent Real-Time Communication(TRTC)은 그룹 오디오/비디오 통화 및 대기 시간이 짧은 인터랙션 라이브 스트리밍을 위한 솔루션을 제공합니다. TRTC를 사용하면 비용 효율적이고 대기 시간이 짧은 고품질 인터랙션 오디오/비디오 서비스를 빠르게 개발할 수 있습니다. 자세한 내용은 [제품 개요](https://intl.cloud.tencent.com/document/product/647/35078)를 참고하십시오.

[](id:que69)
### TRTC Demo는 어떻게 체험해 볼 수 있나요?
자세한 내용은 [Demo 체험](https://intl.cloud.tencent.com/document/product/647/35076)를 참고하십시오.

[](id:que70)
### TRTC를 빨리 시작하려면 어떻게 해야 하나요?
TRTC는 다양한 플랫폼에 대한 Demo 소스 코드를 제공하여 자신의 앱을 빠르게 구축할 수 있도록 합니다. 자세한 내용은 [신규 사용자 가이드](https://intl.cloud.tencent.com/document/product/647/39386)를 참고하십시오.

[](id:que71)
### TRTC에서 클라우드 녹화 및 재생을 활성화하려면 어떻게 해야 하나요?
자세한 내용은 [클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426)을 참고하십시오.


[](id:que73)
### TRTC는 뷰티 필터를 지원하나요?
네, 그렇습니다. TRTC는 AI 뷰티 필터, 메이크업 효과, 얼굴 특징 보정, 그린 스크린 키잉 등 얼굴 인식 기술을 기반으로 다양한 효과를 제공합니다.

- Web에서 뷰티 필터를 사용하려면 [뷰티 필터 활성화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)를 참고하십시오.
- 네이티브 TRTC SDK의 AI 뷰티 필터는 Tencent Effect SDK에서 청구하는 부가 가치 서비스입니다.

>? 현재 iOS 및 Android용 TRTC Professional만 AI 뷰티 필터를 지원합니다.

[](id:que74)
### 중국 본토 밖에서도 TRTC를 사용할 수 있나요?	

중국 본토 외에도 홍콩 및 기타 지역에서도 TRTC를 사용할 수 있습니다.
> ?
> - TRTC는 전 세계적으로 안정적이고 안전한 네트워크 연결을 제공합니다. Tencent Cloud의 독점적인 다단계 주소 지정 알고리즘을 사용하며 전체 네트워크의 노드에 연결할 수 있습니다. 풍부한 고대역폭 리소스와 전 세계적으로 분산된 엣지 서버를 통해 전 세계적으로 평균 end-to-end 대기 시간을 300ms 미만으로 유지할 수 있습니다.
> - 국제 연결은 실제 현지 상황 및 적용 시나리오의 영향을 받을 수 있습니다.

[](id:que75)
### TRTC는 이미지에서 부적절한 콘텐츠 감지를 지원합니까?
TRTC는 라이브 스트리밍 중 음란물, 정치적으로 민감한 기타 부적절한 콘텐츠를 차단합니다.

[](id:que76)
### 방에 있는 모든 사용자의 정보를 어떻게 조회하나요?
현재 방에 있는 모든 사용자의 정보를 조회할 수 없습니다.

[](id:que77)
### TRTC는 다른 RTSP 스트림을 수신할 수 있습니까?
아니요, 할 수 없지만 RTMP 스트리밍을 지원합니다. 자세한 내용은 [RTMP 프로토콜 푸시 스트림에 TRTC 연결하기](https://intl.cloud.tencent.com/document/product/647/44275)를 참고하십시오.

[](id:que78)
### TRTC는 듀얼 채널 인코딩을 지원합니까?
예, TRTC는 듀얼 채널 오디오를 지원합니다.

[](id:que79)
### 스트림을 게시할 때 TRTC는 스트림을 먼저 패키징하거나 인코딩합니까?
데이터 캡처 후 TRTC는 패키징하기 전에 스트림을 먼저 인코딩합니다.

[](id:que80)
### TRTC SDK는 swift를 사용합니까?
Model 레이어는 Objective-C를 사용하고 UI 레이어는 Swift를 사용합니다.

[](id:que81)
### 내 계정이 개인 계정인 경우 TRTC를 사용할 수 있나요?
예, 사용할 수 있습니다.
