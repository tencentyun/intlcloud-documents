## ITRTCCloud @ TXLiteAVSDK

### ITRTCCloud 싱글톤 생성 및 폐기

| API                 | 설명       |
|-----|-----|
| [getTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6fe6c4bad8206322a32a9d75ca835bd) | [ITRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#classManageLiteAV_1_1ITRTCCloud) 싱글톤 객체 가져오기 |
| [destroyTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4a0722972418aa87ae602f7e12d466ac) | [ITRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#classManageLiteAV_1_1ITRTCCloud) 싱글톤 객체 릴리스 |


### TRTCCloudCallback 콜백 설정

| API                 | 설명       |
|-----|-----|
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af4b26fe08378fb4d303cecbaa495e259) | 콜백 인터페이스[ITRTCCloudCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#interfaceManageLiteAV_1_1ITRTCCloudCallback) 설정 |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6a76c8a9f2dbbeb43285c01c4019a71d) | 이벤트 콜백 삭제 |


### 방 관련 인터페이스 함수

| API                 | 설명       |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afbb3a1e6f73f339d47368a7d620a995f) | 방 입장 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a715f5b669ad1d7587ae19733d66954f3) | 방 퇴장 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a94ab2e8a7df0c120def9d4b0c7658d84) | 역할 전환. 라이브 방송 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)만 해당. |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0002794efb0f0d68d7928570a9e18246) | 크로스 룸 통화(호스트 PK) 요청 |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abd656e4c9b6a01231810ae897627e9bc) | 크로스 룸 마이크 연결 비활성화 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae870243f89b5829cd7ac5612ec958cdf) | 멀티미디어 데이터 수신 모드(방 입장 전에 설정해야 적용 가능) 설정 |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0ea3a44e69394b68c5515b117fe76cf5) | 방 전환 |


### CDN 관련 인터페이스 함수

| API                 | 설명       |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9968ab708775bd2908a3b39790f1319e) | Tencent Cloud 라이브 방송 CDN에 스트림 푸시 시작 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afc00ba747be5299cd7235928a628339e) | Tencent Cloud 라이브 방송 CDN에 스트림 푸시 중지 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af003758b499a542b1795f55f41afbd18) | Tencent Cloud 이외의 라이브 스트리밍 CDN에 게시 시작 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | Tencent Cloud 이외의 라이브 스트리밍 CDN에 게시 중지 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad7b4b8bddf959f40b644339986e41f92) | 클라우드 혼합 스트림 트랜스 코딩 매개변수 설정 |


### 비디오 관련 인터페이스 함수

| API                 | 설명       |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a74a3e5ec77196bd9bca67bf422e25b14) | 로컬 영상 화면 미리보기 활성화 |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1ac7c1b6934150c07a7e9ee1918cfebe) | 로컬 영상 화면 미리보기 창 업데이트 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | 로컬 비디오 수집 및 미리보기 중지 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad531b6af4f07d93b937901aea73d9008) | 로컬 비디오 데이터 전송 기능 일시 중지/재개 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa66214a9ebfbe0cd19fc9c9681e9c4b7) | 원격 사용자의 비디오 스트림 구독 및 비디오 렌더링 제어 바인딩 |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a760a5a8c7df8119166f2050dde38dcea) | 원격 비디오 렌더링 창 업데이트 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#add9d112f4206fd4e4f4490163f4a2da3) | 원격 영상 화면 표시 중지 및 원격 사용자의 비디오 데이터 스트림 풀링 중지 |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aaa75cd1b98c226bb7b8a19412b204d2b) | 모든 원격 영상 화면 표시 중지 및 원격 사용자 비디오 데이터 스트림 풀링 중지 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6e8bd59935a710e3e19c673671d48ab1) | 원격 비디오 스트림 수신 일시 중지/재개 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a129fb0485b0ba8b002e5806e57642715) | 모든 원격 비디오 스트림 수신 일시 중지/재개 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad60c4b7c9c9c685fcf2a0e1be0cc2404) | 비디오 인코더 관련 매개변수 설정 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6c51c82c9246a562fe4dabe3b8f4c5e) | 네트워크 트래픽 제어 관련 매개변수 설정 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a509c5bb9ed2e6c30f0a09678290bf2e8) | 로컬 이미지(메인 스트림)의 렌더링 매개변수 설정 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a291f1c48e5446135c29188f759f023cb) | 비디오 인코딩이 출력되는 화면 방향(원격 사용자가 시청하는 화면과 서버가 녹화하는 화면 방향) 설정 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3e6dae3e385f1e15d528ec3d6f57a59c) | 인코더 출력 화면 이미지 모드 설정 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a46d610de4d78069b9dadc29e4674632b) | 원격 이미지 렌더링 모드 설정 |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a214f8a610feda5f192b048afd476d740) | 크고 작은 이미지의 이중 채널 인코딩 모드 활성화 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af85d4c7d523c19a11f029aa81c27d05f) | 지정 userId의 화면(큰 이미지/작은 이미지) 선택 |


