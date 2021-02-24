## Version 8.3 @ 2021.01.15

**새로운 기능**

이 버전에서는 사용자 정의 샘플링 관련 비즈니스 로직이 중점적으로 개선되었습니다.
- iOS & Android & Mac: 오디오 모듈 개선을 통해 [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d)로 캡처한 음성 데이터를 SDK에 전송하여 처리할 때 SDK가 에코 억제 및 노이즈 감소 효과를 유지할 수 있도록 하였습니다.
- iOS & Android: TRTC SDK를 기반으로 오디오 특수효과 및 처리 로직을 지속적으로 강화해야 할 경우, 8.3버전이 귀하의 정답이 되어드릴 것입니다. [setCapturedRawAudioFrameDelegateFormat](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86)과 같은 인터페이스를 통해 오디오 데이터의 콜백 형식(오디오 샘플링 레이트, 오디오 채널 수, 샘플 카운팅 등)을 설정하여 귀하가 선호하는 음성 포맷으로 오디오 데이터를 처리할 수 있기 때문입니다.
- 모든 플랫폼: 비디오 데이터를 자체 샘플링하고 TRTC SDK 자체 오디오 모듈을 사용해야 할 경우 오디오-비디오 동기화가 이루어지지 않는 문제가 발생할 수 있습니다. 이는 SDK 내부 타임라인의 자체 제어 로직으로 인해 발생하는 것으로, 이 문제에 대한 대응책으로 [generateCustomPTS](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) 인터페이스가 제공됩니다. 비디오 화면을 샘플링할 때 이 인터페이스를 사용해서 현재 PTS(타임스탬프)를 기록한 다음 [sendCustomVideoData](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831)를 호출할 때 이 타임스탬프를 적용하면 오디오-비디오 동기화를 유지할 수 있습니다.
- Windows: 버전 SDK에 도메인 포맷에 대한 Socks5 프록시 지원이 추가되었습니다.

**문제 수정**
- 모든 플랫폼: 간혹 오디오 데이터의 타임스탬프에 오류가 발생하여 녹화된 부분에서 오디오-비디오 동기화가 유지되지 않는 문제가 수정되었습니다.
- Windows: 고 DPI 환경에서 창 공유 호환성이 개선되었습니다.
- Windows: 공유할 수 있는 창 목록을 가져올 때 최소화된 창을 추가합니다. 최소화된 창의 축소 이미지는 해당 프로세스의 아이콘으로 표시됩니다.
- Windows: SDK 실행 시 불필요한 DXGI 점유 문제가 수정되었습니다.
- iOS: 수동 포커스 설정을 할 경우 ANR이 발생하는 문제가 수정되었습니다.
- iOS: 가끔 전환 전후로 카메라가 인식되지 않는 문제가 수정되었습니다.
- iOS: VODPlayer 감속 재생 시 크래시 발생 문제가 수정되었습니다.
- iOS: 가끔 방에 입장한 후 헤드셋에서 오디오가 재생되는 문제가 수정되었습니다.
- iOS & Android: 에코 제거 및 잡음 억제 효과가 개선되었으며, 인이어 모니터링에서도 잔향 효과를 들을 수 있게 되었습니다.
- Android: 가끔 하드웨어 디코딩 시 화면 출력 오류가 나타나는 문제가 수정되었습니다.
- Mac: 창 공유 및 고휘도 모드 활성화 시 창 프레임이 반짝이는 문제가 수정되었습니다.
- Mac: 렌더링 투시도 이동 시 블랙 스크린이 발생하는 문제가 수정되었습니다.


## Version 8.2 @ 2020.12.23

**새로운 기능**
- iOS & Android: 로컬 샘플링과 재생된 모든 오디오 데이터의 혼합 콜백이 추가되어 로컬 오디오가 더욱 편리해졌습니다.
- Android: 비디오 렌더링 컴포넌트 TXCloudVideoView가 `addVideoView(new TextureView(getApplicationContext()))` 인터페이스를 지원하여 TextureView를 로컬 렌더링에 사용합니다.
- Android: 사용자 정의 렌더링 콜백이 RGBA 포맷의 비디오 데이터를 지원합니다.
- Windows: 로컬 카메라 샘플링과 원격 비디오 스트리밍 재생을 지원합니다. [ITRTCCloud.snapshotVideo](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96)를 참조 바랍니다.
- Windows: 화면 공유가 addExcludedShareWindow와 addIncludedShareWindow 인터페이스를 통해 지정된 창의 제외 또는 강제 포함 기능을 지원하여 보다 유연한 화면 공유 기능을 제공합니다.
- Mac & iOS: 사용자 정의 렌더링 모드에서도 TRTCCloud.snapshotVideo로 추출한 비디오 이미지 플로우를 호출할 수 있습니다.

**품질 개선**
- Android: 온라인 라이브 방송 코딩 품질이 개선되어 더욱 선명한 영상을 제공합니다.
- Windows: 에코 제거 알고리즘이 개선되어 에코 제거 효과가 향상되었습니다.

**문제 수정**
- iOS: VODPlayer와 TRTC를 동시에 사용할 경우 가끔 오디오 재생 오류가 발생하는 문제가 수정되었습니다.
- Android: 사용자 정의 뷰티 필터가 로컬 렌더링 블랙 스크린을 발생시키는 문제가 수정되었습니다.
- Windows: 가끔 진행 중인 프로세스를 종료할 수 없는 문제가 수정되었습니다.


## Version 8.1 @ 2020.12.03

