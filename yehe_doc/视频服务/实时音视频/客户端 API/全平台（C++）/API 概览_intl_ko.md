## C++ 전체 플랫폼 인터페이스 소개
8.0 버전부터 기존 Windows(C++) 인터페이스를 기반으로 Windows, iOS, Mac, Android 플랫폼에 적용되는 새로운 C++ 인터페이스를 제공합니다.
C++ 인터페이스 통합 방법에 대한 자세한 내용은 각 플랫폼의 통합 가이드를 참고하십시오.  
- [iOS C++ 인터페이스 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35092)  
- [Android C++ 인터페이스 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35093)  
- [Mac C++ 인터페이스 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35094)  
- [Windows 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35095)  

>?
>- 현재 C++ 인터페이스는 라이트 버전(TRTC)에서만 제공됩니다.  
>- TRTC 헤더 파일은 Windows 플랫폼에서 'trtc' 네임스페이스를 자동으로 사용하고 있으므로 다시 지정할 필요가 없습니다.

## ITRTCCloud @ TXLiteAVSDK

### 인스턴스 생성 및 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [getTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ga0ef57994050abf58a18a3defd4cc5fd0) | TRTCCloud 인스턴스 생성(싱글톤 모드) |
| [destroyTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#gaadc9070c962327451dbc949a4c5a4681) | TRTCCloud 인스턴스 폐기(싱글톤 모드)  |
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) |  TRTC 이벤트 콜백 설정 |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | TRTC 이벤트 콜백 제거 |

### 방 관련 인터페이스 함수
| API                 | 설명       |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) | 방 입장 |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | 방 퇴장 |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | 역할 전환 |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | 방 전환 |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab5a0622e5d3d521d79ba4f85c44244eb) | 크로스 룸 통화 요청 |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | 크로스 룸 통화 종료 |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | 구독 모드 설정(방에 입장하기 전에 설정해야 적용됨) |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | 방 서브 인스턴스 생성(멀티 룸 동시 시청용) |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a980cf4d173abfb58c00ef35a20e12c85) | 방 서브 인스턴스 폐기 |

### CDN 관련 인터페이스 함수
| API                 | 설명       |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 시작 |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 중지 |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | Tencent Cloud CDN외에 멀티미디어 스트림 게시 시작 |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Tencent Cloud CDN외에 멀티미디어 스트림 게시 중지 |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | 클라우드 혼합 스트림 레이아웃 및 트랜스 코딩 매개변수 설정  |

### 비디오 관련 인터페이스 함수
| API                 | 설명       |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8ac23e725c7ed75488df1be2ee514884) | 로컬 카메라 미리보기 이미지 활성화(모바일) |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aef6d61f571304066aaf839f7db00a17b) | 로컬 카메라의 미리보기 이미지 활성화(데스크톱) |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0af978a75d5ba671b7ce5f0b81b003c8) | 로컬 카메라의 미리보기 이미지 업데이트 |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | 카메라 미리보기 중지 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) | 로컬 비디오 스트림 배포 일시 중지/재개 |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9) | 원격 사용자의 비디오 스트림 구독 및 비디오 렌더링 컨트롤러 바인딩 |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a027a8b23a363dc91e6ce1c9773ee8664) | 원격 사용자의 비디오 렌더링 컨트롤러 업데이트 |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abd186570272cd61b4a6e4aea870437e1) | 원격 사용자의 비디오 스트림 구독 중지 및 렌더링 컨트롤러 해제 |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | 모든 원격 사용자의 비디오 스트림 구독 중지 및 모든 렌더링 리소스 해제 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) | 원격 사용자의 비디오 스트림 구독 일시 중지/재개 |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | 모든 원격 사용자의 비디오 스트림 구독 일시 중지/재개 |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55b0710284e44ba3703e22b07c3665c8) | 비디오 인코더의 인코딩 매개변수 설정 |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad21668c7550aad44f1ed61265ffceb24) | 네트워크 품질 관리 관련 매개변수 설정 |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | 로컬 비디오 이미지의 렌더링 매개변수 설정 |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | 원격 비디오 이미지의 렌더링 모드 설정 |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | 비디오 인코더에 의한 이미지 출력 방향 설정 |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | 인코더에서 출력되는 이미지의 미러 모드 설정 |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5019a8005cd96662ce2cface662a811e) | 크고 작은 이미지 듀얼 채널 인코딩 모드 활성화 |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad2c6cc256f6e24178cd7c9cd2290ea4d) | 지정된 원격 사용자의 크고 작은 이미지 전환 |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | 영상 화면 캡처 |

