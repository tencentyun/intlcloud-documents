## Version 8.4.1 @ 2021.03.26

**새로운 기능**
- Mac: Mac 운영 체제의 출력 음성 [startSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSystemAudioLoopback) 수집을 지원합니다. Windows와 동일한 SystemLoopback 기능이며, 이 기능을 통해 SDK에서 현재 시스템의 음성을 수집할 수 있습니다. 해당 기능을 활성화하면 호스트가 편리하게 다른 사용자에게 음악 또는 영화 파일을 라이브 방송할 수 있습니다.
- Mac: 시스템 오디오에서 콜백 [onSystemAudioLoopbackError](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSystemAudioLoopbackError)을 수집하여 시스템 오디오 드라이버의 실행 상태를 확인할 수 있습니다.
-  Mac: 화면 공유 시 로컬 미리보기 기능을 지원합니다. 미니 창을 통해 공유할 화면 콘텐츠를 미리 볼 수 있습니다.
- 전체 플랫폼: 뷰티 필터 플러그 인 메커니즘 지원

**품질 최적화**
- 전체 플랫폼: [Music](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) 모드에서의 오디오 품질을 최적화하여 cloubhouse와 유사한 음성 라이브 방송 시나리오에 더욱 적합합니다.
-  전체 플랫폼: 멀티미디어 링크의 네트워크 저항력을 최적화하여 극단적인 네트워크 검색 상황(70%)에서도 멀티미디어가 비교적 원활하게 재생됩니다.
-  Windows: 일부 시나리오의 라이브 방송 음질을 최적화하여 오디오 품질 저하 문제가 대폭 감소되었습니다.
-  Windows: 성능 최적화를 통해 일부 사용 시나리오에서 구버전 대비 성능이 20%~30% 향상되었습니다.

**문제 수정**
- Mac: Mac mini (m1)에서 전체 화면 공유로 전환한 후 다시 특정 창으로 돌아올 때, 원격에서는 여전히 전체 화면 공유 창이 표시되는 문제 수정
- Mac: Mac에서 화면 공유 시 하이라이트되지 않는 문제(Mac 시스템 11.1, 10.14.5에서 녹색 프레임이 나타나지 않는 문제, Mac 시스템 10.3.2에서 녹색 프레임은 나타나지만 창을 확대하면 깜빡이는 문제) 해결
-  Mac: Mac mini m1에서 화면 공유 리스트 획득 crash 시, 하위 레이어 sourceName이 null인 경우 상위 레이어에서 ""를 반환하는 문제 수정
-  Mac: Mac mini m1, getCurrentMicDevice로 인해 crash(sourceName)가 null이 되는 문제 수정
-  Windows: Windows Server 2019 Datacenter x64 시스템에서 데스크톱 공유 실행 시 crash 문제 수정
-  Windows: 창 공유와 동시에 타깃 창의 크기를 변경할 때 가끔 공유가 중지되는 BUG 수정
-  Windows: 일부 모델의 카메라에서 화면을 수집하지 못하는 문제 수정

## Version 8.2.7 @ 2021.01.06