**새로운 기능**
-모든 플랫폼: 통계 정보(onStatistics)에 원격 비디오 랙과 관련된 통계 지표가 추가되었습니다.
-모든 플랫폼: 음량 조절 인터페이스 setAudioPlayoutVolume(100-150)를 통해 오디오 부스터 효과를 적용할 수 있게 되었습니다.
- iOS & Android: setLocalVideoProcessListener 인터페이스가 추가되어 서드파티 뷰티 필터 SDK 통합 지원 기능이 향상되었습니다.
- C#: 최신 버전의 API 인터페이스로 업데이트되었습니다.

**품질 개선**
- 모든 플랫폼: 이어폰 착용 시 음성 처리 알고리즘이 개선되어 오디오 품질이 향상되었습니다.
- Android: 오디오 전처리 알고리즘이 개선되어 3A 알고리즘이 음질에 미치는 영향이 감소되었습니다.

**문제 수정**
- iOS: 가끔 App 강제 종료 시 크래시가 발생하는 문제가 수정되었습니다.
- Android: 프레임 레이트 샘플링이 높을 경우 뷰티 필터 효과에 오류가 발생하는 문제가 수정되었습니다.
- Windows: 고 DPI 환경에서 화면 공유 시 가끔 크래시가 발생하는 문제가 수정되었습니다.


## Version 8.0 @ 2020.11.13

**추가**
- 모든 플랫폼에 C++ 통일 API가 추가되었습니다. cpp_interface/[ITRTCCloud.h](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html)를 참조 바랍니다.
- 모든 플랫폼이 문자열 방 번호를 지원합니다. TRTCParams.strRoomId를 참조 바랍니다.
- 모든 플랫폼에 TXDeviceManager 장치 관리 유형이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.switchRoom이 추가되어 샘플링을 정지하지 않고도 방을 바꿀 수 있게 되었습니다.
- 모든 플랫폼에 API TRTCCloud.startRemoteView 렌더링 원격 비디오 화면 시작 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.stopRemoteView 렌더링 원격 비디오 화면 중지 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.getDeviceManager 장치 관리 유형 획득 기능이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.startLocalAudio 활성화 로컬 오디오의 샘플링과 업스트림이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.setRemoteRenderParams 원격 이미지 설정의 렌더링 설정이 추가되었습니다.
- 모든 플랫폼에 API TRTCCloud.setLocalRenderParams 원격 이미지 설정의 렌더링 설정이 추가되었습니다.

**최적화**
- Android에서 소프트웨어/하드웨어 디코딩 전환 로직이 개선되었습니다.
- Windows에서 System loopback 오디오 샘플링 음질 및 에코 제거 효과가 개선되었습니다.
- Windows에서 오디오 디바이스 선택 로직이 개선되어 Silent rate가 감소했습니다.
- Windows에서 쌍강 절취 효과가 개선되었습니다.
- 모든 플랫폼에서 수동 수신 모드에서 역할 전환 시 발생하는 바로 재생 효과가 개선되었습니다.
- 모든 플랫폼에서 오디오 수신 로직이 개선되어 오디오 효과가 향상되었습니다.
- 모든 플랫폼에서 sendCustomCmdMsg 신뢰성이 개선되었습니다.

**수정**
- iOS에서 muteLocalVideo 호출 시 로컬 비디오 렌더링이 중지되는 문제가 수정되었습니다.
- iOS에서 프론트엔드/백엔드 전환 시 호출 시스템 컴포넌트에서 크래시가 발생하는 문제가 수정되었습니다.
- iOS에서 오디오 활성화 시 인이어 모니터링 오디오가 계속 끊기는 문제가 수정되었습니다.
- Android에서 통화 음량 효과음 재생을 중단시켰을 때 통화가 끊겼을 경우, 효과음이 계속해서 재생되는 문제가 수정되었습니다.
- Android에서 가끔 오디오 샘플링 활성화가 실패하는 문제가 수정되었습니다.
- Windows에서 가끔 로컬 비디오 렌더링 시 블랙 스크린이 발생하는 문제가 수정되었습니다.
- Windows에서 프로세스 종료 시 간혹 크래시가 발생하는 문제가 수정되었습니다.
- Windows에서 블루투스 이어폰 지원이 개선되어 블루투스 이어폰에서 소리가 나지 않는 문제가 수정되었습니다.
- Windows에서 화면 공유 종료 시 포커스 상실 문제가 수정되었습니다.
- 모든 플랫폼에서 상태 콜백 패킷 손실률 통계 오류가 수정되었습니다.



## Version 7.9 @ 2020.10.27
**추가**
- Mac: 화면 공유가 선택된 창의 필터링 기능을 지원합니다. 공유하고 싶지 않은 창을 제거함으로서 보다 개선된 사생활 보호를 제공합니다.
- Windows: 화면 공유의 ‘공유 중’ 알림창 프레임 색상과 프레임 크기 설정 기능을 지원합니다.
- Windows: 화면 공유 기능으로 전체 화면을 공유할 때 고성능 모드를 지원합니다.
- 모든 플랫폼: 사용자 정의 암호 추가 기능을 지원하여 편집이 완료된 오디오/비디오 데이터를 노출된 C 인터페이스를 통해 2차 처리할 수 있게 되었습니다.
- 모든 플랫폼: TRTCRemoteStatistics에 오디오 정보 콜백 `audioTotalBlockTime`과 `audioBlockRate`가 추가되었습니다.