### 오디오 관련 인터페이스 함수
| API                 | 설명       |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a86c80ed357798e50ccf5c7ae47317f4c) | 로컬 오디오 수집 및 게시 활성화 |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | 로컬 오디오 수집 및 게시 중지 |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | 로컬 오디오 스트림 게시 일시 중지/재개 |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | 원격 오디오 스트림 재생 일시 중지/재개 |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | 모든 원격 사용자의 오디오 스트림 재생 일시 중지/재개 |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | 원격 사용자의 오디오 재생 볼륨 설정 |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | 로컬 오디오 수집 볼륨 설정 |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | 로컬 오디오 수집 볼륨 가져오기 |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | 원격 오디오 재생 볼륨 설정 |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | 원격 오디오 재생 볼륨 가져오기 |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | 볼륨 알림 활성화 |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5224523e00d5167eb75cee9b65f72677) | 녹음 시작 |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | 오디오 녹음 중지 |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | 로컬 미디어 녹화 시작 |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | 로컬 미디어 녹화 중지 |

### 디바이스 관리 관련 인터페이스
| API                 | 설명       |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | 디바이스 관리 클래스 가져오기(TXDeviceManager) |

### 뷰티 필터 특수 효과 및 이미지 워터마크
| API                 | 설명       |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | 뷰티 필터, 미백 효과, 안색 보정 등 특수 효과 설정 |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | 워터마크 추가 |

### 배경 음악 및 음향 효과
| API                 | 설명       |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | 음향 효과 관리 클래스 가져오기(TXAudioEffectManager) |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) | 시스템 오디오 수집 활성화(데스크톱 시스템만 해당) |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | 시스템 오디오 수집 비활성화(데스크톱 시스템만 해당) |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | 시스템 오디오 수집 볼륨 설정 |

### 화면 공유 관련 인터페이스
| API                 | 설명       |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd) | 데스크톱 화면 공유 시작(데스크톱 시스템만 해당) |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | 화면 공유 중지 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | 화면 공유 일시 중지 |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | 화면 공유 재개 |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad23c03ad142e8a42c49967ff9ccf9592) | 공유 가능한 화면 및 창 열거(데스크톱 시스템만 지원) |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | 공유할 화면 및 창 선택(데스크톱 시스템만 지원) |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a542913f5081fb2479137a7416c970e2d) |화면 공유(서브스트림)의 비디오 인코딩 매개변수 설정(데스크톱 시스템만 지원) |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | 화면 공유의 오디오 믹싱 볼륨 설정(데스크톱 시스템만 지원) |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff) | 화면 공유 제외 목록에 지정된 창 추가(데스크톱 시스템만 지원) |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf) | 화면 공유 제외 목록에 지정된 창 제거(데스크톱 시스템만 지원) |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | 화면 공유 제외 목록에서 모든 창 제거(데스크톱 시스템만 지원) |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a442186322939f9b93d6c6e0a3ace7bd3) | 화면 공유 포함 목록에 지정된 창 추가(데스크톱 시스템만 지원) |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3674c0ee6514d118fddd9a500ccafb03) | 화면 공유 포함 목록에서 지정된 창 제거(데스크톱 시스템만 지원) |
| [removeAllIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | 화면 공유 포함 목록에서 모든 창 제거(데스크톱 시스템만 지원) |

### 사용자 정의 수집 및 렌더링
| API                 | 설명       |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | 사용자 정의 비디오 수집 모드 활성화/비활성화 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | 수집한 비디오 프레임을 SDK에 전달 |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | 사용자 정의 오디오 수집 모드 활성화 |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | 수집한 오디오 데이터를 SDK에 전달 |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | 사용자 정의 오디오 트랙 활성화/비활성화 |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd) | 사용자 정의 오디오 트랙을 SDK에 믹싱 |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418) | 푸시 스트림 시 믹싱된 외부 오디오 푸시 스트림 볼륨 및 재생 볼륨 설정 |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | 사용자 정의 수집 시 타임스탬프 생성 |
| [setLocalVideoProcessCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3f6d32bdf3cb0fe72b61455304b975c6) | 서드 파티 뷰티 필터에 대한 비디오 데이터 콜백 설정 |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | 로컬 비디오에 대한 사용자 정의 렌더링 콜백 설정 |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | 원격 비디오에 대한 사용자 정의 렌더링 콜백 설정 |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | 오디오 데이터 사용자 정의 콜백 설정 |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7047f52811cefa10cf020ee20db1b087) | 사용자 정의 오디오 재생 활성화 |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac986d3ec66ab6681d94c8eb933b519de) | 재생 가능한 오디오 데이터 가져오기 |

