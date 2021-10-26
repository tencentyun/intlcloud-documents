## TRTCCloud @ TXLiteAVSDK

### 인스턴스 생성 및 이벤트 콜백
| API | 설명 |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) | TRTCCloud 인스턴스 생성(싱글톤 모드) |
| [destroySharedIntance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad8961d03736d8a52df5a3a991d0a77c4) | TRTCCloud 인스턴스 폐기(싱글톤 모드)  |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6a8e20d57b7890e4dbf6652c426d7015) | TRTC 이벤트 콜백 설정 |
| [delegateQueue](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a97158c52f2a4011454b4eb3ee369a8a1) | TRTCCloudDelegate 이벤트 콜백을 구동하는 큐 설정 |

### 방 관련 인터페이스 함수
| API | 설명 |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) | 방 입장 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) | 방 퇴장 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) | 역할 전환 |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7c5a2aa06d649492f546d9c70a5de4a1) | 방 전환 |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) | 크로스 룸 통화 요청 |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abd656e4c9b6a01231810ae897627e9bc) | 크로스 룸 통화 종료 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) | 구독 모드 설정(방에 입장하기 전에 설정해야 적용됨) |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6100a5f395442d38ce9adab922382caf) | 방 서브 인스턴스 생성(멀티 룸 동시 시청용) |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a19e0d7921ac494fb588a4654d97abe86) | 방 서브 인스턴스 폐기 |

### CDN 관련 인터페이스 함수
| API | 설명 |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6d2f4d81f0944072053d7dc9e9265f22) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 시작 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc00ba747be5299cd7235928a628339e) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 중지 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aad42e78d355fd563b959a5053bac54cb) | Tencent Cloud CDN외에 멀티미디어 스트림 게시 시작 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | Tencent Cloud CDN외에 멀티미디어 스트림 게시 중지 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) | On-Cloud MixTranscoding의 레이아웃 및 트랜스 코딩 매개변수 설정 |

### 비디오 관련 인터페이스 함수
| API | 설명 |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | 로컬 카메라의 미리보기 이미지 활성화(모바일) |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | 로컬 카메라의 미리보기 이미지 활성화(데스크톱) |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) | 로컬 카메라의 미리보기 이미지 업데이트 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | 카메라 미리보기 중지 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | 로컬 비디오 스트림 게시 일시 중지/재개 |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2) | 로컬 비디오 일시 중지 이미지 교체 설정 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | 원격 사용자의 비디오 스트림 구독 및 비디오 렌더링 컨트롤러 바인딩 |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a518d3a8a3b4a4cfd8b5e0dfe7899756b) | 원격 사용자의 비디오 렌더링 컨트롤러 업데이트 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | 원격 사용자의 비디오 스트림 구독 중지 및 렌더링 컨트롤러 해제 |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) | 모든 원격 사용자의 비디오 스트림 구독 중지 및 모든 렌더링 리소스를 해제 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | 원격 사용자의 비디오 스트림 구독 일시 중지/재개 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adf7cd002366760749c6f4d1ee9291db1) | 모든 원격 사용자의 비디오 스트림 구독 일시 중지/재개 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) | 비디오 인코더의 인코딩 매개변수 설정 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9) | 네트워크 품질 관리 매개변수 설정 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5d4f0aba952a355f153d374899e6dcec) | 로컬 비디오 이미지의 렌더링 매개변수 설정 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7147d9c93af6a92f594ea394fc796081) | 원격 비디오 이미지의 렌더링 모드 설정 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) | 비디오 인코더에 의한 이미지 출력 방향 설정 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a29a7cae6b4e82098fc342d4f0066d2ad) | 인코더에서 출력되는 이미지의 미러 모드 설정 |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7a8c22e2f02d313590d4c499e18ebe3f) | G-센서 적용 모드 설정 |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2aa9c464203b1c62cbb9ccabccc6334a) | 크고 작은 이미지의 이중 채널 인코딩 모드 활성화 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a49440df0907b12c0ad8fe9e93bdbed0d) | 지정된 원격 사용자의 크고 작은 이미지 전환 |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | 비디오 화면 캡처 |