**최적화**
- iOS: 오디오 모듈의 실행 속도가 개선되어 첫 번째 오디오 프레임을 더 빨리 샘플링하여 전송할 수 있게 되었습니다.
- Windows: 시스템 루프의 에코 제거 알고리즘이 개선되어 시스템 루프백(SystemLoopback) 활성화 시 에코 제거 능력이 강화되었습니다.
- Windows: 화면 공유 기능의 창 샘플링 차폐 방지 능력이 개선되어 창 필터 설정 기능을 지원합니다.
- Android: 대부분의 Android 기종에서 인이어 모니터링 효과가 개선되어 인이어 모니터링 딜레이가 적정 수준까지 감소되었습니다.
- Android: Music 모드(startLocalAudio일 시에 지정)에서의 P2P 딜레이가 개선되었습니다.
- 모든 플랫폼: 수동 구독 모드에서 관객과 호스트 역 전환 시의 음성 유창성이 개선되었습니다.
- 모든 플랫폼: 음성/영상 통화에서 약한 네트워크에 대한 저항성이 개선되어 네트워크 환경이 좋지 않은 상황에서의 오디오 유연성이 향상되었습니다.

**수정**
- iOS: 일부 시나리오에서 가끔 비디오 화면이 렌더링되지 않는 문제가 수정되었습니다.
- iOS: 사용자가 이어폰을 착용한 상태에서 음질이 Default일 경우 가끔 잡음이 발생하는 문제가 수정되었습니다.
- iOS: 현재 알려져 있는 메모리 누수 문제 중 일부가 수정되었습니다.
- iOS: 가끔 replaykit 확장 녹화 종료 시 크래시가 발생하는 문제가 수정되었습니다.
- iOS: 시뮬레이터 환경에서의 편집 문제가 해결되었습니다.
- Android: 일부 모바일 기기가 App에서 장기간 백엔드로 전환된 이후에 다시 프론트엔드로 전환될 경우 가끔 오디오-비디오 동기화가 이루어지지 않는 문제가 수정되었습니다.
- Android: 백엔드 전환 이후 마이크 릴리스가 되지 않는 문제가 수정되었습니다.
- Android: SDK 내부의 일부 OpenGL 리소스가 제때 릴리스되지 않는 문제가 수정되었습니다.
- Windows: 개별 시나리오에서 가끔 잡음이 발생하는 문제가 수정되었습니다.
- 모든 플랫폼: 가끔 발생하는 크래시 문제 중 일부가 해결되어 SDK 안정성이 향상되었습니다.

## Version 7.8 @ 2020.09.29
**추가**
- Mac: 시스템 음량 변화 콜백이 추가되었습니다. 세부 사항은 [TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f)를 참조 바랍니다.
- Windows: 크로스 스크린을 지원하여 지정된 영역에 화면을 공유하는 기능이 추가되었습니다.
- Windows: 창 공유가 필터 기능을 지원하여 지정된 창에 대한 차폐 방지 기능이 추가되었습니다. 세부 사항은 [TRTCCloud.addExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae5141a9331c3675f17fbdc922f376b06)과 [TRTCCloud.removeExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a08504ce347b593c0191904611da5cfd2)를 참조 바랍니다.
- Windows: 시스템 음량 변화 콜백이 추가되었습니다. 세부 사항은 [ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12)를 참조 바랍니다.

**최적화**
- iOS: VODPlayer와 trtc 동시 사용 및 에코 제거를 지원합니다.
- iOS & Mac: 조정화면 푸시스트림을 지원합니다. 사용 방법은 [TRTCCloud.setVideoMuteImage](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2)를 참조 바랍니다.
- Android: 조정화면 푸시스트림을 지원합니다. 사용 방법은 [TRTCCloud.setVideoMuteImage](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d)를 참조 바랍니다.
- Android: 오디오 라우팅 정책이 개선되어 이어폰 착용 시 오디오가 이어폰으로만 재생되는 기능이 지원됩니다.
- Android: 일부 시스템에서 로우 딜레이 샘플링 재생을 지원하여 Android 시스템의 통화 딜레이가 감소되었습니다.
- Android: VODPlayer 와 trtc 동시 사용 및 에코 제거를 지원합니다.
- Windows: 가상 카메라 e2eSoft Vacm가 호환됩니다.
- Windows: startLocalPreview 과 startCameraDeviceTest 동시 호출이 지원됩니다.
- Windows: 화면 공유가 주 경로를 이용하는 동시에, startLocalPreview 호출 시 로컬 미리보기를 활성화합니다.
- Windows: SDK 내부 재생 버퍼로 인한 오디오 딜레이가 커지는 문제가 감소했습니다.
- Windows: 오디오 실행 로직이 개선되어 재생 상황에 한정하여 마이크를 점용하지 않습니다.



**수정**
- iOS: iPhone SE에서 오디오 재생 음량이 작은 문제가 수정되었습니다.
- iOS: 하위 방(TRTCCloud.createSubCloud)에서 muteRemoteAudio 호출 시 크래시가 발생하는 문제가 수정되었습니다.
- iOS: 가끔 렌더링 중 크래시가 발생하는 문제가 수정되었습니다.
- iOS: 프론트엔드/백엔드 전환 시 일부 iPad에서 비디오 랜더링 중 가끔 메인 스레드가 크래시되는 문제가 수정되었습니다.
- iOS: 알려진 메모리 누수 문제가 수정되었습니다.
- iOS: iOS14에서 ‘로컬 네트워크에 있는 장치를 찾아 연결하기’ 알림이 뜨는 문제가 수정되었습니다.
- Mac: getCurrentCameraDevice가 계속 nil을 반환하는 문제가 수정되었습니다.
- Mac: 일부 USB 카메라를 열 수 없는 문제가 수정되었습니다.
- Mac: 화면 공유의 지정 영역 면적이 0일 경우 크래시가 발생하는 문제가 수정되었습니다.
- Android: READ_PHONE_STATE 권한이 설정되지 않았을 경우 Android5.0 기기에서 크래시가 발생하는 문제가 수정되었습니다.
- Android: 블루투스 이어폰을 제거한 후 재연결했을 때, 오디오 샘플링 및 재생 시 오류가 발생하는 문제가 수정되었습니다.
- Android: 알려진 크래시 문제가 수정되었습니다.
- Windows: 64비트 SDK에서 화면 공유 기능을 여러 번 활성화할 경우 크래시가 발생하는 문제가 수정되었습니다.
- Windows: 일부 시스템에서 OpenGL을 사용할 경우 크래시가 발생하는 문제가 수정되었습니다.