### 사용자 정의 메시지 전송 인터페이스
| API                 | 설명       |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | UDP 채널을 사용하여 방의 모든 사용자에게 사용자 정의 메시지 보내기  |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | SEI 채널을 사용하여 방의 모든 사용자에게 사용자 정의 메시지 보내기  |

### 네트워크 테스트 인터페이스
| API                 | 설명       |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#af86b2903b95b6e74f02d701701ce3380) | 네트워크 속도 테스트 시작(방 입장 전 사용) |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | 네트워크 속도 테스트 중지 |

### 디버깅 관련 인터페이스
| API                 | 설명       |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | SDK 버전 정보 가져오기 |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Log 출력 레벨 설정 |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | 콘솔 로그 출력 활성화/비활성화 |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | 로컬 로그 압축 활성화/비활성화 |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | 로컬 로그 저장 경로 설정 |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | 로그 콜백 설정 |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | 대시보드 표시 |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab15fc0877664a8ac257ca4d6e7afc7b0) | 실험용 API 호출 |

### 사용하지 않는 인터페이스
| API                 | 설명       |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | 사용자 정의 비디오 수집 모드 활성화 |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | 수집한 비디오 데이터 전송 |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) |로컬 비디오 스트림 게시 일시 중지/재개 |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) | 원격 사용자 비디오 스트림 구독 일시 중지/재개 |

### 오류 및 경고 이벤트
| API                 | 설명       |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a9724da0b3da9b2eca5736fa8e54aa410) | 오류 이벤트 콜백 |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a53169ea41d90506cccbff507ba1932a4) | 경고 이벤트 콜백 |

### 방 관련 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a236a49e0525615b6435eaa826b7caffe) | 방 입장 성공 여부 이벤트 콜백 |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) | 방 퇴장 이벤트 콜백 |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a248335805c125e225cfec249697f2299) | 역할 전환 이벤트 콜백 |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ac5889e412f38769f2d21887f9bd7eeec) | 방 전환 결과 콜백 |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a62333366a3a1ab09dc2b2f627a8a1bdd) | 크로스 룸 통화 요청 결과 콜백 |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a292d6661cb93ba30ff68b1f88cf173f1) | 크로스 룸 통화 종료 결과 콜백 |