### 오디오 관련 인터페이스 함수
| API | 설명 |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | 로컬 오디오 수집 및 게시 활성화 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab78601c38f1b872b03b662e6856be84c) | 로컬 오디오 수집 및 게시 중지 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9) | 로컬 오디오 스트림 게시 일시 중지/재개 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) | 원격 오디오 스트림 재생 일시 중지/재개 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) | 모든 원격 사용자의 오디오 스트림 재생 일시 중지/재개 |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa62f2af2d86a64c0ebc7b9f00e4a54fe) | 오디오 경로 설정 |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d38580f2c35f7e9828c4e41c56db35a) | 원격 사용자의 오디오 재생 볼륨 설정 |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5475b81c1712323257c10baaf7ad6969) | 로컬 오디오의 수집 볼륨 설정 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7ce26486575e72bc445432929fdff26c) | 로컬 오디오의 수집 볼륨 가져오기 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af2602b1e9dfe932c89dd411f2f227192) | 원격 오디오의 재생 볼륨 설정 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aba445625df38b8676d599df4a67a8407) | 원격 오디오의 재생 볼륨 가져오기 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57d48cb0dbd7705486453b46e30e3fea) | 볼륨 알림 활성화 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9eadd65cef0ac6b9c04ddfd7265afb01) | 오디오 녹음 시작 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac8c12476bbcf3d691060954fcdb6ebe6) | 오디오 녹음 중지 |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b) | 로컬 미디어 녹화 시작 |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#affae72630393980fee79c21f2d20f602) | 로컬 미디어 녹화 중지 |

### 디바이스 관리 관련 인터페이스
| API | 설명 |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a950f3f1c949def9e1e470f467db7b27a) | 디바이스 관리 클래스 가져오기(TXDeviceManager) |

### 뷰티 필터 특수 효과 및 이미지 워터마크
| API | 설명 |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) | 뷰티 필터 관리 클래스 가져오기(TXBeautyManager) |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad0bedbddf415d26cff8242d5842a0908) | 워터 마크 추가 |

### 배경 음악 및 음향 효과
| API | 설명 |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) | 음향 효과 관리 클래스 가져오기(TXAudioEffectManager) |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) | 시스템 오디오 수집 활성화(Mac 시스템만 해당) |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adef486f26a2c7d74a8cccb537367e66a) | 시스템 오디오 수집 중지(데스크톱 시스템만 해당) |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae) | 시스템 오디오 수집 볼륨 설정 |

### 화면 공유 관련 인터페이스
| API | 설명 |
|-----|-----|
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) | 인앱 화면 공유 시작(iOS 13.0 이상만 지원) |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) | 시스템 수준 화면 공유 시작(iOS 11.0 이상만 지원) |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | 데스크탑 화면 공유 시작(데스크탑 시스템만 해당) |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) | 화면 공유 중지 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | 화면 공유 일시 중지 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | 화면 공유 재개 |
| [getScreenCaptureSourcesWithThumbnailSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a37df498cbc8d9b1135e3caafdcee906f) | 공유 가능한 화면 및 창 열거(macOS만 지원) |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) | 공유할 화면 또는 창 선택(macOS만 지원) |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) | 화면 공유(예: 서브스트림)의 비디오 인코딩 매개변수 설정(데스크톱 시스템만 지원) |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a18d3fb6535c9884784c5ad5f8dfd0b12) | 화면 공유의 오디오 믹싱 볼륨 설정(데스크톱 시스템만 지원) |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa567171999b17a7f5655213b193415a7) | 화면 공유 제외 목록에 지정된 창 추가(데스크톱 시스템만 지원) |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a95b1f3fbc6ff755f67f7e9b86240ea5f) | 화면 공유 제외 목록에 지정된 창 제거(데스크톱 시스템만 지원) |
| [removeAllExcludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab2b6a778a528d58e2a42c9adfc7684f2) | 화면 공유 제외 목록에서 모든 창 제거(데스크톱 시스템만 지원) |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233) | 화면 공유 포함 목록에 지정된 창 추가(데스크톱 시스템만 지원) |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a058ac1e2141d6eb1962219167add42bc) | 화면 공유 포함 목록에서 지정된 창 제거(데스크톱 시스템만 지원) |
| [removeAllIncludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a18a20767a0e1076ba16cd473a2512156) | 화면 공유 포함 목록에서 모든 창 제거(데스크톱 시스템만 지원) |

