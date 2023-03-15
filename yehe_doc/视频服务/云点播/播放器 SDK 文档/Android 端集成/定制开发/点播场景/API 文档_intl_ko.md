## TXVodPlayer

### VOD 플레이어

자세한 내용은 [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html)를 참고하십시오.
플레이어는 지정된 VOD 스트림 URL에서 오디오/비디오 데이터를 풀링하고 디코딩 및 로컬 렌더링 후 데이터를 재생합니다.
플레이어에는 다음과 같은 기능이 있습니다.

- FLV, MP4, HLS 파일은 기본 재생(URL 재생)과 VOD 재생(Fileid 재생)의 두 가지 재생 방법으로 재생할 수 있습니다.
- 비디오 스트림의 스크린샷을 캡처할 수 있습니다.
- 제스처를 통해 밝기, 음량, 재생 진행 상황을 조절할 수 있습니다.
- 비디오 해상도는 수동으로 전환하거나 현재 네트워크 대역폭에 맞게 자동으로 전환할 수 있습니다.
- 다른 재생 속도를 지정할 수 있고, 비디오를 수평으로 뒤집을 수 있으며, 하드웨어 가속을 활성화할 수 있습니다.
- 플레이어의 모든 기능에 대한 자세한 내용은 [비디오 재생 개요](https://www.tencentcloud.com/document/product/266/38295)를 참고하십시오.

### 플레이어 구성 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ae69bc2dd060217e595c38f0dc819290a) | 플레이어 구성 정보 설정. 구성에 대한 자세한 내용은 [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html)를 참고하십시오. |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | 플레이어의 렌더링 뷰 TXCloudVideoView 설정.                        |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aeb2f15f370d50b6261b7832f02a0f411) | 플레이어의 렌더링 뷰 TextureView 설정.                             |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | 플레이어의 렌더링 뷰 SurfaceView 설정.                             |
| [setStringOption](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a23eedd175a85f171cb7c34638bab0c45) | 플레이어 비즈니스 매개변수 설정. 매개변수 형식: `<String,Object>`.            |

### 기본 재생 API  
| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | 지정된 HTTP URL에서 비디오 재생 시작. |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac255cbe3a0481014f3d8aa4a6ca4d581) | fileId 형식으로 재생. TXPlayInfoParams 매개변수 전달.        |
| [startPlayDrm](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a1e8443952146701507adb219d8b992b1) | DRM 암호화된 비디오 재생.                                     |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | 재생 중지. |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | 재생 진행 중 여부 가져오기.      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | 스트림 데이터 가져오기를 중지하고 마지막 프레임 이미지를 유지하여 재생 일시 중지. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a41de8150eff044a237990c271d57ea27) | 스트림 데이터를 다시 가져와 재생 재개. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | 비디오 스트림의 지정된 시점(초) 찾기. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aa5d7fcf690ac3a1102ffa3c02192674d) | 비디오 스트림의 지정된 시점(밀리초) 찾기. |
| [getCurrentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a128b89dd39053d6d19d262a5f45110cd) | 현재 재생 시점(초) 가져오기. |
| [getBufferDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#acebd6ae9dd87e10c8959a24d3b6d5e7f) | 총 버퍼 지속 시간(초) 가져오기. |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a83ee44393f1e0db930be75b73ff47812) | 총 비디오 지속 시간(초) 가져오기. |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a37cb584556d48d043b93dfec33c40a97) | 재생 가능한 비디오 재생 시간(초) 가져오기. |
| [getWidth](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a67a0997183f24da19b776d96c1052998) | 비디오 너비 가져오기. |
| [getHeight](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a07efb2a4e9a982688c8bb3c3f21d1092) | 비디오 높이 가져오기. |
| [setAutoPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5e0e3d950eb3f525634adc7a9f60eab7) | startPlay 호출 후 VOD 자동 재생 여부 설정. 기본값: 자동 재생. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a8f767f79fb69496cdbc532fced5dff33) | 재생 시작 시간 설정. |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5f9eadc88ca97238f84226462f095536) | HLS 암호화 token 설정. |
| [getEncryptedPlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#acc32bf00b94774e5314cb733f9f339df) | 암호화된 재생 키 가져오기.                                |
| [setLoop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a3f5ae863c82509d1ed266503e8138781) | 비디오 반복 여부 설정. |
| [isLoop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aaa3fcc823e0fce316dea1cc9162f1c8e) | 루프 재생 상태 반환. |

### 비디오 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | 비디오 하드웨어 디코딩 활성화/비활성화.                                       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6f1c0c128052960f084ef6d1d7a77b09) | 현재 비디오 프레임 이미지 가져오기. <br/>**참고: 이 작업은 시간이 많이 걸리므로 스크린샷은 비동기식으로 다시 호출됩니다.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a4add579d2ec825502c5e3832aced5bc1) | 비디오 이미지 수평 뒤집기 여부 설정.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#add2bcd36c051900d697853155494865b) | VOD 재생 속도 설정. 기본값: 1.0.                                |
| [getBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#af6f9e1e680baa611642fb168007b1c45) | 현재의 재생 비트 레이트 인덱스 반환.                                     |
| [getSupportedBitrates](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aedacfbc888f5446ab2318ea3a7199700) | 재생 주소가 HSL인 경우 지원되는 비트 레이트(해상도) 목록 반환.            |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a61f524a6ed275edaf9e9a0997f64d491) | 원활한 해상도 전환을 위한 현재 재생 비트 레이트 인덱스 설정. 해상도를 전환하려면 잠시 기다려야 할 수도 있습니다. |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | [이미지 채우기 모드](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae) 설정. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | [이미지 렌더링 각도](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f) 설정. |

### 오디오 API

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | --------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | 플레이어 음소거 여부 설정.                      |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | 볼륨 레벨 설정. 값 범위: 0–100.           |
| [setRequestAudioFocus](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a676f0935eca038719f58100d31f169b1) | 오디오 포커스 자동 가져오기 여부 설정. 기본값: 자동 가져오기. |

### 이벤트 공지 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a0735b006fe8c56875665cb66881af144) | 플레이어 콜백 설정(더 이상 사용되지 않으므로 대신 [setVodListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61)를 사용하는 것이 좋습니다). |
| [setVodListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) | 플레이어 콜백 설정.                                 |

### TRTC API

다음 API를 사용하여 VOD 플레이어의 오디오/비디오 스트림을 TRTC를 통해 푸시할 수 있습니다. TRTC 서비스에 대한 자세한 내용은 TRTC [제품 개요](https://cloud.tencent.com/document/product/647/16788) 페이지를 참고하십시오.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ad6bd04b37a89012102e7bb71ea5554a6) | VOD를 [TRTC](https://cloud.tencent.com/document/product/647/16788)에 바인딩. |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5b947acf9f4fc992f0f02f8d87de3334) | [TRTC](https://cloud.tencent.com/document/product/647/16788)에서 VOD 바인딩 해제. |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a8298f704cb659c725da28a27e08afbed) | 비디오 스트림 푸시 시작.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aaa6ecf72bfa9e35078561dd98d62be0c) | 비디오 스트림 푸시 취소.                                             |
| [ publishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | 오디오 스트림 푸시 시작.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a206d786a74ae3b71766755135161773e) | 오디오 스트림 푸시 취소.                                             |

## ITXVodPlayListener

VOD 콜백 공지입니다.
### 기본 SDK 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPlayListener__android.html#aad1d875808cd4a68d429762e492aad05) | VOD 재생 이벤트 알림. 자세한 내용은 [재생 이벤트 목록](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) 및 [이벤트 매개변수](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)를 참고하십시오. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPlayListener__android.html#a2be0a0294ae21e68e736ac8fa4d3085d) | VOD 플레이어의 [네트워크 상태 알림](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737). |

## TXVodPlayConfig

VOD 플레이어 구성 클래스입니다.

### 기본 구성 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | 플레이어의 최대 재접속 시도 횟수 설정.                                         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | 플레이어 재연결 간격(초) 설정.                                 |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ae44a6096c42cdb61adc10370ca2a42b6) | 플레이어 연결 제한 시간(초) 설정.                             |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a6ad0d546e6da3abacd5d4ea8bd6f94de) | 이 API는 더 이상 사용되지 않으므로, 권장하지 않습니다. <br/>MP4 및 HLS 파일에 적용되는 VOD 캐시 디렉터리 설정.                       |
| [setMaxCacheItems](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#acc2f17764df9bb52163dac9faf81f11e) | 이 API는 더 이상 사용되지 않으므로, 권장하지 않습니다. <br/>최대 캐시 파일 수 설정.            |
| [setPlayerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a3594024855210dc07f50a6d7c5f8b088) | 이 API는 더 이상 사용되지 않으므로, 권장하지 않습니다. <br>플레이어 유형 설정.            |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | 사용자 정의 HTTP headers 설정.                                    |
| [setEnableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a3caff179964976945f3754f1ec48a42b) | 정확한 seek 활성화 여부 설정. 기본값: true.                               |
| [setAutoRotate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ab360b681c220c2adb57de2758916b227) | YES로 설정하면 MP4 파일이 설정된 회전 각도에 따라 자동 회전됨.<br>회전 각도는 PLAY_EVT_CHANGE_ROTATION 이벤트에서 얻을 수 있습니다. 기본값: YES. |
| [setSmoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a23fb393011e4663d0dfa765b72665a46) | 다중 비트 레이트 HLS 스트림에 대해 부드러운 전환 활성화 여부 설정. 기본값: false.                             |
| [setCacheMp4ExtName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#aaeccb662be133d4ded4fc17df29b94b5) | 캐시된 MP4 파일 확장자 설정.                                        |
| [setProgressInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a01a46ce89e4979a6397b6deb2525007c) | 진행 콜백 간격(밀리초) 설정.                                 |
| [setMaxBufferSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a2705841bfedb3c44839cc355eaad26dc) | 최대 사전 로딩 버퍼 크기(MB) 설정.                                    |
| [setMaxPreloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a78d73bb26332151cbf5f8aa10240a4a5) | 최대 사전 로딩 버퍼 크기(MB) 설정.                           |
| [setExtInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a080c7ab4f3b6f06e690561889eca3594) | 확장 정보 설정.                                               |
| [setPreferredResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a369c5980be4748b11216a686482e910f) | 비트스트림이 여러 개인 경우 설정된 preferredResolution에 따라 최적의 코드 스트림을 선택하여 재생하며, preferredResolution은 비디오 너비와 높이(width * height)의 곱으로, 재생이 시작되기 전에 설정된 경우에만 적용됨. |
| [setOverlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#abd8626115358e211fcbc5347a34b2e18) | HLS 보안 강화 암호화/복호화 key 설정.                                |
| [setOverlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#adcdc2c60303e4b67757583904836dfab) | HLS 보안 강화 암호화/복호화 Iv 설정.                                 |
| [setEnableRenderProcess](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ab48a6ca2e64a61942f714c2b74710ba8) | 포스트 렌더링 및 포스트 프로덕션 기능 허용 여부.                               |
| [setMediaType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a532518afe8abf910920278a0c21f225f) | 미디어 자산 유형 설정. 기본값: auto 유형.                             |

## TXPlayerGlobalSetting

VOD 플레이어의 전역 구성입니다.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__android.html#adf3cf9c0b96e7eeb97b5e9ed56743df8) | 재생 엔진의 cache 디렉터리 설정. 설정 후 오프라인 다운로드, 사전 다운로드, 플레이어 등 사용 시 이 디렉터리를 먼저 읽고 저장함. |
| [setMaxCacheSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__android.html#a27de4890873400d4d4ff2c624138786d) | 재생 엔진의 최대 캐시 크기 설정. 설정 후 백엔드는 설정 값에 따라 Cache 디렉터리의 파일을 자동으로 지움. 단위: MB. |

## TXVodPreloadManager

VOD 플레이어의 API 클래스 사전 다운로드

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | --------------------------------------------- |
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#a9e52c1e94ef4b2a35fdb6dfbf89f5e92) | TXVodPreloadManager 인스턴스 객체, 싱글톤 모드 가져오기. |
| [startPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#a1968e49655bc231c54247f9189176911) | 사전 다운로드를 실행하기 전에 재생 엔진의 캐시 디렉터리를 설정하십시오.  |
| [stopPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#aa8425852d9c185f71b3933ac61834c5c) | 사전 다운로드 중지.                                  |

## ITXVodPreloadListener

비디오 사전 다운로드 콜백 인터페이스입니다.

| API                                                          | 설명             |
| ------------------------------------------------------------ | ---------------- |
| [onComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPreloadListener__android.html#a2004a619f03a97617661985f0f79a767) | 비디오 사전 다운로드 완료. |
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPreloadListener__android.html#aac11d56117d32f2e1bf6afafb940db77) | 비디오 사전 다운로드 오류. |

## TXVodDownloadManager 

VOD 플레이어의 비디오 다운로드 API 클래스입니다. 현재 중첩되지 않은 m3u8 비디오만 다운로드할 수 있습니다. simpleAES로 암호화된 영상은 보안을 강화하기 위해 Tencent Cloud의 개인 암호화 알고리즘으로 다시 암호화됩니다.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a84b3db42095ccb149b8f9be57ecdc0cc) | TXVodDownloadManager 인스턴스 객체, 싱글톤 모드 가져오기.               |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | 다운로드 HTTP 헤더 설정.                                           |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a123ff28866dca6b525f1f2defde28199) | 다운로드 콜백 방식 설정. 다운로드하기 전에 설정해야 합니다.                           |
| [startDownloadUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a3e6424357de962092cff42d4c1a68654) | 지정된 URL에서 비디오 다운로드 시작.                                        |
| [startDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a1d58d3e216c1016eb8d5cc051dd300f7) | 지정된 fileid의 비디오 다운로드 시작.                                     |
| [stopDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a86b884a71a6a11e729a964478612ed65) | 다운로드 중지. ITXVodDownloadListener.onDownloadStop 호출 시 다운로드 중지 성공. |
| [deleteDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a0dab7dad33ef2b555abf31f07ab6447d) | 다운로드 정보 삭제.                                               |
| [getDownloadMediaInfoList](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#ad82cf86e7bad17efa86df162a4286a05) | 모든 사용자에 대한 다운로드 목록 정보 가져오기.                                 |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#ac8b38266ea66940fdd406487ff45a2fd) | 다운로드 정보 가져오기.                                               |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a7e03beed3e30d3243b91853856da9d53) | 다운로드 정보 가져오기.                                               |

## ITXVodDownloadListener

VOD 다운로드 공지입니다.

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ----------------------------------------------- |
| [onDownloadStart](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a3cbbd786c51f86aba84a182edd054343) | 다운로드 시작                                        |
| [onDownloadProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a4dd74690b9ed22442ba9956d29d69b32) | 다운로드 진행률 업데이트                                    |
| [onDownloadStop](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#ac70254aa0f35a4ba01fc8de93214112b) | 다운로드 중지                                        |
| [onDownloadFinish](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a0b6eb0287eea736f84ebe8c212ab2219) | 다운로드 종료                                        |
| [onDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#ae0faac6397f8df5a2d1e57e56e6e4ec3) | 다운로드 중 오류 발생                              |
| [hlsKeyVerify](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a206077037e4a5f8ef81707ec82514523) | HLS 스트림 다운로드 중에 암호화된 파일이 발견되면 플레이어가 암호 해독 Key를 확인 |


## TXVodDownloadDataSource

다운로드 중에 매개변수로 전달할 수 있는 Tencent Cloud 비디오 fileid 다운로드 소스.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TXVodDownloadDataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aef4a9306eddebbd7920089e48e09b260) | appid，fileid，quality，pSign，username 등 매개변수를 전달하는 함수 빌드 |
| [getAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ab95e1b8c990ed3e41fc623e5e9ed47c3) | 전달된 appid 가져오기                                             |
| [getFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aae60f2e5054da59d0f2d239d0e673cc8) | 전달된 fileid 가져오기                                            |
| [getPSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aa7c355a0046a91c5f302f1602b985462) | 전달된 psign 가져오기                                             |
| [getQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ab03cb85fa393531d1fb702ab1e92008f) | 전달된 quality 가져오기                                           |
| [getUserName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ae3cc9307a896bbfcf570a0d077708f58) | 전달된 userName 가져오기. 기본값: ‘default’                           |
| [getToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a20c1ba8630591cc399a35a7abc535728) | 전달된 token 가져오기                                             |
| [getOverlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a8cceb76d2594cecb6615652a854e3245) | 전달된 overlayKey 가져오기                                        |
| [getOverlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a86ac7a9d6239880059fc109128c9bb4b) | 전달된 overlayIv 가져오기                                         |

### 해상도 Id 상수

| code | 상수 정의                                                     | 설명 |
| ---- | ------------------------------------------------------------ | -------- |
| 0    | [QUALITY_OD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#abb1129f5ddec88f4eb579e96afdd741a) | 기존 해상도     |
| 1    | [QUALITY_FLU](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a5b5a1363633c76ecfb35dea5daf3e0b2) | LD     |
| 2    | [QUALITY_SD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aad857cb177a777ba09aed2a312a3fe1f) | SD     |
| 3    | [QUALITY_HD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a70195f7d2882bf1918f599ff1c555717) | HD     |
| 4    | [QUALITY_FHD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aff4ebd940acb1937be588b6eb7879183) | FHD   |
| 5    | [QUALITY_2K](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a69635e7ebfc9895b840c7a5f1817e7b3) | 2K       |
| 6    | [QUALITY_4K](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a35eb8012dab226b7d0714ad98560715d) | 4K       |
| 1000 | [QUALITY_UNK](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a3380895e1edc2eb4394cac5d2b40fda5) | 미정의   |

## TXVodDownloadMediaInfo

다운로드 진행 상황 및 재생 링크 등 Tencent Cloud VOD 다운로드 정보

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | -------------------------------------------- |
| [getDataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#ab8d408191666ef004ae7d1e4f8d4840a) | fileid를 다운로드할 때 전달된 fileid 다운로드 소스 가져오기         |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a08c13081c0665a4336a0f022c955fb69) | 총 다운로드 시간 가져오기                             |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#aea8be4cac1aaa5b79a1c3faf13ece59c) | 다운로드한 재생 가능 시간 가져오기                       |
| [getSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a3c4029b904a61a9873e6d12785ce19a1) | fileid 다운로드 소스에 대해서만 유효한 다운로드된 파일의 총 크기 가져오기 |
| [getDownloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#ab2ab8161365b107da0cf398c2e683533) | fileid 다운로드 소스에 대해서만 유효한 다운로드된 파일 크기 가져오기 |
| [getProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#afdfeed8666fff88f32b73cbd1d3a2770) | 현재 다운로드 진행률 가져오기                             |
| [getPlayPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a52f40379c9ced15ea1d26d800ad6ac4b) | 재생을 위해 TXVodPlayer에 전달할 수 있는 현재 재생 경로 가져오기    |
| [getDownloadState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a2184d61558a641a71115c9efe9ad3a48) | 다운로드 상태 가져오기                                 |
| [isDownloadFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#aed26755c5919fc7125e4e2400d30d1bc) | 다운로드 완료 여부 결정                             |

### 정적 속성

| code | 속성 정의                                                     | 설명   |
| ---- | ------------------------------------------------------------ | ---------- |
| 0    | [STATE_INIT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a1ac9cfa17538972c579f1bff39c2fe83) | 초기 다운로드 상태 |
| 1    | [STATE_START](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a89be56b1eb6cd1441eae8ee501a995e1) | 다운로드 시작   |
| 2    | [STATE_STOP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a88533f2a5acf4b41400bd14feeab9106) | 다운로드 중지   |
| 3    | [STATE_ERROR](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a7474da17fe98cc77b5bfd257f5f39317) | 다운로드 오류   |
| 4    | [STATE_FINISH](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#abd0a89abf65650e0e16b613e34d8466f) | 다운로드 완료   |

## TXPlayerAuthBuilder

fileId로 암호화된 비디오 재생을 설정합니다.

| API                      | 설명                                                         |
| ------------------------------------------------------------ | -------------------- |
| [setAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#a0b43955512510cd5c4930c236f3666bb) | 애플리케이션 appId.          |
| [setFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#abd423a3f7b11333d1b68506e25e4b77e) | 파일 id.             |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#ac8cc3ccb3adfc2533c4a8fa97274625d) | 암호화된 링크 시간 초과 타임스탬프. |
| [setExper](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#a9855f630f9444c767a8085d68892faa1) | 미리 보기 지속 시간.           |
| [setUs](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#aca22d76e37e78b330084f6b228594894) | 고유한 요청 식별.       |
| [setSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#afb81925d434438d6903b8016b0f26d8d) | 링크 도용 방지 서명.         |
| [setHttps](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#adcd67a70185ef7680ecfe0162aee0273) | https 요청의 사용 여부.     |

## TXBitrateItem

비디오 비트 레이트 정보입니다.

| API                                                          | 설명                       |
| ------------------------------------------------------------ | -------------------------- |
| [index](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a750b5d744c39a06bfb13e6eb010e35d0) | m3u8 파일 스트림 번호.        |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a2474a5474cbff19523a51eb1de01cda4) | 이 스트림의 비디오 너비.           |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#ad12fc34ce789bce6c8a05d8a17138534) | 이 스트림의 비디오 높이.           |
| [bitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#ab5d8e1788d02d0e52941a0778776e289) | 이 스트림의 비디오 비트 레이트.           |
| [compareTo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a1062863c4ed9def2a8af6edb834792a0) | 두 스트림의 비트 레이트 동일 여부. |

## TXImageSprite

스프라이트 이미지 리졸브 유형입니다.

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ---------------------------------- |
| [TXImageSprite](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a0daa097ae5eaabb45ce5899d641108be) | 구조 함수.                         |
| [setVTTUrlAndImageUrls](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#aea98e261dc8911344659a9e6c113f8e8) | 이미지 스프라이트 URL 설정.                   |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a16a3b680fcd8da1468d3ccfe675d47ed) | 썸네일 가져오기.                       |
| [release](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a23b477d0e2d399f75d585d154c346591) | 사용 후에 호출해야 합니다. 그렇지 않으면 메모리 유출이 발생합니다. |

## TXPlayerDrmBuilder

DRM 재생 정보입니다.

| API                      | 설명                                                         |
| ------------------------------------------------------------ | --------------------- |
| [TXPlayerDrmBuilder](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#acee757f8bcb8d6af23f4963184f7b791) | DRM 재생 정보 객체 구성. |
| [setProvisionUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#a5f55511af44ef3e6619988d4002d1aa5) | 인증서 공급자의 url 설정.   |
| [setKeyLicenseUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#ac293b2b09e849a2b54382180c44dc37f) | 복호화 key url 설정.     |
| [setPlayUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#ad3970dca8235512ed26d2afd492de595) | 재생할 미디어 파일의 url 설정.   |

## TXPlayInfoParams

fileId를 통한 비디오 재생을 매개변수 정보입니다.

| API                                                          | 설명                  |
| ------------------------------------------------------------ | ------------------------ |
| [TXPlayInfoParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#a1f5bbdc7d3a4817ace0ff64e70af964c) | 구조 함수.               |
| [getAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#ab95e1b8c990ed3e41fc623e5e9ed47c3) | 애플리케이션 id 가져오기.             |
| [getFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#aae60f2e5054da59d0f2d239d0e673cc8) | 파일 id 가져오기             |
| [getPSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#aa7c355a0046a91c5f302f1602b985462) | Tencent Cloud 비디오의 암호화 서명 가져오기. |



## 오류 코드

### 일반 이벤트

| code | 이벤트 정의                   | 설명                                                    |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | 비디오 재생이 시작되고 로딩 아이콘 애니메이션(있는 경우)이 종료되었습니다.                |
| 2005 | PLAY_EVT_PLAY_PROGRESS     | 비디오 재생 진행률(현재 재생 진행률, 로딩 진행률 및 총 비디오 재생 시간 포함).      |
| 2007 | PLAY_EVT_PLAY_LOADING      | 비디오를 loading하는 중입니다. 비디오 재생이 다시 시작되면 LOADING_END 이벤트가 보고됩니다. |
| 2014 | PLAY_EVT_VOD_LOADING_END   | 비디오 loading이 종료되고 비디오 재생이 재개되었습니다.                       |
| 2006 | PLAY_EVT_PLAY_END          | 비디오 재생이 종료되었습니다.                                              |
| 2013 | PLAY_EVT_VOD_PLAY_PREPARED | 플레이어가 준비되었으며 재생을 시작할 수 있습니다.                                |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | 네트워크는 첫 번째 렌더링 가능한 비디오 데이터 패킷(IDR)을 수신했습니다.                   |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | 비디오 해상도가 변경되었습니다.                                            |
| 2011 | PLAY_EVT_CHANGE_ROTATION   | MP4 동영상이 회전되었습니다.                                          |



### 경고 이벤트

| code  | 이벤트 정의                          | 설명                                                     |
| ------ | ------------------------------------- | ------------------------------------------------------------ |
| \-2301 | PLAY\_ERR\_NET\_DISCONNECT            | 네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없음. 플레이어를 다시 시작하여 연결 재시도 가능.                           |
| \-2305 | PLAY\_ERR\_HLS\_KEY                   | HLS 암호 해독 key 가져오기 실패.                                        |
| 2101   | PLAY\_WARNING\_VIDEO\_DECODE\_FAIL    | 현재 비디오 프레임을 디코딩 실패.                                              |
| 2102   | PLAY\_WARNING\_AUDIO\_DECODE\_FAIL    | 현재 오디오 프레임 디코딩 실패.                                               |
| 2103   | PLAY\_WARNING\_RECONNECT              | 네트워크 연결이 끊어지고 자동 재연결 수행됨(세 번 실패하면 PLAY_ERR_NET_DISCONNECT 이벤트가 발생합니다). |
| 2106   | PLAY\_WARNING\_HW\_ACCELERATION\_FAIL | 하드웨어 디코더 시작 실패. 소프트웨어 디코더가 대신 사용됨.                                            |
| \-2304 | PLAY\_ERR\_HEVC\_DECODE\_FAIL         | H265로 디코딩 실패.                                              |
| \-2303 | PLAY\_ERR\_FILE\_NOT\_FOUND           | 재생할 파일이 존재하지 않음.                                               |

## 플레이어 SDK 상수

아래의 상수 10.0 버전부터 `TXVodConstants`를 통해 대외적으로 제공됩니다.

### 이미지 채우기 모드

| code | 이벤트 정의                                                     | 설명           |
| ---- | ------------------------------------------------------------ | ------------------ |
| 0    | [RENDER_MODE_FULL_FILL_SCREEN](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0645160ad90c67581f7f226a6c0c46ae) | 비디오 이미지 전체 화면 채우기   |
| 1    | [RENDER_MODE_ADJUST_RESOLUTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7bc7babd208fa82866f80e9340a5354c) | 비디오 이미지 화면 맞추기 |

### 이미지 렌더링 각도

| code  | 이벤트 정의                          | 설명                                                     |
| ---- | ------------------------------------------------------------ | -------- |
| 0    | [RENDER_ROTATION_PORTRAIT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad00f3ee125e574cab63d955e03f5f23f) | 일반 세로 화면 |
| 270  | [RENDER_ROTATION_LANDSCAPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga17bdfecb387ddb3b34a96a0474bd73e3) | 오른쪽으로 90도 회전 |

### 이벤트 목록 재생

| code  | 이벤트 정의                          | 설명                                                     |
| ----- | ------------------------------------------------------------ | ------------------------------ |
| 2003  | [VOD_PLAY_EVT_RCV_FIRST_I_FRAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad745daba38f53e17c19f648e51246044) | 네트워크는 첫 번째 비디오 데이터 패킷(IDR) 수신  |
| 2004  | [VOD_PLAY_EVT_PLAY_BEGIN](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gada58f2a016424a22d053ff02818b705e) | 비디오 재생 시작                   |
| 2005  | [VOD_PLAY_EVT_PLAY_PROGRESS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga69a17c951f665b929c0ced3e946b41b0) | 비디오 재생 진행률                   |
| 2006  | [VOD_PLAY_EVT_PLAY_END](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9a4e84bd9d9e9c7ae1db0cfd3875e74a) | 비디오 재생 종료                   |
| 2007  | [VOD_PLAY_EVT_PLAY_LOADING](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga755928f9307a228f5b94c054fe888384) | 비디오 재생 Loading                |
| 2008  | [VOD_PLAY_EVT_START_VIDEO_DECODER](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7c3fc61aaa8865bccee4deb0b237f9e0) | 디코더 시작                     |
| 2009  | [VOD_PLAY_EVT_CHANGE_RESOLUTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa02aa77b481d6817ddd60ca3cad7131e) | 비디오 해상도 변경                 |
| 2010  | [VOD_PLAY_EVT_GET_PLAYINFO_SUCC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaebd8ad6fe4c09ebb9205422ed072b61f) | VOD 파일 정보 가져오기 성공           |
| 2011  | [VOD_PLAY_EVT_CHANGE_ROTATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga440c3d89bec97cea7170d293d590d5fd) | 비디오 회전 정보                   |
| 2013  | [VOD_PLAY_EVT_VOD_PLAY_PREPARED](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga81e281a76a84d61f9f76cc45d51b7bd7) | 비디오 로딩 완료                   |
| 2014  | [VOD_PLAY_EVT_VOD_LOADING_END](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga22ef1d7404af3661eb6b600a6e6399fd) | loading 종료                    |
| 2026  | [VOD_PLAY_EVT_RCV_FIRST_AUDIO_FRAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaecd3bbe2687021e769985deb88bd04ce) | 오디오 첫 재생                   |
| 2103  | [VOD_PLAY_WARNING_RECONNECT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga029b64e10522699e622bd42706d10f65) | 네트워크 연결이 끊긴 후 자동 재접속 실행됨       |
| -2301 | [VOD_PLAY_ERR_NET_DISCONNECT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae0ebb051cf1166a8c71cd0b981d260cc) | 네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없음 |
| -2303 | [VOD_PLAY_ERR_FILE_NOT_FOUND](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga1e71f9fdafabb1bd16fab933c308d070) | 파일이 존재하지 않음                     |
| -2304 | [VOD_PLAY_ERR_HEVC_DECODE_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga79b7f1b580d0cab34fc5616ae474660f) | h265로 디코딩 실패                   |
| -2305 | [VOD_PLAY_ERR_HLS_KEY](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa3130bf22ec63513ddca17ef3a24267a) | HLS 암호 해독 key 가져오기 실패             |
| -2306 | [VOD_PLAY_ERR_GET_PLAYINFO_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0b2d0a807f32a21c215eb0d523d1ba67) | VOD 파일의 정보 가져오기 실패           |
| 2106  | [VOD_PLAY_WARNING_HW_ACCELERATION_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaf669a195862852295bbfd67d77143097) | 하드웨어 디코더 시작 실패, 소프트웨어 디코더가 대신 사용됨         |
| -5    | [VOD_PLAY_ERR_INVALID_LICENSE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gafde8fcf56aeef512220ea06e92db2e40) | license가 유효하지 않아 재생 실패       |

### 재생 이벤트 매개변수

| 이벤트 정의                                                     | 설명                     |
| ------------------------------------------------------------ | ---------------------------- |
| [EVT_UTC_TIME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gafee483734d4d3a831a30c602406e77d6) | UTC 시간                      |
| [EVT_TIME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga5cb5e37938b510270847d4f5c751a594) | 이벤트 발생 시간                 |
| [EVT_DESCRIPTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga103453280f89ab536f1cc18f7b3cbf53) | 이벤트 설명                     |
| [EVT_PARAM1](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad627c73ec08206efdd221293acc5e716) | 이벤트 매개변수1                    |
| [EVT_PARAM2](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa15b5dbb07de07d1b2dbe14cfcd4c3f8) | 이벤트 매개변수2                    |
| [EVT_PLAY_COVER_URL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga40e4910ac679c2301b56d2b353782c45) | 비디오 썸네일                     |
| [EVT_PLAY_URL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gac913635a62c07ee774965c946db60cae) | 비디오 URL                     |
| [EVT_PLAY_NAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga018b2b66f3393288356448fd2520049b) | 비디오 이름                     |
| [EVT_PLAY_DESCRIPTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga78f0b6a56bce879ab53e5c955ae9b72a) | 비디오 소개                     |
| [EVT_PLAY_PROGRESS_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0aa1661deb8e647fab5fd9f49e80c7f9) | 재생 진행률(밀리초)             |
| [EVT_PLAY_DURATION_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga3abe5f92aa39728811ef148c2a9ad830) | 총 재생 시간(밀리초)             |
| [EVT_PLAY_PROGRESS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga3f1f479ffccbb042f9fdf3f21a3276fc) | 재생 진행률                     |
| [EVT_PLAY_DURATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga2c453eed399f105eec5803a3894ad81d) | 총 재생 시간                     |
| [EVT_PLAYABLE_DURATION_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga315c2ebea16fbabde6dfa05b46365ec1) | VOD 파일의 재생 가능 시간(밀리초)       |
| [EVT_PLAYABLE_RATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gab00428b5d3902980f809f281ab3113cd) | 재생 속도                     |
| [EVT_PLAYABLE_DURATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga27916804840b52c8b012c65f23f5295c) | VOD 파일의 재생 가능 시간               |
| [EVT_IMAGESPRIT_WEBVTTURL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gac5b62b9cd23553e5caa4ea25b8093594) | 이미지 스프라이트 web vtt 파일의 다운로드 URL |
| [EVT_IMAGESPRIT_IMAGEURL_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8b4b82a700fad6dc290c6b9df836b379) | 이미지 스프라이트의 다운로드 URL            |
| [EVT_DRM_TYPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8f621b0e05158b432a9bfce15b51929d) | 암호화 유형                     |
| [EVT_CODEC_TYPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9aea07e52f99dfc5ce83e627207c3013) | 비디오 인코딩 유형                 |
| [EVT_KEY_FRAME_CONTENT_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaf27d14de4e5ba1057f1687fb953bf0d6) | 비디오 키 프레임 설명 정보           |
| [EVT_KEY_FRAME_TIME_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaad3ea1d65ffad606f0e72b45229c883a) | 키 프레임 시간                   |

### 네트워크 상태 알림 매개변수 재생

| 이벤트 정의                                                     | 설명            |
| ------------------------------------------------------------ | ------------------- |
| [NET_STATUS_CPU_USAGE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga66b91ad00c61489fc2d7465999d1a77a) | CPU 사용률           |
| [NET_STATUS_VIDEO_WIDTH](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga12f4f516e8a103c43cf1fd3409e3a076) | 해상도 width       |
| [NET_STATUS_VIDEO_HEIGHT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaccbc5e1a57b7575b7ecf812cb939002e) | 해상도 height      |
| [NET_STATUS_VIDEO_FPS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga2ceaa8d4f26f94231cceb46ebc1ec01f) | 현재 비디오 프레임 레이트        |
| [NET_STATUS_VIDEO_GOP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gacd77aba1bb25077ecd03269c311479b8) | 현재 비디오 GOP         |
| [NET_STATUS_VIDEO_BITRATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa7190fc964cf23a567b56d9793ad5737) | 비디오 데이터의 비트레이트      |
| [NET_STATUS_AUDIO_BITRATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae77d554c71c9e298e09ae39cde8ff698) | 오디오 데이터의 비트레이트      |
| [NET_STATUS_NET_SPEED](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae2899ec3669bbf6261cead660c6e797c) | 네트워크 속도            |
| [NET_STATUS_AUDIO_CACHE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga71bf377ea1925873217c1c5ee600af53) | 오디오 프레임 수            |
| [NET_STATUS_VIDEO_CACHE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9e8fcc05e66967e0eb3348da202c7cde) | 비디오 프레임 수            |
| [NET_STATUS_AUDIO_INFO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga4107d46355fbcb54973cdfb82f25a2f4) | 현재 스트림의 오디오 정보    |
| [NET_STATUS_NET_JITTER](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga04f0c226d2b7571d07f118e05f43dc3a) | 네트워크 지터        |
| [NET_STATUS_SERVER_IP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0d7111f8bfbb9aba0d2ea9e2c8d6d7bd) | 연결된 Server IP |
| [NET_STATUS_VIDEO_DPS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga1ef238d0f43788fa5a5e01ea3d1cfce7) | 디코더에서 출력되는 비디오의 현재 프레임 레이트  |
| [NET_STATUS_QUALITY_LEVEL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8f86732d6a56638c8697c20e614c8d68) | 네트워크 품질            |

### 플레이어 미디어 자산 유형

| code | 이벤트 정의                                                     | 설명                  |
| ---- | ------------------------------------------------------------ | ------------------------- |
| 0    | [MEDIA_TYPE_AUTO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7d204fdc431c5c3ffea9f5da094edf5f) | auto 유형                  |
| 1    | [MEDIA_TYPE_HLS_VOD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae915784aa6e5b694a599cb79bb5f6051) | 어댑티브 비트레이트 스트리밍 hls VOD 미디어 자산 |
| 2    | [MEDIA_TYPE_HLS_LIVE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gacf7595f6e4617ad0da6e120ada7c7605) | 어댑티브 비트레이트 스트리밍 hls 라이브 스트림 미디어 자산 |

### 분류되지 않은 변수

| code | 이벤트 정의                                                     | 설명            |
| ---- | ------------------------------------------------------------ | ------------------- |
| -1   | [INDEX_AUTO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa49e56e7580286e85bce4c88feddb057) | 어댑티브 비트레이트 index |