### 사용자 관련 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a43704996ae1f50749b7c7140755350f1) | 사용자 방 입장 |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a5f7c705f3894d3a430ef1fac8bf8e2c5) | 사용자 방 퇴장 |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) | 원격 사용자가 메인 비디오 화면 게시/게시 취소함|
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a460922e4fb4b000d1dbd27b596dd0e5c) | 원격 사용자가 서브 영상 화면을 게시/게시 취소함 |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a6f449dc5294e369750bc15a39eaa856c) | 원격 사용자가 오디오를 게시/게시 취소함 |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad28d27badd56ac274c44720cc9f253d5) | SDK가 로컬 또는 원격 사용자의 첫 번째 화면 프레임을 렌더링하기 시작함 |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a123616289b3219bc36137bc77e8e8b7a) | SDK가 원격 사용자의 첫 번째 화면 프레임을 재생하기 시작함 |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a454ea7e7103b2838440cafba3e524433) | 첫 번째 로컬 비디오 프레임 게시 |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0bd950cb774fd40cfdc2fbff885295d2) | 첫 번째 로컬 오디오 프레임 게시 |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a967a9b593385a8081083e84d3f5648b5) | 원격 비디오 상태 변경 이벤트 콜백 |

### 네트워크 및 기술 메트릭에 대한 통계 콜백
| API                 | 설명       |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a377441bace65d98a1218817914a12ecb) | 네트워크 품질 실시간 통계 콜백 |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ae7e4117f9c8004c9bcc5a29d64e840c9) | 멀티미디어 기술 메트릭에 대한 실시간 통계 콜백 |

### 클라우드 연결 상태 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a34c34705bb67127ff6d28700cf2ab591) | SDK와 클라우드 연결이 끊김 |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#afe74dff22fde93fe0f07fcf18153d334) | SDK와 클라우드 다시 연결 중 |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ae90cd149a676418016cb8736b217f1a8) | SDK와 클라우드가 다시 연결됨 |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a455264cfcf2a7a3f022f3bce0659f9f7) | 서버 속도 테스트 결과 콜백 |

### 하드웨어 관련 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a13a9ad0933b7ab872987e432f005e8ad) | 카메라 준비 완료 |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0ba02a5d9009ebb9c4e80c0c43c80bca) | 마이크 준비 완료 |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a61df1f9eec0bfcebf421be865275ffc5) | 볼륨 |
| [onDeviceChange](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ac86c1b0d445a33f6340394b3b78490bd) | 로컬의 상태가 변경됨(데스크톱 시스템만 해당) |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a40eeba4a6034450bc055b8f62c763520) | 현재 마이크 시스템의 수집 볼륨이 변경됨 |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad87c12c924b781b3b8429f8e8aafc338) | 현재 시스템의 재생 볼륨이 변경됨 |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a296665d16719c02dc055c983f88b40c3) | 시스템 오디오 수집 활성화 성공 여부 이벤트 콜백(Mac 시스템만 해당) |
| [onTestMicVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a9f0101fa8222c6163f1b23fcce81e22b) | 마이크 테스트 볼륨 콜백 |
| [onTestSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a04bb10b06af17cdc43b7831336736539) | 스피커 테스트 볼륨 콜백 |

### 사용자 정의 메시지 수신 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0a5690652db3902e98e1168bad12ec1a) | 사용자 정의 메시지 수신 이벤트 콜백 |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab5d0cb61c24b77ecdb177ff19fc95075) | 사용자 정의 메시지 손실 이벤트 콜백 |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab364b929cd0d9ffff6e47c20ec52372c) | SEI 메시지 수신 콜백 |

### CDN 관련 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a345ab7b45a9d0027926dbf580e8e0258) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 시작 이벤트 콜백 |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a8e046f5bd34498b13ae057caaab64913) | Tencent Cloud CSS CDN에 멀티미디어 스트림 게시 중지 이벤트 콜백 |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a16164548764979e84d3b5301f28890ff) | Tencent Cloud CSS CDN외에 멀티미디어 스트림 게시 시작 이벤트 콜백 |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0da75e040521c0945c3735f4893e6c09) | Tencent Cloud CSS CDN외에 멀티미디어 스트림 게시 중지 이벤트 콜백 |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0f11cee9e2659f7ea8484fdffd6b8583) | 클라우드 혼합 스트리밍의 레이아웃 및 트랜스 코딩 매개변수 설정 이벤트 콜백 |