### 사용자 정의 수집 및 렌더링
| API | 설명 |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | 사용자 정의 비디오 수집 모드 활성화/비활성화 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | 수집한 비디오 프레임을 SDK에 전달 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) | 사용자 정의 오디오 수집 모드 활성화 |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a62cab4ec7c336ae135c2f681aca25da1) | 수집한 오디오 데이터를 SDK에 전달 |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1101d883d65882f735e3d17f874a25cb) | 사용자 정의 오디오 트랙 활성화/비활성화 |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9f408915460e86e889056066ca4e0908) | 사용자 정의 오디오 트랙을 SDK에 믹싱 |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abd8823c40d31e122ed34f7ac33c678a6) | 푸시 스트림 시 믹싱된 외부 오디오 푸시 스트림 볼륨 및 재생 볼륨 설정 |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) | 사용자 정의 수집 시 타임스탬프 생성 |
| [setLocalVideoProcessDelegete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2f73c33b1010a63bd3a06e639b3cf348) | 서드 파티 뷰티 필터에 대한 비디오 데이터 콜백 설정 |
| [setLocalVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aba3d309645d27304b6d4ea31b21a4cda) | 로컬 비디오에 대한 사용자 정의 렌더링 콜백 설정 |
| [setRemoteVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5244e73ac27599370f966575e11959ff) | 원격 비디오에 대한 사용자 정의 렌더링 콜백 설정 |
| [setAudioFrameDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01726b03b102c32222a2a26b16abcd48) | 사용자 정의 오디오 데이터 콜백 설정 |
| [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) | 로컬 마이크에서 수집한 원본 오디오 프레임의 콜백 형식 설정 |
| [setLocalProcessedAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9ec7c7123eb2f333769508de193ea51f) | 전처리된 로컬 오디오 프레임의 콜백 형식 설정 |
| [setMixedPlayAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a24ad642b88cd3b2ca2d3044d72817090) | 시스템에서 재생할 오디오 프레임의 콜백 형식 설정 |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a325da4ec57db06b91b74da8699b47d7c) | 사용자 정의 오디오 재생 활성화 |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aeebe3811918c8250d32d872fee83a2c2) | 재생 가능한 오디오 데이터 가져오기 |

### 사용자 정의 메시지 전송 인터페이스
| API | 설명 |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acbc86da0cb558c549f42e7e987c7beaf) | UDP 채널을 사용하여 방의 모든 사용자에게 사용자 정의 메시지 보내기  |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6de26e5efddf899d31158e4d48f17c02) | SEI 채널을 사용하여 방의 모든 사용자에게 사용자 정의 메시지 보내기  |

### 네트워크 테스트 인터페이스
| API | 설명 |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a058556b224315dcde3601ab621a09dee) | 네트워크 속도 테스트 시작(입장 전 사용) |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a58d732ba648d1f9a3a460c02de79bb9b) | 네트워크 속도 테스트 중지 |

### 디버깅 관련 인터페이스
| API | 설명 |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ace5acd2fe597b6656b45aaa93e3e45a1) | SDK 버전 정보 가져오기 |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9d2b6a99e137a9667743edc8ac909493) | 로그 출력 수준 설정 |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a177c4f1fbb2a011ff496417dc0245667) | 콘솔 로그 인쇄 활성화/비활성화 |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa51a341a43a854ac6e3fa1d0093fec95) | 로컬 로그 압축 활성화/비활성화 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a93b48089741f7022aea1f8f93ce8fff9) | 로컬 로그 저장 경로 설정 |
| [setLogDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a41497e4242e3c42acfa35730cdc1ddf6) | 로그 콜백 설정 |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3bd71c8a99029c1a4708bf1c176aa299) | 대시보드 표시 |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aad41ff6d5b5565046911acf27bb3dee4) | 대시보드 여백 설정 |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | 실험용 API 호출 |