**추가**
- Windows & Mac: [switchRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRoom) 방 전환 추가
- Windows & Mac: [setLocalRenderParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalRenderParams) 로컬 이미지(주요)를 설정하는 렌더링 매개변수 추가
- Windows & Mac: [setRemoteRenderParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteRenderParams) 원격 이미지를 설정하는 렌더링 매개변수 추가
- Windows & Mac: [startPlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPlayMusic) 배경 음악 재생 실행 추가
- Windows & Mac: [stopPlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPlayMusic) 배경 음악 재생 중지 추가
- Windows & Mac: [pausePlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pausePlayMusic) 배경 음악 재생 일시 중지 추가
- Windows & Mac: [resumePlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumePlayMusic) 배경 음악 다시 재생 추가
- Windows & Mac: [getMusicDurationInMS](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getMusicDurationInMS) 배경 음악 파일 총 시간 획득 추가, 단위: 밀리초
- Windows & Mac: [seekMusicToPosInTime](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#seekMusicToPosInTime) 배경 음악 재생 진행률 설정 추가
- Windows & Mac: [setAllMusicVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAllMusicVolume) 배경 음악 음량 설정 추가, 배경 음악 오디오 믹싱 시 배경 음악 음량 조절에 사용
- Windows & Mac: [setMusicPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMusicPlayoutVolume) 배경 음악 로컬 재생 음량 설정 추가
- Windows & Mac: [setMusicPublishVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMusicPublishVolume) 배경 음악 원격 재생 음량 설정 추가
- Windows & Mac: [onSwitchRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSwitchRoom) 방 전환 콜백 추가
- Windows & Mac: [setRemoteAudioVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteAudioVolume) 원격 사용자 재생 음량 설정 추가
- Windows & Mac: [snapshotVideo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#snapshotVideo) 비디오 화면 캡처 추가
- Windows & Mac: [onSnapshotComplete](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSnapshotComplete) 화면 캡처 완료 시 콜백 추가

**개선**
- Windows & Mac: enterRoom 및 switchRoom 시 string 유형의 strRoomId 지원
- Windows & Mac: 기타 bug 수정

## Version 7.9.348 @ 2020.11.12

**개선**
- Windows: 녹음 경로 설정 시 중국어 경로 폴더 미지원 수정
- Windows: 창에서 특정 구역 캡처 시 차단 방지 지원

## Version 7.8.342 @ 2020.10.10

**추가**
- Windows & Mac: [onAudioDeviceCaptureVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) 현재 오디오 수집 디바이스 음량 변경 콜백 추가
- Windows & Mac: [onAudioDevicePlayoutVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) 현재 오디오 재생 디바이스 음량 변경 콜백 추가

## Version 7.7.330 @ 2020.09.11

**추가**
Windows & Mac: [setAudioQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioQuality) 추가, 오디오 품질 설정에 사용

**개선**
- Windows: 일부 저가형 카메라의 지나치게 높은 CPU 사용률 문제 최적화
- Windows: 멀티 USB 카메라와 마이크에 대한 호환성 최적화로 디바이스의 실행 성공률 향상
- Windows: 카메라와 마이크 디바이스 선택 정책 최적화로 카메라 또는 마이크 사용 중 소켓으로 인한 샘플링 오류 문제 방지
- Windows & Mac: 기타 bug 수정

## Version 7.6.300 @ 2020.08.26

**추가**
Windows & Mac: [setCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceMute), [getCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceMute), [setCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDeviceMute), [getCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDeviceMute) 추가, PC의 마이크 및 스피커 제어에 사용

## Version 7.5.210 @ 2020.08.11

**개선**
- Windows & Mac: SDK 콜백 비순차 문제 수정
- Windows & Mac: 렌더링 모드 전환 시 크래쉬 문제 해결 
- Windows & Mac: 일부 해상도 렌더링 실패 문제 수정 
- Windows & Mac: 기타 bug 수정

## Version 7.4.204 @ 2020.07.01

**개선**
- Windows: Windows 플랫폼의 반향 제거(AEC) 효과 최적화
- Windows: Windows 플랫폼의 카메라 수집 디바이스 호환성 향상
- Windows: Windows 플랫폼의 오디오 디바이스(마이크 및 스피커) 호환성 향상
- Windows: Windows 버전 onPlayAudioFrame 콜백의 UserID가 부정확한 문제 수정
- Windows: 64비트에서 시스템 오디오 믹싱 지원

## Version 7.2.174 @ 2020.04.20

**개선**
- Mac: Mac에서 가끔 로컬 사용자 정의 렌더링 해상도가 일치하지 않는 문제 수정
- Windows: Windows의 getCurrentCameraDevice 로직을 최적화하여 카메라 미사용 시 첫번째 디바이스를 기본 디바이스로 반환
- Windows: 화면 공유 시 하이라이트 창이 회색으로 보이는 문제 수정
- Windows: Win10 시스템에서 화면 공유 썸네일 획득 시 가끔 랙이 걸리는 문제 수정
- Windows & Mac: 역할 전환 시 가끔 사용자 정의 스트림 ID가 즉시 적용되지 않는 문제 수정
- Windows & Mac: 화면 공유 설정 인코딩 매개변수가 적용되지 않는 문제 수정
- Windows: Windows 화면 공유 후 webrtc에서 오랫동안 기다려야 화면을 볼 수 있는 문제 수정

## Version 7.1.157 @ 2020.04.02

**추가**

[메인 채널](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoStreamType)을 사용한 [화면 공유](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) 지원

**개선**
- [혼합 스트림 사전 설정 템플릿](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode)의 활용성 최적화
- [혼합 스트림](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig) 최적화로 성공률 향상
- Windows 화면 공유 최적화


## Version 7.0.149 @ 2020.03.019

**추가**

[trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141) 파일 추가로 typescript를 사용하는 개발자의 편리성 향상
