## TRTCCloud @ TXLiteAVSDK

### 인스턴스 생성 및 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac5da416bb06d461c7e1e555e3fd143ee) | TRTCCloud 인스턴스 생성(싱글톤 모드) |
| [destroySharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a69e76ca12b727c7cbcbdda274fc007a2) | TRTCCloud 인스턴스 폐기(싱글톤 모드)  |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a22fe2f31f2ef62fb3c6cba083dc6c016) | TRTC 이벤트 콜백 설정 |
| [setListenerHandler](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a48c867145dcc09289f7af41871b4fdd9) | TRTCCloudDelegate 이벤트 콜백을 구동하는 큐 설정 |

### 방 관련 API
| API  | 설명         |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) | 방 입장 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) | 방 퇴장 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) | 역할 전환 |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09fbe471def0c1790357fc2b70149784) | 방 전환 |
| [ConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) | 크로스 룸 통화 요청 |
| [DisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af777ac398ac47c8e5649c983fa2053fa) | 크로스 룸 통화 종료 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) | 구독 모드 설정(방에 입장하기 전에 설정해야 적용됨) |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3c4a93d24e0ef076168b44cf3545a8d4) | 방 서브 인스턴스 생성(멀티 룸 동시 시청용) |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6dc091ead812c50497c4b4e87e5c2fcf) | 방 서브 인스턴스 폐기 |

### CDN 관련 인터페이스 함수
| API  | 설명         |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c168a9aa35ccd0b24981526425e4730) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 시작 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3067efa528fb9ffb8cf7685ce29925d4) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 중지 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41aefb8be652f8f6803020e543acaadc) | Tencent Cloud CDN 외에 멀티미디어 스트림 게시 시작 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0e1e8a1eb1cac3f5e5d4433b4aa21e8e) | Tencent Cloud CDN 외에 멀티미디어 스트림 게시 중지 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af7cf5544f9b8027e9526c32319a13838) | 클라우드 혼합 스트림 레이아웃 및 트랜스 코딩 매개변수 설정  |

### 비디오 관련 인터페이스 함수
| API  | 설명         |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) | 로컬 카메라 미리보기 이미지 활성화(모바일) |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae91432ada1767f793c460c7b897b6809) | 로컬 카메라의 미리보기 이미지 업데이트 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af6ee50bf2c4c592294061077fc727505) | 카메라 미리보기 중지 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | 로컬 비디오 스트림 게시 일시 중지/재개 |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d) | 로컬 비디오 일시 중지 교체 이미지 설정 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | 원격 사용자의 비디오 스트림 구독 및 비디오 렌더링 컨트롤러 바인딩 |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9be8a4c5ea4da16fb1ca42e8e258effd) | 원격 사용자의 비디오 렌더링 컨트롤러 업데이트 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | 원격 사용자의 비디오 스트림 구독 중지 및 렌더링 컨트롤러 해제 |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) | 모든 원격 사용자의 비디오 스트림 구독 중지 및 모든 렌더링 리소스 해제 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | 원격 사용자의 비디오 스트림 구독 일시 중지/재개 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2d8a7b74068026a85158262cc9aedd66) | 모든 원격 사용자의 비디오 스트림 구독 일시 중지/재개 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) | 비디오 인코더의 인코딩 매개변수 설정 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a02631a5e4251657875535c38ab319239) | 네트워크 품질 관리 관련 매개변수 설정 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a916eab6c78587300165008f61a473f8b) | 로컬 비디오 이미지의 렌더링 매개변수 설정 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2e37d4b9555c58148ad507938375505f) | 원격 비디오 이미지의 렌더링 모드 설정 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272afecae1d291033cb9cd4b1d7b52e0) | 비디오 인코더 이미지 출력 방향 설정 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a32d9ba3696b305373508253f9bee8236) | 인코더에서 출력되는 이미지의 미러 모드 설정 |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abbbe1548bfba0bd082a08478ce35e9bc) | G-센서 어댑티브 모드 설정 |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3a040c5012cf572b9dfabcca87f2cbb7) | 크고 작은 이미지 듀얼 채널 인코딩 모드 활성화 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2a018cc1010587ea9b0fbd791eb3c54f) | 지정된 원격 사용자의 크고 작은 이미지 전환 |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae75285c95fc53651e24fa23c4141093b) | 영상 화면 캡처 |