### 폐기 인터페이스
| API | 설명 |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abb57991f5e4f4ca1b95c2181a7e538c8) | 마이크 볼륨 설정 |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1336146862fb742de6cbe5718f9b7008) | 뷰티 필터, 미백 효과, 안색 보정 효과 단계 설정 |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae0e4341ef565cc5ba28101574179cd56) | 눈 확대 필터의 강도 설정 |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | 갸름한 얼굴 필터의 강도 설정 |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | V라인 필터의 강도 설정 |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a145d4ed3d5790a449a9884d282420216) | 턱 늘이기/줄이기 필터의 강도 설정 |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | 얼굴 축소 필터의 강도 설정 |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae94b107a9c476337585906c79b42ee95) | 코 축소 필터의 강도 설정 |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3aa8c561d744e3d921dff6186a6e4ade) | 애니메이션 스티커 설정 |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | 애니메이션 스티커 음소거 |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | 화면 공유 시작 |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) | 컬러 필터 설정 |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3b0d7db70674f961c14b316f4e8e7a2b) | 컬러 필터의 강도 설정 |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | 그린 스크린 비디오 설정 |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4d9983591fa2a847e226b7a30e8db294) | 배경 음악 재생 활성화 |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a11004f1ba27b057985850a25307b0bec) | 배경 음악 재생 비활성화 |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa4b92d4c989e99612f6c4dab03a78764) | 배경 음악 재생 중지 |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aed6e8f224b5f834b1bc0c15f9701f692) | 배경 음악 재생 중지 |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac1f96932d02198cd045ee96f1306c8ba) | 배경 음악의 총 길이(단위:ms) 가져오기 |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7fd043ae358c43f6a178837fb2846ef9) | 배경 음악 재생 진행율 설정 |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adbfc8e226df7c6caaaca1a89a9842f23) | 배경 음악 볼륨 설정 |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a08c468f48d99aef0e89716111db1f422) | 배경 음악 로컬 재생 볼륨 설정 |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a0cf0c090285038b23843c646009073d1) | 배경 음악 원격 재생 볼륨 설정 |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a555cde4eda63d13bbad0dbdba7094a47) | 리버브 효과 설정 |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa60f54923826cc59d8a4526669c4ea5e) | 음성 변조 유형 설정 |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2ae175694198a9b3d1b1647b7ce1dae0) | 음향 효과 재생 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | 효과음 볼륨 설정 |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | 효과음 중지 |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7066509af1de32c290b7cc297cd00f2b) | 모든 음향 효과 중지 |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6b345c95b5b68198d8dbc64a3652ed35) | 모든 음향 효과의 볼륨 설정 |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab0d46ccb8fca811851b30e7731958024) | 사운드 효과 일시 중지 |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a207dd8909c05d4a8a1431d33e644d4fe) | 사운드 효과 일시 중지 |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa26564f3388bc249ecbd2813d9c45390) | 인이어 모니터링 활성화(또는 비활성화) |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | 원격 영상 화면 표시 시작 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | 원격 영상 화면 표시 중지 및 원격 사용자의 비디오 데이터 스트림 가져오기 중지 |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) | 원격 이미지의 렌더링 모드 설정 |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90) | 원격 이미지의 시계 방향 회전 각도 설정 |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) | 로컬 이미지의 렌더링 모드 설정 |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4d2d95ad8fbaf8edce18667aa835848e) | 로컬 이미지의 시계 방향 회전 각도 설정 |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af68f13fba5a02e4e9ca338596fb64916) | 로컬 카메라의 미리보기 이미지의 미러 모드 설정 |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) | 원격 사용자의 서브스트림 이미지 표시 시작 |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acab6e31898857af876af66e779216203) | 원격 사용자의 서브스트림 이미지 표시 중지 |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a487b3cd9a6b41581d4b45c752c5ede4c) | 서브스트림 이미지의 채우기 모드 설정 |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a72c66b67eacd24a0e796a3213219fb6d) | 서브스트림 이미지의 시계 방향 회전 각도 설정 |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b2d43a3955480f2d6200bf20e66f3cf) | 큰 화면/작은 화면 시청 우선순위 설정 |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53) | 음질 설정 |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | 음질 설정 |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa9a1952f442020bc92ce1beb65959e56) | 카메라 전환 |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8662b8ecab04a55a321ee9f16d0680a7) | 현재 카메라의 줌 지원 여부 쿼리 |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | 카메라 줌 비율 설정(초점 거리) |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acd005524f8e2c2fbfcc415049e666ced) | 플래시 지원 여부 쿼리 |
| [enbaleTorch](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af6b128ee01d91a63dc1976db7a9be555) | 플래시 켜기/끄기 |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a0e164f727b990581a42f97dca1bf7548) | 카메라 초점 설정 지원 여부 쿼리 |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6a77cc99c41b926cd99909ae1ace39ae) | 카메라의 초점 위치 설정 |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5af361145f04227ff1a451fee2705a77) | 얼굴 위치 자동 인식 지원 여부 쿼리 |
| [enableAutoFaceFoucs](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a32a8f584879b17f211df75494a5be96c) | 얼굴 자동 초점 켜기/끄기 |
| [startCameraDeviceTestInView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1bd6289b969adde0096c83d6a5532332) | 카메라 테스트 시작 |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b67fa3f322efe538d924b381c06e676) | 카메라 테스트 시작 |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa6f467c12fcea7e09cc97861d511498a) | 마이크 테스트 시작 |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8cca1c5913ac021987680195075e5fc9) | 마이크 테스트 시작 |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a60aa520016687bea03f17cb4ec19c1b6) | 스피커 테스트 시작 |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf383f971dc54f0254b2d40f100cc9ca) | 스피커 테스트 정지 |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5e267aa0d820f78b761be1d485369b3b) | 마이크 목록 가져오기 |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afa6a82cbf407b0bd6eb63093940e189d) | 현재 마이크 장치 가져오기 |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) | 현재 사용 중인 마이크 선택 |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af69d237159163eebcb6876e767d7692e) | 현재 마이크 볼륨 가져오기 |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa6810f64c153e779697dc2d5bd30f6a) | 현재 마이크 볼륨 가져오기 |
| [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae9c936081b96348ce047337a1d3bb7b0) | 현재 시스템 마이크의 음소거 상태 가져오기 |
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) | 현재 시스템 마이크의 음소거 상태 설정 |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5b888d0ebe697fdc5e11759f1b154fc3) | 스피커 장치 목록 가져오기 |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9d6d48c3937e3cb2632ced9a6a002368) | 현재 사용 중인 스피커 가져오기 |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6c951071ac218930680febd84314ee05) | 사용할 스피커 설정 |
| [getCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa25ac85f6f84b352175aebb9c7007247) | 현재 스피커 볼륨 가져오기 |
| [setCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a019001b23569c8b6da7f3276af58e0a7) | 현재 스피커 볼륨 설정 |
| [getCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a793d11364882c7fac7f9200f8761400c) | 현재 시스템 스피커 음소거 여부 가져오기 |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a738ea0dffd48d5bc2b05b146eb79ec46) | 현재 시스템 스피커 음소거 여부 설정 |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a0a1b764ff4238afaeaba41ee728a1451) | 카메라 목록 가져오기 |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa238683cb00f508b05b9ac031a17bc37) | 현재 사용 중인 카메라 가져오기 |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) | 현재 사용할 카메라 선정 |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab098daa610ae506dbf6c2a4f666ae32c) | 시스템 볼륨 유형 설정 |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | 비디오 화면 캡처 |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | 사용자 정의 비디오 수집 모드 활성화 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | 사용자가 수집한 비디오 데이터 전송 |
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) | 인앱 화면 공유 시작(iOS) |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) | 전체 시스템 화면 공유 시작(iOS) |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | 로컬 비디오 스트림 게시 일시 중지/재개 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | 원격 사용자의 비디오 스트림 구독 일시 중지 / 재개 |