### 오디오 관련 인터페이스 함수

| API                 | 설명       |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad81ec081fa63f5bb2ba0979a405766ff) | 로컬 오디오 수집 및 업스트림 활성화 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab78601c38f1b872b03b662e6856be84c) | 로컬 오디오 수집 및 업스트림 비활성화 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a16d9b4a197a7bc1955240a1ede889246) | 로컬 오디오 음소거/음소거 취소 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a57006bbedfbbe508ad18e04021767125) | 지정 원격 사용자 오디오 음소거/음소거 취소 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9c118b189a47109289528b3c00019649) | 모든 사용자 오디오 음소거/음소거 취소 |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a53681962139b81140f2d66abc4ea6a0f) | SDK 수집 볼륨 설정 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad3dd226f138590f0e2c6b03f108c4e38) | SDK 수집 볼륨 가져오기 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | SDK 재생 볼륨 설정 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#acd6e6336d8f314cef76de9da831a58dd) | SDK 재생 볼륨 가져오기 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a28e0bc3692cbad87ee7d07f2d018b4ba) | 볼륨 크기 표시 활성화 또는 비활성화 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a38e565f1b02f28757f7a40d9ae1dcc4a) | 녹음 시작 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac8c12476bbcf3d691060954fcdb6ebe6) | 녹음 중지 |


### 디바이스 관련 인터페이스 함수

| API                 | 설명       |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aedb2fed650caceab82b00c48585916d9) | 디바이스 관리 모듈 가져오기 |


### 뷰티 필터 특수 효과 및 이미지 워터마크

| API                 | 설명       |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#add2a188f795e5a93ab00a6aee601da25) | 뷰티 필터, 미백, 안색 보정 효과 레벨 설정 |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4845a45a629f050f4f5bbb295d035c41) | 워터마크 설정 |


### 음향 특수 효과 및 보이스 특수 효과

| API                                                          | 설명                       |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad3a3c7b20c5420fce97c5828d614047f) | 음향 효과 관리 ITXAudioEffectManager 가져오기 |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a966d1b9ed824365f567497b052c2ca41) | 시스템 오디오 수집 활성화 |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adef486f26a2c7d74a8cccb537367e66a) | 시스템 오디오 수집 비활성화 |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad4f30caacc7252472ed21a17bfb4ebdd) | 시스템 오디오 수집 볼륨 설정 |


### 화면 공유 관련 인터페이스 함수

| API                 | 설명       |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac7d05e0eb209b774489a3f843081b2fb) | 화면 공유 실행 |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | 화면 수집 중지 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | 화면 공유 일시 중지 |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | 화면 공유 재개 |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae11fbc1c3d29f40fa29dd3c45a739a96) | 공유 가능한 화면 창 열거.   startScreenCapture 전에 호출할 것을 권장. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a766dd7fa395c2e3ae6cc26781c1ef98b) | 화면 공유 매개변수 설정. 화면 공유 과정 중에도 호출 가능. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a67e267ae6043ae873580a2a56306a1d8) | 화면 공유 인코더 매개변수 설정 |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a91d9fb6b6e037dc0d4e65b40e8bf781f) | 화면 공유 오디오 믹싱 볼륨 크기 설정 |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab975f0d54e63bf810b1a92539ad78057) | 지정 창을 화면 공유 제외 리스트에 추가. 제외 리스트에 추가된 창은 공유되지 않음. |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3794c820d0d45cf55802b7162df063c9) | 지정 창을 화면 공유 제외 리스트에서 제거 |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a179d325cc9f043d049cdedc35a64497a) | 모든 창을 화면 공유 제외 리스트에서 제거 |

