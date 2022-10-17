## TXVodPlayer

### VOD 플레이어

자세한 내용은 [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html)를 참고하십시오.
플레이어는 지정된 VOD 스트림 URL에서 오디오/비디오 데이터를 풀링하고 디코딩 및 로컬 렌더링 후 데이터를 재생합니다.
플레이어에는 다음과 같은 기능이 있습니다.

- FLV, MP4, HLS 파일은 기본 재생(URL 재생)과 VOD 재생(Fileid 재생)의 두 가지 재생 방법으로 재생할 수 있습니다.
- 비디오 스트림의 스크린샷을 캡처할 수 있습니다.
- 제스처를 통해 밝기, 음량, 재생 진행 상황을 조절할 수 있습니다.
- 비디오 해상도는 수동으로 전환하거나 현재 네트워크 대역폭에 맞게 자동으로 전환할 수 있습니다.
- 다른 재생 속도를 지정할 수 있고, 비디오를 수평으로 뒤집을 수 있으며, 하드웨어 가속을 활성화할 수 있습니다.
- 플레이어의 모든 기능에 대한 자세한 내용은 [비디오 재생 개요](https://intl.cloud.tencent.com/document/product/266/38295)를 참고하십시오.

### 플레이어 구성 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ae69bc2dd060217e595c38f0dc819290a) | 플레이어 구성 정보를 설정합니다. 구성에 대한 자세한 내용은 [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html)를 참고하십시오. |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | 플레이어의 렌더링 뷰 TXCloudVideoView를 설정합니다.                        |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aeb2f15f370d50b6261b7832f02a0f411) | 플레이어의 렌더링 뷰 TextureView를 설정합니다.                             |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | 플레이어의 렌더링 뷰 SurfaceView를 설정합니다.                             |
| setStringOption                                              | 플레이어 비즈니스 매개변수를 `<String,Object>` 형식으로 설정합니다.                |

### 기본 재생 API  
| API                                                          | 설명                       |
| ------------------------------------------------------------ | --------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | 지정된 HTTP URL에서 비디오 재생을 시작합니다. |
| startPlay | TXPlayInfoParams 매개변수를 전달하여 지정된 fileId의 비디오 재생을 시작합니다. |
| [ stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | 재생을 중지합니다. |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | 재생 진행 중 여부를 가져옵니다.      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | 스트림 데이터 가져오기를 중지하고 마지막 프레임 이미지를 유지하여 재생을 일시 중지합니다. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a41de8150eff044a237990c271d57ea27) | 스트림 데이터를 다시 가져와 재생을 재개합니다. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | 비디오 스트림의 지정된 시점(초)을 찾습니다. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aa5d7fcf690ac3a1102ffa3c02192674d) | 비디오 스트림의 지정된 시점(밀리초)을 찾습니다. |
| [getCurrentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a128b89dd39053d6d19d262a5f45110cd) | 현재 재생 시점을 초 단위로 가져옵니다. |
| [getBufferDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#acebd6ae9dd87e10c8959a24d3b6d5e7f) | 총 버퍼 지속 시간(초)을 가져옵니다. |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a83ee44393f1e0db930be75b73ff47812) | 총 비디오 지속 시간(초)을 가져옵니다. |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a37cb584556d48d043b93dfec33c40a97) | 재생 가능한 비디오 재생 시간(초)을 가져옵니다. |
| [getWidth](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a67a0997183f24da19b776d96c1052998) | 비디오 너비를 가져옵니다. |
| [getHeight](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a07efb2a4e9a982688c8bb3c3f21d1092) | 비디오 높이를 가져옵니다. |
| [setAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5e0e3d950eb3f525634adc7a9f60eab7) | startPlay 호출 후 VOD 자동 시작 여부를 설정합니다. VOD는 기본적으로 자동 시작됩니다. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a8f767f79fb69496cdbc532fced5dff33) | 재생 시작 시간을 설정합니다. |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5f9eadc88ca97238f84226462f095536) | HLS 암호화를 위한 token을 설정합니다. |
| [setLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a3f5ae863c82509d1ed266503e8138781) | 비디오 반복 여부를 설정합니다. |
| [isLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aaa3fcc823e0fce316dea1cc9162f1c8e) | 루프 재생 상태를 반환합니다. |