## Version 7.7 @ 2020.09.08

**최적화**

- 모든 플랫폼: 보조 경로(화면 공유)의 실행 속도가 향상되었습니다.
- iOS: 내부 스레드 모델이 개선되어 30번 경로 이상에서 동시 재생 시나리오의 실행 안정성이 향상되었습니다.
- iOS & Android: Audio 모듈 성능이 개선되어 SOF의 샘플링 딜레이가 향상되었습니다. 신규 버전에서는 첫 번째 오디오 프레임을 더 빨리 획득할 수 있습니다.
- iOS & Android: VOD 플레이어와 TRTC를 동시에 사용할 경우의 음량 크기 및 음질이 향상되었습니다.
- iOS & Android: wav 오디오 포맷의 배경 음악과 효과음 파일 지원이 추가되었습니다.
- Windows: 일부 저가형 카메라의 과도하게 높은 CPU 사용률 문제가 수정되었습니다.
- Windows: 멀티 USB 카메라와 마이크에 대한 호환성이 개선되어 기기의 실행 성공률이 향상되었습니다.
- Windows: 카메라와 마이크 기기의 선택 정책이 개선되어 카메라 또는 마이크 사용 중 소켓으로 인해 샘플링 오류가 발생하는 문제를 피할 수 있게 되었습니다.

**수정**

- 모든 플랫폼: 네크워크가 약한 경우, muteLocalVideo 및 muteLocalAudio 인터페이스 호출 시 가끔 재생 오류가 발생하는 버그가 수정되었습니다.
- iOS: 저가형 iPhone 또는 iPad에서 오디오 재생 시 가끔 재생에 실패하는 버그가 수정되었습니다.
- iOS: iPad Pro에서 화면 공유 기능으로 인해 공유된 화면이 늘어나는 문제가 수정되었습니다.
- iOS: 사용자가 권한을 거절했음에도 App 내부 화면 기여가 계속해서 화면 녹화 권한을 요청하는 문제가 수정되었습니다.
- Windows: 노트북 또는 데스크톱이 장시간 미사용 시, 나가기 [onExitRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) 이벤트 알림이 콜백되지 않는 문제가 수정되었습니다.
- Windows: Music 음질 모드에서 시스템 오디오 루프백 [stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23)을 활성화하면 에코가 새는 문제가 수정되었습니다.
- Windows: enterRoom과 exitRoom을 빠르게 호출하여 방 입장/퇴장을 할 경우 가끔 소리가 들리지 않는 버그가 수정되었습니다.
- Windows: Visual Stuido 2010 프로젝트에서 SDK의 편집 호환성 문제가 수정되었습니다.
- Windows: 수동 수신 모드([setDefaultStreamRecvMode(false，false)](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5))에서 onUserVideoAvailable 이벤트 콜백을 중복 수신하는 문제가 수정되었습니다.


## Version 7.6 @ 2020.08.21
**추가**

- Windows: HWND 유형의 렌더링 창의 실시간 조정을 보다 쉽게 할 수 있는 [updateLocalView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae5211a2739df8d8ec6017559b3aa0299)와 [updateRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8c8247cbc679ea144ffb393b6b940c9e) 인터페이스가 추가되었습니다.
- Windows: 현재 Windows Pc가 음소거로 설정되어 있는지를 확인하는 데 사용할 수 있는 [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) 인터페이스가 추가되었습니다.
- Windows: 현재 Windows Pc를 음소거로 설정할 수 있는 [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) 인터페이스가 추가되었습니다.
- Mac: View 렌더링 지역의 실시간 조정을 더 쉽게 할 수 있는 [updateLocalView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) 및 [updateRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) 인터페이스가 추가되었습니다.
- Mac: 현재 Mac이 음소거로 설정되어 있는지 확인하는 데 사용할 수 있는 [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f) 인터페이스가 추가되었습니다.
- Mac: 현재 Mac을 음소거로 설정할 수 있는 [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) 인터페이스가 추가되었습니다.
- iOS: View 렌더링 지역의 실시간 조정을 더 쉽게 할 수 있는 [updateLocalView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) 및 [updateRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) 인터페이스가 추가되었습니다.
- iOS: TRTCCloudDelegate에 [onCapturedRawAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) 콜백을 추가하고, 몇몇 콜백 함수의 이름을 변경했습니다. 변경된 이름은 각각 순서대로 [onLocalProcessedAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0), [onRemoteUserAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a), [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e)입니다.
- Android: TRTCCloudListener에 [onCapturedRawAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) 콜백을 추가하고, 몇몇 콜백 함수의 이름을 변경했습니다. 변경된 이름은 각각 순서대로 [onLocalProcessedAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46), [onRemoteUserAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902), [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7)입니다.

**최적화**

- 모든 플랫폼: enterRoom의 프로토콜 정책이 개선되어 방 입장 속도와 성공률이 향상되었습니다.
- 모든 플랫폼: 다수의 오디오를 구독할 경우에 발생하는 전반적 성능 소모와 랙 문제가 개선되었습니다.
- Mac: 화면 공유에 지정된 창의 지정된 영역 공유 기능이 지원됩니다.

**수정**

