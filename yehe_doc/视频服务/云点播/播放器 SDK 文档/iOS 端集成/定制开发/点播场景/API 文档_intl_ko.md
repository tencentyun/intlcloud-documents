## TXVodPlayer

### VOD 플레이어

자세한 내용은 [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html)를 참고하십시오.
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
| [config](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | VOD를 구성합니다. 구성에 대한 자세한 내용은 [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html)를 참고하십시오. |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | startPlay 호출 직후 재생 시작 여부를 설정합니다. 기본값: YES.                         |
| [token](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | HLS 암호화를 위한 token을 설정합니다. 토큰이 설정되면 플레이어는 URL의 파일 이름 앞에 `voddrm.token.TOKEN TextureView`를 자동으로 추가합니다. |
| [loop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | SurfaceView 반복 여부를 설정합니다.                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | 비디오 렌더링 콜백을 설정합니다.(하드웨어 인코딩에서만 지원)                                 |
| [setExtentOptionInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a842c8863f91f274031be0109a5cb28f5) | `<NSString *, id>` 형식으로 플레이어 비즈니스 매개변수를 설정합니다.             |

### 기본 재생 API  
| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ac1af59fe9e4bc2b390661787097d2c8b) | 지정된 HTTP URL에서 비디오 재생을 시작합니다. |
| [startPlayDrm:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaa492de602b58d75b0489435b20be811) | 표준 Fairplay drm으로 암호화된 파일 재생을 시작합니다.                 |
| [startPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a0b4db90eafbc8c4d9be498e5ffefe961) | 지정된 fileId의 비디오 재생을 시작합니다. |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | 재생을 중지합니다. |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | 재생 진행 중 여부를 가져옵니다.      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 스트림 데이터 가져오기를 중지하고 마지막 프레임 이미지를 유지하여 재생을 일시 중지합니다. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 스트림 데이터를 다시 가져와 재생을 재개합니다. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | 비디오 스트림의 지정된 시점(초)을 찾습니다. |
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | 현재 재생 시점을 초 단위로 가져옵니다. |
| [duration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | 총 비디오 지속 시간(초)을 가져옵니다. |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | 재생 가능한 비디오 재생 시간(초)을 가져옵니다. |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | 비디오 너비를 가져옵니다. |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | 비디오 높이를 가져옵니다. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | 재생 시작 시간을 설정합니다. |
| [setupVideoWidget:insertIndex:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a370c35a44549bad3a162741c288b8eb8) | Video 렌더링 View를 생성합니다. 이 컨트롤은 비디오 콘텐츠를 표시합니다. |
| [removeVideoWidget](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#adf77d29895e70602556fdc51b931951e) | Video 렌더링 View를 제거합니다.                            |

### 비디오 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | 현재 비디오 프레임 이미지를 가져옵니다. <br>**참고: 이 작업은 시간이 많이 걸리므로 스크린샷은 비동기식으로 다시 호출됩니다.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | 비디오 이미지 수평 뒤집기 여부를 설정합니다.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | VOD 재생 속도를 설정합니다. 기본값: 1.0.                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | 현재 재생 비트 레이트 인덱스를 반환합니다.                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | 원활한 해상도 전환을 위한 현재 재생 비트 레이트 인덱스를 설정합니다. <br>해상도를 전환하려면 잠시 기다려야 할 수도 있습니다. |
| [supportedBitrates](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1c7f996e3c1e5ec04fe3f3b184491495) | 재생 주소가 master playlist인 경우 지원되는 비트레이트(해상도)를 반환합니다.     |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | [이미지 채우기 모드](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)를 설정합니다. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | [이미지 렌더링 각도](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)를 설정합니다. |
| [enterPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ae0118065e4d29cb7dbab4ccd0ba6b3e5) | PIP(Picture In Picture) 모드로 전환합니다.                                             |
| [exitPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a5f0bc0ade6e99f31392f6f8d897ae84c) | PIP 모드를 종료합니다                                             |

### 오디오 API

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | 플레이어 음소거 여부를 설정합니다.            |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | 볼륨 레벨을 설정합니다. 값 범위: 0 – 100. |

### 이벤트 공지 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | 이벤트 콜백. [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) 사용을 권장합니다. |
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | 플레이어 콜백을 설정합니다.                                 |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | 비디오 렌더링 콜백을 설정합니다(하드웨어 인코딩에서만 지원).                  |

### TRTC API

다음 API를 사용하여 VOD 플레이어의 오디오/비디오 스트림을 TRTC를 통해 푸시할 수 있습니다. TRTC 서비스에 대한 자세한 내용은 TRTC [제품 개요](https://cloud.tencent.com/document/product/647/16788)를 참고하십시오.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | VOD를 [TRTC](https://cloud.tencent.com/document/product/647/16788)에 바인딩합니다. |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | [TRTC](https://cloud.tencent.com/document/product/647/16788)에서 VOD 바인딩을 해제합니다. |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | 비디오 스트림 푸시를 시작합니다.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | 비디오 스트림 푸시를 취소합니다.                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | 오디오 스트림 푸시를 시작합니다.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | 오디오 스트림 푸시를 취소합니다.                                             |

### 클래스 메소드

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [getEncryptedPlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#acdb2823140afb92657f840b7b765636d) | 암호화된 재생 키 가져오기.                            |
| [isSupportPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a2b0eae752e8cd548572e747a85602c71) | Picture In Picture(PIP) 기능 지원 여부. |

## TXVodPlayListener

VOD 콜백 공지입니다.
### 기본 SDK 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent:event:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | VOD 재생 이벤트 공지입니다. 자세한 내용은 [재생 이벤트 목록](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) 및 [이벤트 매개변수](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)를 참고하십시오. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | VOD 플레이어 [네트워크 상태 공지](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)입니다. |
| [onPlayer:pictureInPictureStateDidChange:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#ac0e5e698f62a9d8a58b0e8e63fc8afb1) | PIP 상태 콜백입니다.                                             |
| [onPlayer:pictureInPictureErrorDidOccur:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a4dcee189760af5752bd112a725994d0b) | PIP 오류 상태 콜백입니다.                                         |

## TXVodPlayConfig

VOD 플레이어 구성 클래스입니다.

### 기본 구성 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | 플레이어의 최대 재접속 시도 횟수를 설정합니다.                                         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | 플레이어 재연결 간격(초)을 설정합니다.                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | 플레이어 연결 제한 시간(초)을 설정합니다.                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | 이 API는 더 이상 사용되지 않으므로, [TXPlayerGlobalSetting##setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html) 사용을 권장합니다.  <br>VOD MP4 및 HLS 파일에 적용되는 비디오 캐시 디렉터리입니다. |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | 이 API는 더 이상 사용되지 않으므로, [TXPlayerGlobalSetting#setMaxCacheSizeMB](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html) 사용을 권장합니다. <br>최대 캐시 파일 수입니다. |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | 플레이어 유형을 설정합니다.                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | 사용자 정의 HTTP headers를 설정합니다.                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | 정확한 seek 활성화 여부를 설정합니다. 기본값: true.                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | MP4 파일 재생 시 YES로 설정하면 파일에 설정된 회전 각도에 따라 자동으로 회전됩니다. <br>회전 각도는 PLAY_EVT_CHANGE_ROTATION 이벤트에서 얻을 수 있습니다. 기본값: YES. |
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | 다중 비트 레이트 HLS 스트림에 대해 부드러운 전환 활성화 여부를 설정합니다. 기본값: false.                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | 진행 콜백 간격을 밀리초 단위로 설정합니다.                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | 최대 사전 로딩 버퍼 크기를 MB 단위로 설정합니다.                                    |
| [maxPreloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3ae31483070f62cf35abd9003ccce0e0) | 최대 사전 로딩 버퍼 크기(MB)를 설정합니다.                           |
| [firstStartPlayBufferTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a5a6373341623385672a12e9e3617c1c2) | 첫 번째 버퍼링의 비디오 데이터 로딩 지속 시간(ms)을 설정합니다. 기본값: 100ms.          |
| [nextStartPlayBufferTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ab17865763b40e7d86913dd2c6fb3110f) | 버퍼링(충분하지 않은 버퍼링된 데이터에 대한 보조 버퍼링 또는 seek로 인한 진행률 표시줄 드래그 버퍼링) 시 버퍼링 중지까지의 최소 데이터 크기(ms)입니다. 기본값: 250ms. |
| [overlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#adc41276c8fa265cb622657b581ba3f3b) | HLS 보안 강화 암호화/복호화 key를 설정합니다.                                |
| [overlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3de0b922b54d46f11a8e203026d44fed) | HLS 보안 강화 암호화/복호화 Iv를 설정합니다.                                 |
| [extInfoMap](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a55b7d33d270ac9004aad798bd6027879) | 확장 정보를 설정합니다.                                               |
| [preferredResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#afcfb593028655bbac25a753f8ffe9904) | HLS 비트스트림이 여러 개인 경우 구성된 preferredResolution에 따라 최적의 비트스트림을 선택하여 방송을 시작 *합니다. 여기서, preferredResolution은 비디오 너비와 높이(width * height)의 곱으로, 재생이 시작되기 전에 설정된 경우에만 적용됩니다 |
| [enableRenderProcess](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3b7f6694446ab09764315f003192fc5a) | 기본적으로 활성화되어 있는 초해상도 플러그 인과 같은 포스트렌더링 및 포스트프로덕션 기능 허용 여부를 설정합니다.     |
| [playerPixelFormatType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ac1ae36ec22cc49f49ceb7842cb86be3b) | 비디오 렌더링 객체에서 호출하는 비디오 형식입니다.                                 |
| [keepLastFrameWhenStop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ace241f4953a14aac301ecd1e196de3f8) | stopPlay가 호출될 때 마지막 이미지 프레임 유지 여부입니다. 기본값: NO.           |
| [mediaType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a5877610faab7f5148bc34072a0c92a5b) | 미디어 자산 유형을 설정합니다.                                               |
|                                                              |                                                              |

## TXPlayerGlobalSetting

VOD 플레이어의 전역 구성입니다.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__ios.html#a604b66ab880e7a5d056ce5c3132ddf48) | 플레이어 엔진의 캐시 디렉터리를 설정합니다. 설정 후 이 디렉터리는 사전 다운로드 및 플레이어 사용 시 먼저 읽기 및 저장됩니다. |
| [setMaxCacheSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__ios.html#ad511345d985ae9bc271a1e867c3f71f0) | 플레이어 엔진의 최대 캐시 크기를 설정합니다. 설정 후 백엔드는 설정 값에 따라 Cache 디렉터리의 파일을 자동으로 지웁니다. 단위 MB. |

## TXVodPreloadManager

VOD 플레이어의 API 클래스 사전 다운로드

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a84882e4d61f22f51a18d3b639d881138) | 싱글톤 모드에서 TXVodPreloadManager 인스턴스 객체를 가져옵니다.                |
| [startPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#af67a02c9fba5c07f83b2d36d24b764fd) | 사전 다운로드를 시작하기 전에 재생 엔진 캐시 디렉터리 TXPlayerGlobalSetting#setCacheFolderPath 및 캐시 크기 TXPlayerGlobalSetting#setMaxCacheSize를 설정합니다. |
| [stopPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a5c29884349c8f6436eff8f70f302d33e) | 사전 다운로드 중지                                                   |

### 비디오 사전 다운로드 콜백

| API                                                          | 설명        |
| ------------------------------------------------------------ | -------------- |
| [onComplete:url:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#aa887ac7b6bcf155eb22816f880eed270) | 다운로드 완료 콜백입니다. |
| [onError:url:error:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a07e337f1e638e458a3e761507deec525) | 다운로드 오류 콜백입니다. |

## TXVodDownloadManager

VOD 플레이어의 동영상 다운로드 API 클래스

### TXVodDownloadDataSource

| API                                                          | 설명                  |
| ------------------------------------------------------------ | ------------------------- |
| [auth](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a59eb64ffe11d0bdee5c67009f5ebdd8c) | fileid 정보                |
| [quality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ab674303410c354ab3d0d6957b86dcf14) | 다운로드 해상도. 기본값: 원본 해상도       |
| [token](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a2f0d5a61a262b1362f51c943b6a03f17) | 주소가 암호화된 경우 token 입력 |
| [templateName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0c960f307400330cb261513cde7c2906) | 해상도 템플릿                |
| [fileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a66c446aeaf5eef1ee21764d4bdf7b8ae) | 파일 Id                    |
| [pSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0411129c1f5cf0bdfac7baabeb12c7a2) | 서명 정보                  |
| [appId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a5b3217c0ab223c526d557b09d2b0d6c0) | 애플리케이션의 appId. 필수          |
| [userName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac38202c6f4861ad216f9fbc5d962b5ab) | 계정 이름                  |
| [overlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adc41276c8fa265cb622657b581ba3f3b) | HLS EXT-X-KEY 암호화/복호화 매개변수  |
| [overlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a3de0b922b54d46f11a8e203026d44fed) | 암호화/복호화 매개변수 overlayIv      |

### TXVodDownloadMediaInfo

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------- |
| [isDownloadFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#aca53b9773ade9052bc8ff2592bea0c01) | 다운로드 완료 여부                    |
| [dataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a74a85fcd734fe688c3a65083dc815a6a) | fileid 다운로드 객체(옵션)          |
| [url](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a43481294fa1d2f0ebe7cff14b17726cc) | 다운로드 url                         |
| [userName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac38202c6f4861ad216f9fbc5d962b5ab) | 계정 이름                        |
| [duration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac6e4b2a3cf932b33832d4e4e4e7cd0de) | 지속 시간                            |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a1945ed3669e000f80e294331d6c302b4) | 재생 가능 시간                      |
| [size](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a439227feff9d7f55384e8780cfc2eb82) | 총 파일 크기(byte)          |
| [downloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a15989d553be239ea233f9957236fa767) | 다운로드한 파트의 크기(byte)          |
| [segments](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a32e4172d8952ac9f1db668982da57128) | 총 세그먼트 수                        |
| [downloadSegments](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac2e85e36301b166ed1bb92844f6f5399) | 다운로드한 세그먼트 수                  |
| [progress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac7abb4766cd3f65c31f56279d7decff8) | 진행률                            |
| [playPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a6567e969a0aa9ef88a4a2ff601ea8527) | 재생을 위해 TXVodPlayer에 전달할 수 있는 재생 경로 |
| [speed](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a218b4f7c6cc2681a99c23a3b089d68b1) | 다운로드 속도(byte/s)              |
| [downloadState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ae87c7de3c7e2888cfe6298bc25c4f9be) | 다운로드 상태                        |

### TXVodDownloadManager

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [shareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a8a1039302b46bec56fcc15c2ffdcbf16) | 싱글톤 모드에서 TXVodDownloadManager 인스턴스 객체를 가져옵니다.               |
| [setDownloadPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a5ca035da8c8f8771f08fe15c6857a304) | 다운로드 루트 디렉터리를 설정합니다.                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ad69aaf8885027863ea19657425ef1974) | 다운로드 HTTP 헤더를 설정합니다.                                           |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a507e1dcc250a5764bd84d6e8a6598b23) | 다운로드 콜백 방식을 설정합니다. 다운로드하기 전에 설정해야 합니다.                           |
| [startDownloadUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac886a33c24af3bea16b4b2b9ab1bcfde) | 지정된 URL에서 비디오 다운로드를 시작합니다.                                        |
| [startDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a6093eec0836566ad15a4fdeb2b0682e9) | 지정된 FileID의 비디오 다운로드를 시작합니다.                                     |
| [stopDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#af1c09ed1089c935a46d6f9d8f1587dc4) | 다운로드를 중지합니다. ITXVodDownloadListener.onDownloadStop이 다시 호출되면 다운로드가 성공적으로 중지됩니다. |
| [deleteDownloadFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a9564ad5e676445ffe2cccdbfacfd7b11) | 다운로드한 파일을 삭제합니다.                                               |
| [deleteDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a8f38d437419ecbe1d906e5826893194e) | 다운로드 정보를 삭제합니다.                                               |
| [getDownloadMediaInfoList](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adad0276021a21fdfca8b1925b8c46ca5) | 모든 사용자의 다운로드 목록을 가져옵니다.                                 |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a255dd9b7ce63b862e0674ba144a68aac) | 다운로드 정보를 가져옵니다.                                               |
| [getOverlayKeyIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a4b0e452471aa28879bd855886127bcfd) | HLS EXT-X-KEY를 가져옵니다.                                          |
| [genRandomHexStringForHls](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0c96770dd135d266dfc14779fedad775) | 암호화 구성 암호화를 위한 임의의 숫자를 가져옵니다.                                             |
| [encryptHexStringHls:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ab6277c0f8c42ee94a1a56055ead6ea13) | 암호화합니다.                                                       |

### TXVodDownloadDelegate

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [onDownloadStart](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ad375a3205d19472a2e5f22fbce384f6a) | 다운로드가 시작되었습니다.                                        |
| [onDownloadProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a7fcc9b089f4cabcd1b843fdccbd7f58b) | 다운로드 진행률이 업데이트되었습니다.                                    |
| [onDownloadStop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a11ad404425936a29dd9f2edc1aaca8f6) | 다운로드가 중지되었습니다.                                        |
| [onDownloadFinish](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a4453811b7217726930d8f05b62cc4902) | 다운로드가 종료되었습니다.                                        |
| [onDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adf5abf41239950b68347a085704db523) | 다운로드 중 오류가 발생했습니다.                              |
| [hlsKeyVerify](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a32e5b4e7d5eaa14a9b144747e174390f) | HLS 스트림 다운로드 중에 암호화된 파일이 발견되면 플레이어가 암호 해독 Key를 확인합니다. |

### [TXDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga625ad66cfaed6a449961936a37740dd9)

다운로드 오류 코드

| 열거 값                | 설명           |
| --------------------- | ------------------ |
| TXDownloadSuccess     | 다운로드 완료           |
| TXDownloadAuthFaild   | fileid 인증 실패     |
| TXDownloadNoFile      | 이 해상도 파일 없음     |
| TXDownloadFormatError | 미지원 형식         |
| TXDownloadDisconnet   | 네트워크 연결 끊김           |
| TXDownloadHlsKeyError | HLS 암호 해독 key 가져오기 실패 |
| TXDownloadPathError   | 다운로드 디렉터리 액세스 실패   |

### [TXVodDownloadMediaInfoState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga7378c6cdd737126deb060ee3eb31f00a)

다운로드 상태

| 열거 값                            | 설명   |
| --------------------------------- | ---------- |
| TXVodDownloadMediaInfoStateInit   | 초기 다운로드 상태 |
| TXVodDownloadMediaInfoStateStart  | 다운로드 시작   |
| TXVodDownloadMediaInfoStateStop   | 다운로드 중지   |
| TXVodDownloadMediaInfoStateError  | 다운로드 오류   |
| TXVodDownloadMediaInfoStateFinish | 다운로드 완료   |

### [TXVodQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga7079416c4ef1fec0f33755d7a2bc7c58)

다운로드한 비디오의 해상도

| 열거 값          | 설명 |
| --------------- | -------- |
| TXVodQualityOD  | 기존 해상도     |
| TXVodQualityFLU | LD     |
| TXVodQualitySD  | SD     |
| TXVodQualityHD  | HD     |
| TXVodQualityFHD | FHD   |
| TXVodQuality2K  | 2K       |
| TXVodQuality4K  | 4K       |

## TXPlayerAuthParams

fileId로 암호화된 비디오 재생을 설정합니다

| API                                                          | 설명                 |
| ------------------------------------------------------------ | -------------------- |
| [appId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a5b3217c0ab223c526d557b09d2b0d6c0) | 애플리케이션 appId.         |
| [fileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a66c446aeaf5eef1ee21764d4bdf7b8ae) | 파일 id.             |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a4f13e124e054004dcd7930ecd6df0f57) | 암호화된 링크 시간 초과 타임스탬프. |
| [exper](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a9e4e9de0c34814be700575f5ebdf725e) | 미리 보기 지속 시간.           |
| [us](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a6a5fc78b476fcbcdcc2a9888faa75ea3) | 고유한 요청 식별.       |
| [sign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a37aa22c94233901cd1afee101f759348) | 링크 도용 방지 서명.         |
| [https](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a33d23e482c312a90cae72781bdfa1c4a) | https 요청 사용 여부.    |

## TXBitrateItem

HLS 다중 비트레이트 정보

| API                                                          | 설명             |
| ------------------------------------------------------------ | ------------------- |
| [index](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#a43d1d245fab4496928fe2e287fdc3f59) | m3u8 파일 스트림 번호. |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#ab581e554cfc9559c9e2cd57ecf126d02) | 이 스트림의 비디오 너비.    |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#a1cdeaaebe1687fd7b3237fd45e3d5740) | 이 스트림의 비디오 높이.    |
| [bitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#abee909d3e29c2c87de16464920736759) | 이 스트림의 비디오 비트레이트.    |

## TXImageSprite

스프라이트 이미지 리졸브 툴입니다.

| API                                                          | 설명             |
| ------------------------------------------------------------ | ---------------- |
| [setVTTUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__ios.html#a0075e38dc6b4291851c35f896ce7a28d) | 이미지 스프라이트 URL을 설정합니다. |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__ios.html#a4561e9ea43d7273caf9197d96f5f7307) | 썸네일을 가져옵니다.     |

## TXPlayerDrmBuilder

VOD Drm Constructor.

| API                                                          | 설명             |
| ------------------------------------------------------------ | ---------------- |
| [certificateUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#a24e49ee9ffc468e63b10c120af3a842f) | 인증서 공급자 URL. |
| [keyLicenseUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#a1d393eafdb9cc90f7f6beeeb8eb94157) | 암호 해독 key의 URL.   |
| [playUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#ab08c768d03824654011cf36aedc16193) | 재생 URL.       |

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
| ----- | --------------------------------- | ------------------------------------------------------------ |
| -2301 | PLAY_ERR_NET_DISCONNECT           | 네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없습니다. 플레이어를 다시 시작하여 더 많은 연결 재시도를 수행할 수 있습니다.    |
| -2305 | PLAY_ERR_HLS_KEY                  | HLS 암호 해독 key를 가져오는 데 실패했습니다.                                      |
| 2101  | PLAY_WARNING_VIDEO_DECODE_FAIL    | 현재 비디오 프레임을 디코딩하는 데 실패했습니다.                                         |
| 2102  | PLAY_WARNING_AUDIO_DECODE_FAIL    | 현재 오디오 프레임을 디코딩하는 데 실패했습니다.                                         |
| 2103  | PLAY_WARNING_RECONNECT            | 네트워크 연결이 끊어지고 자동 재연결이 수행되었습니다(세 번의 시도 실패 후 PLAY_ERR_NET_DISCONNECT 이벤트 발생). |
| 2106  | PLAY_WARNING_HW_ACCELERATION_FAIL | 하드웨어 디코더를 시작하는 데 실패했으며 소프트웨어 디코더가 대신 사용되었습니다.                                     |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL         | H265로 디코딩하는 데 실패했습니다.                                              |
| -2303 | PLAY_ERR_FILE_NOT_FOUND           | 재생할 파일이 존재하지 않습니다.                                           |

## 플레이어 SDK 상수

### [이벤트 코드 및 오류 코드 정의](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#gabc22cbb50603d49430a22f2812d9e616)

| 열거 값                                   | 의미                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| VOD_PLAY_EVT_RCV_FIRST_I_FRAME           | 재생 이벤트: 첫 번째 비디오 프레임을 성공적으로 수신                             |
| VOD_PLAY_EVT_RCV_FIRST_AUDIO_FRAME       | 재생 이벤트: 첫 번째 오디오 프레임을 성공적으로 수신                             |
| VOD_PLAY_EVT_PLAY_BEGIN                  | 재생 이벤트: 재생 시작됨                                       |
| VOD_PLAY_EVT_PLAY_PROGRESS               | 재생 이벤트: 재생 진행 상황 업데이트, VOD 플레이어(VodPlayer)에게만 적용          |
| VOD_PLAY_EVT_PLAY_END                    | 재생 이벤트: 재생 종료됨                                       |
| VOD_PLAY_EVT_PLAY_LOADING                | 재생 이벤트: 데이터 버퍼링 중                                         |
| VOD_PLAY_EVT_START_VIDEO_DECODER         | 재생 이벤트: 비디오 디코더 시작됨                                 |
| VOD_PLAY_EVT_CHANGE_RESOLUTION           | 재생 이벤트: 비디오 해상도가 변경                                 |
| VOD_PLAY_EVT_GET_PLAYINFO_SUCC           | 재생 이벤트: VOD 파일의 정보 가져오기 성공, VOD 플레이어(VodPlayer)에게만 적용 |
| VOD_PLAY_EVT_CHANGE_ROTATION             | 재생 이벤트: MP4 동영상의 회전 각도가 변경, VOD 플레이어(VodPlayer)에게만 적용 |
| VOD_PLAY_EVT_VOD_PLAY_PREPARED           | 재생 이벤트: 비디오 로딩 완료, VOD 플레이어(VodPlayer)에게만 적용          |
| VOD_PLAY_EVT_VOD_LOADING_END             | 재생 이벤트: 비디오 버퍼링이 종료, VOD 플레이어(VodPlayer)에게만 적용          |
| VOD_PLAY_EVT_STREAM_SWITCH_SUCC          | 재생 이벤트: 서로 다른 해상도 간에 비디오 스트림 전환 완료 |
| VOD_PLAY_EVT_VOD_PLAY_TCP_CONNECT_SUCC   | TCP 연결 성공                                                 |
| VOD_PLAY_EVT_VOD_PLAY_FIRST_VIDEO_PACKET | 첫 번째 데이터 프레임을 성공적으로 수신                                                 |
| VOD_PLAY_EVT_VOD_PLAY_SEEK_COMPLETE      | 비디오 재생 Seek 완료                                           |
| VOD_PLAY_EVT_AUDIO_SESSION_INTERRUPT     | 재생 이벤트: Audio Session이 다른 App에 의해 중단(iOS에만 적용) |
| VOD_PLAY_ERR_NET_DISCONNECT              | 라이브 스트리밍 오류: 네트워크 연결이 끊겼고 3번의 재시도 후에도 다시 연결할 수 없음. |
| VOD_PLAY_ERR_FILE_NOT_FOUND              | VOD 오류: 재생할 파일이 존재하지 않음                                     |
| VOD_PLAY_ERR_HLS_KEY                     | VOD 오류: HLS 암호 해독 키 가져오기 실패                              |
| VOD_PLAY_ERR_GET_PLAYINFO_FAIL           | VOD 오류: VOD 파일 정보 가져오기 실패                         |

### [PIP 오류 유형](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#ga2b903483a07868f795ed52c27bfc08ac)

| 열거 값                                           | 의미                                         |
| ------------------------------------------------ | -------------------------------------------- |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_NONE                | 오류 없음                                       |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_DEVICE_NOT_SUPPORT  | 디바이스 및 시스템 버전 미지원(iPad iOS9+ PIP만 지원) |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PLAYER_NOT_SUPPORT  | 플레이어 미지원                                 |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_VIDEO_NOT_SUPPORT   | 비디오 미지원                                   |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_IS_NOT_POSSIBLE | PIP 컨트롤러 사용 불가                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_ERROR_FROM_SYSTEM   | PIP 컨트롤러가 오류 보고                               |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PLAYER_NOT_EXIST    | 플레이어 객체가 존재하지 않음                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_IS_RUNNING      | PIP 기능이 실행 중                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_NOT_RUNNING     | PIP 기능이 시작되지 않음                             |

### [PIP 컨트롤러 상태](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#ga96479f1446227115f7183ae97a1527e3)

| 열거 값                             | 의미           |
| ---------------------------------- | -------------- |
| TX_VOD_PLAYER_PIP_STATE_UNDEFINED  | 미설정 상태     |
| TX_VOD_PLAYER_PIP_STATE_WILL_START | PIP 곧 시작 |
| TX_VOD_PLAYER_PIP_STATE_DID_START  | PIP 시작됨 |
| TX_VOD_PLAYER_PIP_STATE_WILL_STOP  | PIP 곧 종료 |
| TX_VOD_PLAYER_PIP_STATE_DID_STOP   | PIP 종료됨 |
| TX_VOD_PLAYER_PIP_STATE_RESTORE_UI | UI 재설정        |