### 사용자 정의 수집 및 렌더링

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------- |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a87dace307d0df1eb4a5801d65517f40b) | 비디오 사용자 정의 수집 모드 활성화        |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4b0e29533e0fea8dfb1bd207ec68a577) | 사용자가 수집한 비디오 데이터 SDK에 전송 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6cf1f1f480d3a6228f55d7e57ad506a8) | 오디오 사용자 정의 수집 모드 활성화        |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a12c6c039a6ffda1519fe4fcbc6e863a0) | 사용자가 수집한 오디오 데이터를 SDK에 전송 |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a427084cbb7613b229b5b29c8a9479497) | 로컬 비디오 사용자 정의 렌더링 설정        |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1b795d10cdb8a959505c09c443667d59) | 원격 비디오 사용자 정의 렌더링 설정       |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a33d475c807ae068e71183a0de14b6cd7) | 오디오 데이터 콜백 설정              |

### 사용자 정의 메시지 발송

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------ |
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a92ed9ed2ba1bd3c65c21c223aa05aab4) | 사용자 정의 메세지를 방 안에 있는 모든 사용자에게 전송     |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6c64e92e73628496c4f3e35d25b4e57b) | 적은 양의 사용자 정의 데이터를 비디오 프레임에 삽입 |


### 네트워크 테스트 

| API                 | 설명       |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af9a96c20afda0325655f5cff4878e62f) | 네트워크 속도 테스트 시작(통화 품질에 영향을 미칠 수 있으니 영상 통화 중에는 테스트하지 마십시오) |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a58d732ba648d1f9a3a460c02de79bb9b) | 네트워크 속도 테스트 중지 |

### LOG 관련 인터페이스 함수

| API                                                          | 설명                       |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af48f494210612771269b3c3893683403) | SDK 버전 정보 가져오기         |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab941d390cf7df8034c522edd8dd2f3eb) | Log 출력 레벨 설정         |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a452f7778aaba21498765444f907bb0a0) | 콘솔 로그 출력 활성화/비활성화  |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af6d9f433c0c17ca34b040c51403865db) | Log 로컬 압축 활성화/비활성화 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa735664fb9f7636744f4b0f3e4482669) | 로그 저장 경로 설정          |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1a5f967baf4f3772820e1c03a78447d) | 로그 콜백 설정              |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a08d4c264ef3f43eea7616e4264a1e4e6) | 대시보드 표시                |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2a3f591a5091fa7db2158cfd7440cd68) | 실험용 API  호출       |