### 오류 및 경고 이벤트
| API | 설명 |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a10a711eb68abcacc1ca690501fc7c9fb) | 오류 이벤트 콜백 |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a25ac0da9ad798a2313bdf8f296828541) | 경고 이벤트 콜백 |

### 방 관련 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) | 방 입장 성공 여부 이벤트 콜백 |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) | 방 퇴장 이벤트 콜백 |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ade2c2eab48a30e7ca1c9246e573b7f28) | 역할 전환 이벤트 콜백 |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ad848cbee89f8b6258c9f03f4cb253a31) | 방 전환 결과 콜백 |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) | 크로스 룸 통화 요청 결과 콜백 |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a26b34d83afac68928a156096862c9c06) | 크로스 룸 통화 종료 결과 콜백 |

### 사용자 관련 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) | 사용자가 현재 방에 입장함 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) | 사용자가 현재 방에서 퇴장함 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) | 원격 사용자가 메인 비디오 화면 게시/게시 취소함|
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) | 원격 사용자가 서브 비디오 화면 게시/게시 취소함|
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) | 원격 사용자가 오디오 게시/게시 취소함|
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7fc7fd0144af2bc4ce0797f9de530d96) | SDK가 로컬 또는 원격 사용자의 첫 번째 화면 프레임 렌더링을 시작함 |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aafc4536f552199368e48c8527783c410) | SDK가 원격 사용자의 첫 번째 오디오 프레임 재생을 시작함 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a17567554f413629a80b5970bdffdff7b) | 첫번째 로컬 비디오 프레임이 이미 게시됨 |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#acb73daf4ce82cd03f787f057b233b412) | 첫번째 로컬 오디오 프레임이 이미 게시됨 |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af7fef48407b65423871ed6f7652e4176) | 원격 비디오 상태 변경 이벤트 콜백 |