- 모든 플랫폼: 방에서 퇴장하지 않은 상태에서 다른 방에 입장할 경우 SDK에서 onEnterRoom이 트리거되지 않는 버그가 수정되었습니다.
- 모든 플랫폼: 블랙 스크린을 유발할 수 있는 몇몇 내부 버그가 수정되었습니다.
- 모든 플랫폼: startRemoteSubStreamView 사전 호출 시 공유된 화면이 정상적으로 표시되지 않는 문제가 수정되었습니다.
- Windows: 알려진 몇몇 핸들 및 GDI 누락이 수정되었습니다.
- Windows: 알려진 크래시 문제 다수가 수정되었습니다.
- Windows: 카메라와 마이크를 뺀 후 다시 꽂았을 때 자동으로 장치가 활성화되지 않는 문제가 수정되었습니다.
- iOS: iOS 10에서 배경음악 인터페이스를 특정 규칙의 파일 경로로 이동했을 때 크래시가 발생하는 버그가 수정되었습니다.
- Android: 빈번하고 빠른 enterRoom 및 exitRoom 이후 가끔 소리가 들리지 않는 문제가 수정되었습니다.
- Android: 가끔 녹화 시 화면 흐림 현상이 나타나는 문제가 수정되었습니다.


## Version 7.5 @ 2020.07.31

**추가**

- 더블 스택 IPV6와 IPV6 only에 대한 지원이 추가되었습니다.
- 특급 소형 수업 지원에 사용되는 다수 방에서의 풀 스트림 능력이 향상되었습니다.
- 클라우드 MCU 혼합 스트림에 배경 이미지(모니터링 필요에 따라 이미지는 TRTC 콘솔에 먼저 업로드해야 함) 설정 기능이 추가되었습니다.
- 클라우드 MCU 혼합 스트림에 A+B=>C와 A+B=>A 모드가 추가로 지원됩니다.
- 실시간 상태 콜백 onStatistics에 재생 버퍼 시간 필드 jitterBufferDelay가 추가되었습니다.

**최적화**

- 클라이언트간 마이크 연결 딜레이가 감소되었습니다. 7.5버전 클라이언트간 통화 및 마이크 연결 딜레이가 7.4버전 기준 40% 감소되었습니다.
- 모바일 디바이스의 인이어 모니터링 딜레이가 감소되었으며, 인이어 모니터링에 변성 및 잔향과 같은 음향효과 설정이 지원됩니다.
- 클라이언트 네트워크 지터 평가 알고리즘이 개선되어 재생 딜레이가 감소되었습니다.
- Android SDK의 클라이언트간 마이크 연결 통화 딜레이가 감소되었습니다.
- 인이어 모니터링 딜레이 문제가 한층 더 개선되었습니다.
- 재생 view 동적 전환 시 블랙 스크린이 발생하는 문제가 개선되었습니다.

**수정**

- 하나의 함수에서 연속으로 playBGM과 pauseBGM을 호출하면 재생이 되지 않는 문제가 수정되었습니다.
- 가끔 방에서 나간 이후에도 onEnterRoom 콜백을 수신할 수 있는 문제가 수정되었습니다.
- 일부 모델에서 초저해상도 인코딩 및 복구가 되지 않는 문제가 수정되었습니다. 

##  Version 7.4 @ 2020.06.24 

**최적화**

인이어 모니터링이 음량 설정을 지원합니다.

**수정**

- Android 버전에서 가로세로 화면 전환 시 로컬 화면이 깜빡이는 문제가 수정되었습니다.
- 일부 Android 핸드폰에서 사용자 정의 비디오를 전송하면 정상적으로 인코딩이 진행되지 않는 문제가 수정되었습니다.
- 오디오 처리 시 가끔 데이터 패키지에서 크래시가 발생하는 문제가 수정되었습니다.



##  Version 7.3 @ 2020.06.01

**추가**

- 기존 인터페이스가 호환되는 상황에서 신규 음향효과 관리 인터페이스 TXAudioEffectManager가 추가되었습니다. 해당 기능은 더욱 빠르고 다양한 음향효과 편집을 지원합니다.
- 비디오 편집 매개변수 setVideoEncoderParam에 minVideoBitrate 옵션이 추가되었습니다. 화질 요구사항이 높은 생방송 클라이언트에게 추천합니다.

**최적화**

- 오디오에 순간 노이즈 감소 기능이 지원됩니다. setAudioQuality(TRTCAudioQualitySpeech)를 통해 활성화할 수 있습니다.
- 음향효과 파일이 asset 팩 음향효과 파일을 지원합니다.
- 로컬 비디오 해상도가 향상되었습니다.
- 사용자 정의 렌더링 재생에 텍스쳐 매핑 방식이 지원되어 성능 저하 문제가 개선되었습니다.
- 카메라 샘플링 해상도 선택 로직이 개선되어 시각 효과가 향상되었습니다.
- 에코 처리 효과가 향상되었습니다.
- 모든 링크에서 128kbps 고음질 입체 음성을 지원합니다. setAudioQuality(TRTCAudioQualityMusic) 인터페이스를 통해 설정할 수 있습니다.
- SPEECH 음성 모드를 지원합니다. 회의장에서 사용되는 음성 통화에 적합합니다. 더 강력한 노이즈 감소(ANS) 효과를 원하실 경우 setAudioQuality(TRTCAudioQualitySpeech)에서 설정하실 수 있습니다.
- 다중 배경음악 병행 재생 기능이 지원됩니다. 보컬과 서브보컬이 분리된 노래방 시나리오 지원에 사용됩니다. 배경음악 순환 재생도 함께 지원됩니다.
- muteLocalVideo 호출 후 startLocalPreview를 호출함으로써 ‘미리보기만 하고 푸시 스트림은 하지 않는’ 효과를 지원합니다. enterRoom 전 startLocalPreview 호출로 해당 기능을 실행하실 수 있습니다.