### 사용하지 않는 인터페이스 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7104b3996ed49714cd34cbca71e6efb2) | 마이크 볼륨 크기 설정                                       |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | 화면 공유 실행                                               |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a177d006b52fdc3232d8ad0ef9dfbfd50) | 배경 음악 재생 실행                                           |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a11004f1ba27b057985850a25307b0bec) | 배경 음악 재생 중지                                           |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa4b92d4c989e99612f6c4dab03a78764) | 배경 음악 재생 일시 중지                                           |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aed6e8f224b5f834b1bc0c15f9701f692) | 배경 음악 계속 재생                                           |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0abf49e1884aad560fb7741afc16cf64) | 음악 파일 총 시간 가져오기. 단위: 밀리초.                               |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a034da21d55333df96f1f912432d7eb64) | 배경 음악 재생 진행률 설정                                          |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2ce1461e15c3d000e02b3c99d126843e) | 배경 음악 재생 볼륨 크기 설정                                 |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6c967a33924903c4f2dc6b9daf050cf) | 배경 음악 로컬 재생 볼륨 크기 설정                             |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af398e75cb3334b5ed5911f74ac138949) | 배경 음악 원격 재생 볼륨 크기 설정                             |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aacf76f546a4b47abc13e046d0bd38328) | 음향 효과 재생                                                   |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a942a6f358980c8520e2155fb4ef55bd0) | 음향 효과 볼륨 설정                                               |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a61561195216ac575235b67d410070563) | 음향 효과 중지                                                   |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7066509af1de32c290b7cc297cd00f2b) | 모든 음향 효과 중지                                               |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a19416181cce88c58052a4eb2e87adeb8) | 모든 음향 효과 볼륨 설정                                         |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a43f83a1323cc39c1610c61cf79ab652c) | 음향 효과 일시 중지                                                   |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a23b65446d7dd9835da888b5285867629) | 음향 효과 재개                                                   |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a45d88faf382acd56d0dd3ec8ce3744e2) | 화면 공유 매개변수 설정                                           |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3cf91279c13a4f10f8d955b0b6ed1a46) | 원격 영상 화면 표시 시작                                       |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a998268e8e9c857367d4ff75a3232daad) | 원격 영상 화면 표시 중지 및 원격 사용자의 비디오 데이터 스트림 풀링 중지     |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ada1aa39d0b579f0f939d17c3ca78df92) | 로컬 이미지 렌더링 모드 설정                                     |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1dceb7f02cf974f6944c5c306b86cab6) | 원격 이미지 렌더링 모드 설정                                     |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8d5dc6995392c71257493353e3571e86) | 로컬 이미지의 시계 방향 회전 각도 설정                               |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0290931f9fb237a9ab38c37d5e911a54) | 원격 이미지의 시계 방향 회전 각도 설정                               |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a050a53b8bed638f76a64ad82ecd89078) | 로컬 카메라 미리보기 화면의 이미지 모드 설정                           |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5c153269c676a12b20327f9600f9206d) | 원격 사용자의 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 표시 시작 |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a41c333a00cc151c909b7d0fe4f4b34b5) | 원격 사용자의 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 표시 중지 |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8ee2941c51edc2218fa224c03b650a78) | 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 표시 모드 설정 |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7edb64ac7d4e6755d7f79d75d94770fd) | 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 시계 방향 회전 각도 설정 |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5cc9f8652845ff0d7adc5b2d24b8a269) | 시청자 비디오 품질 우선 순위 설정                               |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae241d03683fdde1e033078a6057f609c) | 오디오 품질 설정                                               |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3177329bc84e94727a1be97563800beb) | 로컬 오디오 수집 및 업스트림 활성화                                   |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae9b8a8e04f14a10827af80c6cf3fd390) | 카메라 디바이스 리스트 가져오기                                         |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afc1cb1512326ff70fd2f303726af9475) | 사용할 카메라 설정                                         |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3cd193c8867f5332297e0d664b2a9516) | 현재 사용중인 카메라 가져오기                                       |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aae179b7da159ec44d748345cb79cb645) | 마이크 디바이스 리스트 가져오기                                         |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5bcd6e1c8526f2ffb4a04477bdd84abb) | 현재 선택한 마이크 가져오기                                       |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2591a4c670807e507a1cd70a0c574df7) | 사용할 마이크 설정                                         |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad86183c23657588ef232a6d9796e11c0) | 시스템의 현재 마이크 디바이스 볼륨 가져오기                                 |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a585cb97ea5fbf80bb7f57f3fa2a49c27) | 시스템의 현재 마이크 디바이스 볼륨 설정                               |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2e69c8cefc75cd5a0bb6277d83faba4a) | 스피커 디바이스 리스트 가져오기                                         |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4a9c4c8a642976a234b1a5ce607e370d) | 현재 스피커 디바이스 가져오기                                       |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3881585d770b639260437b3127c6a5d7) | 사용할 스피커 설정                                         |
| [getCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad83afd5da873a7b6c690c02c3f5d32a4) | 시스템의 현재 스피커 디바이스 볼륨 가져오기                                 |
| [setCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a72a814a76c9a16cbf5cfdeefdb37ca13) | 시스템의 현재 스피커 디바이스 볼륨 설정                                 |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adfdfd81465003ac6d21e5be20c119c41) | 카메라 테스트 시작                                         |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1b67fa3f322efe538d924b381c06e676) | 카메라 테스트 중지                                             |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0bab0a75a4f96746974918126255c66c) | 마이크 테스트 활성화                                             |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8cca1c5913ac021987680195075e5fc9) | 마이크 테스트 중지                                             |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac7f15eee92377d3bb5d1b7ec5e99d3be) | 스피커 테스트 활성화                                             |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abf383f971dc54f0254b2d40f100cc9ca) | 스피커 테스트 중지                                             |


