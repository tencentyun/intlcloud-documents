## Version 9.3.201 @ 2022.01.05

**새로운 기능**
Windows & Mac: [onSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTestResult) 네트워크 속도 테스트 결과 콜백을 추가했습니다.

**개선**
- Windows & Mac: [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest)를 개선하여 네트워크 속도 테스트를 시작합니다.
- Windows & Mac: [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) 로컬 비디오 스트리밍 일시 중지/재개를 개선하여, streamType 매개변수를 추가했습니다.
- Windows & Mac: [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream)을 개선하여 지정된 원격 비디오 스트림 수신을 일시 중지하고 streamType 매개변수를 추가했습니다.
- Windows & Mac: [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) 화면 공유 매개변수 설정을 개선하여, source, captureRect, property 세 매개변수를 지원합니다.
- Windows & Mac: [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture)를 개선하여 화면 공유를 시작하고 params 매개변수를 추가했습니다.

**문제 수정**
- Mac: Mac OS 12 새 시스템의 카메라 캡처 문제.
- Windows & Mac: 약한 네트워크 제어 정책을 최적화하여 원활성을 향상하였습니다.
- Windows: AGC 알고리즘을 최적화해 소리가 너무 작거나 소리가 너무 큰 문제가 발생할 확률을 낮췄습니다.
- Winodws: 화면 공유 시 수집 프레임 레이트 예외 문제가 수정되었습니다.

## Version 8.9.102 @ 2021.08.11

**새로운 기능**
Windows & Mac: onStatistics 콜백에 gatewayRtt [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) 필드를 추가했습니다.

**문제 수정**
- Mac: 특수 모델에 로그 작성 시 발생하는 crash를 수정했습니다.
- Mac: setAudioCaptureVolume(0) API로 마이크를 비활성화하면 마이크 감지 볼륨이 0이 되는 문제를 수정했습니다.
- Windows: 성능을 최적화하여 카메라 활성화 후 검은색 화면이 나타나는 문제를 수정했습니다.
- Windows: 해상도 자동 감소 후 화면 캡처가 복구되지 않는 문제를 수정했습니다.
- Windows & Mac: 기타 bug 수정.

## Version 8.6.101 @ 2021.05.28

**새로운 기능**
- Windows & Mac: 인터페이스 추가, 화면 공유 시 가림막 애플리케이션 창 지원: [addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow), [removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow), [removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow).
- Windows & Mac: 공유 가능한 창 리스트 인터페이스 획득 [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources), 반환 값 리스트 요소에 isMinimizeWindow 필드 추가.
- Windows & Mac: 구조 함수 전송 매개변수 지원.

**문제 수정**
- Windows: 플러그 인 로딩에서 중국어 경로를 지원하지 않는 문제.
- Windows & Mac: webgl context lost 문제.
- Windows & Mac: 듀얼 경로 인코딩 활성화로 방에 입장한 후 작은 화면 비디오 스트림으로 전환 시 로컬에 표시되는 원격 참석자의 화면이 멈추는 문제.
- Windows & Mac: 클라이언트가 방에 입장한 후 풀 스트림 시 원격 참석자의 화면이 흐려졌다가 다시 점차 선명해지는 문제.

## Version 8.4.1 @ 2021.03.26

**새로운 기능**
- Mac: Mac 운영 체제의 출력 음성 [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback) 수집을 지원합니다. Windows와 동일한 SystemLoopback 기능이며, 해당 기능을 통해 SDK에서 현재 시스템의 음성을 수집할 수 있습니다. 해당 기능을 활성화하면 호스트가 편리하게 다른 사용자에게 음악 또는 영화 파일을 라이브 방송할 수 있습니다.
- Mac: 시스템 오디오에서 [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError) 콜백을 수집하여 시스템 오디오 드라이버의 실행 상태 확인 가능.
-  Mac: 화면 공유 시 로컬 미리보기 기능을 지원합니다. 미니 창을 통해 공유할 화면 콘텐츠를 미리 볼 수 있습니다.
- 전체 플랫폼: 뷰티 필터 플러그 인 메커니즘 지원.

**품질 최적화**
- 전체 플랫폼: cloubhouse와 같은 음성 라이브 방송 시나리오에 더욱 적합하도록 [Music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) 모드에서의 음질이 최적화되었습니다.
-  전체 플랫폼: 멀티미디어 링크의 네트워크 저항력을 최적화하여 70%라는 극도로 열악한 네트워크 상황에서도 멀티미디어가 비교적 원활하게 재생됩니다.
-  Windows: 일부 시나리오의 라이브 방송 음질을 최적화하여 오디오 품질 저하 문제가 대폭 감소되었습니다.
-  Windows: 성능 최적화를 통해 일부 사용 시나리오에서 구버전 대비 성능이 20% - 30% 향상되었습니다.

**문제 수정**
- Mac: Mac mini (m1)에서 전체 화면 공유로 전환한 후 다시 특정 창으로 돌아올 때, 원격에서는 여전히 전체 화면 공유 창이 표시되는 문제 수정.
- Mac: Mac에서 화면 공유 시 하이라이트되지 않는 문제(Mac 시스템 11.1, 10.14.5에서 녹색 프레임이 나타나지 않는 문제, Mac 시스템 10.3.2에서 녹색 프레임은 나타나지만 창을 확대하면 깜빡이는 문제) 해결.
-  Mac: Mac mini m1에서 화면 공유 리스트 획득 crash 시, 하위 레이어 sourceName이 null인 경우 상위 레이어에서 ""를 반환하는 문제 수정.
-  Mac: Mac mini m1, getCurrentMicDevice로 인해 crash(sourceName)가 null이 되는 문제 수정
-  Windows: Windows Server 2019 Datacenter x64 시스템에서 데스크톱 공유 실행 시 발생하는 crash 문제가 수정되었습니다.
-  Windows: 창 공유와 동시에 타깃 창의 크기를 변경할 때 간혹 공유가 중지되는 BUG가 수정되었습니다.
-  Windows: 일부 모델의 카메라에서 화면을 수집하지 못하는 문제가 수정되었습니다.

