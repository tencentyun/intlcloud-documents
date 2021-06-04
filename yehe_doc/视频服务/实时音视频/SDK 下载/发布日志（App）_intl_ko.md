## Version 8.6 @ 2021.05.08
- 전체 플랫폼: 네트워크 트래픽 제어 알고리즘이 최적화되어 멀티미디어 전송 품질이 더욱 향상되었습니다.
- 전체 플랫폼: 역할 전환으로 마이크 켜짐/꺼짐 시 원활하게 오디오가 재생되도록 최적화되었습니다.
- iOS&Mac&Windows: 오디오 처리 모듈이 최적화되어 SPEECH 모드와 DEFAULT 모드의 음성 품질이 향상되었습니다.
- iOS&Mac: 높은 CPU 시나리오에서 사용자 정의 오디오 수집 맞춤성이 최적화되었습니다.
- iOS&Android: 비디오 녹화 시 서브 채널을 통한 공유로 데스크톱 버전 정렬을 지원합니다.
- Mac: Apple M1 아키텍처에 대한 네이티브 지원이 추가되었습니다.
- Windows: 메모리 할당 로직이 최적화되어 안정성이 향상되었습니다.


## Version 8.5 @ 2021.03.24
**새로운 기능**
-  Mac: 화면 공유 기능이 최적화되어 타깃 창 공유 시 동시에 다른 창을 지정해 함께 공유할 수 있습니다. 자세한 내용은 API [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233)를 참조하십시오.
-  전체 플랫폼: 새로운 방송 기능이 추가되었습니다. [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#classcom_1_1tencent_1_1rtmp_1_1TXVodPlayer)와 TRTCCloud를 바인딩하여 현재 재생 중인 VOD 콘텐츠를 TRTC 서브 채널 푸시 스트림을 통해 공유할 수 있습니다.
-  전체 플랫폼: 서브 채널 사용자 정의 수집이 추가되었습니다. API [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629)를 참조하십시오.
-  전체 플랫폼: 사용자 정의 믹싱 기능이 추가되었습니다. 사용자의 오디오 트랙을 SDK의 오디오 처리 프로세스에 혼합할 수 있으며, SDK가 먼저 두 오디오 트랙을 혼합한 후 다시 배포합니다. 자세한 내용은 API [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f)을 참조하십시오.
-  전체 플랫폼: 지정 퓨어 비디오 혼합 스트림을 지원하여 더 효율적으로 혼합 스트림을 제어합니다.

**품질 최적화**
- Mac: startSystemAudioLoopback에서 듀얼 사운드 채널을 지원합니다.
- Windows: 슬라이드 창을 선택해 화면 공유 시 방송 창을 자동으로 전환합니다.
- 전체 플랫폼: 상태 콜백에 end to end 딜레이가 추가되었습니다.

**문제 수정**
- iOS: 일부 디바이스에서 가끔 백그라운드 OpenGL에 렌더링 crash가 발생하는 문제가 최적화되었습니다.
- iOS: 화면 정지 시 화면 공유를 재생하면 재생되지 않는 문제가 최적화되었습니다.


## Version 8.4 @ 2021.02.08
**새로운 기능**
- Mac: Mac 운영 체제의 출력 음성 수집을 지원합니다. Windows와 동일한 SystemLoopback 기능이며, 이 기능을 통해 SDK에서 현재 시스템의 음성을 수집할 수 있습니다. 해당 기능을 활성화하면 호스트가 편리하게 다른 사용자에게 음악 또는 영화 파일을 라이브 방송할 수 있습니다.
-  Mac: 화면 공유 시 로컬 미리보기 기능을 지원합니다. 미니 창을 통해 공유할 화면 콘텐츠를 미리 볼 수 있습니다.
-  Windows: 프로세스 음량 조절 기능이 추가되었습니다. [setApplicationPlayVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1)을 사용해 시스템 음량 믹서의 음량 크기를 설정할 수 있습니다.
-  전체 플랫폼: 로컬 멀티미디어 녹화 기능이 추가되었습니다. 호스트가 푸시 스트림 중에 로컬 오디오와 비디오를 mp4 파일로 녹음 및 녹화할 수 있습니다. 자세한 내용은 [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b)을 참조하십시오.

**품질 최적화**
- 전체 플랫폼: [Music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) 모드에서의 오디오 품질을 최적화하여 cloubhouse와 유사한 음성 라이브 방송 시나리오에 더욱 적합합니다.
-  전체 플랫폼: 멀티미디어 링크의 네트워크 저항력을 최적화하여 극단적인 네트워크 검색 상황(70%)에서도 멀티미디어가 비교적 원활하게 재생됩니다.
-  Windows: 일부 시나리오의 라이브 방송 음질을 최적화하여 오디오 품질 저하 문제가 대폭 감소하였습니다.
-  Windows: 성능 최적화를 통해 일부 사용 시나리오에서 구버전 대비 성능이 20%~30% 향상되었습니다.

**문제 수정**
-  Windows: Windows Server 2019 Datacenter x64 시스템에서 데스크톱 공유 실행 시 crash가 발생하는 문제가 수정되었습니다.
-  Windows: 창 공유와 동시에 타깃 창의 크기를 변경할 때 가끔 공유가 중지되는 BUG가 수정되었습니다.
-  Windows: 일부 모델의 카메라에서 화면을 수집하지 못하는 문제가 수정되었습니다.
-  iOS: snapvideoshot에서 CAAnimation에 랙이 발생하는 문제가 수정되었습니다.
-  iOS&Mac: 동일한 View 로테이션 스트림을 사용해 카메라 화면 및 공유 화면을 표시할 때 공유 화면이 블랙 스크린이 되는 문제가 수정되었습니다.
-  iOS: iPhone 6s에서 3rd party 뷰티 필터 모듈 사용 시 화면이 뿌옇게 되는 문제가 수정되었습니다.
-  iOS: VOD와 TRTC 동시 사용 시 VOD 재생을 중지하면 가끔 crash가 발생하는 문제가 수정되었습니다.
-  Android: 블루투스 이어폰 사용 중에 전화가 와서 연결이 끊어졌을 시, 전화 수신 거부 후 음성이 마이크를 통해 재생되는 문제가 수정되었습니다.

## Version 8.3 @ 2021.01.15

**새로운 기능**

이 버전에서는 사용자 정의 수집 관련 비즈니스 로직을 중점적으로 최적화되었습니다.
- iOS & Android & Mac: 오디오 모듈이 최적화되었습니다. [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d)로 캡처한 오디오 데이터를 SDK에 전송하여 처리할 때 SDK가 에코 억제 및 노이즈 감소 효과를 유지할 수 있습니다.
- iOS & Android: TRTC SDK를 기반으로 오디오 특수효과 및 처리 로직을 지속적으로 강화해야 할 경우 8.3 버전을 사용하면 더욱 간편해집니다. [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86)과 같은 인터페이스를 통해 오디오 데이터의 콜백 포맷(오디오 샘플링 레이트, 오디오 채널 수, 샘플링 포인트 등)을 설정하여 사용자가 선호하는 음성 포맷으로 오디오 데이터를 처리할 수 있습니다.
- 모든 플랫폼: 비디오 데이터를 자체 수집하고 TRTC SDK 자체 오디오 모듈을 사용해야 할 경우 오디오-비디오 동기화가 이루어지지 않는 문제가 발생할 수 있습니다. 이는 SDK 내부 타임라인의 자체 제어 로직으로 인해 발생하는 것으로, 이 문제에 대한 대응책으로 [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) 인터페이스가 제공됩니다. 비디오 화면을 수집할 때 이 인터페이스를 사용해서 현재 PTS(타임스탬프)를 기록한 다음 [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831)를 호출할 때 이 타임스탬프를 적용하면 오디오/비디오 동기화를 유지할 수 있습니다.
- Windows: 버전 SDK에 도메인 포맷에 대한 Socks5 프록시 지원이 추가되었습니다.

**문제 수정**
- 모든 플랫폼: 간혹 오디오 데이터의 타임스탬프에 오류가 발생하여 녹화된 부분에서 오디오-비디오 동기화가 유지되지 않는 문제가 수정되었습니다.
- Windows: 고 DPI 환경에서 창 공유 호환성이 최적화되었습니다.
- Windows: 공유할 수 있는 창 목록을 가져올 때 최소화된 창을 추가합니다. 최소화된 창의 썸네일은 해당 프로세스의 아이콘으로 표시됩니다.
- Windows: SDK 실행 시 불필요한 DXGI 점유 문제가 수정되었습니다.
- iOS: 수동 포커스를 설정할 경우 ANR이 발생하는 문제가 수정되었습니다.
- iOS: 가끔 전환 전후로 카메라가 인식되지 않는 문제가 수정되었습니다.
- iOS: VODPlayer 감속 재생 시 crash가 발생하는 문제가 수정되었습니다.
- iOS: 가끔 방에 입장한 후 헤드셋에서 오디오가 재생되는 문제가 수정되었습니다.
- iOS & Android: 에코 제거 및 잡음 억제 효과가 최적화되어 인이어 모니터링에서도 잔향 효과를 들을 수 있습니다.
- Android: 가끔 하드웨어 디코딩 시 화면 출력 오류가 나타나는 문제가 수정되었습니다.
- Mac: 창 공유 및 고휘도 모드 활성화 시 창 프레임이 반짝이는 문제가 수정되었습니다.
- Mac: 렌더링 투시도 이동 시 블랙 스크린이 발생하는 문제가 수정되었습니다.


## Version 8.2 @ 2020.12.23

**새로운 기능**
- iOS&Android: 로컬 수집과 재생된 모든 오디오 데이터의 혼합 콜백이 추가되어 로컬 오디오 녹음이 더욱 편리해졌습니다.
- Android: 비디오 렌더링 모듈 TXCloudVideoView에서 `addVideoView(new TextureView(getApplicationContext()))` 인터페이스를 통해 TextureView를 로컬 렌더링에 사용하도록 지원합니다.
- Android: 사용자 정의 렌더링 콜백에서 RGBA 포맷의 비디오 데이터를 지원합니다.
- Windows: 로컬 카메라 수집과 원격 비디오 스트림 캡처 재생을 지원합니다. [ITRTCCloud.snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96)를 참조하십시오.
- Windows: 화면 공유에서 addExcludedShareWindow와 addIncludedShareWindow 인터페이스를 통해 지정된 창 제외 또는 강제 포함 기능을 지원하여 보다 유연한 화면 공유 기능을 제공합니다.
- Mac&iOS: 사용자 정의 렌더링 모드에서도 TRTCCloud.snapshotVideo를 호출하여 비디오 스트림 이미지를 추출할 수 있습니다.

**품질 최적화**
- Android: 온라인 라이브 방송 인코딩 품질이 최적화되어 더욱 선명한 비디오 화면을 제공합니다.
- Windows: 에코 제거 알고리즘이 최적화되어 에코 제거 효과가 향상되었습니다.

**문제 수정**
- iOS: VODPlayer와 TRTC를 동시에 사용할 경우 가끔 오디오 재생 오류가 발생하는 문제가 수정되었습니다.
- Android: 사용자 정의 뷰티 필터로 인한 로컬 렌더링 블랙 스크린 문제가 수정되었습니다.
- Windows: 가끔 현재 진행 중인 프로세스를 종료할 수 없는 문제가 수정되었습니다.


## Version 8.1 @ 2020.12.03

**새로운 기능**
-모든 플랫폼: 통계 정보(onStatistics)에 원격 비디오 랙과 관련된 통계 지표가 추가되었습니다.
-모든 플랫폼: 음량 조절 인터페이스 setAudioPlayoutVolume(100-150)를 통해 오디오 부스터 효과를 적용할 수 있습니다.
- iOS&Android: setLocalVideoProcessListener 인터페이스가 추가되어 3rd party 뷰티 필터 SDK 통합 지원 기능이 향상되었습니다.
- C#: 최신 버전의 API 인터페이스로 업데이트되었습니다.

**품질 최적화**
- 모든 플랫폼: 이어폰 착용 시 음성 처리 알고리즘이 최적화되어 오디오 품질이 향상되었습니다.
- Android: 오디오 전처리 알고리즘이 최적화되어 3A 알고리즘이 음질에 미치는 영향이 감소하였습니다.

**문제 수정**
- iOS: 가끔 App 강제 종료 시 크래쉬가 발생하는 문제가 수정되었습니다.
- Android: 프레임 레이트 수집이 높을 경우 뷰티 필터 효과에 오류가 발생하는 문제가 수정되었습니다.
- Windows: 고 DPI 환경에서 화면 공유 시 가끔 크래쉬가 발생하는 문제가 수정되었습니다.


## Version 8.0 @ 2020.11.13

**추가**
- 모든 플랫폼에 C++ 통합 API가 추가되었습니다. cpp_interface/[ITRTCCloud.h](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html)를 참조하십시오.
- 모든 플랫폼에서 문자열 방 번호를 지원합니다. TRTCParams.strRoomId를 참조하십시오.
- 모든 플랫폼에 TXDeviceManager 장치 관리 클래스가 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.switchRoom이 추가되어 수집을 중단하지 않고 직접 방을 전환할 수 있습니다.
- 모든 플랫폼에 API TRTCCloud.startRemoteView 원격 비디오 화면 렌더링 시작 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.stopRemoteView 원격 비디오 화면 렌더링 중지 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.getDeviceManager 장치 관리 유형 획득 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.startLocalAudio 로컬 오디오 수집과 업스트림 활성화 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.setRemoteRenderParams 원격 이미지의 렌더링 사양 설정이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.setLocalRenderParams 로컬 이미지의 렌더링 사양 설정이 추가되었습니다.

**최적화**
- Android에서 소프트웨어/하드웨어 디코딩 전환 로직이 최적화되었습니다.
- Windows에서 System loopback 오디오 음질 수집 및 에코 제거 효과가 최적화되었습니다.
- Windows에서 오디오 디바이스 선택 로직을 최적화하여 Silent rate가 감소하였습니다.
- Windows에서 동시 음성 제거 효과가 최적화되었습니다.
- 모든 플랫폼에서 수동 수신 모드 역할 전환 시 발생하는 바로 재생 효과가 최적화되었습니다.
- 모든 플랫폼에서 오디오 수신 로직이 최적화되어 오디오 효과가 향상되었습니다.
- 모든 플랫폼에서 sendCustomCmdMsg 신뢰성이 최적화되었습니다.

**수정**
- iOS에서 muteLocalVideo 호출 시 로컬 비디오 렌더링이 일시 중지되는 문제가 수정되었습니다.
- iOS에서 프론트/백그라운드 전환 시 호출 시스템 모듈에서 크래쉬가 발생하는 문제가 수정되었습니다.
- iOS에서 오디오 활성화 시 인이어 모니터링 오디오가 계속 끊기는 문제가 수정되었습니다.
- Android에서 통화 소리가 끊길 때 전화를 끊어도 효과음이 계속해서 재생되는 문제가 수정되었습니다.
- Android에서 가끔 오디오 수집 실행에 실패하는 문제가 수정되었습니다.
- Windows에서 가끔 로컬 비디오 렌더링 시 블랙 스크린이 발생하는 문제가 수정되었습니다.
- Windows에서 프로세스 종료 시 가끔 crash가 발생하는 문제가 수정되었습니다.
- Windows에서 블루투스 이어폰 지원을 최적화하여 블루투스 이어폰에서 소리가 나지 않는 문제가 수정되었습니다.
- Windows에서 화면 공유 종료 시 포커스 상실 문제가 수정되었습니다.
- 모든 플랫폼에서 상태 콜백 패킷 손실률 통계 오류가 수정되었습니다.



## Version 7.9 @ 2020.10.27
**추가**
- Mac: 화면 공유에 선택 창 필터링 기능을 지원합니다. 공유하지 않는 창은 제거하여 보다 개선된 사생활 보호를 제공합니다.
- Windows: 화면 공유의 ‘공유 중’ 알림창 프레임 색상과 프레임 크기 설정 기능을 지원합니다.
- Windows: 화면 공유 기능으로 전체 화면을 공유할 때 고성능 모드를 지원합니다.
- 모든 플랫폼: 사용자 정의 암호화를 지원해 인코딩된 멀티미디어 데이터를 노출된 C 인터페이스를 통해 2차 처리할 수 있습니다.
- 모든 플랫폼: TRTCRemoteStatistics에 오디오 랙 정보 콜백 `audioTotalBlockTime`과 `audioBlockRate`가 추가되었습니다.

**최적화**
- iOS: 오디오 모듈의 실행 속도가 최적화되어 첫 번째 오디오 프레임을 더 빨리 수집해 전송할 수 있습니다.
- Windows: 시스템 루프백의 에코 제거 알고리즘이 최적화되어 시스템 루프백(SystemLoopback) 활성화 시 에코 제거 능력이 강화되었습니다.
- Windows: 화면 공유 기능의 창 수집 차단 방지 기능이 최적화되어 창 필터 설정 기능을 지원합니다.
- Android: 대부분의 Android 모델에서 인이어 모니터링 효과를 최적화하여 인이어 모니터링 딜레이가 적정 수준까지 감소합니다.
- Android: Music 모드(startLocalAudio인 경우 지정)에서의 P2P 딜레이가 최적화되었습니다.
- 모든 플랫폼: 수동 구독 모드에서 시청자와 호스트 역할 전환 시의 오디오 유연성이 최적화되었습니다.
- 모든 플랫폼: 멀티미디어 통화에서 약한 네트워크에 대한 저항성이 최적화되어 네트워크 환경이 좋지 않은 상황에서의 오디오 유연성이 향상되었습니다.

**수정**
- iOS: 일부 시나리오에서 가끔 비디오 화면이 렌더링되지 않는 문제가 수정되었습니다.
- iOS: 사용자가 이어폰을 착용하고 음질이 Default인 상태에서 가끔 잡음이 발생하는 문제가 수정되었습니다.
- iOS: 현재 알려진 일부 메모리 누수 문제가 수정되었습니다.
- iOS: replaykit 확장 녹화 종료 시 가끔 crash가 발생하는 문제가 수정되었습니다.
- iOS: 시뮬레이터 환경에서의 컴파일 문제가 해결되었습니다.
- Android: 일부 모바일 기기에서 App이 장시간 동안 백그라운드로 전환된 이후에 다시 프론트로 전환될 경우 가끔 오디오-비디오 동기화가 이루어지지 않는 문제가 수정되었습니다.
- Android: 백그라운드 전환 이후 마이크 릴리스가 되지 않는 문제가 수정되었습니다.
- Android: SDK 내부의 일부 OpenGL 리소스가 제때 릴리스되지 않는 문제가 수정되었습니다.
- Windows: 개별 시나리오에서 가끔 잡음이 발생하는 문제가 수정되었습니다.
- 모든 플랫폼: 가끔 일부 크래쉬가 발생하는 문제를 수정하여 SDK 안정성이 향상되었습니다.

## Version 7.8 @ 2020.09.29
**추가**
- Mac: 시스템 음량 변화 콜백이 추가되었습니다. 자세한 내용은 [TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f)를 참조하십시오.
- Windows: 스크린 간 영역을 지정하여 화면을 공유하는 기능이 추가되었습니다.
- Windows: 창 공유에 지정 창 필터링을 추가해 차단을 방지합니다. 자세한 내용은 [TRTCCloud.addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5141a9331c3675f17fbdc922f376b06) 및 [TRTCCloud.removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a08504ce347b593c0191904611da5cfd2)를 참조하십시오.
- Windows: 시스템 음량 변화 콜백이 추가되었습니다. 자세한 내용은 [ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12)를 참조하십시오.

**최적화**
- iOS: VODPlayer와 trtc 동시 사용 및 에코 제거를 지원합니다.
- iOS&Mac: 조정화면 푸시스트림을 지원합니다. 사용 방법은 [TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2)를 참조하십시오.
- Android: 조정화면 푸시스트림을 지원합니다. 사용 방법은 [TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d)를 참조하십시오.
- Android: 오디오 라우팅 정책이 최적화되어 이어폰 착용 시 오디오가 이어폰으로만 재생되는 기능이 지원됩니다.
- Android: 일부 시스템에서 저딜레이 수집 재생을 지원하여 Android 시스템의 통화 딜레이가 감소하였습니다.
- Android: VODPlayer와 trtc 동시 사용 및 에코 제거를 지원합니다.
- Windows: 가상 카메라 e2eSoft Vacm과 호환됩니다.
- Windows: startLocalPreview와 startCameraDeviceTest 동시 호출을 지원합니다.
- Windows: 화면을 메인 채널로 공유하고, startLocalPreview 호출 시 로컬 미리보기를 활성화합니다.
- Windows: SDK 내부 재생 버퍼로 인한 오디오 딜레이가 커지는 문제가 감소하였습니다.
- Windows: 오디오 실행 로직이 최적화되어 재생 상황에 한정해 마이크를 점유하지 않습니다.



**수정**
- iOS: iPhone SE 재생 음량이 작은 문제가 수정되었습니다.
- iOS: 하위 방(TRTCCloud.createSubCloud)에서 muteRemoteAudio 호출 시 crash가 발생하는 문제가 수정되었습니다.
- iOS: 가끔 렌더링 중 crash가 발생하는 문제가 수정되었습니다.
- iOS: 프론트/백그라운드 전환 시 일부 iPad에서 비디오 렌더링 중 가끔 메인 스레드가 크래쉬되는 문제가 수정되었습니다.
- iOS: 알려진 메모리 누수 문제가 수정되었습니다.
- iOS: iOS14에서 ‘로컬 네트워크에 있는 장치를 찾아 연결하기’ 알림이 뜨는 문제가 수정되었습니다.
- Mac: getCurrentCameraDevice가 계속 nil을 반환하는 문제가 수정되었습니다.
- Mac: 일부 USB 카메라를 열 수 없는 문제가 수정되었습니다.
- Mac: 화면 공유의 지정 영역 면적이 0일 경우 crash가 발생하는 문제가 수정되었습니다.
- Android: READ_PHONE_STATE 권한이 설정되지 않았을 경우 Android5.0 디바이스에서 crash가 발생하는 문제가 수정되었습니다.
- Android: 블루투스 이어폰을 제거한 후 재연결했을 때, 오디오 수집 및 재생 시 오류가 발생하는 문제가 수정되었습니다.
- Android: 알려진 crash 문제가 수정되었습니다.
- Windows: 64비트 SDK에서 화면 공유 기능을 여러 번 활성화할 경우 crash가 발생하는 문제가 수정되었습니다.
- Windows: 일부 시스템에서 OpenGL을 사용할 경우 crash가 발생하는 문제가 수정되었습니다.


## Version 7.7 @ 2020.09.08

**최적화**

- 모든 플랫폼: 서브 채널(화면 공유)의 바로 재생 속도가 최적화되었습니다.
- iOS: 내부 스레드 모델이 최적화되어 30개 이상의 채널에서 동시 재생하는 시나리오에서의 실행 안정성이 향상되었습니다.
- iOS&Android: Audio 모듈 기능이 최적화되어 첫 번째 프레임의 수집 딜레이가 향상되어 최신 버전에서는 첫 번째 오디오 프레임을 더 빨리 획득할 수 있습니다.
- iOS&Android: VodPlayer와 TRTC를 동시에 사용할 경우의 음량 크기 및 음질이 최적화되었습니다.
- iOS&Android: wav 오디오 포맷의 배경 음악과 효과음 지원 파일이 추가되었습니다.
- Windows: 일부 저가형 카메라의 CPU 사용률이 지나치게 높은 문제가 최적화되었습니다.
- Windows: 멀티 USB 카메라와 마이크에 대한 호환성이 최적화되어 디바이스의 실행 성공률이 향상되었습니다.
- Windows: 카메라와 마이크 기기 선택 정책이 최적화되어 카메라 또는 마이크 사용 중 소켓으로 인해 수집 오류가 발생하는 문제가 방지됩니다.

**수정**

- 모든 플랫폼: 네트워크가 약한 경우, muteLocalVideo 및 muteLocalAudio 인터페이스 호출 시 가끔 재생 오류가 발생하는 BUG가 수정되었습니다.
- iOS: 저가형 iPhone 또는 iPad에서 오디오 재생 시 가끔 재생에 실패하는 BUG가 수정되었습니다.
- iOS: iPad Pro에서 화면 공유 시 공유된 화면이 늘어나는 문제가 수정되었습니다.
- iOS: App 내부 화면에서 사용자가 권한을 거절했음에도 지속적으로 화면 녹화 권한을 요청하는 문제가 수정되었습니다.
- Windows: 노트북 또는 데스크톱이 장기간 휴면 상태일 때, 퇴장 [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) 이벤트 공지가 콜백되지 않는 문제가 수정되었습니다.
- Windows: Music 음질 모드에서 시스템 오디오 루프백 [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23)을 활성화하면 에코가 누락되는 문제가 수정되었습니다.
- Windows: enterRoom과 exitRoom을 빠르게 호출하여 방 입장/퇴장을 할 경우 가끔 소리가 들리지 않는 BUG가 수정되었습니다.
- Windows: SDK의 Visual Stuido 2010 프로젝트 컴파일 편집 호환성 문제가 수정되었습니다.
- Windows: 수동 수신 모드([setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5))에서 onUserVideoAvailable 이벤트 콜백을 중복 수신하는 문제가 수정되었습니다.


## Version 7.6 @ 2020.08.21
**추가**

- Windows: HWND 유형의 렌더링 창을 더 쉽게 실시간으로 조정할 수 있는 [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5211a2739df8d8ec6017559b3aa0299)와 [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8c8247cbc679ea144ffb393b6b940c9e) 인터페이스가 추가되었습니다.
- Windows: 현재 Windows PC가 음소거로 설정되어 있는지를 확인하는 데 사용할 수 있는 [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) 인터페이스가 추가되었습니다.
- Windows: 현재 Windows PC를 음소거로 설정할 수 있는 [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) 인터페이스가 추가되었습니다.
- Mac: View 렌더링 영역을 더 쉽게 실시간으로 조정할 수 있는 [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb)와 [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) 인터페이스가 추가되었습니다.
- Mac: 현재 Mac이 음소거로 설정되어 있는지 확인하는 데 사용할 수 있는 [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f) 인터페이스가 추가되었습니다.
- Mac: 현재 Mac을 음소거로 설정할 수 있는 [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) 인터페이스가 추가되었습니다.
- iOS: View 렌더링 영역을 더 쉽게 실시간으로 조정할 수 있는 [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb)와 [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) 인터페이스가 추가되었습니다.
- iOS: TRTCCloudDelegate에 [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) 콜백을 추가하고, 기타 몇 가지 콜백 함수 이름을 변경했습니다. 순서대로 [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0), [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a), [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e)입니다.
- Android: TRTCCloudListener에 [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) 콜백을 추가하고, 기타 몇 가지 콜백 함수 이름을 변경했습니다. 순서대로 [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46), [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902), [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7)입니다.

**최적화**

- 모든 플랫폼: enterRoom의 프로토콜 정책이 최적화되어 방 입장 속도와 성공률이 향상되었습니다.
- 모든 플랫폼: 다수의 오디오를 구독할 경우에 발생하는 전반적 성능 소모와 랙 문제가 최적화되었습니다.
- Mac: 화면 공유에 지정 창의 지정한 영역 공유 기능을 지원합니다.

**수정**

- 모든 플랫폼: 방에서 퇴장하지 않은 상태에서 다른 방에 입장할 경우 SDK에서 onEnterRoom이 트리거되지 않는 BUG가 수정되었습니다.
- 모든 플랫폼: 블랙 스크린을 유발할 수 있는 몇몇 내부 BUG가 수정되었습니다.
- 모든 플랫폼: startRemoteSubStreamView 사전 호출 시 공유된 화면이 정상적으로 표시되지 않는 문제가 수정되었습니다.
- Windows: 알려진 일부 핸들 및 GDI 누락이 수정되었습니다.
- Windows: 알려진 다수의 crash 문제가 수정되었습니다.
- Windows: 카메라와 마이크를 뺀 후 다시 꽂았을 때 자동으로 장치가 활성화되지 않는 문제가 수정되었습니다.
- iOS: iOS 10에서 배경 음악 인터페이스를 특정 규칙의 파일 경로로 전송했을 때 크래쉬가 발생하는 BUG가 수정되었습니다.
- Android: 빈번하고 빠른 enterRoom 및 exitRoom 이후 가끔 소리가 들리지 않는 문제가 수정되었습니다.
- Android: 가끔 푸시 스트림 화면이 블랙 스크린으로 녹화되는 문제가 수정되었습니다.


## Version 7.5 @ 2020.07.31

**추가**

- 더블 스택 IPV6와 IPV6 only에 대한 지원이 추가되었습니다.
- 소그룹 수업 지원에 사용되는 다수 방 입장 시 풀 스트림 기능이 추가되었습니다.
- 클라우드 MCU 혼합 스트림에 배경 이미지(모니터링이 필요하므로 이미지는 TRTC 콘솔에 먼저 업로드해야 함) 설정 기능이 추가되었습니다.
- 클라우드 MCU 혼합 스트림에 A+B=>C와 A+B=>A 모드가 추가로 지원됩니다.
- 실시간 상태 콜백 onStatistics에 재생 버퍼 시간 필드 jitterBufferDelay가 추가되었습니다.

**최적화**

- 클라이언트 간 마이크 연결 딜레이가 감소하였습니다. 7.5 버전 클라이언트 간 통화 및 마이크 연결 딜레이가 7.4 버전 기준 40% 감소하였습니다.
- 모바일 디바이스의 인이어 모니터링 딜레이가 감소하였으며, 인이어 모니터링에 음성 변조 및 잔향 등과 같은 음향 효과 설정이 지원됩니다.
- 클라이언트 네트워크 지터 평가 알고리즘이 최적화되어 재생 딜레이가 감소하였습니다.
- Android SDK의 end-to-end 마이크 연결 통화 딜레이가 감소하였습니다.
- 인이어 모니터링 딜레이 문제가 한층 더 최적화되었습니다.
- 재생 view 동적 전환 시 블랙 스크린이 발생하는 문제가 최적화되었습니다.

**수정**

- 하나의 함수에서 연속으로 playBGM과 pauseBGM을 호출하면 재생되지 않는 문제가 수정되었습니다.
- 가끔 방에서 나간 이후에도 onEnterRoom 콜백을 수신하는 문제가 수정되었습니다.
- 일부 모델에서 초저해상도 인코딩 및 복구가 되지 않는 문제가 수정되었습니다. 

##  Version 7.4 @ 2020.06.24 

**최적화**

인이어 모니터링에서 음량 설정을 지원합니다.

**수정**

- Android 버전에서 가로-세로 화면 전환 시 로컬 화면이 깜빡이는 문제가 수정되었습니다.
- 일부 Android 핸드폰에서 사용자 정의 비디오를 전송하면 정상적으로 인코딩되지 않는 문제가 수정되었습니다.
- 오디오 처리 시 가끔 데이터 패킷에서 크래쉬가 발생하는 문제가 수정되었습니다.



##  Version 7.3 @ 2020.06.01

**추가**

- 기존 인터페이스가 호환되는 상황에서 신규 음향 효과 관리 인터페이스 TXAudioEffectManager가 추가되었습니다. 해당 기능은 더욱 빠르고 다양한 음향 효과 기능을 지원합니다.
- 비디오 인코딩 매개변수 setVideoEncoderParam에 minVideoBitrate 옵션이 추가되었습니다. 화질 요구 사항이 높은 라이브 방송 클라이언트에게 추천합니다.

**최적화**

- 오디오에 순간 노이즈 감소 기능이 지원됩니다. setAudioQuality(TRTCAudioQualitySpeech)를 통해 활성화할 수 있습니다.
- asset 패키지 음향 효과 파일을 지원합니다.
- 로컬 비디오 해상도가 향상되었습니다.
- 사용자 정의 렌더링 재생에 텍스쳐 매핑 방식이 지원되어 성능 저하가 감소하였습니다.
- 카메라 수집 해상도 선택 로직이 최적화되어 시각 효과가 향상되었습니다.
- 에코 처리 효과가 최적화되었습니다.
- 모든 링크에서 128kbps 고음질 입체 음성을 지원합니다. setAudioQuality(TRTCAudioQualityMusic) 인터페이스를 통해 설정할 수 있습니다.
- SPEECH 음성 모드를 지원합니다. 회의 시나리오의 음성 통화에 적합합니다. 더 강력한 노이즈 감소(ANS) 효과를 원하는 경우 setAudioQuality(TRTCAudioQualitySpeech)에서 설정할 수 있습니다.
- 다중 배경 음악 동시 재생 기능이 지원됩니다. 메인 보컬과 코러스가 분리된 노래방 시나리오 지원에 사용됩니다. 배경음악 순환 재생도 함께 지원됩니다.
- muteLocalVideo를 호출한 후 startLocalPreview를 호출하면 ‘미리보기만 하고 푸시 스트림은 하지 않는’ 효과를 지원합니다. enterRoom 전 startLocalPreview를 호출해 해당 기능을 실행할 수 있습니다.

**수정**

- 사용자 정의 비디오 수집 시 가끔 SDK 내부 OpenGL 콘텍스트 오류 crash가 발생하는 문제가 수정되었습니다.
- 방 입장 전 setLocalVideoRenderListener 사용자 정의 렌더링 콜백이 트리거되지 않는 문제가 수정되었습니다.
- 가로 화면 모드에서 전/후 카메라로 전환 시 재생 화면이 거꾸로 표시되는 문제가 수정되었습니다.
- 방 입장 전 startLocalPreview을 호출하면 방 입장 후에 가끔 화면이 뿌옇게 나타나는 문제가 수정되었습니다.
- 하드 코더에서 가끔 crash가 발생하는 문제가 수정되었습니다.
- 로컬 오디오 녹화 시 가끔 끊김 현상이 발생하는 Bug가 수정되었습니다.
- 푸시 스트림 일시 중지(muteLocalVideo, muteLocalAudio) 시 강제 종료 또는 crash 발생 후 다시 방에 입장하면 멀티미디어가 자동으로 재생되지 않는 문제가 수정되었습니다.



## Version 7.2 @ 2020.04.16 

**추가**

Android에 핸드폰 녹화 기능이 추가되었습니다. 해당 기능은 핸드폰에서의 라이브 방송 녹화에 적용됩니다.

**최적화**

- 통화 시나리오에서 중저가 Android 핸드폰의 성능 소모를 최적화하여 통화 품질이 향상되었습니다.
- 필터, 그린 스크린과 같은 시각 효과 인터페이스를 최적화하고 TXCBeautyManager 클래스에 통합하여 통합 호출 방식을 구현했습니다.

**수정**

역할 전환 시 사용자 정의 ID가 가끔 제때 적용되지 않는 문제가 수정되었습니다.



## Version 7.1 @ 2020.03.27 

**최적화**

- C++ STL 기본 라이브러리 완전 정적 컴파일을 지원합니다.
- 통화 음량이 기본적으로 ANS, AGC를 활성화하여 통화 모드에서의 음질이 향상되었습니다.
- 혼합 스트림 사전 설정 템플릿의 활용성이 최적화되었습니다.
- 혼합 스트림이 최적화되어 성공률이 향상되었습니다.

**수정**

- 방에 입장한 이후 AGC를 반복해서 활성/비활성화할 경우 처리한 오디오가 전부 0이 되는 문제가 수정되었습니다.
- 속도 측정 시 다른 API 호출의 응답이 느려지는 문제가 수정되었습니다.
- 시스템에 의해 전화가 중단된 이후 음량이 2배로 증가하고 노이즈가 섞이는 문제가 수정되었습니다.
- 방 입장 시 자동으로 릴레이하는 문제가 수정되었습니다.



##  Version 7.0 @ 2020.03.09 

- 3A 활성화 정책이 최적화되었습니다.
- mcu 혼합 스트림 활용성이 향상되었습니다.
- 약한 네트워크에서의 지터 방지 능력이 최적화되어 네트워크가 약한 환경에서 오디오가 보다 원활해졌습니다.
- 여러 차례 교대로 방 입장과 퇴장을 반복할 경우 메모리 누수가 발생하는 문제가 해결되었습니다.



##  Version 6.9 @ 2020.01.14 

**추가**

- Android 10.0 시스템에 대한 지원이 추가되었습니다.
- API: snapshotVideo()가 추가되어 로컬 및 원격 비디오의 화면을 캡처할 수 있습니다.
- API: pauseAudioEffect, resumeAudioEffect 음향 효과가 추가되어 일시 중지/복구 제어 기능을 지원합니다.
- API: setBGMPlayoutVolume, setBGMPublishVolume, BGM이 추가되어 로컬 재생과 푸시 스트림 오디오 믹싱을 지원합니다.
- API: setRemoteSubStreamViewRotation 서브 채널 비디오 재생이 추가되어 렌더링 회전 각도 조정을 지원합니다.
- 일종의 전역 음량 유형 모드인 setSystemVolumeType(TRTCSystemVolumeTypeVOIP)이 추가되어 통화 음량 사용을 항상 사용합니다. 블루투스 이어폰의 자체 마이크에서 발생하는 수집 전환 문제 해결에 사용됩니다.
- enterRoom 매개변수 TRTCParams에 streamId 속성이 추가되었습니다. 현재 사용자의 CDN 라이브 방송 스트리밍 ID 설정에 사용해 라이브 방송 CDN 바인딩이 더욱 편리해집니다.
- enterRoom 매개변수 TRTCParams에 cloudRecordFileName 속성이 추가되어 해당 라이브 방송의 클라우드 녹화 파일명을 설정할 수 있습니다.
- 시나리오 TRTCAppSceneAudioCall이 추가되어 enterRoom 시 설정할 수 있습니다. 해당 시나리오에서 음성 통화와 관련된 TRTC SDK가 전반적으로 최적화되었습니다.
- 시나리오 TRTCAppSceneVoiceChatRoom이 추가되었습니다. enterRoom 시 설정할 수 있으며, TRTC SDK를 활성화하여 음성 인터랙션 채팅방 시나리오를 최적화할 수 있습니다.

**최적화**

- 비디오 스트림 중단에 대한 녹화 서비스의 저항력을 최적화하여 원격 녹화 파일의 완전성을 확보합니다.
- 일부 모델에서 하드웨어 디코딩 시 오디오-비디오가 동기화되지 않는 문제가 최적화되었습니다.
- 비디오 화면이 1080P 고해상도 수집을 지원하여 핸드폰 라이브 방송을 PC로 시청하는 시나리오에서의 화면 해상도가 향상되었습니다.
- 에러 코드 최적화로 방 입장 에러 코드가 간소화되었습니다.
- 가끔 바로 재생이 지연되던 문제가 최적화되었습니다.

**수정**

- 가끔 HTTP 모듈에서 crash가 발생하는 문제가 수정되었습니다.
- 음향 효과 재생 시 가끔 콜백이 완료되지 않는 문제가 수정되었습니다.
- 가끔 방 입장 실패 이후 복구가 되지 않는 문제가 수정되었습니다.



##  Version 6.8 @ 2019.11.15 

**추가**

- 인이어 모니터링 기능이 추가되었습니다.
- 방 입장 시 수동 풀 스트림을 지정할 수 있는 기능이 추가되었습니다.
- 뷰티 필터와 포토샵 동적 효과 인터페이스가 통합된 getBeautyManager인터페이스가 추가되었습니다.
- 엔터프라이즈 버전에 피부 미백, 눈 미백, 치아 미백, 주름 제거, 눈밑 지방 제거 등과 같은 신규 포토샵 기능이 추가되었습니다.
- onRemoteUserEnterRoom / onRemoteUserLeaveRoom 콜백이 추가되었습니다. 마이크를 켜지 않은 호스트의 방 입장/퇴장 공지를 지원합니다.

**최적화**

- pts 생성 메커니즘이 최적화되었습니다.
- 네트워크 전환 후 자동으로 더 원활한 액세스 포인트를 선택하도록 최적화되었습니다.
- startRemoteView에서 사전 호출을 지원합니다.

**수정**

알려진 crash 문제 등 안정성 문제가 수정되었습니다.



## Version 6.7 @ 2019.09.30 

**추가**

- AAR 패키지에 권한 획득 설정이 추가되었습니다.
- Android 8.0 이상 시스템의 CPU 점유율 평가가 추가되었습니다.

**최적화**

- 푸시 소모 시간이 최적화되었습니다.
- 사용자가 재생 음량을 독립적으로 조절할 수 있는 기능을 지원합니다.

## Version 6.6 @ 2019.08.02 

**추가**

- 오디오 로컬 녹화 기능이 추가되었습니다.
- 첫 프레임 오디오 및 비디오 전송 콜백 인터페이스가 추가되었습니다.
- 시스템 음량 유형 설정 인터페이스가 추가되었습니다.
- 음향 효과 인터페이스가 추가되었습니다. 짧은 음향 효과 재생을 지원합니다.
- 오디오 사용자 정의 콜백 인터페이스가 출력한 데이터를 수정할 수 있게 되었습니다.

**최적화**

- 방 입장이 최적화되어 입장 소모 시간이 단축되고 입장 성공률이 향상되었습니다.
- 원격 비디오 인터페이스 mute 기능을 지원합니다.
- 방 입장 에러 코드가 통합되었습니다. onEnterRoom을 통해 콜백되며, result&lt;0은 방 입장 오류를 의미합니다.
- Demo 최적화 및 저딜레이 대형 방이 추가되었습니다.
- 플레이어에 음량 설정 인터페이스와 음량 크기 콜백 인터페이스가 추가되었습니다.
- 사용자 정의 전송 비디오가 로컬 렌더링을 지원합니다.
- 사용자 정의 수집 및 전송 비디오는 1080P를 지원합니다.
- 로컬 및 원격 렌더링에서 SurfaceView 방식을 지원합니다.

**수정**

- 릴레이 혼합 스트림 관련 문제가 수정되었습니다.
- 로컬 미리보기 각도가 맞지 않는 문제가 수정되었습니다.



##  Version 6.5 @ 2019.06.12 

**추가**

라이브 방송 모드(TRTCAppSceneLIVE)에 ‘저딜레이 대형 방’ 기능이 추가되었습니다.

- 멀티미디어 최적화를 위한 UDP 프로토콜을 적용함으로써 약한 네트워크에 대한 저항 능력이 강화되었습니다.
- 평균 시청 딜레이 시간이 1초로, 시청자와 호스트 간의 인터랙션 적극성이 향상되었습니다.
- 한 방에 최대 10만 명까지 입장할 수 있습니다.

**최적화**

- 약한 네트워크 환경에서 오디오-비디오가 동기화되지 않는 Bug가 최적화되었습니다.
- onStatistics 상태 콜백이 최적화되어 존재하는 스트림만 콜백합니다.
- 라이브 방송 TXLivePlayer 재생 버퍼 로직이 최적화되어 랙 비율이 감소하였습니다.
- 먼저 muteLocalVideo 후 취소 시 재생 화면 복구 속도가 최적화되었습니다.
- 딜레이와 패킷 손실률이 높은 네트워크 환경에서의 QoE 알고리즘이 최적화되어 약한 네트워크에 대한 저항성이 향상되었습니다.
- 디코더 성능이 최적화되어 초저가형 Android 휴대폰에서 딜레이가 점차 증가하는 Bug를 수정했습니다.
- 오디오 평가 알고리즘(enableAudioVolumeEvaluation)이 최적화되어 음량 평가가 더욱 빠르게 이루어집니다.
- 영상 통화(TRTCAppSceneVideoCall) 모드에서의 QoE 알고리즘이 최적화되어 약한 네트워크 환경에서도 더욱 원활한 1v1 통화 모드가 지원됩니다.

  

**수정**

- 가끔 enterRoom 시 콜백하지 않는 Bug가 수정되었습니다.
- 오디오 수집 비활성화 후 재생을 해도 소리가 들리지 않는 Bug가 수정되었습니다.
- 로컬 렌더링 view를 삭제 후 다시 추가했을 때 그린 스크린이 발생하는 Bug가 수정되었습니다.
- 사용자 정의 렌더링 콜백(setRemoteVideoRenderDelegate)에서 원격 화면 해상도가 540P 이상일 경우 콜백을 10회만 하는 Bug가 수정되었습니다.



## Version 6.4 @ 2019.04.25 

**추가**

- 로컬 표시 이미지와 인코더 출력 이미지 인터페이스가 추가되었습니다.
- 혼합 스트림 setMixTranscodingConfig API의 설정 콜백 함수가 추가되었습니다.
- 엔터프라이즈 버전에 눈 확대, 얼굴 축소, V라인, 움직이는 스티커 기능이 추가되었습니다.

**최적화**

- 약한 네트워크 환경에서의 원활성이 향상되었습니다.
- 음량 크기 콜백 알고리즘이 최적화되어 음량 콜백 값이 더욱 합리적으로 변경되었습니다.
- 사용자 정의 오디오, 비디오 데이터 전송 시 외부 지정 데이터 프레임 타임스탬프가 지원됩니다.
- setMixTranscodingConfig 인터페이스가 강화되어 roomID 매개변수를 지원합니다. 크로스 룸 마이크 연결 혼합 스트림에 사용됩니다.
- setMixTranscodingConfig 인터페이스가 강화되어 pureAudio 매개변수를 지원합니다. 음성 통화 전용 시나리오에서의 음성 혼합 스트림 및 녹화에 사용됩니다.
- 저가형 Android 기기에서의 720p 비디오 디코딩 성능 문제가 최적화되었습니다.

**수정**
- 음성 핸즈프리 전환이 이루어지지 않는 Bug가 수정되었습니다.
- 라이브 방송(TXLivePlayer) 딜레이가 증가한 이후에 복구되지 않는 Bug가 수정되었습니다.
- 라이브 방송 시나리오 setVideoEncoderRotation이 적용되지 않는 Bug가 수정되었습니다.
- Android에서 마이크 권한을 허용하지 않은 경우 오류가 콜백되지 않는 Bug가 수정되었습니다.
- Android 9.0 시스템에서 Demo를 열었을 때 창이 팝업되는 문제가 수정되었습니다.
- 음량 조절 버튼으로 시청자 측 음량을 조절할 수 없는 문제가 수정되었습니다.



## Version 6.3 @ 2019.04.02 

**추가**

- Android 플랫폼 64비트 지원이 추가되었습니다.
- 사용자 정의 비디오 수집 인터페이스 TRTCCloud >> sendCustomVideoData가 추가되었습니다.
- 사용자 정의 오디오 수집 인터페이스 TRTCCloud >> sendCustomAudioData가 추가되었습니다.
- 사용자 정의 비디오 렌더링 인터페이스 TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate가 추가되었습니다.
- 사용자 정의 오디오 데이터 콜백 인터페이스 TRTCCloud >> setAudioFrameDelegate가 추가되었습니다. 다음과 같은 기능을 지원합니다.
  - 마이크 수집 데이터 반환: TRTCAudioFrameDelegate >> onCapturedAudioFrame
  - 각 채널 원격 사용자의 오디오 데이터 반환: TRTCAudioFrameDelegate >> onPlayAudioFrame
  - 혼합 후 스피커로 재생한 오디오 데이터 반환: TRTCAudioFrameDelegate >>onMixedPlayAudioFrame





## Version 6.2 @ 2019.03.08 

**추가**

- 필터 농도 설정 인터페이스 setFilterConcentration()이 추가되었습니다.
- sendSEIMsg() 인터페이스가 추가되었습니다. 비디오 프레임의 SEI 헤드 정보를 통한 사용자 정의 메시지 발송을 지원하며, 일반적으로 비디오 스트림에 타임스탬프 정보를 삽입하는 데 사용합니다.
- 크로스 룸 통화 기능인 connectOtherRoom이 추가되었습니다. 이미 존재하는 두 개의 TRTC 방을 서로 연결하는 기능으로, 라이브 룸 호스트 PK에 사용됩니다.



**최적화**

- CPU 사용률 및 안정성이 최적화되었습니다.
- 약한 네트워크(연결 상태가 좋지 않은 네트워크 환경)에서의 화면 해상도가 향상되었습니다.
- TRTCCloud의 다중 인스턴스 기능을 취소하고 생성 모드를 단일 인스턴스 모드로 변경하여 다수의 TRTCCloud 인스턴스가 서로의 네트워크 리소스를 점유하지 않고 체험 효과에 영향을 미치지 않도록 방지합니다.

**수정**

음성 통화 전용 시나리오(예: 마피아 게임)에서 릴레이 푸시 스트림 기능을 복구하려면 TRTCParam의 bussInfo 필드를 함께 사용해야 합니다.



##  Version 6.1 @ 2019.01.31 

**최적화**

- 화면 공유 스트림 보기 기능을 지원합니다.
- 사용자 정의 비디오 데이터 전송을 지원합니다.
- CDN 푸시 및 혼합 스트림 구현이 최적화되었습니다.
- 방 입장 시 라이브 방송과 영상 통화 시나리오로 구분됩니다.
- 안정성이 개선되고, 가끔 crash가 발생하는 문제가 해결되었습니다.
- 트래픽 제어가 최적화되어 약한 네트워크 환경에서의 성능이 향상되었습니다.



## Version 6.0 @ 2019.01.18 

**최적화**

- 아키텍처가 LiteAV 커널로 업데이트되었습니다.
- 새로운 QoS 알고리즘을 적용하여 랙 발생률이 감소하고 원활성이 향상되었습니다.
- 새로운 Audio 모듈을 적용하여 각종 네트워크 상황에서의 오디오 품질이 대폭 최적화되었습니다.
- 대형/소형 스트림 듀얼 채널 인코딩 기능을 지원합니다(Windows와 Mac 디바이스에서만 활성화 추천).
- CDN 푸시 및 혼합 스트림 기능을 지원합니다.