### 오디오 관련 인터페이스 함수
| API  | 설명         |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | 로컬 오디오 수집 및 게시 활성화 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272bba21d046347ac42d76069ba5972c) | 로컬 오디오 수집 및 게시 중지 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86) | 로컬 오디오 스트림 게시 일시 중지/재개 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) | 원격 오디오 스트림 재생 일시 중지/재개 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) | 모든 원격 사용자의 오디오 스트림 재생 일시 중지/재개 |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4a3dda74823afa597b42b981257e9e22) | 오디오 경로 설정 |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3dabe4a4e13509cf1bd5b3d58aabaa06) | 원격 사용자의 오디오 재생 볼륨 설정 |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6af5e2c4819a683042f382688aff41e9) | 로컬 오디오 수집 볼륨 설정 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a81037b960fb2b3501b1e8e60f2b5f9f3) | 로컬 오디오 수집 볼륨 가져오기 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b20e1eec637c82190c5264d78d686af) | 원격 오디오 재생 볼륨 설정 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5a1636fa1300b0b4e2829846c36450a2) | 원격 오디오 재생 볼륨 가져오기 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a43e99323fd5680fd377b95b97f0885c3) | 볼륨 알림 활성화 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8b04666d32535637308605d5e15b7220) | 오디오 녹음 시작 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7d55e5f15d1291afc89f7e1dfe0a25d8) | 오디오 녹음 중지 |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5d6bf60e9d3051f601988e55106b296c) | 로컬 미디어 녹화 시작 |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae982c3c04c0195711ee4e56132522c4b) | 로컬 미디어 녹화 중지 |
| [checkAudioCapabilitySupport](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a225161d0c1028708b4c043653ea0ee4b) | 특정 오디오 기능 지원 여부 쿼리(Android만 해당) |
| [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6d7f5080d804137be1bd3541f533b275) | 원격 오디오 스트림의 스마트 동시 재생 정책 설정 |

### 디바이스 관리 관련 인터페이스
| API  | 설명         |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae66395bc404d205fcd7fe9082ca85ce9) | 디바이스 관리 클래스 가져오기(TXDeviceManager) |

### 뷰티 필터 특수 효과 및 이미지 워터마크
| API  | 설명         |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) | 뷰티 필터 관리 클래스 가져오기(TXBeautyManager) |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1083aaf0441e3d90ce6641d278a97a63) | 워터마크 추가 |

### 배경 음악 및 음향 효과
| API  | 설명         |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) | 음향 효과 관리 클래스 가져오기(TXAudioEffectManager) |

### 화면 공유 관련 인터페이스
| API  | 설명         |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | 화면 공유 시작 |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab6c3014f6f88c775aa91fccea19ce8a4) | 화면 공유 중지 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | 화면 공유 일시 중지 |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e) | 화면 공유 재개 |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a34d994fbba559994aaf3a1f20420a885) | 화면 공유(서브 스트림)의 비디오 인코딩 매개변수 설정(데스크톱 및 모바일 시스템 모두 지원) |