## Version 8.2.7 @ 2021.01.06

**추가**
- Windows & Mac: [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) 방 전환 추가.
- Windows & Mac: [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) 로컬 이미지(주요)를 설정하는 렌더링 매개변수 추가.
- Windows & Mac: [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) 원격 이미지를 설정하는 렌더링 매개변수 추가.
- Windows & Mac: [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) 배경 음악 재생 실행 추가.
- Windows & Mac: [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) 배경 음악 재생 중지 추가.
- Windows & Mac: [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) 배경 음악 재생 일시 중지 추가.
- Windows & Mac: [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) 배경 음악 다시 재생 추가.
- Windows & Mac: [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) 배경 음악 파일 총 시간 획득 추가, 단위: 밀리초.
- Windows & Mac: [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) 배경 음악 재생 진행률 설정 추가.
- Windows & Mac: [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) 배경 음악 음량 설정 추가, 배경 음악 오디오 믹싱 시 배경 음악 음량 조절에 사용.
- Windows & Mac: [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) 배경 음악 로컬 재생 음량 설정 추가.
- Windows & Mac: [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) 배경 음악 원격 재생 음량 설정 추가.
- Windows & Mac: [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) 방 전환 콜백 추가.
- Windows & Mac: [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) 원격 사용자 재생 음량 설정 추가.
- Windows & Mac: [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) 비디오 화면 캡처 추가.
- Windows & Mac: [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) 화면 캡처 완료 시 콜백 추가.

**개선**
- Windows & Mac: enterRoom 및 switchRoom 시 string 유형의 strRoomId 지원.
- Windows & Mac: 기타 bug 수정.

## Version 7.9.348 @ 2020.11.12

**개선**
- Windows: 녹음 경로 설정 시 중국어 경로 폴더 미지원 수정.
- Windows: 창에서 특정 구역 캡처 시 차단 방지 지원.

## Version 7.8.342 @ 2020.10.10

**추가**
- Windows & Mac: [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) 현재 오디오 수집 디바이스 음량 변경 콜백 추가.
- Windows & Mac: [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) 현재 오디오 재생 디바이스 음량 변경 콜백 추가.

## Version 7.7.330 @ 2020.09.11

**추가**
Windows & Mac: [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) 추가, 오디오 품질 설정에 사용.

**개선**
- Windows: 일부 저가형 카메라의 지나치게 높은 CPU 사용률 문제가 최적화되었습니다.
- Windows: 멀티 USB 카메라와 마이크에 대한 호환성 최적화로 디바이스의 실행 성공률이 향상되었습니다.
- Windows: 카메라와 마이크 디바이스 선택 정책 최적화로 카메라 또는 마이크 사용 중 소켓으로 인한 샘플링 오류 문제를 방지하였습니다.
- Windows & Mac: 기타 bug 수정.

## Version 7.6.300 @ 2020.08.26

**추가**
Windows & Mac: [setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute), [getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute), [setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute), [getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute) 추가, PC의 마이크 및 스피커 제어에 사용.

## Version 7.5.210 @ 2020.08.11

**개선**
- Windows & Mac: SDK 콜백 비순차 문제 수정.
- Windows & Mac: 렌더링 모드 전환 시 크래쉬 문제 해결. 
- Windows & Mac: 일부 해상도 렌더링 실패 문제 수정. 
- Windows & Mac: 기타 bug 수정.

## Version 7.4.204 @ 2020.07.01

**개선**
- Windows: Windows 플랫폼의 반향 제거(AEC) 효과 최적화.
- Windows: Windows 플랫폼의 카메라 수집 디바이스 호환성 향상.
- Windows: Windows 플랫폼의 오디오 디바이스(마이크 및 스피커) 호환성 향상.
- Windows: Windows 버전 onPlayAudioFrame 콜백의 UserID가 부정확한 문제 수정.
- Windows: 64비트에서 시스템 오디오 믹싱 지원

## Version 7.2.174 @ 2020.04.20

**개선**
- Mac: Mac에서 가끔 로컬 사용자 정의 렌더링 해상도가 일치하지 않는 문제 수정.
- Windows: Windows의 getCurrentCameraDevice 로직을 최적화하여 카메라 미사용 시 첫번째 디바이스를 기본 디바이스로 반환.
- Windows: 화면 공유 시 하이라이트 창이 회색으로 보이는 문제 수정.
- Windows: Win10 시스템에서 화면 공유 썸네일 획득 시 가끔 랙이 걸리는 문제 수정.
- Windows & Mac: 역할 전환 시 가끔 사용자 정의 스트림 ID가 즉시 적용되지 않는 문제 수정.
- Windows & Mac: 화면 공유 설정 인코딩 매개변수가 적용되지 않는 문제 수정.
- Windows: Windows 화면 공유 후 webrtc에서 오랫동안 기다려야 화면을 볼 수 있는 문제 수정.

## Version 7.1.157 @ 2020.04.02

**추가**

[메인 채널](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType)을 사용한 [화면 공유](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) 지원.

**개선**
- [혼합 스트림 사전 설정 템플릿](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode)의 활용성 최적화.
- [혼합 스트림](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig) 최적화로 성공률 향상.
- Windows 화면 공유 최적화.


## Version 7.0.149 @ 2020.03.019

**추가**

[trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141) 파일 추가로 typescript를 사용하는 개발자의 편리성 향상.