## TRTCCloudCallback @ TXLiteAVSDK

Tencent Cloud 영상 통화 기능의 콜백 인터페이스 유형

### 오류 이벤트 및 경고 이벤트

| API                 | 설명       |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7c34b7b7918c7db1a2b3fb4dbf90213d) | 오류 콜백. SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 맞게 사용자에게 적절한 인터페이스를 제공. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aad50ebc5637840fecd88ae1fed6510a5) | 경고 콜백: 랙 또는 복구 가능한 디코딩 실패 등 심각하지 않은 문제를 알릴 때 사용 |

### 방 이벤트 콜백

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9540be761c1563aa2d8eddb62ccb5578) | 방 입장 콜백                  |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad5ac26478033ea9c0339462c69f9c89e) | 방 퇴장 이벤트 콜백                |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a720d216a5b81d02669810cab9e9f3232) | 역할 전환 결과 콜백                  |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a4fb0e99751e6c15a1e5f702e643640b9) | 크로스 룸 통화(호스트 PK) 요청 결과 콜백 |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a53d2f8b13139a59202cb198bc92deb85) | 크로스 룸 통화(호스트 PK) 종료 결과 콜백 |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6b698ae14a2bf21542bce4be4ea09610) | 방 전환(switchRoom) 결과 콜백  |

### 구성원 이벤트 콜백

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a966b16d2f3042c0c45d9f372126c455a) | 사용자가 현재 방에 입장함 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a2a84fc3062a578584f219210f6b9bba7) | 사용자가 현재 방에서 퇴장함 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad76012a12ae044c3a30e248070eb0fb2) | 사용자의 카메라 비디오 활성화 여부                         |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a52ad5b09959df6e940aec7fb9615de9c) | 사용자의 화면 공유 활성화 여부                          |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#abd6c0a2a5994b95d7d467deaacf36269) | 사용자의 오디오 업스트림 활성화 여부                           |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a04e7917781c8cd3fec23a976acf05f80) | 로컬 또는 원격 사용자의 첫 번째 프레임 화면 렌더링 시작               |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1942830ce2261dc25f80e973cd104fd8) | 원격 사용자의 첫 번째 프레임 오디오(로컬 오디오는 공지 안 함) 재생 시작 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a266f7551ab47384616b36ad2783615d1) | 첫 번째 프레임 로컬 비디오 데이터 발송 완료                    |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#acb73daf4ce82cd03f787f057b233b412) | 첫 번째 프레임 로컬 오디오 데이터 발송 완료                     |


### 통계 및 품질 콜백

| API                 | 설명       |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa7694d95e5c47ec79dd06572a8a89c94) | 네트워크 품질: 해당 콜백은 2초에 한 번 트리거되고 현재의 네트워크 업스트림/다운스트림 품질을 통계함  |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a61c2b1f320733667a5208e424998b886) | 기술 메트릭 통계 콜백 |

### 서버 이벤트 콜백

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aed43a70b4a95eb95181e2b410013bf54) | SDK와 서버 연결이 끊김 |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | SDK와 서버 다시 연결 중 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | SDK와 서버가 다시 연결됨 |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6c3984e5bf71912718638884107ad408) | 서버 속도 테스트 콜백. SDK는 여러 서버 IP에 속도 테스트를 진행하며 모든 IP의 속도 테스트 결과는 해당 콜백을 통해 공지됨.|