### 사용자 정의 수집 및 렌더링
| API  | 설명         |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | 사용자 정의 비디오 수집 모드 활성화/비활성화 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | 수집한 비디오 프레임을 SDK에 전송 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a206b9ce3594aa535b633d4f7c8f97210) | 사용자 정의 오디오 수집 모드 활성화 |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a30a542b7d540c8699595a22ca3401f29) | 수집한 오디오 데이터를 SDK에 전송 |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7b7d3707d2ed8e8f1221faf73af49027) | 사용자 정의 오디오 트랙 활성화/비활성화 |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a899a1e9d42c9bf9ce1474aec13ac6747) | 사용자 정의 오디오 트랙을 SDK에 믹싱 |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a362490afb9028595635b52d041a2bfb0) | 푸시 스트림 시 믹싱된 외부 오디오의 푸시 스트림 볼륨 및 재생 볼륨 설정  |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b36383129314d70f150c08de182e2b8) | 사용자 정의 수집 시 타임스탬프 생성 |
| [setLocalVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b565dc8c77df7fb826f0c45d8ad2d85) | 타사 뷰티 필터에 대한 비디오 데이터 콜백 설정 |
| [setLocalVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa3cbb7a501c3151d94473965e2538c7a) | 로컬 비디오에 대한 사용자 정의 렌더링 콜백 설정 |
| [setRemoteVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4fca6803d13e4c7ff00dcac2974637e4) | 원격 비디오에 대한 사용자 정의 렌더링 콜백 설정 |
| [setAudioFrameListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034b6fce9a517267acd874c243efc575) | 오디오 데이터 사용자 정의 콜백 설정 |
| [setCapturedRawAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9047b34857b12d85688b3b3f1ca1c3f0) | 로컬 마이크에서 수집한 원본 오디오 프레임의 콜백 형식 설정 |
| [setLocalProcessedAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac0f65e13815edc05ebd765826a94e3dc) | 전처리된 로컬 오디오 프레임의 콜백 형식 설정 |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a98a2e38d75366fbc2c4da92fec5c0a30) | 시스템에서 재생할 오디오 프레임의 콜백 형식 설정 |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803) | 사용자 정의 오디오 재생 활성화 |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c1c268173ab9b1bc24d34766e433931) | 재생 가능한 오디오 데이터 가져오기 |

### 사용자 정의 메시지 전송 인터페이스
| API  | 설명         |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa4847ad53acc9ab5990194b21ff5b070) | UDP 채널을 사용하여 방의 모든 사용자에게 사용자 정의 메시지 보내기  |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034f9e1effbdadf8b9bfb7f3f06486c4) | SEI 채널을 사용하여 방의 모든 사용자에게 사용자 정의 메시지 보내기  |

### 네트워크 테스트 인터페이스
| API  | 설명         |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6db053500be88a8735bfc69730447912) | 네트워크 속도 테스트 시작(방 입장 전 사용) |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3e862cef0e818ddecdc3dc4d66a6f8f9) | 네트워크 속도 테스트 중지 |

### 디버깅 관련 인터페이스
| API  | 설명         |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aeb5168abbd62c631b65247e6289d1e2d) | SDK 버전 정보 가져오기 |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0ec9520dda7e2062f7455956d093113b) | Log 출력 레벨 설정 |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2942d9d05045d3f0e0add45a3e10b3ee) | 콘솔 로그 출력 활성화/비활성화 |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a495d2122a4098ab371d825c1f0bb90f5) | 로컬 로그 압축 활성화/비활성화 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a44c20358d08da798e0f15d142c9c3914) | 로컬 로그 저장 경로 설정 |
| [setLogListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a299a71f4addb3638c7790de446fbdf37) | 로그 콜백 설정 |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2cdb5d447114534f53bad5bdc48afba) | 대시보드 표시 |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa2014c293033e9ea60aa6ffd525ee2fa) | 대시보드 여백 설정 |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f331dd0cfff51ab5a3becf4950a55e) | 실험용 인터페이스 호출 |
| [setNetEnv](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a28ae49c86c5e5ba7e5ad2eae171bde76) | TRTC 백그라운드 클러스터 설정 (Tencent Cloud R&D 팀만 해당) |

