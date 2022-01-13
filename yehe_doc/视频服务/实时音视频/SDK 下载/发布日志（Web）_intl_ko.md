버전 번호 `major.minor.patch`의 자세한 규칙은 다음과 같습니다.
  - major: 메이저 버전 번호로, 중요한 버전 재구성 시 해당 필드의 숫자가 증가하며 일반적으로 각 메이저 버전 간의 인터페이스는 호환되지 않습니다.
  - minor: 마이너 버전 번호로, 각 마이너 버전 번호 간에는 인터페이스가 호환되며 인터페이스 추가 또는 최적화 시 해당 필드의 숫자가 증가합니다.
  - patch: 패치 번호로, 기능 개선 또는 오류 복구 시 해당 필드의 숫자가 증가합니다.

>!
> - 제품의 안정성 및 온라인 지원을 위해 항상 최신 버전을 유지하시기 바랍니다.
> - 버전 업데이트에 대한 주의 사항은 [업데이트 가이드](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)를 참고하십시오.

## Version 4.11.8 @2021.11.05

**Improvement**

- iOS 15.0에서 동영상 재생 시 간헐적으로 검은 화면이 나오는 문제가 해결되었습니다. 자세한 내용은 [iOS Safari 기존 문제 case 6](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html#h2-4)을 참고하십시오.
- iOS 15.1 푸시 스트리밍의 크래시 문제가 해결되었습니다. 자세한 내용은 [iOS Safari 기존 문제 case 7](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html#h2-4)을 참고하십시오.

## Version 4.11.7 @2021.09.30

**Improvement**

- 주요 인터페이스에 대한 매개변수 유형의 강력한 인증이 향상되었습니다.
- 개발 모드 (LogLevel는 [Debug](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.LogLevel)임)에서 중국어 오류 메시지 알림을 지원합니다.
- 장비 수집 예외 발생 시 자동 수집 복구 성공률이 향상되었습니다.
- 시스템 절전 모드 및 재부팅 후 통화 복구 로직을 최적화했습니다.
- trtc.esm.js 및 trtc.umd.js를 추가해 다양한 시나리오의 요구를 충족시킵니다. [참고 가이드](https://www.npmjs.com/package/trtc-js-sdk).

## Version 4.11.6 @2021.09.10

**Improvement**

시그널링 스케쥴링 로직을 최적화하여 네트워크가 좋지 않은 상황에서의 방 입장 성공률을 높였습니다.

## Version 4.11.5 @2021.09.04

**Improvement**

- 동적 신호 채널 스케줄링을 지원하여 열악한 네트워크 조건에서 연결 성공률을 개선했습니다.
- 크로스 룸 혼합 스트림을 지원합니다. 자세한 내용은 [Client.startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)를 참고하십시오.

**Bug Fixed**

- 재연결 후 간혹 stream-added 이벤트 콜백을 수신하지 못하는 문제를 수정했습니다.
- 화면 공유가 장시간 지속되면 간혹 프레임 속도가 0으로 떨어지는 현상이 수정되었습니다.


## Version 4.11.4 @2021.08.20

**Improvement**

- oppo & vivo 내장 브라우저에 대한 H.264 지원 확인의 정확도가 향상되었습니다.
- 수집 자동 재개 로직을 추가했습니다(수집 오류 발생 시 트리거됨).
- subscribe API에 대한 시간 초과 로직이 추가되었습니다. 자세한 내용은 오류 코드 [API_CALL_TIMEOUT](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.API_CALL_TIMEOUT)을 참고하십시오.

**Bug Fixed**

- 일부 이전 버전의 iOS Safari에서 간혹 스트림을 가져오지 못하는 문제를 수정했습니다.
- 기기 전환 후 mute 상태가 정확하지 않은 현상이 수정되었습니다.
- 타임 아웃 후 방 입장 API를 다시 호출할 때 간혹 예외가 발생하는 현상이 수정되었습니다.
- 원격 스트림이 게시 취소된 후 오디오/비디오 플레이어가 적시에 종료되지 않는 문제가 수정되었습니다.

## Version 4.11.3 @2021.07.30

**Improvement**

- publish & subscribe API에 대한 예외 처리 로직을 최적화했습니다.
- 오디오 믹싱 플러그인에 대한 복구 정책을 최적화했습니다.

**Bug Fixed**

- 간혹 Peer-leave 알림이 정확하지 않은 문제를 수정합니다.

## Version 4.11.2 @2021.07.23

**Improvement**

- turn server 스케줄링을 지원하여 연결 성공률을 향상시켰습니다.
- [Client.getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteMutedState) 원격 사용자에게 서브 스트림 비디오가 있는지 여부를 나타내는 hasSmall 속성을 추가했습니다.

**Bug Fixed**

- LocalStorage가 비활성화된 경우 SDK를 사용할 수 없는 문제가 수정되었습니다.
- 간혹 publish 예외가 발생할 때 API 요청이 rejected 되지 않는 문제가 수정되었습니다.


## Version 4.11.1 @2021.06.25

**Improvement**

- 뷰티 필터 플러그인을 지원합니다. 자세한 내용은 [뷰티 필터 활성화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)를 참고하십시오.
- 통계 정확도가 향상되었습니다.

## Version 4.11.0 @2021.06.18

**Feature**

이중 스트림(기본 및 서브 스트림)을 지원합니다. [이중 스트림 활성화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html) 튜토리얼을 참고하십시오.

**Improvement**

이벤트 알림 순서를 최적화했습니다.

## Version 4.10.3 @2021.06.11

**Improvement**

- 품질 측정 로직을 최적화하여 서버측 API를 통해 통화 품질 통계를 얻을 수 있습니다.
- [ClientEvent.NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)에 rtt 및 패킷 loss에 대한 통계를 추가했습니다.
- 반복 호출로 인한 예외를 방지하기 위해 API 검증 로직을 최적화했습니다.
- 재생 로직을 최적화하여 오디오 로딩 시간을 줄였습니다.

## Version 4.10.2 @2021.05.24

**Improvement**

- switchDevice 인터페이스 구현 로직 최적화로 간혹 HUAWEI 브라우저의 전면 카메라 전환이 불가능한 문제 방지
- [StreamEvent.CONNECTION_STATE_CHANGED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) 이벤트 공지 정확성 향상

**Bug Fixed**

- 간혹 Native 화면 공유 재생이 불가능한 문제 수정
- 재연결 후 간혹 stream-removed 이벤트를 받지 못하는 문제 수정

## Version 4.10.1 @2021.04.30

**Feature**

- [StreamEvent.CONNECTION_STATE_CHANGED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) 이벤트 추가로 수신 Stream 연결 상태 변경 지원
- [Client.getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getTransportStats) 인터페이스의 다운스트림 RTT 통계 데이터 획득 지원
- [Client.getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteVideoStats) 인터페이스의 서브스트림(화면 공유) 통계 데이터 획득 지원

**Improvement**

[Client.switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole) 인터페이스의 구현 로직 최적화

**Bug Fixed**

- mute 관련 이벤트가 간혹 stream-added 전에 트리거 되는 문제 수정
- 방 입장 후 간혹 소리가 들리지 않는 문제 수정

## Version 4.10.0 @2021.04.16

**Feature**

- 인터페이스 [Client.startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startPublishCDNStream)을 추가하여 Tencent Cloud CDN 및 3rd party CDN에 스트림 푸시 전송
- 인터페이스 [Client.stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#stopPublishCDNStream)을 추가하여 Tencent Cloud CDN 및 3rd party CDN에 스트림 푸시 중지

**Improvement**

[LocalStream.switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#switchDevice), [LocalStream.addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#addTrack), [LocalStream.removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#removeTrack) 인터페이스의 매개변수 검증 로직 최적화

## Version 4.9.0 @ 2021.03.19

**Feature**

- 클라우드 혼합 스트림에서 프리셋 레이아웃 모드 지원. 자세한 내용은 [Client.startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode) 인터페이스를 참고하십시오.
- 음량 콜백 지원. 자세한 내용은 [Client.enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#enableAudioVolumeEvaluation) 인터페이스를 참고하십시오.

**Improvement**

Websocket의 기본 포트를 443으로 변경

**Bug Fixed**

- live 모드에서 시청자가 호스트의 입장/퇴장 공지를 받지 못하는 문제 수정
- 문자열 방 번호 사용 시 간혹 재연결에 실패하는 문제 수정

**Breaking Change**

[TRTC.checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements)에서 상세한 검증 결과 반환. 자세한 내용은 [인터페이스 문서](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements) 및 [업데이트 가이드](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)를 참고하십시오.

## Version 4.8.6 @ 2021.03.01

**Improvement**

풀 스트림 스테레오 음향 재생 지원
>! iOS 플랫폼은 현재 지원하지 않습니다.

**Bug Fixed**

모바일 디바이스 음소거 및 화면 정지 시 Web에서 stream-removed 이벤트가 수신되는 문제 수정

## Version 4.8.5 @ 2021.01.29

**Improvement**

- [Client.setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setTurnServer)에서 멀티 turn server 설정 지원
- userId 검증 로직 최적화

**Bug Fixed**

푸시 스트림 후 간혹 mute 상태가 부정확한 문제 수정

## Version 4.8.4 @ 2021.01.15

**Improvement**

- [LocalStream.setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile) 인터페이스에서 동적 호출 지원
- 대시 보드 데이터 리포트 로직 최적화
- 자동 재생 제한 시 처리 로직 최적화. 자세한 내용은 [자동 재생 제한 처리 제안](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)을 참고하십시오.
- 디바이스 연결/해제 자동 복구 실패 시 처리 로직 최적화. 자세한 내용은 [DEVICE_AUTO_RECOVER_FAILED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED)를 참고하십시오.

**Bug Fixed**

푸시 스트림 재시도 후 간혹 mute 상태가 부정확한 문제 수정

## Version 4.8.3 @ 2021.01.07

**Improvement**

방 입장 인터페이스 roomId 매개변수 검증 로직 최적화

**Bug Fixed**

- v4.8.2 버전의 3rd party 종속 결여 문제 수정
- 오디오만 구독 시 간혹 오디오가 나오지 않는 문제 수정
- iOS 자동 재생 제한 후 간혹 resume 오디오가 나오지 않고 getAudioLevel이 0이 되는 문제 수정

## Version 4.8.2 @ 2020.12.31

**Improvement**

- 방 입장 인터페이스 roomId 매개변수 검증 로직 최적화. 자세한 내용은 [인터페이스 문서](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) 및 [업데이트 가이드](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)를 참고하십시오.
- peer-join 및 peer-leave 이벤트 공지 시기 최적화

**Bug Fixed**

방 퇴장 시 간혹 `Cannot read property 'isConnected' of null` 오류가 보고되는 문제 수정

**Breaking Change**

사용되지 않는 setDefaultMuteRemoteStreams를 삭제했습니다. 대신 [TRTC.createClient 의 autoSubscribe 매개변수](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 사용하십시오.

## Version 4.8.1 @ 2020.12.25

**Bug Fixed**

- Windows에서 간혹 원격 사용자의 오디오가 들리지 않는 문제 수정
- client.getRemoteVideoStats() 인터페이스의 빈 데이터 반환 문제 수정

## Version 4.8.0 @ 2020.12.18

**Feature**

- 클라우드 혼합 스트림 트랜스 코딩 지원
- 모든 플랫폼에서 문자열 방 번호 지원. 자세한 내용은 [TRTC.createClient의 useStringRoomId 매개변수](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 참고하십시오.
- 자동 구독 비활성화 지원. 자세한 내용은 [TRTC.createClient의 autoSubscribe 매개변수](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 참고하십시오.

**Improvement**

- h264 지원 검증 로직 최적화
- 디바이스 전환 로직 최적화
- hasAudio/hasVideo 인터페이스 상태 판단 로직 최적화

**Bug Fixed**

- 인터넷이 끊긴 후 재연결 시 간혹 실패 오류가 보고되는 문제 수정
- iOS Safari에서 빈번하게 add/remove track 블랙 스크린 현상이 발생하는 문제 수정

## Version 4.7.1 @ 2020.11.27

**Improvement**

- 미디어 디바이스 변경 시(예: 포트 헐거워짐, 디바이스 연결/해제 등)의 자동 복구 채택 로직 최적화
- 디바이스 복구 실패 시 표시하는 에러 코드 추가: [DEVICE_AUTO_RECOVER_FAILED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED)

**Bug Fixed**

- Chrome/87 버전에서 간혹 블랙 스크린 현상이 보고되는 문제 수정
- Native 푸시 카메라 + 화면 공유 시 Web에서 중복 구독하거나 구독을 취소하는 경우 화면 공유 스트림이 사라지는 문제 수정

## Version 4.7.0 @ 2020.11.20

**Feature**

데스크톱 Firefox M56+ 및 데스크톱 Edge M80+ 지원

**Improvement**

- 업스트림 비트 레이트 제어 로직 최적화
- 미디어 디바이스 획득 재시도 로직 최적화
- Websocket 재연결 로직 최적화
- 디바이스 변경 시의 푸시 스트림 자동 복구 로직 최적화로 오디오 믹싱 상태에서 마이크 연결/해제 시 푸시 스트림 자동 복구 지원

**Breaking Change**

[TRTC.checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements)에서 상세한 검증 결과 반환. 자세한 내용은 [인터페이스 문서](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements) 및 [업데이트 가이드](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)를 참고하십시오.

## Version 4.6.7 @ 2020.11.05

**Bug Fixed**

- Chrome에서 하드웨어 가속 활성화 시 풀 스트림 시청에 간혹 랙이 발생하는 문제 수정
- iOS WeChat의 브라우저에서 방 입장 및 풀 스트림이 불가능한 문제 수정

## Version 4.6.6 @ 2020.10.23

**Improvement**

- 업스트림 peerConnection 재연결 로직 최적화
- 다운스트림 peerConnection 재연결 로직 최적화
- TRTC.checkSystemRequirements 검증 로직 최적화
- Safari 화면 공유 지원. 자세한 내용은 [화면 공유 사용 튜토리얼](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)을 참고하십시오.

**Bug Fixed**

자동 재생 정책 제한으로 인한 오디오 재생 수동 복구 후 getAudioLevel 값이 0이 되는 문제 수정

## Version 4.6.5 @ 2020.10.14

**Improvement**

- WebSocket 신호 터널 재연결 로직 최적화로 연결 안정성 개선
- 로그 출력 로직 최적화

**Bug Fixed**

- Chrome에서 재구독 후 getAudioLevel 인터페이스에서 0을 반환하는 문제 수정
- Safari에서 재구독 후 재생 시 오디오가 나오지 않는 문제 수정
- replaceTrack으로 업스트림 오디오 트랙을 전환한 후 getLocalVideoStats 인터페이스에서 undefined를 반환하는 문제 수정
- 모바일 디바이스 통화 중 네트워크 유형 전환 시 간혹 WebSocket 연결이 끊기는 문제 수정

## Version 4.6.4 @ 2020.09.24

**Improvement**

방 퇴장 후 네트워크 품질 통계 중지

**Bug Fixed**

- Chrome 56에서 방 입장 시 오류가 보고되는 문제 수정
- 모바일에서 릴레이 푸시할 경우 화면이 회전하는 문제 수정
- 퓨어 오디오 푸시 스트림 시 클라우드 녹화에 오류가 발생하는 문제 수정
- 해상도 불일치로 인해 카메라 연결이 해제된 후 푸시 스트림 자동 복구에 실패하는 문제 수정

## Version 4.6.3 @ 2020.08.28

**Improvement**

- 호환성 검증 로직 최적화
- 로그 리포트 로직 최적화
- 업스트림 비트 레이트 제어 로직 최적화

## Version 4.6.2 @ 2020.08.14

**Improvement**

- 업스트림 비트 레이트 조정 로직 최적화
- switchRole 매개변수 검증 로직 최적화
- 업스트림 네트워크 품질 계산 로직 최적화
- 오류 안내 정보 최적화
- 푸시 스트림 수집 디바이스 변경 검증 시 푸시 스트림 상태 자동 복구

**Bug Fixes**

unpublish 완료 후 곧바로 publish 재시도 실패 오류가 보고되는 문제 수정

## Version 4.6.1 @ 2020.07.28

**Improvement**

- [TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.isScreenShareSupported) Safari는 화면 공유를 지원하지 않습니다.
- subscribe & unsubscribe 인터페이스의 매개변수 검증 로직 개선
- 네트워크 품질 로그 추가

**Bug Fixes**

- 미디어 디바이스에 대한 라이선스가 없고 TRTC.createStream 인터페이스에서 전송한 디바이스 ID가 빈 문자열일 때 SDK에서 OverconstrainedError를 보고하는 문제 수정
- 업스트림 peerConnection이 끊긴 경우 로그가 출력되지 않는 문제 수정

## Version 4.6.0 @ 2020.07.16

**Feature**

NETWORK_QUALITY 이벤트 추가

## Version 4.5.0 @ 2020.07.02

**Feature**

createStream 인터페이스에 screenAudio 매개변수 추가

**Bug Fixes**

- Android 브라우저에서 에코 제거 효과가 적용되지 않는 문제 수정
- getTransportStats 인터페이스에서 rtt 값을 NAN으로 반환하는 문제 수정

## Version 4.4.0 @ 2020.05.28

**Feature**

Chrome 74 이상에서 화면 공유 수집 시스템(Windows) 또는 현재 Tab 페이지(Mac)의 오디오 지원
  
## Version 4.3.14 @ 2020.04.29

**Bug Fixes**

미니프로그램 오디오 muted unmute 이벤트 수정
  
## Version 4.3.13 @ 2020.04.16

**Improvement**

가용성 검증 로직 최적화

## Version 4.3.12 @ 2020.04.13

**Bug Fixes**

잠재적인 RTCPeerConnection의 상태 변화 이상 수정
  
## Version 4.3.11 @ 2020.03.28

**Improvement**

휴대폰 QQ 브라우저 검증 추가. 휴대폰 QQ 브라우저에서는 현재 TRTC 데스크톱 브라우저 SDK를 지원하지 않습니다.

**Bug Fixes**

Boolean 반환값 유형 수정

## Version 4.3.10 @ 2020.03.17

**Improvement**

- 환경 검증 로직 최적화
- RtcError에 name code 추가

## Version 4.3.9 @ 2020.03.13

**Improvement**

- 배포 환경 자동 검증 추가
- 로그 최적화

## Version 4.3.8 @ 2020.02.24

**Improvement**

createClient에 streamId userdefinerecordid 필드 추가

## Version 4.3.7 @ 2020.02.21

**Improvement**

화면 공유 시 디바이스 전환 오류 안내

**Bug Fixes**

- 디바이스 전환 시 MediaStream을 릴리스하는 경우 디바이스 점유 문제 해결
- 구독 인터페이스에 잠재적 오류 처리 기능 추가

## Version 4.3.6 @ 2020.02.05

**Bug Fixes**

Stream.resume() 멀티미디어 재생 순서 조정으로 iOS 상의 WeChat 브라우저 자동 재생 이상 문제 수정

## Version 4.3.5 @ 2020.02.05

**Improvement**

publish 시간 초과 검사를 추가하여 신호 발송 성공률 향상

## Version 4.3.4 @ 2020.01-06

**Improvement**
 
core-js를 v3.6.1로 업데이트
  
**Bug Fixes**

- unpublish 시간 초과 후 외부에 오류 이벤트 안내
- V8 최적화 후 3rd party 라이브러리로 인해 발생하는 문제 수정

## Version 4.3.3  @ 2019.12.25

**Improvement**

- webrtc 지원 여부를 직접 검증하는 기능 추가
- sdp 응답 메커니즘 최적화
- 리포트 로직 최적화

**Bug Fixes**

turn URL 프로토콜 포맷 수정

## Version 4.3.2 @ 2019.12.09

**Improvement**

- 다운스트림 연결 ICE 끊김 발생 시 자동으로 재연결하는 메커니즘 추가
- STUN 홀 펀칭 링크 제거로 내부 네트워크 사용자 연결 성공률 및 연결 속도 향상
- 서버에서 교정된 UTC 시간을 로그 리포트 타임스탬프에 동일하게 사용
- ICE 오류 리포트 최적화
- avmonitor 모니터링에 더 많은 주요 이벤트 리포트 추가

**Bug Fixes**

- WebSocket 신호 터널 1005 오류 시 재연결 및 재연결 오류 프로세스 수정
- 다운스트림 패킷 손실률 리포트 문제 수정

## Version 4.3.1 @ 2019.11.23

**Improvement**

통화 중 업스트림 링크 ICE 끊김 발생 시 자동으로 재연결하는 메커니즘 추가

**Bug Fixes**

STUN 홀 펀칭 실패 후 host 공용 IP 유형의 ICE Candidate가 적용되지 않는 문제 수정

## Version 4.3.0 @ 2019.11.15

**Feature**

Client.getTransportStats() API 추가

**Improvement**

- 더 구체적인 리포트 로그 추가
- 이벤트 바인딩 해제에 와일드카드 지원
- 연결 타임아웃 시간 5초로 연장
- 배포 타임아웃 시간 5초로 연장

**Bug Fixes**

zone.js의 프로토타입 체인 수정으로 인한 SDK 판단 오류 문제 수정

## Version 4.2.0 @ 2019.11.04

**Feature**

Client.off() 인터페이스에 클라이언트 이벤트 바인딩 취소 추가

**Improvement**

- 통화 상태 통계 최적화
- Client.publish()에 권한 검사 추가
- Stream.play()/resume()에 자동 재생 오류 안내 추가

**Bug Fixes**

LocalStream.switchDevice() 카메라 전환 시 블랙 스크린 현상이 발생하는 문제 수정

## Version 4.1.1 @ 2019.10.24

**Bug Fixes**

- 로그 유실 문제 수정
- 인터넷이 끊겨 재연결되는 원격 사용자 유실 문제 수정

## Version 4.1.0 @ 2019.10.17

**Feature**

- Stream.play() 인터페이스에서 HTMLDivElement 객체 전송 지원
- 오디오 비트 레이트 조정 설정 추가. 개발자는 LocalStream.setAudioProfile()을 통해 오디오 속성을 설정할 수 있으며, 현재 두 가지 Profile(standard, high)을 지원합니다.

**Bug Fixes**

- 구버전 Chrome의 WebAudio Context 수량 제한 문제 수정
- replaceTrack()에서 로컬 멀티미디어 플레이어가 재시작되지 않는 문제 수정
- LocalStream.setScreenProfile()에서 사용자 정의 속성 설정이 적용되지 않는 문제 수정
- audio/video player 재시작 및 상태 리포트 문제 수정

## Version 4.0.0 @ 2019.10.11

TRTC 데스크톱 브라우저의 SDK 재구성 버전은 객체 역할이 보다 명확하고 semantics가 더 간결한 Client/Stream 모드 인터페이스를 제공합니다.
재구성 버전은 구버전과 호환되지 않으며, 인터페이스 변경 외에도 다음과 같은 기능을 제공합니다.

- App에서 SDK의 LocalStream.setVideoProfile() 인터페이스를 통해 비디오 속성(해상도, 프레임 레이트, 비트 레이트)을 완벽하게 제어할 수 있습니다. 구버전의 Tencent Cloud 콘솔을 통한 '화면 설정(Spear Role)'은 지원하지 않습니다.
- SDK는 Stream 객체에 멀티미디어 플레이어를 캡슐화하여 멀티미디어 재생을 완벽하게 제어합니다.
- 원격 스트림에 대한 구독 및 구독 취소 기능을 제공합니다. 개발자는 Client.subscribe()/unsubscribe() 인터페이스를 통해 원격 스트림의 오디오, 비디오, 멀티미디어 데이터 스트림 수신을 효율적으로 제어할 수 있습니다.