### 하드웨어 디바이스 이벤트 콜백

| API                                                          | 설명                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aaa74021e5fd2564afb2df50e25eedeff) | 카메라 준비 완료                                            |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#afdac7dee94451913a4dc9982badc8035) | 마이크 준비 완료                                            |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa6b7c420cd4effacaf16eb73a5da288f) | user ID의 볼륨 및 원격 총 불륨 등 볼륨 크기 알림에 사용되는 콜백 |
| [onDeviceChange](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#acda9040715f8a332d36ca9d6e4015ff9) | 로컬 디바이스 연결 상태 콜백                                         |
| [onTestMicVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a24817d5d5810778ea1e3465d6ac3609c) | 마이크 테스트 볼륨 콜백                                        |
| [onTestSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a03f4eb9af917dcc5d62717f1c1940ffc) | 스피커 테스트 볼륨 콜백                                        |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a28d95bff7fe7a5c8062e07e92dffd02d) | 현재 오디오 수집 디바이스 볼륨 변화 공지                              |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a79f4f4302849a5c71892986a93b17246) | 현재 오디오 재생 디바이스 볼륨 변화 공지                              |


### 사용자 정의 메시지 수신 콜백

| API                 | 설명       |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a139d77ca75e7baee6a9017beca20fff3) | 사용자 정의 메세지 수신 콜백 |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a048194ab37bec16c6ee068ac7ee9fef3) | 사용자 메세지 손실 콜백 |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9c16a1ce79d6d50c3576330d0493fd1b) | SEI 메세지 수신 콜백 |

### CDN 릴레이 푸시 콜백

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a765ef1ca062295a1d84ac262e27ed5a8) | Tencent Cloud 라이브 방송 CDN에 푸시 스트림을 시작하는 콜백으로 TRTCCloud의 startPublishing() 인터페이스에 상응함 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a47a960139fb4732ff90999fa79139544) | Tencent Cloud 라이브 방송 CDN에 푸시 스트림을 중지하는 콜백으로 TRTCCloud의 stopPublishing() 인터페이스에 상응함 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9cb1e74a2446045924d8959e7232732e) | CDN으로 릴레이 푸시 스트림 활성화 콜백                              |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1b9f3dab153a4b9d84217de1c590d25b) | CDN으로 릴레이 푸시 스트림 중지 콜백                              |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a0f02456093b0a82629695ec15c945e88) | 클라우드 혼합 스트림 트랜스 코딩 매개변수 설정 콜백으로 TRTCCloud의 setMixTranscodingConfig() 인터페이스에 상응함 |

### 화면 공유 콜백

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onScreenCaptureCovered](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aca39d43f65ee8d5007ce075d8c808dc1) | 화면 공유 창이 차단되어 캡처가 불가능할 경우 SDK는 해당 콜백을 통해 사용자에게 차단된 창을 제거할 것을 공지 |
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7d15537d26fb001045ff95157d59ed3f) | 화면 공유 시작 시, SDK는 해당 콜백을 통해 공지                     |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9e49f6e6887d63e3e817033681f0ad95) | 화면 공유 일시 중지 시, SDK는 해당 콜백을 통해 공지                     |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a399959bd81e349cb76c9b7c939202410) | 화면 공유 복구 시, SDK는 해당 콜백을 통해 공지                     |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad0c359a7cefb8f246d498a3fbf52b1ac) | 화면 공유 중지 시, SDK는 해당 콜백을 통해 공지                     |

### 사용하지 않는 인터페이스 콜백

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | -------------------------------------- |
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a3d806371c6912d889e9e0bc198e2d2bd) | 호스트가 현재 방에 입장함(폐기됨) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1d6099d0439eec6c44abfe166ccb8aee) | 호스트가 현재 방에서 퇴장함(폐기됨) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#abe967d855abae66836877fe0dacf8b5f) | 음향 효과 종료(폐기됨) |
| [onPlayBGMBegin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a61d9fa641b1790094e955aeb355cca92) | 배경 음악 재생 시작(폐기됨) |
| [onPlayBGMProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6ce46d86ba3f04613c8c3eb16f96ae44) | 배경 음악 재생 진행률 콜백(폐기됨) |
| [onPlayBGMComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aff8d7c6c3d2a5984ddd6448008041340) | 배경 음악 재생 종료(폐기됨) |