### 사용하지 않는 인터페이스
| API  | 설명         |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab356494d1b7dd924be69b23aa631a85a) | 마이크 볼륨 설정 |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) | 뷰티 필터, 미백 효과, 안색 보정 효과 단계 설정 |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4ff69ce783f648f23dd737641344ac52) | 눈 확대 필터 강도 설정 |
| [setFaceSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78a159a2a45d24dbd5722eb73d237e8a) | 갸름한 얼굴 필터 강도 설정 |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a58bb7ce1fbbc40a50647d64693ac5d41) | V라인 필터 강도 설정 |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a774eb948494cecec024771434ccd9d3c) | 턱 늘이기/줄이기 필터 강도 설정 |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa14091f0d02330cbd02da5186e9dd874) | 얼굴 축소 필터 강도 설정 |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3f806534b2596d7e29ea0ea6c070b591) | 코 축소 필터 강도 설정 |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a521a0446d0922d480a1eec4b86f1ecb2) | 애니메이션 스티커 설정 |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a066cbf8f4f6c1cd23fe9451b82c5a073) | 애니메이션 스티커 음소거 설정 |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a925323ab809957ccaeb4cef30841cb72) | 컬러 필터 설정 |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5fb4c8bc9948e61a75b9ef85f618309d) | 컬러 필터 강도 설정 |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aef56a36b901d5e525ee539e7d5642063) | 그린 스크린 비디오 설정 |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3df738557f5c658c37174ac9aeae9684) | 배경 음악 재생 |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3ee7bdd15de4ba9010aa5ece3abff0ab) | 배경 음악 재생 중지 |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a21ddee03e6f4cec028a24e5d5e30955e) | 배경 음악 재생 중지 |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aaa8b34ef2b334bd22a1cb6541a4c6702) | 배경 음악 재생 중지 |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae7342a8bcfda22a872aa684f06a4677f) | 배경 음악의 총 길이(단위:ms) 가져오기 |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78f901b6175352a31b0236776bfdc661) | 배경 음악 재생 진행률 설정 |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ada9c2b4aaf9a1a9ab9cd846593fdf9e6) | 배경 음악 볼륨 설정 |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab1e1c94c9efd967dbffb46d3ba08fef5) | 배경 음악 로컬 재생 볼륨 설정 |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a535eab48f9df390f4de5ebd5afcd59e3) | 배경 음악 원격 재생 볼륨 설정 |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6f4f89be3c810acfa2430ad65fd7ea68) | 리버브 효과 설정 |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37acaf3b2539e0b1c18123a646e91189) | 음성 변조 유형 설정 |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad1ed7667282eccfac1992c1e547a5aeb) | 음향 효과 재생 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | 음향 효과 볼륨 설정 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | 음향 효과 재생 중지 |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a770543c80d3a5629a26d1382535fb6c4) | 모든 음향 효과 중지 |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9bb41c4ff1a5b24ca742fe3ce45a2bc0) | 모든 음향 효과 볼륨 설정 |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab32923d04ce164b82879b3e05833959f) | 음향 효과 일시 중지 |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a33ab6e798d3da245435166464b702d4f) | 음향 효과 일시 중지 |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9306bca7c6a13e0443a3fa1b40c9f343) | 인이어 모니터링 활성화(또는 비활성화) |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | 원격 영상 화면 표시 시작 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | 원격 영상 화면 표시 중지 및 원격 사용자의 비디오 데이터 스트림 가져오기 중지 |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) | 원격 이미지 렌더링 모드 설정 |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8478d804d2a07520ce2bc5466b727839) | 원격 이미지 시계 방향 회전 각도 설정 |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) | 로컬 이미지 렌더링 모드 설정 |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69) | 로컬 이미지 시계 방향 회전 각도 설정 |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1) | 로컬 카메라 미리보기 이미지의 미러 모드 설정 |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#acdbe3829d20f58cedd5a0c2f49ea24dc) | 원격 사용자 서브스트림 이미지 표시 시작 |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae5f540d795425046c9166b0a2361a8de) | 원격 사용자 서브스트림 이미지 표시 중지 |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a73f66e66ffee44e19ebb4d8c56c89718) | 서브스트림 이미지 채우기 모드 설정 |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#affdf177b468fdf40a41782e2e47524cc) | 서브스트림 이미지 시계 방향 회전 각도 설정 |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2efc2703c86ee009bd4a1d440d0c1e0) | 큰 화면/작은 화면 시청 우선순위 설정 |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55) | 음질 설정 |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | 음질 설정 |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1b43a65a32f9dcb81b39b9c51c5bc4c6) | 카메라 전환 |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac7ae26eca2f9a673121803d6d175b034) | 현재 카메라의 줌 지원 여부 쿼리 |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9f761eebdf04f724e0d1591c41c6045f) | 카메라 줌 비율 설정(초점 거리) |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a645183ba7c0cea748973796cb38aad8c) | 플래시 지원 여부 쿼리 |
| [enableTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09253f6547914d54058831b61325e770) | 플래시 켜기/끄기 |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abd39aca40adfc8da6beaf32141f84cfa) | 카메라 초점 설정 지원 여부 쿼리 |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa7c65fb033727804e7a79b8f135c776c) | 카메라 초점 위치 설정 |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a23f25ffb81215a32517da78455459ff2) | 얼굴 위치 자동 인식 지원 여부 쿼리 |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5438dcc45dc2f26a3771a5feddcdef5d) | 시스템 볼륨 유형 설정 |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | 사용자 정의 비디오 수집 모드 활성화 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | 수집한 비디오 데이터 전송 |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | 화면 공유 시작(Android) |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | 로컬 비디오 스트림 게시 일시 중지/재개 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | 원격 사용자 비디오 스트림 구독 일시 중지/재개 |
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6db053500be88a8735bfc69730447912) |  네트워크 속도 테스트 시작(방 입장 전 사용) |