### 비디오 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | 비디오 하드웨어 디코딩을 활성화/비활성화합니다.                                       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6f1c0c128052960f084ef6d1d7a77b09) | 현재 비디오 프레임 이미지를 가져옵니다. <br>**참고: 이 작업은 시간이 많이 걸리므로 스크린샷은 비동기식으로 다시 호출됩니다.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a4add579d2ec825502c5e3832aced5bc1) | 미러 이미지를 설정합니다.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#add2bcd36c051900d697853155494865b) | VOD 재생 속도를 설정합니다. 기본값: 1.0.                                |
| [getBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#af6f9e1e680baa611642fb168007b1c45) | 현재 재생 비트 레이트 인덱스를 반환합니다.                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a61f524a6ed275edaf9e9a0997f64d491) | 원활한 해상도 전환을 위한 현재 재생 비트 레이트 인덱스를 설정합니다. 해상도를 전환하려면 잠시 기다려야 할 수도 있습니다. |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | [이미지 채우기 모드](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)를 설정합니다. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | [이미지 렌더링 각도](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)를 설정합니다. |

### 오디오 API

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | --------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | 플레이어 음소거 여부를 설정합니다.                      |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | 볼륨 레벨을 설정합니다. 값 범위: 0–100.           |
| [setRequestAudioFocus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a676f0935eca038719f58100d31f169b1) | 오디오 포커스 자동 가져오기 여부를 설정합니다. 오디오 포커스는 기본적으로 자동 가져오기 됩니다. |

### 이벤트 공지 API

| API                      | 설명                   |
| ---------------------- | ---------------------- |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a0735b006fe8c56875665cb66881af144) | 플레이어 콜백을 설정합니다(사용되지 않았으므로 대신 [setVodListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61)를 사용하는 것이 좋습니다). |
| [setVodListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) | 플레이어 콜백을 설정합니다.                                 |
| [onNotifyEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a1e4be8c3cfef68a8909d66a9243b6ec5) | VOD 재생 이벤트 알림입니다.                                 |
| [onNetSuccess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ae6febac01c1cba85f8fe387a0c14d9d0) | VOD 네트워크 상태 알림입니다.                             |
| [onNetFailed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a74942758292eb41138c7a01ed9056da2) | fileId에 의한 재생에 대한 네트워크 예외 알림입니다.                         |

### TRTC API