### 네트워크 및 기술 메트릭에 대한 통계 콜백
| API | 설명 |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28) | 네트워크 품질에 대한 실시간 통계 콜백 |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afb0811035e97c8544dbc9ecbef461dd9) | 멀티미디어 기술 메트릭 대한 실시간 통계 콜백 |

### 클라우드 연결 상태 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aed43a70b4a95eb95181e2b410013bf54) | SDK와 클라우드 연결이 끊김 |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | SDK와 클라우드 다시 연결 중 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | SDK와 클라우드가 다시 연결됨 |

### 하드웨어 관련 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aaa74021e5fd2564afb2df50e25eedeff) | 카메라 준비 완료 |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afdac7dee94451913a4dc9982badc8035) | 마이크 준비 완료 |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a1859305732dfd03de63c9b780f99d513) | 현재 오디오 경로가 변경됨(모바일만 해당) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7775c3fbd84b8da3b7a75bdea27ed5c5) | 볼륨 크기에 대한 피드백 콜백 |
| [onDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a0152908c497bd5ee5225251d9e93e500) | 로컬의 상태가 변경됨(데스크톱 시스템만 해당) |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a1c36efd81dc4edf88fc3bc6af83b1b5a) | 현재 마이크 시스템의 수집 볼륨이 변경됨 |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f) | 현재 시스템의 재생 볼륨이 변경됨 |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676) | 시스템 오디오 수집 활성화 성공 여부 이벤트 콜백(Mac 시스템만 해당) |

### 사용자 정의 메시지 수신 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a324311b3d4f3930d9a50b8449b155dd3) | 사용자 정의 메시지 수신 이벤트 콜백 |
| [onMissCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af1b8e7d0f73773eca509afc1cf4c9ece) | 사용자 정의 메시지 손실 이벤트 콜백 |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6e4365456cb4df6e1bdf870511b72042) | SEI 메시지 수신 콜백 |

