## TXVodPlayer

### VOD 플레이어

자세한 내용은 [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html)를 참고하십시오.
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
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | VOD를 구성합니다. 구성에 대한 자세한 내용은 [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html)를 참고하십시오. |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | startVodPlay 호출 직후 재생 시작 여부를 설정합니다. 기본값: YES.                         |
| [token](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | HLS 암호화를 위한 token을 설정합니다. 토큰이 설정되면 플레이어는 URL의 파일 이름 앞에 `voddrm.token.TOKEN TextureView`를 자동으로 추가합니다. |
| [loop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | SurfaceView 반복 여부를 설정합니다.                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | 비디오 렌더링 콜백을 설정합니다.(하드웨어 인코딩에서만 지원)                                 |
| [setExtentOptionInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a842c8863f91f274031be0109a5cb28f5) | <NSString *, id> 형식으로 플레이어 비즈니스 매개변수를 설정합니다.             |

### 기본 재생 API  
| API                                                          | 설명                       |
| ------------------------------------------------------------ | --------------------------- |
| [startVodPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a89ac47a6b808c8ca424a65adb8870bc6) | HTTP URL에서 비디오를 재생합니다. v10.7부터는 `startPlay`가 `startVodPlay`로 대체되었으며, 재생 기능을 사용하기 위해서는 `V2TXLivePremier#setLicence` 또는 `TXLiveBase#setLicence`를 호출하여 License를 설정해야 합니다(License는 한 번만 설정하면 됩니다). 그렇지 않으면 재생이 실패합니다(검은 화면). 라이브 스트림 퍼블리싱 License, UGSV License 또는 비디오 재생 License를 사용하여 재생 기능을 활성화할 수 있습니다. |
| [startVodPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#acfae73abaadc60e2e1091ffae0c5c700) | VOD fileId로 비디오를 재생합니다. v10.7부터 `startPlayWithParams`가 `startVodPlayWithParams`로 대체되었으며, 재생 기능을 사용하기 위해서는 `V2TXLivePremier#setLicence` 또는 `TXLiveBase#setLicence`를 호출하여 License를 설정해야 합니다(License는 한 번만 설정하면 됩니다). 그렇지 않으면 재생이 실패합니다(검은 화면). 라이브 스트림 퍼블리싱 License, UGSV License 또는 비디오 재생 License를 사용하여 재생 기능을 활성화할 수 있습니다. |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | 재생을 중지합니다. |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | 재생 진행 중 여부를 가져옵니다.      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 스트림 데이터 가져오기를 중지하고 마지막 프레임 이미지를 유지하여 재생을 일시 중지합니다. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 스트림 데이터를 다시 가져와 재생을 재개합니다. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | 비디오 스트림의 지정된 시점(초)을 찾습니다. |
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | 현재 재생 시점을 초 단위로 가져옵니다. |
| [duration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | 총 비디오 지속 시간(초)을 가져옵니다. |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | 재생 가능한 비디오 재생 시간(초)을 가져옵니다. |
| [width](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | 비디오 너비를 가져옵니다. |
| [height](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | 비디오 높이를 가져옵니다. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | 재생 시작 시간을 설정합니다. |

### 비디오 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | 현재 비디오 프레임 이미지를 가져옵니다. <br>**참고: 이 작업은 시간이 많이 걸리므로 스크린샷은 비동기식으로 다시 호출됩니다.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | 미러 이미지를 설정합니다.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | VOD 재생 속도를 설정합니다. 기본값: 1.0.                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | 현재 재생 비트 레이트 인덱스를 반환합니다.                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | 원활한 해상도 전환을 위한 현재 재생 비트 레이트 인덱스를 설정합니다. <br>해상도를 전환하려면 잠시 기다려야 할 수도 있습니다. |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | [이미지 채우기 모드](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae)를 설정합니다. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | [이미지 렌더링 각도](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f)를 설정합니다. |

### 오디오 API

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | 플레이어 음소거 여부를 설정합니다.            |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | 볼륨 레벨을 설정합니다. 값 범위: 0 – 100. |

### 이벤트 공지 API

| API                      | 설명                   |
| ---------------------- | ---------------------- |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | 이벤트 콜백. [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) 사용을 권장합니다. |
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | 플레이어 콜백을 설정합니다.                                 |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | 비디오 렌더링 콜백을 설정합니다(하드웨어 인코딩에서만 지원).                  |

### TRTC API

다음 API를 사용하여 VOD 플레이어의 오디오/비디오 스트림을 TRTC를 통해 푸시할 수 있습니다. TRTC 서비스에 대한 자세한 내용은 TRTC [제품 개요](https://intl.cloud.tencent.com/document/product/647/35078) 페이지를 참고하십시오.

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | VOD를 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)에 바인딩합니다. |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)에서 VOD 바인딩을 해제합니다. |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | 비디오 스트림 푸시를 시작합니다.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | 비디오 스트림 푸시를 취소합니다.                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | 오디오 스트림 푸시를 시작합니다.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | 오디오 스트림 푸시를 취소합니다.                                             |

## TXVodPlayListener

VOD 콜백 공지입니다.
### 기본 SDK 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | VOD 재생 이벤트 공지. 자세한 내용은 [재생 이벤트 목록](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) 및 [이벤트 매개변수](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594)를 참고하십시오. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | VOD 플레이어의 [네트워크 상태 공지](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737)입니다. |

## TXVodPlayConfig

VOD 플레이어 구성 클래스입니다.

### 기본 구성 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | 플레이어의 최대 재접속 시도 횟수를 설정합니다.                                         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | 플레이어 재연결 간격(초)을 설정합니다.                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | 플레이어 연결 제한 시간(초)을 설정합니다.                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | MP4 및 HLS 파일에 적용되는 VOD 캐시 디렉터리를 설정합니다.                       |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | 최대 캐시 파일 수를 설정합니다.                                           |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | 플레이어 유형을 설정합니다.                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | 사용자 정의 HTTP headers를 설정합니다.                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | 정확한 seek 활성화 여부를 설정합니다. 기본값: true.                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | MP4 파일 재생 시 YES로 설정하면 파일에 설정된 회전 각도에 따라 자동으로 회전됩니다. <br>회전 각도는 PLAY_EVT_CHANGE_ROTATION 이벤트에서 얻을 수 있습니다. 기본값: YES. |
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | 다중 비트 레이트 HLS 스트림에 대해 부드러운 전환 활성화 여부를 설정합니다. 기본값: false.                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | 진행 콜백 간격을 밀리초 단위로 설정합니다.                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | 최대 사전 로딩 버퍼 크기를 MB 단위로 설정합니다.                                    |
| maxPreloadSize                                               | 최대 사전 로딩 버퍼 크기를 MB 단위로 설정합니다.                           |
| firstStartPlayBufferTime                                     | 첫 번째 버퍼링 동안 로딩해야 하는 비디오 데이터의 지속 시간을 ms 단위로 설정합니다. 기본값: 100ms.          |
| nextStartPlayBufferTime                                      | 버퍼링을 중지하기 위해 버퍼링된 최소 데이터 크기를 설정합니다(버퍼링된 데이터 부족에 대한 보조 버퍼링 또는 seek로 인한 진행률 표시줄 드래그 버퍼링). 기본값: 250ms. |
| overlayKey                                                   | HLS 보안 강화 암호화 및 암호 해독 key를 설정합니다.                                   |
| overlayIv                                                    | HLS 보안 강화 암호화 및 복호화 Iv를 설정합니다.                                    |
| extInfoMap                                                   | 확장 정보를 설정합니다.                                               |
| preferredResolution                                          | HLS 비트스트림이 여러 개인 경우 구성된 preferredResolution에 따라 가장 선호하는 비트스트림 재생 *을 시작합니다. 여기서 preferredResolution은 비디오 너비와 높이를 곱한 것으로(width * height), 재생이 시작되기 전에 설정된 경우에만 적용됩니다. |
| enableRenderProcess                                          | 기본적으로 활성화되어 있는 초해상도 플러그 인과 같은 포스트렌더링 및 포스트프로덕션 기능 허용 여부를 설정합니다.     |

## TXPlayerGlobalSetting

VOD 플레이어의 전역 구성입니다.

| API                | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | 재생 엔진의 cache 디렉터리를 설정합니다. 설정 후 이 디렉터리를 사전 다운로드 및 플레이어 사용 중에 먼저 읽고 저장합니다. |
| setMaxCacheSize    | 재생 엔진의 최대 캐시 크기를 MB 단위로 설정합니다. 설정 후 백엔드는 설정 값에 따라 Cache 디렉터리의 파일을 자동으로 지웁니다. |

## TXVodPreloadManager

VOD 플레이어의 API 클래스 사전 다운로드

| API           | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| sharedManager | 싱글톤 모드에서 TXVodPreloadManager 인스턴스 객체를 가져옵니다.                    |
| startPreload  | 사전 다운로드를 시작하기 전에 재생 엔진 캐시 디렉터리TXPlayerGlobalSetting#setCacheFolderPath 및 캐시 크기TXPlayerGlobalSetting#setMaxCacheSize를 설정합니다. |
| stopPreload   | 사전 다운로드를 중지합니다.                                                   |

## TXVodDownloadManager

VOD 플레이어의 비디오 다운로드 API 클래스

| API                      | 설명                                                         |
| ------------------------ | ------------------------------------------------------------ |
| shareInstance            | 싱글톤 모드에서 TXVodDownloadManager 인스턴스 객체를 가져옵니다.                   |
| setDownloadPath          | 다운로드 루트 디렉터리를 설정합니다.                                               |
| setHeaders               | 다운로드 HTTP 헤더를 설정합니다.                                               |
| setListener              | 다운로드 전에 설정해야 하는 다운로드 콜백 방법을 설정합니다.                             |
| startDownloadUrl         | 지정된 URL에서 비디오 다운로드를 시작합니다.                                            |
| startDownload            | 지정된 FileID의 비디오 다운로드를 시작합니다.                                         |
| stopDownload             | 다운로드를 중지합니다. ITXVodDownloadListener.onDownloadStop이 다시 호출되면 다운로드가 성공적으로 중지됩니다. |
| deleteDownloadFile       | 다운로드한 파일을 삭제합니다.                                                 |
| deleteDownloadMediaInfo  | 다운로드 정보를 삭제합니다.                                                 |
| getDownloadMediaInfoList | 모든 사용자의 다운로드 목록을 가져옵니다.                                   |



## ITXVodDownloadListener

VOD 다운로드 공지입니다.

| API                | 설명                                         |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | 다운로드가 시작되었습니다.                                     |
| onDownloadProgress | 다운로드 진행률이 업데이트되었습니다.                                 |
| onDownloadStop     | 다운로드가 중지되었습니다.                                    |
| onDownloadFinish   | 다운로드가 종료되었습니다.                                     |
| onDownloadError    | 다운로드 중 오류가 발생했습니다.                           |
| hlsKeyVerify       | HLS 스트림 다운로드 중에 암호화된 파일이 발견되면 플레이어가 암호 해독 Key를 확인합니다. |



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
| 2011 | PLAY_EVT_CHANGE_ROTATION   | MP4 비디오가 회전되었습니다.                                          |



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