**수정**

- 사용자 정의 비디오 샘플링 시 가끔 SDK 내부 OpenGL 컨텍스트 오류 크래시가 발생하는 문제가 수정되었습니다.
- 방 입장 전 setLocalVideoRenderListener 사용자 정의 렌더링 콜백이 트리거되지 않는 문제가 수정되었습니다.
- 가로 화면 모드에서 전/후 카메라로 전환 시 재생 화면이 거꾸로 표시되는 문제가 수정되었습니다.
- 방 입장 전 startLocalPreview을 호출하면 방 입장 후에 가끔 화면 출력 오류가 나타나는 문제가 수정되었습니다.
- 하드 코더에서 가끔 크래시가 발생하는 문제가 수정되었습니다.
- 로컬 오디오 녹화 시 가끔 끊김 현상이 발생하는 버그가 수정되었습니다.
- 푸시 스트림 중지(muteLocalVideo, muteLocalAudio) 시 강제 종료 또는 크래시 후 다시 방에 입장하면 오디오/비디오가 자동 재생되지 않는 문제가 수정되었습니다.



## Version 7.2 @ 2020.04.16 

**추가**

Android에 핸드폰 녹화 기능이 추가되었습니다. 해당 기능은 핸드폰을 사용한 생방송을 지원합니다.

**최적화**

- 통화 시나리오에서 중저가 Android 핸드폰의 성능 소모량이 개선되어 통화 품질이 향상되었습니다.
- 필터, 그린 스크린과 같은 시각 효과 인터페이스를 개선하고 TXCBeautyManager에 통합하여 통일된 호출 방식을 구현했습니다.

**수정**

역할 전환 시 사용자 정의 ID가 가끔 제때 적용되지 않는 문제가 수정되었습니다.



## Version 7.1 @ 2020.03.27 

**최적화**

- C++ STL 기초 라이브러리의 완전 정적 편집
- 통화 음량이 기본적으로 ANS, AGC를 활성화하여 통화 모드에서의 음질이 향상되었습니다.
- 혼합 스트림 사전 설정 템플릿 활용성이 개선되었습니다.
- 혼합 스트림이 개선되어 성공률이 향상되었습니다.

**수정**

- 방에 입장한 이후 AGC를 반복해서 활성/비활성화할 경우 처리한 오디오가 전부 0이 되는 문제가 수정되었습니다.
- 속도 측정 시 다른 API 호출의 응답이 느려지는 문제가 수정되었습니다.
- 시스템에 의해 전화가 중단된 이후 음량이 2배로 증가하고 노이즈가 섞이는 문제가 수정되었습니다.
- 방 입장 시 자동으로 릴레이를 하는 문제가 수정되었습니다.



##  Version 7.0 @ 2020.03.09 

- 3A 활성화 정책이 개선되었습니다.
- mcu 혼합 스트림 활용성이 향상되었습니다.
- 약한 네트워크에서의 지터 방지 능력이 향상되어 네트워크가 약한 환경에서 오디오가 보다 원활해졌습니다.
- 여러 차례 교대로 방 입장과 퇴장을 반복할 경우 메모리 누수가 발생하는 문제가 해결되었습니다.



##  Version 6.9 @ 2020.01.14 

**추가**

- Android 10.0 시스템에 대한 지원이 추가되었습니다.
- API: snapshotVideo()가 추가되어 로컬 및 원격 비디오의 화면을 캡처할 수 있습니다.
- API: pauseAudioEffect, resumeAudioEffect 음향효과가 추가되어 일시정지/복구 제어 기능을 지원합니다.
- API: setBGMPlayoutVolume, setBGMPublishVolume, BGM이 추가되어 로컬 재생과 푸시 스트림 오디오 믹싱을 지원합니다.
- API: setRemoteSubStreamViewRotation 우회 비디오 재생이 추가되어 렌더링 각도 회전 조정을 지원합니다.
- 전역 음량 형식 모드: setSystemVolumeType(TRTCSystemVolumeTypeVOIP)이 추가되어 계속적인 통화 음량 사용을 지원합니다. 블루투스 이어폰의 자체 마이크에서 발생하는 샘플링 전환 문제 해결에 사용됩니다.
- enterRoom 매개변수 TRTCParams에 streamId 속성이 추가됩니다. 현재 사용자의 CDN 라이브 방송 스트리밍 ID 설정에 사용되어 CDN 라이브 방송 바인딩을 편리하게 할 수 있도록 합니다.
- enterRoom 매개변수 TRTCParams에 cloudRecordFileName 속성이 추가됩니다. 클라우드에 녹화되는 라이브 방송의 파일명을 설정할 수 있습니다.
- 시나리오 TRTCAppSceneAudioCall이 추가되었습니다. enterRoom 시 설정할 수 있습니다. 해당 시나리오에서 음성 통화와 관련된 TRTC SDK에 대한 전반적 개선이 이루어졌습니다.
- 시나리오 TRTCAppSceneVoiceChatRoom이 추가되었습니다. enterRoom 시 설정할 수 있으며, TRTC SDK를 활성화하면 음성 채팅방 시나리오를 최적화할 수 있습니다.

**최적화**

- 비디오 스트리밍 중 중단에 대한 녹화 서비스의 저항력을 강화하여 원거리 녹화 파일의 완전성을 확보했습니다.
- 일부 기종에서 하드웨어 디코딩 시 오디오/비디오 동기화가 이루어지지 않는 문제가 개선되었습니다.
- 비디오 화면이 1080P 고해상도 샘플링을 지원하여 핸드폰 라이브 방송을 PC로 시청하는 시나리오에서의 화면 해상도가 향상되었습니다.
- 에러 코드 개선 및 방 입장 에러 코드가 간소화되었습니다.
- 파일이 가끔 몇 초씩 느리게 열리던 문제가 수정되었습니다.