다음 API를 사용하여 VOD 플레이어의 오디오/비디오 스트림을 TRTC를 통해 푸시할 수 있습니다. TRTC 서비스에 대한 자세한 내용은 TRTC [제품 개요](https://intl.cloud.tencent.com/document/product/647/35078) 페이지를 참고하십시오.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ad6bd04b37a89012102e7bb71ea5554a6) | VOD를 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)에 바인딩합니다. |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5b947acf9f4fc992f0f02f8d87de3334) | [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)에서 VOD 바인딩을 해제합니다. |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a8298f704cb659c725da28a27e08afbed) | 비디오 스트림 푸시를 시작합니다.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aaa6ecf72bfa9e35078561dd98d62be0c) | 비디오 스트림 푸시를 취소합니다.                                             |
| [ publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | 오디오 스트림 푸시를 시작합니다.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a206d786a74ae3b71766755135161773e) | 오디오 스트림 푸시를 취소합니다.                                             |

## ITXVodPlayListener

VOD 콜백 공지입니다.
### 기본 SDK 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXVodPlayListener__android.html#aad1d875808cd4a68d429762e492aad05) | VOD 재생 이벤트 알림. 자세한 내용은 [재생 이벤트 목록](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) 및 [이벤트 매개변수](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)를 참고하십시오. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXVodPlayListener__android.html#a2be0a0294ae21e68e736ac8fa4d3085d) | VOD 플레이어의 [네트워크 상태 알림](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737). |

## TXVodPlayConfig

VOD 플레이어 구성 클래스입니다.

### 기본 구성 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | 플레이어의 최대 재접속 시도 횟수를 설정합니다.                                         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | 플레이어 재연결 간격을 초 단위로 설정합니다.                                 |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#ae44a6096c42cdb61adc10370ca2a42b6) | 플레이어 연결 제한 시간(초)을 설정합니다.                             |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a6ad0d546e6da3abacd5d4ea8bd6f94de) | MP4 및 HLS 파일에 적용되는 VOD 캐시 디렉터리를 설정합니다.                       |
| [setMaxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#acc2f17764df9bb52163dac9faf81f11e) | 최대 캐시 파일 수를 설정합니다. 이 API는 더 이상 사용되지 않습니다. 전역 구성을 위해 TXPlayerGlobalSetting#setMaxCacheSize를 사용합니다. |
| [setPlayerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a3594024855210dc07f50a6d7c5f8b088) | 플레이어 유형을 설정합니다.                                             |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | 사용자 정의 HTTP headers를 설정합니다.                                    |
| [setEnableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a3caff179964976945f3754f1ec48a42b) | 정확한 seek 활성화 여부를 설정합니다. 기본값: true.                               |
| [setAutoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#ab360b681c220c2adb57de2758916b227) | YES로 설정하면 MP4 파일이 설정된 회전 각도에 따라 자동으로 회전됩니다.<br>회전 각도는 PLAY_EVT_CHANGE_ROTATION 이벤트에서 얻을 수 있습니다. 기본값: YES. |
| [setSmoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a23fb393011e4663d0dfa765b72665a46) | 다중 비트 레이트 HLS 스트림에 대해 부드러운 전환 활성화 여부를 설정합니다. 기본값: false.                             |
| [setCacheMp4ExtName](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#aaeccb662be133d4ded4fc17df29b94b5) | 캐시된 MP4 파일 확장자를 설정합니다.                                        |
| [setProgressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a01a46ce89e4979a6397b6deb2525007c) | 진행 콜백 간격을 밀리초 단위로 설정합니다.                                 |
| [setMaxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a2705841bfedb3c44839cc355eaad26dc) | 최대 사전 로딩 버퍼 크기를 MB 단위로 설정합니다.                                    |
| setMaxPreloadSize                                            | 최대 사전 로딩 버퍼 크기를 MB 단위로 설정합니다.                           |
| setExtInfo                                                   | 확장 정보를 설정합니다.                                               |
| setPreferredResolution                                       | HLS 비트스트림이 여러 개인 경우 구성된 preferredResolution 에 따라 가장 선호하는 비트스트림 재생을 시작합니다. 여기서 preferredResolution은 비디오 너비와 높이를 곱한 것(width * height)으로 재생이 시작되기 전에 설정된 경우에만 효과가 나타납니다. |

## TXPlayerGlobalSetting

VOD 플레이어의 전역 구성입니다.

| API                | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | 재생 엔진의 cache 디렉터리를 설정합니다. 설정 후 다운로드, 사전 다운로드 및 플레이어 사용 중에 이 디렉터리를 먼저 읽어와 저장합니다. |
| setMaxCacheSize    | 재생 엔진의 최대 캐시 크기를 MB 단위로 설정합니다. 설정 후 백엔드는 설정 값에 따라 Cache 디렉터리의 파일을 자동으로 지웁니다. |

## TXVodPreloadManager

VOD 플레이어의 API 클래스 사전 다운로드

| API          | 설명                                                         |
| ------------ | ------------------------------------------------------------ |
| getInstance  | 싱글톤 모드에서 TXVodPreloadManager 인스턴스 객체를 가져옵니다.                    |
| startPreload | 사전 다운로드를 시작하기 전에 재생 엔진 캐시 디렉터리 TXPlayerGlobalSetting#setCacheFolderPath 및 캐시 크기TXPlayerGlobalSetting#setMaxCacheSize를 설정합니다. |
| stopPreload  | 사전 다운로드를 중지합니다.                                                   |

## TXVodDownloadManager 

VOD 플레이어의 비디오 다운로드 API 클래스입니다. 현재 중첩되지 않은 m3u8 비디오만 다운로드할 수 있습니다. simpleAES로 암호화된 영상은 보안을 강화하기 위해 Tencent Cloud의 개인 암호화 알고리즘으로 다시 암호화됩니다.

| API                      | 설명                                                         |
| ------------------------ | ------------------------------------------------------------ |
| getInstance              | 싱글톤 모드에서 TXVodDownloadManager 인스턴스 객체를 가져옵니다.                   |
| setHeaders               | 다운로드 HTTP 헤더를 설정합니다.                                               |
| setListener              | 다운로드 전에 설정해야 하는 다운로드 콜백 방법을 설정합니다.                             |
| startDownloadUrl         | 지정된 URL에서 비디오 다운로드를 시작합니다.                                          |
| startDownload            | 지정된 fileid 의 비디오 다운로드를 시작합니다.                                         |
| stopDownload             | 다운로드를 중지합니다. ITXVodDownloadListener.onDownloadStop이 다시 호출되면 다운로드가 성공적으로 중지됩니다. |
| deleteDownloadMediaInfo  | 다운로드 정보를 삭제합니다.                                                 |
| getDownloadMediaInfoList | 모든 사용자의 다운로드 목록을 가져옵니다.                                   |
| getDownloadMediaInfo     | 다운로드 정보를 가져옵니다.                                   |

## ITXVodDownloadListener

VOD 다운로드 공지입니다.

| API                | 설명                                         |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | 다운로드 시작                                     |
| onDownloadProgress | 다운로드 진행률 업데이트                                 |
| onDownloadStop     | 다운로드 중지                                     |
| onDownloadFinish   | 다운로드 종료                                     |
| onDownloadError    | 다운로드 중 오류 발생                           |


## TXVodDownloadDataSource

다운로드 중에 매개변수로 전달할 수 있는 Tencent Cloud 비디오 fileid 다운로드 소스.

| API                        | 설명                                         |
| ------------------         | -------------------------------------------- |
| TXVodDownloadDataSource    | appid, fileid, quality, pSign 및 username과 같은 매개변수를 전달하는 함수 빌드                                    |
| getAppId  | 전달된 appid 가져오기                                |
| getFileId  | 전달된 fileid 가져오기                                |
| getPSign     | 전달된 psign 가져오기                                     |
| getQuality   | 전달된 quality 가져오기                                     |
| getUserName    | 전달된 userName 가져오기, 기본은 “default”                          |


## TXVodDownloadMediaInfo

다운로드 진행 상황 및 재생 링크 등 Tencent Cloud VOD 다운로드 정보

| API                        | 설명                                         |
| ------------------         | -------------------------------------------- |
| getDataSource    | fileid가 비디오 다운로드를 위해 전달한 fileid 로 지정된 다운로드 소스 가져오기                                    |
| getDuration  | 다운로드한 비디오의 총 재생 시간 가져오기                                |
| getPlayableDuration  | 다운로드한 비디오의 재생 가능 시간 가져오기                                |
| getSize     | 다운로드 중인 파일의 전체 크기를 가져옵니다. 이 API는 fileid로 다운로드할 때만 적용           |
| getDownloadSize   | 다운로드한 파일의 크기를 가져옵니다. 이 API는 fileid에 의한 다운로드에만 적용                                    |
| getProgress    | 현재 다운로드 진행률 가져오기                         |
| getPlayPath    | 재생을 위해 TXVodPlayer에 전달할 수 있는 현재 재생 경로 가져오기                         |
| getDownloadState    | 다운로드 상태 가져오기                       |
| isDownloadFinished    | 다운로드 완료 여부 결정                       |


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

| code   | 이벤트 정의                                  | 설명                                                    |
| ------ | ------------------------------------- | ------------------------------------------------------- |
| \-2301 | PLAY\_ERR\_NET\_DISCONNECT            | 네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없습니다. 플레이어를 다시 시작하여 더 많은 연결 재시도를 수행할 수 있습니다.                           |
| \-2305 | PLAY\_ERR\_HLS\_KEY                   | HLS 암호 해독 key를 가져오는 데 실패했습니다.                                        |
| 2101   | PLAY\_WARNING\_VIDEO\_DECODE\_FAIL    | 현재 비디오 프레임을 디코딩하는 데 실패했습니다.                                              |
| 2102   | PLAY\_WARNING\_AUDIO\_DECODE\_FAIL    | 현재 오디오 프레임 디코딩 실패입니다.                                               |
| 2103   | PLAY\_WARNING\_RECONNECT              | 네트워크 연결이 끊어지고 자동 재연결이 수행되었습니다(세 번 실패하면 PLAY_ERR_NET_DISCONNECT 이벤트가 발생합니다). |
| 2106   | PLAY\_WARNING\_HW\_ACCELERATION\_FAIL | 하드웨어 디코더를 시작하는 데 실패했으며 소프트웨어 디코더가 대신 사용되었습니다.                                            |
| \-2304 | PLAY\_ERR\_HEVC\_DECODE\_FAIL         | H265로 디코딩하는 데 실패했습니다.                                              |
| \-2303 | PLAY\_ERR\_FILE\_NOT\_FOUND           | 재생할 파일이 존재하지 않습니다.                                               |