### 오류 및 경고 이벤트
| API  | 설명         |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a511d0007e1990e63e853e46ce3f02670) | 오류 이벤트 콜백 |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9871472ee8195dfc5d0c34fae3294465) | 경고 이벤트 콜백 |

### 방 관련 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) | 방 입장 성공 여부 이벤트 콜백 |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) | 방 퇴장 이벤트 콜백 |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6a4b7f39bc5dfb0c5d75ef8802e2e758) | 역할 전환 이벤트 콜백 |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9778a84932f02de9be52ea7513f606c1) | 방 전환 결과 콜백 |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) | 크로스 룸 통화 요청 결과 콜백 |
| [onDisConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6f7db4f0aaadad2cdfa822ba0060414c) | 크로스 룸 통화 종료 결과 콜백 |

### 사용자 관련 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a891f38e4cdeaf3ff18937726f0269c2c) | 사용자 방 입장 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abfec3607f97823956fad77a7a63dc441) | 사용자 방 퇴장 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) | 원격 사용자가 메인 영상 화면을 게시/게시 취소함 |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) | 원격 사용자가 서브 영상 화면을 게시/게시 취소함 |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) | 원격 사용자가 오디오를 게시/게시 취소함 |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0c1ccf1bec2d3261e9f11894b32e357e) | SDK가 로컬 또는 원격 사용자의 첫 번째 화면 프레임을 렌더링하기 시작함 |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a3516aaef4cb63e512cd713e4ec96d118) | SDK가 원격 사용자의 첫 번째 화면 프레임을 재생하기 시작함 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a181788d7441d41022ce014095ee05353) | 첫 번째 로컬 비디오 프레임 게시 |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#acb73daf4ce82cd03f787f057b233b412) | 첫 번째 로컬 오디오 프레임 게시 |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aa75cd2a93cfb096357e2de226ff2ea47) | 원격 비디오 상태 변경 이벤트 콜백 |

### 네트워크 및 기술 메트릭에 대한 통계 콜백
| API  | 설명         |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b) | 네트워크 품질에 대한 실시간 통계 콜백 |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a24a6ee3b3709a42af226be7258521612) | 멀티미디어 기술 메트릭에 대한 실시간 통계 콜백 |
| [onSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0dc9967589d6d3277f0e429e520f2c51) | 네트워크 속도 테스트 결과 콜백 |

### 클라우드 연결 상태 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aed43a70b4a95eb95181e2b410013bf54) | SDK와 클라우드 연결이 끊김 |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | SDK와 클라우드 다시 연결 중 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | SDK와 클라우드가 다시 연결됨 |

### 하드웨어 관련 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aaa74021e5fd2564afb2df50e25eedeff) | 카메라 준비 완료 |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#afdac7dee94451913a4dc9982badc8035) | 마이크 준비 완료 |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1a608275247d2912e26bd83f648d6378) | 오디오 경로가 변경됨(모바일만 해당) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4e3b79968ccbb86de5b79e326a2daafa) | 볼륨 |

### 사용자 정의 메시지 수신 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a51fd654c5ec030ff84f208f2ba50298d) | 사용자 정의 메시지 수신 이벤트 콜백 |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a98af11ba5b25d3124bd9533dc5197127) | 사용자 정의 메시지 손실 이벤트 콜백 |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3640e6bf80a1f93991644701e9b0d96) | SEI 메시지 수신 콜백 |

### CDN 관련 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a03d0ef687b2973b9b13cb041bd35bb85) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 시작 이벤트 콜백 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3cb7e5ceb69954d762eafca5a0e3a62) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 중지 이벤트 콜백 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a64df36d6c56dd69d8b6f051fd9fffcbc) | Tencent Cloud CDN 외에 멀티미디어 스트림 게시 시작 이벤트 콜백 |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c3d63538897ddb9ed1b170819c41dca) | Tencent Cloud CDN 외에 멀티미디어 스트림 게시 중지 이벤트 콜백 |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af1c79a5ec3e0c106939e7f0d7849d694) | 클라우드 혼합 스트림 레이아웃 및 트랜스 코딩 매개변수 설정 이벤트 콜백 |