### 화면 공유 관련 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a8baff9a6c699ea1d82c5e7abb6ded97b) | 화면 공유 활성화 이벤트 콜백 |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a32acecdafd9058cc7d70a3abe6995051) | 화면 공유 일시 중지 이벤트 콜백 |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a63c073daf1ad93cfa2e6c79695434e22) | 화면 공유 재개 이벤트 콜백 |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4d182e6b60d8be536e69253d906af84d) | 화면 공유 중지 이벤트 콜백 |
| [onScreenCaptureCovered](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a490f827ffd6e7728a6ec49cba63875b1) | 화면 공유 창이 가려짐 이벤트 콜백(Windows만 해당) |

### 로컬 녹화 및 화면 캡처 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4a40b1b338d93c871f73354d1d45f24b) | 로컬 녹화 작업 시작 이벤트 콜백 |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0b226b8e627dad7850a880d48ffb91dd) | 로컬 녹화 작업 진행 중 이벤트 콜백 |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4455252d3e0f5d869db18641e24da106) | 로컬 녹화 작업 종료 이벤트 콜백 |
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a10501027a79d1d05231319570c0e5603) | 로컬 화면 캡처 완료 이벤트 콜백 |

### 사용하지 않는 이벤트 콜백
| API                 | 설명       |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad606b861a3545832fb4821a7e0230925) | 호스트가 현재 방에 입장함(폐기됨) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#abbc4fe2ccac90f77c80f55d46d6c8951) | 호스트가 현재 방에서 퇴장함(폐기됨) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aab3c91276b6e570ea9acfe1581e1aa51) | 음향 효과 종료(폐기됨) |
| [onPlayBGMBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad93b8204416558e63c18349bf29ff592) | 배경 음악 재생 시작(폐기됨) |
| [onPlayBGMProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a1879cc4e50492431a3346828e9130f21) | 배경 음악 재생 진행률 콜백(폐기됨) |
| [onPlayBGMComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#abaf89c758a4dd21e21db488e997bef2a) | 배경 음악 재생 종료(폐기됨) |

### 비디오 데이터 사용자 정의 콜백
| API                 | 설명       |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aea602851c96370558a7eeb850d7eb6b8) | 사용자 정의 비디오 렌더링 콜백 |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aa416979597d1bec68dc268a9432619ae) | 타사 뷰티 필터 컴포넌트에 의한 비디오 처리 콜백 |

### 오디오 데이터 사용자 정의 콜백
| API                 | 설명       |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a1488e35460441c351cab75d9702498f6) | 로컬 마이크에서 수집된 원본 오디오 데이터 콜백 |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#affb432a77f938d1e8dfb6c0d5488dbcf) | 로컬에서 수집하고 오디오 모듈에서 전처리된 오디오 데이터 콜백 |
| [onPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab841da62beb88a9fa9bce58d25df6f23) | 각 원격 사용자의 오디오 믹싱 전 오디오 데이터 |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a6649f62d4138d9bc73ae484e63dec081) | 재생하기 위해 시스템에 제출되기 전 각 채널에서 믹싱된 오디오 데이터 콜백 |

### 기타 이벤트 콜백 인터페이스
| API                 | 설명       |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a2fa3d9997c9810ffa6a95e0a7a4a50d0) | 로컬 LOG 출력 콜백 |