**수정**

- 가끔 HTTP 컴포넌트에서 크래시가 발생하는 문제가 수정되었습니다.
- 음향효과 재생 시 가끔 콜백이 완료되지 않는 문제가 수정되었습니다.
- 가끔 방 입장 실패 이후 복구가 되지 않는 문제가 수정되었습니다.



##  Version 6.8 @ 2019.11.15 

**추가**

- 인이어 모니터링 기능이 추가되었습니다.
- 방 입장 시 수동 풀 스트림을 지정할 수 있게 되었습니다.
- 인터페이스 getBeautyManager 추가 및 뷰티 필터와 포토샵 동적 효과 인터페이스 통합이 이루어졌습니다.
- 엔터프라이즈 버전에 피부 미백, 치아 미백, 주름 개선, 하안검 제거 등과 같은 신규 포토샵 기능이 추가되었습니다.
- onRemoteUserEnterRoom / onRemoteUserLeaveRoom 콜백이 추가되었습니다. 마이크가 없는 사용자의 라이브 방송 입장/퇴장 알림을 지원합니다.

**최적화**

- pts 생성 메커니즘이 개선되었습니다.
- 네트워크 전환 이후 자동으로 더 나은 액세스 포인트를 선택하도록 개선되었습니다.
- startRemoteView가 사전 호출을 지원합니다.

**수정**

알려진 크래시 문제 등 안정성 문제가 수정되었습니다.



## Version 6.7 @ 2019.09.30 

**추가**

- AAR 패키지에 권한 획득 설정이 추가되었습니다.
- Android 8.0 이상 시스템의 CPU 점용 평가가 추가되었습니다.

**최적화**

- 푸시 소모 시간이 최적화되었습니다.
- 단일 사용자가 재생 음량을 독립적으로 조절할 수 있는 기능을 지원합니다.

## Version 6.6 @ 2019.08.02 

**추가**

- 오디오 로컬 녹화 기능이 추가되었습니다.
- 첫 프레임 오디오, 비디오 발송 콜백 인터페이스가 추가되었습니다.
- 시스템 음량 유형 설정 인터페이스가 추가되었습니다.
- 음향효과 인터페이스가 추가되었습니다. 짧은 음향효과 재생을 지원합니다.
- 오디오 사용자 정의 콜백 인터페이스가 출력한 데이터를 수정할 수 있게 되었습니다.

**최적화**

- 방 입장이 개선되어 입장 소모 시간이 감소하고, 입장 성공률이 향상되었습니다.
- 원격 비디오 인터페이스 mute가 지원됩니다.
- 방 입장 오류 코드가 통일됩니다. onEnterRoom 콜백을 통해 result&lt;0 방 입장 오류가 표시됩니다.
- Demo가 개선되었으며 저딜레이 대형 방 지원이 추가되었습니다.
- 플레이어에 음량 설정 인터페이스와 음량 크기 콜백 인터페이스가 추가되었습니다.
- 사용자 정의 발송 비디오가 로컬 렌더링을 지원합니다.
- 사용자 정의 샘플링 발송 비디오가 1080P를 지원합니다.
- 로컬 및 원격 렌더링이 SurfaceView 방식을 지원합니다.

**수정**

- 릴레이 혼합 스트림 관련 문제가 수정되었습니다.
- 로컬 미리보기 각도가 맞지 않는 문제가 수정되었습니다.



##  Version 6.5 @ 2019.06.12 

**추가**

라이브 방송 모드(TRTCAppSceneLIVE)에 ‘저딜레이 대형 방’ 기능이 추가되었습니다.

- 오디오/비디오 최적화를 위한 UDP 프로토콜을 채용함으로써 약한 네트워크에 대한 저항 능력이 강화되었습니다.
- 평균 시청 딜레이를 1초로 만들어 시청자와 호스트간 적극적인 상호작용이 가능해졌습니다.
- 하나의 방에 최대 10만 명이 입장할 수 있게 되었습니다.

**최적화**

- 약한 네트워크 환경에서의 오디오-비디오 동기화가 이루어지지 않는 버그가 개선되었습니다.
- onStatistics 상태 콜백이 개선되었습니다. 콜백이 존재하는 스트림에 한합니다.
- 라이브 방송 TXLivePlayer 재생 버퍼 로직이 개선되어 랙 비율이 감소했습니다.
- 선 muteLocalVideo 이후 재생 취소 시 화면 복구 속도가 개선되었습니다.
- 딜레이와 패킷 손실률이 높은 네트워크 환경에서의 QoE 알고리즘이 개선되어 약한 네트워크에 대한 저항력이 강화되었습니다.
- 디코더 성능을 개선하여 초저가형 Android 핸드폰에서 딜레이가 점차 증가하는 버그를 수정했습니다.
- 오디오 평가 알고리즘(enableAudioVolumeEvaluation)이 개선되어 음량 평가가 더욱 빠르게 이루어집니다.
- 영상 통화(TRTCAppSceneVideoCall) 모드에서의 QoE 알고리즘이 개선되어 1v1 통화 모드의 경우 약한 네트워크 환경에서의 원활함이 더욱 향상되었습니다.

  

**수정**

- 가끔 enterRoom 시 콜백이 오지 않는 버그가 수정되었습니다.
- 오디오 샘플링 중지 이후 재생을 해도 소리가 들리지 않는 버그가 수정되었습니다.
- 로컬 렌더링 view를 삭제한 이후 다시 추가했을 때 그린 스크린이 발생하는 버그가 수정되었습니다.
- 사용자 정의 렌더링 콜백(setRemoteVideoRenderDelegate)과 관련해 원격 화면 해상도가 540P 이상일 경우 콜백을 10회만 하는 버그가 수정되었습니다.



