## TXLivePlayer
 
### 비디오 플레이어

자세한 내용은 [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html)를 참고하십시오.

TXLivePlayer는 라이브 스트림의 오디오/비디오 데이터를 디코딩하고 로컬 렌더링을 수행합니다. 다음 기능을 제공합니다.

- Tencent Cloud의 재생 주소의 경우 저지연 재생을 사용하여 라이브 스트리밍 마이크 연결을 구현합니다.
- Tencent Cloud의 재생 주소의 경우 라이브 스트리밍 타임 시프트를 사용하여 라이브 뷰와 타임 시프트 뷰 간의 원활한 전환을 구현합니다.
- 사용자 정의 오디오/비디오 데이터 처리를 통해 프로젝트 요구 사항에 따라 라이브 스트림의 오디오/비디오 데이터를 처리한 다음 렌더링 및 재생할 수 있습니다.

### SDK 기본 함수 

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | 재생 콜백을 설정합니다. 자세한 내용은 `TXLivePlayListener.h` 파일의 자세한 정의를 참고하십시오.     |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | 비디오 처리 콜백을 설정합니다. 자세한 내용은 `TXVideoCustomProcessDelegate.h` 파일의 자세한 정의를 참고하십시오. |
| [audioRawDataDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a4d08f185792a92a087aff32b52b6b7b9) | 오디오 처리 콜백을 설정합니다. 자세한 내용은 `TXAudioRawDataDelegate.h` 파일의 자세한 정의를 참고하십시오. |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | 하드웨어 가속을 활성화할지 여부를 설정합니다. 기본값: NO.                               |
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aac73c062f0bbe5d97be40d85b68cb98a) | [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aac73c062f0bbe5d97be40d85b68cb98a) 재생 구성 항목을 설정합니다. 자세한 내용은 `TXLivePlayConfig.h` 파일의 세부 정의를 참고하십시오. |
| [recordDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7a3f4c66d5019d8e8899823e04be924d) | 쇼트 비디오 녹화 콜백을 설정합니다. 자세한 내용은 `TXLiveRecordListener.h` 파일의 자세한 정의를 참고하십시오. |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a946828345d302a28708d78fa1a931763) | startPlay 호출 직후 재생 시작 여부를 설정합니다. 이 API는 VOD에만 적용됩니다. 기본값: YES.           |


### 기본 재생 API

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [setupVideoWidget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a9195fa66ee874328a5b48400f2a0cb14) | Video 렌더링 View를 만듭니다. 이 컨트롤은 비디오 콘텐츠를 표시하는 데 사용됩니다. |
| [removeVideoWidget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#adf77d29895e70602556fdc51b931951e) | Video 렌더링 Widget을 제거합니다.                           |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a37e97416ec7a5853d217679be49cea26) | 지정된 URL에서 RTMP 오디오/비디오 스트림을 재생합니다.                |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | 오디오/비디오 스트림을 중지합니다.                                 |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7d3378ad416bfd00522acaedefc47dda) | 재생 진행 중 여부를 가져옵니다.                                     |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | 재생을 일시 중지합니다.                                         |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a41de8150eff044a237990c271d57ea27) | 재생을 재개합니다. 이 API는 VOD 및 라이브 스트리밍에 사용할 수 있습니다.                       |


### 비디오 API

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | -------------------- |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | 비디오 이미지의 방향을 설정합니다.     |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | 이미지 자르기 모드를 설정합니다. |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa24051e4c0271d994a5008cfc2db4775) | 스크린샷을 캡처합니다. |               |


### 오디오 API

| API                                                          | 설명                                |
| ------------------------------------------------------------ | -------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | 플레이어를 음소거/음소거 해제합니다.                             |
| [setVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a5a3bf801bad5591a3d8fe284aa6b3134) | 볼륨 레벨을 설정합니다.                             |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#ad56c52832a8efe45d6e0c50049406d74) | 오디오 재생 모드(스피커 또는 핸드셋)를 설정합니다. |
| [setAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a87d74a7afe3f768bd9e7ca276a189533) | 볼륨 레벨 콜백을 설정합니다.                 |


### 실시간 스트리밍 타임 시프트 API

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ------------------------------------------ |
| [prepareLiveSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#acf638c46e1e866ef06abda5ac938f07f) | 라이브 스트리밍 타임 시프트를 준비하고 라이브 스트리밍의 재생 시작 시간을 가져옵니다. |
| [resumeLive](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a4fa26fd4aea472d02de56d5f0bf653bf) | 타임 시프트 재생에서 라이브 재생을 재개합니다.                   |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | -                                          |


### 비디오 녹화 API

| API                                                          | 설명             |
| ------------------------------------------------------------ | ---------------- |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7224d5a8ab5fadc1d4c0fe1feb6ac972) | 쇼트 비디오 녹화를 시작합니다. |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a13313c5410c2a10a704b991f28141e6e) | 쇼트 비디오 녹화를 중지합니다. |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | 재생 속도를 설정합니다.   |


### 기타 API

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ----------------------------------------- |
| [setLogViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa906f88b51df74ab8f3c1125d9856293) | 렌더링 view와 상태 플로팅 view 사이의 여백을 설정합니다. | 
| [showVideoDebugLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a70ec322b088ad3c38b5a41d7528467f2) | 재생 상태 통계 및 이벤트 메시지 플로팅 view를 표시할지 여부를 설정합니다. |
| [switchStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a88751ad91dff45a9d6cc96dbda903b69) | FLV 라이브 스트림을 부드럽게 전환합니다.                        |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | 실험용 API를 호출합니다.                     |


### 열거 값

| 열거된 값                                                         | 설명                   |
| ------------------------------------------------------------ | ---------------------- |
| [TX_Enum_PlayType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#gaa164f735d1c349ce715f313c5d75892a) | 라이브 스트리밍 및 VOD 유형을 지원합니다. |


## TXLivePlayConfig

### TXLivePlayer 매개변수 구성 모듈

자세한 내용은 [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__ios.html#interfaceTXLivePlayConfig)를 참고하십시오.

[TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html) 매개변수를 설정하는 데 사용되며, 대부분 재생 시작 후 설정하면 적용되지 않습니다.

## TXLivePlayListener

### TXLivePlayer 콜백 알림

자세한 내용은  [TXLivePlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html)를 참고하십시오.

| API                                                          | 설명        |
| ------------------------------------------------------------ | -------------- |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html#a1e33d0cf9ed5f89ea2db32d0d7db9701) | 라이브 스트리밍 이벤트 공지. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html#aee80e62b7950c7d0a75ab97d993c10c6) | 네트워크 상태 공지. |