### 비디오 관련 열거 값 정의
| API                 | 설명       |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gace04ad7a0bf531f4d09dc6a540f09f95) | 비디오 해상도 |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaa6787a9059d7b725a30ffcf9f4aabb64) | 비디오 종횡비 모드 |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga461563be214e8f0579a79741f37d18e3) | 비디오 스트림 유형 |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga496a32286104187149b4e40284cbfb36) | 영상 화면 채우기 모드 |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga4f8ab82260baa03f83f123ebeaa82b2e) | 영상 화면 회전 방향 |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga46f49720df57d17b267054cb9ee4d079) | 뷰티 필터(피부 보정) 알고리즘 |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga98b07c6c79303f486682b3b92fa88c7e) | 비디오 픽셀 형식 |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga3a075ea5603cdd730550b37fc0032c68) | 비디오 데이터 전송 방식 |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga778fcc2797d6076745997327c8b20009) | 비디오 미러 이미지 유형 |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga65de3d8416c7faabe1a8b77a6fd9cc7c) | 로컬 영상 화면 캡처 데이터 소스 |

### 네트워크 관련 열거 값 정의 
| API                 | 설명       |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaa57f4545ef7331e3157eee1639d28780) | 응용 시나리오 |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga42ff820a33d9f3535d203fd5d6782cb5) | 역할 |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga6615b296e31fc3d03c0df92e9755b5aa) | QoS 제어 모드(폐기됨) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga60efcaeea7692bbce8dc362856683319) | 화질 선호도 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCQualityInfo) | 네트워크 품질 |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga9ab84e3f9458dacd479937e5a24c95f2) | 비디오 상태 유형 |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga37b6311e4d5ba7376070ba65de520865) | 비디오 상태 변동 원인 |

### 오디오 관련 열거 값 정의 
| API                 | 설명       |
|-----|-----|
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga96f3d4cdcf3baa9df39ab4e1b3f0eb40) | 오디오 품질 |

### 기타 열거 값 정의
| API                 | 설명       |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gafa83683b4840bcb3200d1da63c10276d) | Log 레벨 |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gad96fcfd4a65c0f99579b0c35ef86645d) | 화면 공유 타깃 유형(데스크톱만 해당) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaec50c849a17b7706f6989d718fc6b7df) | 클라우드 혼합 스트리밍 레이아웃 모드 |
| [TRTCLocalRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga92580ecee493fb524b84234305316238) | 미디어 녹화 유형 |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga323584f89d0479be0a1b554ec05672f7) | 혼합 스트림 입력 유형 |
| [TRTCDeviceType](https://liteav.sdk.qcloud.com/doc/api/en/namespaceliteav.html#abaf3d3254d2b2e11fb2064478975be17) | 디바이스 유형(데스크톱 플랫폼만 해당) |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga5adbddb520b6eea48142c3b5be740205) | 오디오 녹음 콘텐츠 유형 |

### TRTC 핵심 유형 정의 
| API                 | 설명       |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCParams) | 방 입장 매개변수 |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVideoEncParam) | 비디오 인코딩 매개변수 |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCNetworkQosParam) | 네트워크 트래픽 제어(Qos) 매개변수 세트 |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCRenderParams) | 영상 화면 렌더링 매개변수 |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCQualityInfo) | 네트워크 품질 |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVolumeInfo) | 볼륨 크기 |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSpeedTestResult) | 네트워크 속도 테스트 결과 |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVideoFrame) | 비디오 프레임 정보 |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioFrame) | 오디오 프레임 데이터 |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ac5b1947f21f77726cbff822eaf0003f9) | 클라우드 혼합 스트리밍 각 채널 화면에 대한 설명 정보 |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCTranscodingConfig) | 클라우드 혼합 트래픽의 레이아웃 및 트랜스 코딩 매개변수 |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCPublishCDNParam) | Tencent Cloud CDN외에 멀티미디어 스트림을 게시할 때 설정해야 하는 푸시 매개변수 |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioRecordingParams) | 로컬 오디오 파일 녹화 매개변수 |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCLocalRecordingParams) | 로컬 미디어 파일 녹화 매개변수 |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioEffectParam) | 음향 효과 매개변수(폐기됨) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSwitchRoomConfig) | 방 전환 매개변수 |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCScreenCaptureSourceInfo) | 화면 공유 타깃 정보(데스크톱 시스템만 해당) |