### CDN 관련 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a75c6bf4a7c7ec60a24aabfe8e47ea1f4) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 시작 이벤트 콜백 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a379dcf84e15f93b64efe2cb9f362877c) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 중지 이벤트 콜백 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a817783f364bf9f6f0a1df4bc26bad628) | Tencent Cloud CSS CDN외에 멀티미디어 스트림 게시 시작 이벤트 콜백 |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aab032eb48a56e8351ada60ce5b510d5e) | Tencent Cloud CSS CDN외에 멀티미디어 스트림 게시 중지 이벤트 콜백 |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ab5c98341b7536b5b65c04b835c4d28fb) | 클라우드 혼합 스트리밍의 레이아웃 및 트랜스 코딩 매개변수 설정 이벤트 콜백 |

### 화면 공유 관련 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7d15537d26fb001045ff95157d59ed3f) | 화면 공유 활성화 이벤트 콜백 |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a9cc6106085b2049838e21bb50e192786) | 화면 공유 일시 중지 이벤트 콜백 |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ae9c08ef9dd260cf6fd946209fda8a011) | 화면 공유 재개 이벤트 콜백 |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a323d2b3e5b8b364722e0b161ab11c816) | 화면 공유 중지 이벤트 콜백 |

### 로컬 녹화 및 로컬 화면 캡쳐 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a044ce179ac4bc0bc987a3b74ecd911e7) | 시작된 로컬 녹화 작업 이벤트 콜백 |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ab4250c05ea4b843c27385f77d5004fc3) | 진행중인 로컬 녹화 작업 진행 상황 이벤트 콜백 |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ae78ca25acea4152bfd9d0ccf71bd4108) | 종료된 로컬 녹화 작업 이벤트 콜백 |

### 폐기된 이벤트 콜백
| API | 설명 |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af26948706dc0dff24946470066e9c4e0) | 호스트가 현재 방에 입장(폐기됨) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a72f0a872a13500cb5394f77c586ab3f5) | 호스트가 현재 방에서 퇴장(폐기됨) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#accb36b0eb1d1b72f32cf72617bb1c730) | 음향 효과 종료(폐기됨) |

### 비디오 데이터 사용자 정의 콜백
| API | 설명 |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7b43888945a9d12f088ed99a5854e3c1) | 사용자 정의 비디오 렌더링 콜백 |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8d4f000b4169a64a8a8af15e51e5dd95) | 3rd party 뷰티 필터에 의한 비디오 처리 콜백 |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5f6d5ef01d3cd610959433107f78aa60) | SDK의 OpenGL 컨텍스트 폐기에 대한 알림 |

### 오디오 데이터 사용자 정의 콜백
| API | 설명 |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) | 로컬 마이크에서 수집된 원본 오디오 데이터 콜백 |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0) | 로컬에서 수집하고 오디오 모듈에서 전처리된 오디오 데이터 콜백 |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a) | 각 원격 사용자의 오디오 믹싱 전 오디오 데이터 |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e) | 재생하기 위해 시스템에 제출되기 전에 각 채널에서 믹싱된 오디오 데이터 콜백 |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a905748efe966e94ec1212fda14161aee) | SDK에서 수집 완료 및 재생될 모든 믹싱 오디오 데이터 |

### 기타 이벤트 콜백 인터페이스
| API | 설명 |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ab1364c78a6f31a8c08d0138c4f6e9647) | 로컬 LOG 출력 콜백 |