## Version 6.4 @ 2019.04.25 

**추가**

- 로컬 표시 이미지와 인코더 출력 이미지 인터페이스가 추가되었습니다.
- 혼합 스트림 setMixTranscodingConfig API의 설정 콜백 함수가 추가되었습니다.
- 엔터프라이즈 버전에 눈 확대, 안면 축소, V자 턱 및 모션 행거 기능이 추가되었습니다.

**최적화**

- 약한 네트워크 환경에서의 유창성이 향상되었습니다.
- 음량 크기 콜백 알고리즘이 개선되어 음량 콜백 수치가 더욱 합리적으로 변경되었습니다.
- 사용자 정의 오디오, 비디오 데이터 발송 시 외부 지정 데이터 프레임 타임스탬프가 지원됩니다.
- setMixTranscodingConfig 인터페이스가 강화되어 roomID 매개변수를 지원합니다. 각 방 간 마이크 연결 스트리밍에 사용됩니다.
- setMixTranscodingConfig 인터페이스가 강화되어 pureAudio 매개변수를 지원합니다. 음성 통화 전용 시나리오에서의 음성 혼합 스트림 및 녹화에 사용됩니다.
- 저가형 Android 기기에서의 720p 비디오 디코딩 성능 문제가 개선되었습니다.

**수정**
- 음성 핸즈프리 전환이 이루어지지 않는 버그가 수정되었습니다.
- 라이브 방송(TXLivePlayer) 딜레이가 증가한 이후에 복구되지 않는 버그가 수정되었습니다.
- 라이브 방송 시나리오 setVideoEncoderRotation이 적용되지 않는 버그가 수정되었습니다.
- Android에서 마이크 권한을 금지한 이후 오류 콜백이 오지 않는 버그가 수정되었습니다.
- Android 9.0 시스템에서 Demo를 열었을 때 창이 팝업되는 문제가 수정되었습니다.
- 음량 조절 버튼으로 시청자 측 음성을 조절할 수 없는 문제가 수정되었습니다.



## Version 6.3 @ 2019.04.02 

**추가**

- Android 플랫폼 64비트 지원이 추가되었습니다.
- 사용자 정의 비디오 샘플링 인터페이스: TRTCCloud >> sendCustomVideoData가 추가되었습니다.
- 사용자 정의 비디오 샘플링 인터페이스: TRTCCloud >> sendCustomAudioData가 추가되었습니다.
- 사용자 정의 비디오 렌더링 인터페이스: TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate가 추가되었습니다.
- 사용자 정의 오디오 데이터 콜백 인터페이스: TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate가 추가되었습니다. 다음을 지원합니다.
  - 마이크 샘플링 데이터 반환: TRTCAudioFrameDelegate >> onCapturedAudioFrame
  - 각 원격 사용자의 오디오 데이터 반환: TRTCAudioFrameDelegate >> onPlayAudioFrame
  - 혼합 이후 스피커로 재생한 오디오 데이터 반환: TRTCAudioFrameDelegate >>onMixedPlayAudioFrame





## Version 6.2 @ 2019.03.08 

**추가**

- 필터 농도 설정 인터페이스 setFilterConcentration()이 추가되었습니다.
- sendSEIMsg() 인터페이스가 추가되었습니다. 비디오 프레임의 SEI 헤드 정보가 사용자 정의 메시지를 발송하는 것을 지원합니다. 비디오 스트리밍 중 타임스탬프 정보 삽입에 사용됩니다.
- 라이브 룸 간 통화 기능인 connectOtherRoom이 추가되었습니다. 이미 존재하는 두 개의 TRTC 방을 서로 연결하는 기능으로, 라이브 방송 중 호스트 PK에 사용됩니다.



**최적화**

- CPU 사용률 및 안정성이 개선되었습니다.
- 약한 네트워크(연결 상태가 좋지 않은 네트워크 환경)에서의 화면 해상도가 향상되었습니다.
- TRTCCloud의 다중 인스턴스 기능을 취소하고 생성 모드를 단일 인스턴스 모드로 변경하여 다수의 TRTCCloud 인스턴스가 서로의 네트워크 리소스를 점유하는 일이 없도록 하였습니다.

**수정**

음성 통화 전용 시나리오(예: 마피아 게임)에서 릴레이 푸시 스트림 기능을 복구하려면 TRTCParam의 bussInfo 필드를 함께 사용해야 합니다.



##  Version 6.1 @ 2019.01.31 

**최적화**

- 화면 공유 스트리밍 관전 기능을 지원합니다.
- 사용자 정의 비디오 데이터 발송을 지원합니다.
- CDN 푸시와 혼합 스트림 구현이 개선됩니다.
- 방 입장이 라이브 방송과 영상 통화 시나리오로 구분됩니다.
- 안정성이 개선되고, 가끔 발생하는 크래시 문제가 해결되었습니다.
- 트레픽 제어가 개선되어 약한 네트워크 환경에서의 성능이 향상되었습니다.



## Version 6.0 @ 2019.01.18 

**최적화**

- 아키텍처가 LiteAV 커널로 업데이트되었습니다.
- 새로운 QoS 알고리즘을 채용하여 렉 발생률이 감소하고 원활성이 향상되었습니다.
- 새로운 Audio 모듈을 채용하여 각종 네트워크 상황에서의 오디오 품질이 대폭 향상되었습니다.
- 대형/소형 스트리밍 듀얼 채널 인코딩 기능을 지원합니다(Windows와 Mac 기기에서만 활성화할 것을 추천).
- CDN 푸시와 혼합 스트림 기능을 지원합니다.





