### 화면 공유 관련 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a7d15537d26fb001045ff95157d59ed3f) | 화면 공유 활성화 이벤트 콜백 |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a12c57991389e32f04a56774df5d1ce76) | 화면 공유 일시중지 이벤트 콜백 |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ade88963a254d297d3be1993e8a599f6e) | 화면 공유 재개 이벤트 콜백 |
| [onScreenCaptureStopped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c09b21b733da7d314d1db2cb03c8bcb) | 화면 공유 중지 이벤트 콜백 |

### 로컬 녹화 및 화면 캡처 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6d252931944577cc08d40db1f5ecd7bb) | 로컬 녹화 작업 시작 이벤트 콜백 |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22f09234dc198d33fa38bbb595fb5764) | 로컬 녹화 작업 진행 중 이벤트 콜백 |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0a3eef0daeb5107290cb5190ceb9467b) | 로컬 녹화 작업 종료 이벤트 콜백 |

### 사용하지 않는 이벤트 콜백
| API  | 설명         |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aff18b3bc5b1e448b21b7614e5716e73e) | 호스트가 현재 방에 입장함(폐기됨) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0d1361e52e96b4c7c1a5f1b89f4ef0fb) | 호스트가 현재 방에서 퇴장함(폐기됨) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abe967d855abae66836877fe0dacf8b5f) | 음향 효과 종료(폐기됨) |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ab77a0dff287e1642527cd414fc5fe5f5) | 서버 속도 테스트 결과 콜백(폐기됨) |

### 비디오 데이터 사용자 정의 콜백
| API  | 설명         |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a41b44f9b0583bbf56ad9e96065ea825c) | 사용자 정의 비디오 렌더링 콜백 |
| [onGLContextCreated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af4a7a3a4e4945bf216d87f81b6926dab) | SDK의 OpenGL 컨텍스트 생성 알림 |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22afb08b2a1a18563c7be28c904b166a) | 타사 뷰티 필터 컴포넌트에 의한 비디오 처리 콜백 |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a5f6d5ef01d3cd610959433107f78aa60) | SDK의 OpenGL 컨텍스트 폐기에 대한 알림 |

### 오디오 데이터 사용자 정의 콜백
| API  | 설명         |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) | 로컬에서 수집되고 오디오 모듈에서 전처리된 오디오 데이터 콜백 |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46) | 로컬에서 수집되고 오디오 모듈에서 전처리, 사운드 처리 및 BGM 믹싱된 오디오 데이터 콜백 |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902) | 각 원격 사용자의 오디오 믹싱 전 오디오 데이터 |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7) | 재생하기 위해 시스템에 제출되기 전 각 채널에서 믹싱된 오디오 데이터 콜백 |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a96923a9286a88b83d6890f607884ceb3) | SDK의 모든 믹싱된 오디오 데이터(수집 및 재생 대기 중 포함) |

### 기타 이벤트 콜백 인터페이스
| API  | 설명         |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a77d78090666e330606b670bf8ce2d854) | 로컬 LOG 출력 콜백 |

### 비디오 관련 열거 값 정의
| API  | 설명         |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp01d5e1111c2ba49a53879c343fd484f2) | 비디오 해상도 |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp509a1d5f7a44e1d60cf25e4afb640347) | 비디오 종횡비 모드 |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp8f7c7bceb683fdba0c3cb0a4766dd281) | 비디오 스트림 유형 |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFillMode) | 영상 화면 채우기 모드 |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp9edface2441370ef72f70dd4945ff0f9) | 영상 화면 회전 방향 |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa173483f8f2f9cbfd604328c0a8cba50) | 뷰티필터(피부 보정) 알고리즘 |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpde7f16ea7692e7c649e9a16638f48dbe) | 비디오 픽셀 형식 |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2c1424df181810edcbd68a9d2cb4adde) | 비디오 데이터 전송 방식 |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa367a3c86bde4916b80b03acd05ec218) | 비디오 미러 이미지 유형 |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSnapshotSourceType) | 로컬 영상 화면 캡처 데이터 소스 |

