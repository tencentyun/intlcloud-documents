## TXLivePlayer

### 비디오 플레이어

자세한 내용은 [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html)를 참고하십시오.
 
TXLivePlayer는 라이브 스트림의 오디오 및 비디오 데이터를 디코딩하고 로컬 렌더링을 수행합니다. 다음 기능을 제공합니다.

- Tencent Cloud의 재생 주소의 경우 저지연 재생을 사용하여 라이브 스트리밍 마이크 연결을 구현합니다.
- Tencent Cloud의 재생 주소의 경우 라이브 스트리밍 타임 시프트를 사용하여 라이브 뷰와 타임 시프트 뷰 간의 원활한 전환을 구현합니다.
- 사용자 정의 오디오/비디오 데이터 처리를 통해 프로젝트 요구 사항에 따라 라이브 스트림의 오디오/비디오 데이터를 처리한 다음 렌더링 및 재생할 수 있습니다.

### SDK 기본 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) | [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) 인스턴스를 생성합니다. |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#aec057eaad309a040e689eae94d81f6c2) | [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) 재생 구성 항목을 설정합니다. |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a0735b006fe8c56875665cb66881af144) | 스트림 푸시 콜백을 설정합니다.                                           |


### 기본 재생 API  

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------- |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | 플레이어의 렌더링 View를 설정합니다.     |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a966517cd67d967afe969b3d275239934) | 재생을 시작합니다.                |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | 재생을 중지합니다.                      |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | 재생 진행 중 여부를 가져옵니다.                  |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | 재생을 일시 중지합니다.                      |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a41de8150eff044a237990c271d57ea27) | 재생을 다시 시작합니다.                      |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | 로컬 렌더링에 Surface 모드를 사용합니다. |
| [setSurfaceSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#adfa92e76bde9450b135c48f531e5434d) | 렌더링 Surface 크기를 설정합니다.       |


### 재생 구성 API

| API                                                          | 설명                  |
| ------------------------------------------------------------ | ---------------------- |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | 재생 렌더링 모드를 설정합니다.     |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | 이미지 렌더링 각도를 설정합니다.     |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | 하드웨어 가속을 활성화합니다.         |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | 플레이어 음소거 여부를 설정합니다.     |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a3f0305de6ccd826ab62c442408416df9) | 오디오 재생 모드를 설정합니다.     |
| [setVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6715d5315d47c73b3838f2cb771e7b58) | 볼륨 레벨을 설정합니다.             |
| [switchStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a53f1f75a9a06e03bbb35e2ff5368c6f9) | 해상도를 전환합니다.         |
| [setAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#acd5e085b916732b2141ddae9ef93fc21) | 볼륨 레벨 콜백을 설정합니다. |


### 로컬 녹화 및 스크린샷 API

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | -------------------- |
| [setVideoRecordListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#acd229e0c77d3eea61dc0762557417478) | 녹화 콜백을 설정합니다.   |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#aed6b1e9d26a36166ee31c0544bd95ca4) | 비디오 녹화를 시작합니다.       |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a13313c5410c2a10a704b991f28141e6e) | 비디오 녹화를 중지합니다.       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a1377ad3e2678d3fef21f5037e274dd1a) | 재생 중에 로컬에서 스크린샷을 캡처합니다. |


### 사용자 정의 데이터 처리 API

| API                                                          | 설명                       |
| ------------------------------------------------------------ | --------------------------- |
| [addVideoRawData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a31d3d4067f5e61b80d7b750a6b5d97e2) | 소프트웨어 디코딩 데이터 캐리어 Buffer를 설정합니다 |
| [setVideoRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a093d4928d038dcc1c5413e771b5f8962) | 소프트웨어 디코딩 비디오 데이터 콜백을 설정합니다.    |
| [setAudioRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a36183b7ad026bc3e9718e82e38497e96) | 오디오 데이터 콜백을 설정합니다.          |


### 실시간 스트리밍 타임 시프트 API

| API                                                          | 설명        |
| ------------------------------------------------------------ | -------------- |
| [prepareLiveSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a081d01beb281348300bd9e9689949c59) | 라이브 스트리밍 타임 시프트를 준비합니다. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | 실시간 스트림 재생 시간을 찾습니다. |
| [resumeLive](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a4fa26fd4aea472d02de56d5f0bf653bf) | 라이브 스트리밍을 다시 시작합니다. |


### 스크린샷 콜백 API

자세한 내용은 [ITXSnapshotListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXSnapshotListener)를 참고하십시오.

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ---------- |
| [onSnapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) | 캡쳐한 스크린샷입니다. |


### 소프트웨어 디코딩을 위한 비디오 데이터 콜백 API

자세한 내용은[ITXVideoRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXVideoRawDataListener)를 참고하십시오.

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ------------------------------ |
| [onVideoRawDataAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a466e71718261727174795a3cd2b95d9e/34775#onvideorawdataavailable) | 소프트웨어 디코더에 의해 디코딩된 프레임입니다. |


### 원시 오디오 데이터 콜백 API

자세한 내용은 [ITXAudioRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXAudioRawDataListener)를 참고하십시오.

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ---------------------------------- |
| [onPcmDataAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a33e835ad16580a93ae40e0723368af32) | PCM 형식의 오디오 재생 데이터입니다. |
| [onAudioInfoChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a2aa86c3f5bd33047692b3d4dd0a59c32) | 오디오 재생 정보입니다.                 |


### 플레이어 볼륨 콜백 API

자세한 내용은 [ITXAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXAudioVolumeEvaluationListener)를 참고하십시오.

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | --------------------------------------- |
| [onAudioVolumeEvaluationNotify](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ae83090684b162568b729c010acd69828) | 플레이어의 볼륨 레벨, 값 범위[0, 100]. |

## TXLivePlayConfig

### TXLivePlayer 매개변수 구성 모듈

자세한 내용은 [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#classcom_1_1tencent_1_1rtmp_1_1TXLivePlayConfig)를 참고하십시오.

[TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) 매개변수를 설정하는 데 사용되며, 대부분은 재생 시작 후 설정하면 적용되지 않습니다.

### 일반적인 API

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ---------------------------- |
| [setAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ad2b54e62edb8d9cf287ac34a0ee0bc6e) | 캐시 시간 자동 조정 여부를 설정합니다.   |
| [setCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ac911ed6c1650c8723d11bb4aaa49f73f) | 플레이어 캐시 시간을 설정합니다.         |
| [setMaxAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ab400433f30e53d4827b8c16c449c107c) | 최대 캐시 시간을 설정합니다.         |
| [setMinAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#af495df5fea5e42779c007c5600e7bc4a) | 최소 캐시 시간을 설정합니다.         |
| [setVideoBlockThreshold](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a5d403dd5553d58ce309f26dbec61e20f) | 플레이어에 대한 비디오 랙 알람 임계값을 설정합니다. |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | 플레이어의 최대 재접속 시도 횟수를 설정합니다.         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | 플레이어 재접속 간격을 설정합니다.         |


### 전용 API

| API                                                          | 설명        |
| ------------------------------------------------------------ | -------------- |
| [setEnableMessage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a7c8e9ce786b57f2fddf921c4f336523d) | 메시지 채널을 활성화합니다. |
| [enableAEC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a2fb8e9e6f182cdd49f1260484cc484e5) | 음향 반향 제거(AEC)를 설정합니다. |


## ITXLivePlayListener

### TXLivePlayer 콜백 알림

자세한 내용은 [ITXLivePlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html)를 참고하십시오.

| API                                                          | 설명        |
| ------------------------------------------------------------ | -------------- |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html#a57e1f63dbe15f1242e3b842d0454f74f) | 재생 이벤트 알림입니다. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html#a826de3acd9a9d2da1604a076772f2f2e) | 네트워크 상태 알림입니다. |