### 비디오 관련 열거 값의 정의
| API | 설명 |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5) | 비디오 해상도 |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gafdfe57c064658b38b78b0fd11e2706c0) | 비디오 종횡비 모드 |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga1974ff7e5e78b4455925faf74e38f1e8) | 비디오 스트림 유형 |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga1a66aad6fff71205c7a266268e16f55c) | 비디오 화면 채우기 모드 |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gae8bd6b06a2ca5f89f9b3cea393fc6eb9) | 비디오 화면 회전 방향 |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga9bafd3233be6cec1b380d469017ed3e6) | 뷰티 필터(피부 보정) 알고리즘 |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gabb58c142deac29da242c957f21c963e3) | 비디오 픽셀 형식 |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga0fce6f58df3d3021696d15eff683ed8b) | 비디오 데이터 전송 방식 |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga13da9775774c3251999f1e46d279305f) | 비디오 미러 이미지 유형 |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga50f989651c9f893de7716ffbc2d2a5fc) | 로컬 비디오 화면 캡처 데이터 소스 |

### 네트워크 관련 열거 값의 정의
| API | 설명 |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga6ab617b26cf503a8c1bfec34a9918dbe) | 응용 시나리오 |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gad147b9b0249d0c2759cf1514c8978881) | 역할 |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga915f86fec1b00787147d40a189444823) | 트래픽 제어 모드(폐기됨) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga2c460e7365ad67ee0213545b0a67aa6d) | 화질 선호도 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | 네트워크 품질 |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga0a200753a7e0c539ce4f584cd8d17510) | 비디오 상태 유형 |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga349e42c3f8a2de5a031e90a1240d7f54) | 비디오 상태 변경 원인 유형 |

### 오디오 관련 열거 값의 정의
| API | 설명 |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga346b09a7691ce8c9813bac0feb057d08) | 오디오 샘플링 레이트 |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) | 오디오 품질 |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga81305fea3aae73346d04f0013e0194d4) | 오디오 경로(오디오 재생 모드) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) | 오디오 리버브 모드 |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) | 음성 변조 유형 |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaac0cd0da9dd789dcec4ba16471006f23) | 시스템 볼륨 유형(모바일만 해당) |

### 기타 열거 값의 정의
| API | 설명 |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gacefec5143acae6d0524b5500f0155908) | Log 레벨 |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga894251078222f9ac4ba5815aac4b493c) | G-센서 스위치(모바일만 해당) |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaeabd30a270055e48105a34c781c782b0) | 화면 공유 타깃 유형(데스크톱만 해당) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga907c7b1ef1f09fb7417a549e82110855) | 클라우드 혼합 스트리밍 레이아웃 모드 |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga4bb9927d377aa27b781fcfef5cf1058a) | 미디어 녹화 유형 |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga9359cd77f4759e5b1a82fe1b94de638d) | 혼합 스트림 입력 유형 |
| [TRTCMediaDeviceType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga4a04a7c25ed48ab15603e8c3db115b95) | 디바이스 유형(데스크톱 플랫폼만 해당) |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gade0f3fa25d9d1c876660e230152567b0) | 오디오 녹음 콘텐츠 유형 |

### TRTC 핵심 유형 정의
| API | 설명 |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) | 방 입장 매개변수 |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) | 비디오 인코딩 매개변수 |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCNetworkQosParam) | 네트워크 트래픽 제어(Qos) 매개변수 세트 |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCRenderParams) | 비디오 화면 렌더링 매개변수 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | 네트워크 품질 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCVolumeInfo) | 볼륨 크기 |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult) | 네트워크 속도 테스트 결과 |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCVideoFrame) | 비디오 프레임 정보 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrame) | 오디오 프레임 데이터 |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCMixUser) | 클라우드 혼합 스트리밍 각 채널 화면에 대한 설명 정보 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCTranscodingConfig) | 클라우드 혼합 스트리밍의 레이아웃 및 트랜스 코딩 매개변수 |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCPublishCDNParam) | Tencent Cloud CDN외에 멀티미디어 스트림을 게시할 때 설정해야 하는 푸시 매개변수 |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams) | 로컬 오디오 파일 녹음 매개변수 |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCLocalRecordingParams) | 로컬 미디어 파일 녹화 매개변수 |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioEffectParam) | 음향 효과 매개변수(폐기됨) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSwitchRoomConfig) | 방 전환 매개변수 |