### 비디오 데이터 프레임의 사용자 정의 프로세싱 콜백

| API                 | 설명       |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a473b28cb74e44a9629c21b64ca23bf98) | 사용자 정의 비디오 렌더링 콜백 |


### 음성 데이터 프레임의 사용자 정의 프로세싱 콜백(읽기 전용)

콜백 함수는 SDK 내부 스레드에서 동기화되어 표시되므로 시간이 소모되는 작업은 하지 마시기 바랍니다. 
>? 필요에 따라 관련 함수 사용을 정의하시고 불필요한 성능 저하를 야기하는 작업은 피하십시오.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCapturedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a329db3f999a740633c2446368f9babb0) | 로컬 마이크가 수집한 오디오 데이터 콜백                             |
| [onPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a12f83dbce03e0770d09f9910e58ec72c) | 각 원격 사용자의 오디오 믹싱 전 오디오 데이터 (특정 채널의 음성을 문자로 전환하려면 믹싱 전 원본 데이터를 사용해야 함) |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1e620894f820b28e94d644cfcdea3c17) | 각 채널 오디오 데이터를 믹싱한 후 스피커로 재생한 오디오 데이터                  |

### 로그 관련 콜백

| API                 | 설명       |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ab96d17528679cb05cf1f28978b2cf432) | 로그 출력 시의 콜백 |


## 주요 클래스 정의

| 클래스 이름 | 설명 |
|-----|-----|
| [TRTCImageBuffer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a115d7544222e40e31d1766f7770f4619) | 이미지 캐시 |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a78b6e0861f6c951b7269e5b0e13b8c36) | 화면 수집 정보 |
| [SIZE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1SIZE) | buffer 길이와 너비 기록 |
| [ITRTCScreenCaptureSourceList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#interfaceManageLiteAV_1_1ITRTCScreenCaptureSourceList) | 화면 창 리스트 |
| [ITRTCDeviceCollection](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__csharp.html#interfaceManageLiteAV_1_1ITRTCDeviceCollection) | 디바이스 리스트 |
| [ITRTCDeviceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__csharp.html#interfaceManageLiteAV_1_1ITRTCDeviceInfo) | 디바이스 Item 정보 |
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | 방 입장 관련 매개변수 |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a43a83bd5122296aa87cc7f6e964921c5) | 비디오 인코딩 매개변수 |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a7cd5c078b248a32557a85226f1d30697) | 네트워크 트래픽 제어 관련 매개변수 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#af6aab62536869726ee32b158ddbbf5ce) | 비디오 품질 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#abdeba26e639757957fd75f528ba14f6e) | 볼륨 크기 |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a0f5d7607bc170be903d207b4e0c87fab) | 비디오 프레임 데이터 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a3c9f428bf1fc390b37a9c74accf226c6) | 오디오 프레임 데이터 |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a8858167e09ab4d55f5e49c89bd4a1848) | 네트워크 속도 테스트 결과 |
| [RECT](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1RECT) | 직사각형의 네 개 점 좌표 기록 |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#ac5b1947f21f77726cbff822eaf0003f9) | 클라우드 혼합 스트림의 모든 서브 채널 위치 정보 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a6066a5537ad8c1bc6158d43e8a4765db) | 클라우드 혼합 스트림(트랜스 코딩) 설정 |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a0b977361cb4d84b1ece0b26c949dcde6) | CDN 릴레이 푸시 스트림 매개변수 |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a724e3aa5cbc2249b7ce31bd7f9362d7b) | 녹음 매개변수 |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCAudioEffectParam) | 음향 효과 재생 |
| [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCLocalStatistics) | 사용자의 로컬 멀티미디어 통계 정보 |
| [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCRemoteStatistics) | 원격 구성원 멀티미디어 통계 정보 |
| [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#structManageLiteAV_1_1TRTCStatistics) | 통계 데이터 |