### 네트워크 관련 열거 값 정의
| API  | 설명         |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa53ec28e9d73b79c701a709f44efbebe) | 응용 시나리오 |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp32cd3ba884366b8a2d45cad705f28b18) | 역할 |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp39c937e1be1c70563f58a5a6fdde96a1) | QoS 제어 모드(폐기됨) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp3a953a9777c6e1447a27bc454f9f00b9) | 화질 선호도 |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp43d6beae8b3d7c79f02df2f125c090a7) | 네트워크 품질 |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5f5cc2365ee675bbc0f5a14095b1e0fc) | 비디오 상태 유형 |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp66f48a69ecc92051ca32055008a19c3e) | 비디오 상태 변동 원인 |

### 오디오 관련 열거 값 정의
| API  | 설명         |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2b7efdf7211746ab55166bb4d55ed619) | 오디오 샘플링 레이트 |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp96d66d1098694549803eaba6baedb9c0) | 오디오 품질 |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7340a7d82950a691c95bde594a44959f) | 오디오 경로(오디오 재생 모드) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp30e899d6cb29154e1d73867d199b7191) | 오디오 리버브 모드 |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpac19166c196a2905657f2a3b52a68ce0) | 음성 변조 유형 |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp70bfa071c4ebab5e7ed1811a780a53d9) | 시스템 볼륨 유형(모바일만 해당) |
| [TRTCAudioCapabilityType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp29e12a3869cc165605dc0121e56888a3) | 시스템에서 지원하는 오디오 기능 유형(Android 장치만 해당) |

### 기타 열거 값 정의
| API  | 설명         |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2f4911d8563ae1db783b963d626681d8) | Log 레벨 |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7821baad731a6db4d8977d304fafce63) | G-센서 스위치(모바일만 해당) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5e2e800d31dc99373db17e2def3afc99) | 클라우드 혼합 스트림 레이아웃 모드 |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpaa193560ab798cc5dcdb9624ce9740aa) | 미디어 녹화 유형 |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa7e631ba74d7c9f6832a6ad3be7a81af) | 혼합 스트림 입력 유형 |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp25c9df32061d8ad991f04b21fc6acacb) | 오디오 녹음 콘텐츠 유형 |

### TRTC 핵심 유형 정의
| API  | 설명         |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | 방 입장 매개변수 |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam) | 비디오 인코딩 매개변수 |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCNetworkQosParam) | 네트워크 트래픽 제어(Qos) 매개변수 세트 |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCRenderParams) | 영상 화면 렌더링 매개변수 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCQualityInfo) | 네트워크 품질 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVolumeInfo) | 볼륨 크기 |
| [TRTCSpeedTestParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestParams) | 속도 테스트 매개변수 |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestResult) | 네트워크 속도 테스트 결과 |
| [TRTCTexture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCTexture) | 비디오 텍스쳐 데이터(Android만 해당, 텍스처 ID 및 EGL 환경 포함) |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFrame) | 비디오 프레임 정보 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrame) | 오디오 프레임 데이터 |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ac5b1947f21f77726cbff822eaf0003f9) | 클라우드 혼합 스트림의 각 채널 화면에 대한 설명 정보 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a6066a5537ad8c1bc6158d43e8a4765db) | 클라우드 혼합 스트림의 레이아웃 및 트랜스 코딩 매개변수 |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCPublishCDNParam) | Tencent Cloud CDN 외에 멀티미디어 스트림을 게시할 때 설정해야 하는 푸시 매개변수 |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams) | 로컬 오디오 파일 녹음 매개변수 |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCLocalRecordingParams) | 로컬 미디어 파일 녹화 매개변수 |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ad82a59c2209c0596dabaee1152820494) | 음향 효과 매개변수(폐기됨) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a1b79e0e45a5f137df2e1995af7c0885c) | 방 전환 매개변수 |
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9b833660fc60bd0b4e0c0625d2ad84f6) | 오디오 사용자 정의 콜백 형식 매개변수 |
| [TRTCScreenShareParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCScreenShareParams) | 화면 공유 매개변수(Android 플랫폼만 적용) |

