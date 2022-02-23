## TRTCCloud @ TXLiteAVSDK

Tencent Cloud 영상 통화 기능의 주요 인터페이스.

- **주요 문서 주소**: [TRTC Electron SDK](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- **인스턴스 코드 주소**: [TRTC Electron Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)

### TRTC 객체 생성
```js
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
```

v7.9.348부터 TRTC Electron SDK에 typescript를 사용하는 개발자에게 편리한 trtc.d.ts 파일이 추가되었습니다.

```javascript
import TRTCCloud from 'trtc-electron-sdk';

const rtcCloud: TRTCCloud = new TRTCCloud();
// SDK 버전 가져오기
rtcCloud.getSDKVersion();
```

### 콜백 설정
```js
subscribeEvents = (rtcCloud) => {
    rtcCloud.on('onError', (errcode, errmsg) => {
    console.info('trtc_demo: onError :' + errcode + " msg" + errmsg);
    }); 
    rtcCloud.on('onEnterRoom', (elapsed) => {
    console.info('trtc_demo: onEnterRoom elapsed:' + elapsed);
    });
    rtcCloud.on('onExitRoom', (reason) => {
    console.info('onExitRoom: userenter reason:' + reason);
    });
};


subscribeEvents(this.rtcCloud);
```

### TRTCCloud 싱글톤 생성 및 폐기

| API | 설명 |
|-----|-----|
| [getTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.getTRTCShareInstance) | dll 동적 로딩 시, [TRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html) 객체 싱글톤 생성에 사용. |
| [destroyTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.destroyTRTCShareInstance) | [TRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html) 싱글톤 객체를 릴리스하고 리소스를 정리. |

### 방 관련 API

| API | 설명 |
|-----|-----|
| [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) | 방 입장. 방이 없으면 시스템에서 자동으로 생성. |
| [exitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom) | 방 퇴장. |
| [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) | 방 전환. |
| [switchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole) | 역할 전환. 라이브 방송 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)에만 적용. |
| [connectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom) | 크로스 룸 마이크 연결(호스트 크로스 룸 PK) 요청. |
| [disconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#disconnectOtherRoom)| 크로스 룸 마이크 연결(호스트 크로스 룸 PK) 비활성화. |
| [setDefaultStreamRecvMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode) | 오디오 및 비디오 데이터 수신 모드를 설정합니다(방 입장 전 설정 시 적용됨). |


### CDN 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishing) | Tencent Cloud 라이브 방송 CDN에 푸시 스트림 시작. |
| [stopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishing) | Tencent Cloud 라이브 방송 CDN에 푸시 스트림 중지. |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishCDNStream) | Tencent Cloud 이외의 라이브 스트리밍 CDN에 게시 시작. |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishCDNStream) | Tencent Cloud 이외의 라이브 스트리밍 CDN에 게시 중지. |
| [setMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig) | 클라우드 혼합 스트림 트랜스 코딩 매개변수 설정. |


### 비디오 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) | 로컬 카메라 캡처 및 미리보기 시작. |
| [stopLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalPreview) | 로컬 카메라 캡처 및 미리보기 중지. |
| [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) | 사용자 영상 화면 차단 여부 확인. |
| [startRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) | 원격 비디오 화면 표시 시작. |
| [stopRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView) | 원격 영상 화면 표시 중지 및 원격 사용자의 비디오 데이터 스트림 풀링 중지. |
| [stopAllRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView) | 모든 영상 화면 표시 중지 및 원격 사용자의 비디오 데이터 스트림 풀링 중지. |
| [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream) | 지정 원격 비디오 스트림 수신 일시 중지. |
| [muteAllRemoteVideoStreams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteVideoStreams) | 모든 원격 비디오 스트림 수신 중지. |
| [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) | 비디오 인코더 관련 매개변수 설정. |
| [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam) | 네트워크 트래픽 제어 관련 매개변수 설정. |
| [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) | 로컬 이미지(메인 스트림)의 렌더링 매개변수 설정. |
| [setLocalViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode) | 폐기된 인터페이스: 로컬 이미지 렌더링 모드 설정. |
| [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) | 원격 이미지의 렌더링 매개변수 설정. |
| [setRemoteViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewFillMode) | 폐기된 인터페이스: 원격 이미지 렌더링 모드 설정. |
| [setLocalViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewRotation) | 폐기된 인터페이스: 로컬 이미지의 시계 방향 회전 각도 설정. |
| [setRemoteViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewRotation) | 폐기된 인터페이스: 원격 이미지의 시계 방향 회전 각도 설정. |
| [setVideoEncoderRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderRotation) | 비디오 인코딩 출력(원격 사용자가 시청하고 서버에 녹화된) 화면 방향 설정. |
| [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) | 폐기된 인터페이스: 로컬 카메라 화면 미리보기 이미지 모드 설정. |
| [setVideoEncoderMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderMirror) | 인코더로 출력된 화면의 이미지 모드 설정. |
| [enableSmallVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableSmallVideoStream) | 크고 작은 이미지의 이중 채널 인코딩 모드 활성화. |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteVideoStreamType) | 지정 userId의 화면(큰 이미지/작은 이미지) 선택. |
| [setPriorRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setPriorRemoteVideoStreamType) | 폐기된 인터페이스: 시청자 비디오 품질 우선 순위 설정. |
| [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) | 영상 화면 캡처. |


### 오디오 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) | 로컬 오디오 수집 및 업스트림 활성화. |
| [stopLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalAudio) | 로컬 오디오 수집 및 업스트림 비활성화. |
| [muteLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalAudio) | 로컬 오디오 음소거. |
| [muteRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio) | 특정 사용자의 오디오를 음소거하고 해당 원격 사용자의 오디오 데이터 스트림 풀링 중지. |
| [muteAllRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio) | 모든 사용자의 오디오를 음소거하고 원격 사용자의 오디오 데이터 스트림 풀링 중지. |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioCaptureVolume) | SDK 수집 볼륨 설정. |
| [getAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioCaptureVolume) | SDK 수집 볼륨 가져오기. |
| [setAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioPlayoutVolume) | SDK 재생 볼륨 설정. |
| [getAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioPlayoutVolume) | SDK 재생 볼륨 가져오기. |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableAudioVolumeEvaluation) | 볼륨 크기 알람 활성화/비활성화. |
| [startAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startAudioRecording) | 녹음 시작. |
| [stopAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioRecording) | 녹음 중지. |
| [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) | 폐기된 인터페이스: 볼륨 품질 설정. |
| [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) | 원격 사용자의 재생 볼륨 설정. |


### 카메라 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [getCameraDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCameraDevicesList) | 카메라 디바이스 리스트 가져오기. |
| [setCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice) | 사용할 카메라 설정. |
| [getCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentCameraDevice) | 현재 사용하는 카메라 가져오기. |


### 오디오 디바이스 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [getMicDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMicDevicesList) | 마이크 디바이스 리스트 가져오기. |
| [getCurrentMicDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDevice) | 현재 선택한 마이크 가져오기. |
| [setCurrentMicDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDevice) | 사용할 마이크 설정. |
| [getCurrentMicDeviceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceVolume) | 시스템의 현재 마이크 디바이스 볼륨 가져오기. |
| [setCurrentMicDeviceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceVolume) | 시스템의 현재 마이크 디바이스 볼륨 설정. |
| [setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute) | 시스템의 현재 마이크 디바이스 음소거 상태 설정. |
| [getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute) | 시스템의 현재 마이크 디바이스 음소거 여부 가져오기. |
| [getSpeakerDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSpeakerDevicesList) | 스피커 디바이스 리스트 가져오기. |
| [getCurrentSpeakerDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDevice) | 현재 스피커 디바이스 가져오기. |
| [setCurrentSpeakerDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDevice) | 사용할 스피커 설정. |
| [getCurrentSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerVolume) | 시스템의 현재 스피커 디바이스 볼륨 가져오기. |
| [setCurrentSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerVolume) | 시스템의 현재 스피커 디바이스 볼륨 설정. |
| [setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute) | 시스템의 현재 스피커 디바이스 음소거 상태 설정. |
| [getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute) | 시스템의 현재 스피커 디바이스 음소거 여부 가져오기. |

### 뷰티 필터 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [setBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle) | 뷰티 필터, 미백, 안색 보정 효과 레벨 설정. |
| [setWaterMark](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setWaterMark) | 워터마크 설정. |


### 서브스트림 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteSubStreamView) | 폐기된 인터페이스: 원격 사용자의 서브스트림(화면 공유) 화면 렌더링 시작. |
| [stopRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteSubStreamView) | 폐기된 인터페이스: 원격 사용자의 서브스트림(화면 공유) 화면 렌더링 중지. |
| [setRemoteSubStreamViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewFillMode) | 폐기된 인터페이스: 서브스트림(화면 공유) 화면의 렌더링 모드 설정. |
| [setRemoteSubStreamViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewRotation) | 폐기된 인터페이스: 서브스트림(화면 공유) 화면의 시계 방향 회전 각도 설정. |
| [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources) | 공유할 수 있는 창 목록 열거. |
| [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) | 화면 공유 매개변수 설정. 화면 공유 과정 중에도 호출 가능. |
| [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) | 화면 공유 실행. |
| [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) | 화면 공유 일시 중지. |
| [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture) | 화면 공유 재개. |
| [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) | 화면 공유 중지. |
| [setSubStreamEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamEncoderParam) | 서브스트림(화면 공유)의 인코더 매개변수 설정. |
| [setSubStreamMixVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamMixVolume) | 서브스트림(화면 공유)의 오디오 믹싱 볼륨 크기 설정. |
| [addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow) | 지정 창을 화면 공유 제외 리스트에 추가. 제외 리스트에 추가된 창은 공유되지 않음. |
| [removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow) | 지정 창을 화면 공유 제외 리스트에서 제거. |
| [removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow) | 모든 창을 화면 공유 제외 리스트에서 제거. |


### 사용자 정의 메시지 발송

| API | 설명 |
|-----|-----|
| [sendCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendCustomCmdMsg) | 사용자 정의 메세지를 방 안에 있는 모든 사용자에게 전송. |
| [sendSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendSEIMsg) | 적은 양의 사용자 정의 데이터를 비디오 프레임에 삽입. |


### 배경 오디오 믹싱 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [playBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playBGM) | 폐기된 인터페이스: 배경 음악 재생 실행. |
| [stopBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopBGM) | 폐기된 인터페이스: 배경 음악 재생 중지. |
| [pauseBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseBGM) | 폐기된 인터페이스: 배경 음악 재생 일시 중지. |
| [resumeBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeBGM) | 폐기된 인터페이스: 배경 음악 계속 재생. |
| [getBGMDuration](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getBGMDuration) | 폐기된 인터페이스: 배경 음악 파일 총 시간 가져오기. 단위: 밀리초. |
| [setBGMPosition](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPosition) | 폐기된 인터페이스: 배경 음악 재생 진행률 설정. |
| [setBGMVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMVolume) | 폐기된 인터페이스: 배경 음악 재생 볼륨 크기 설정. |
| [setBGMPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPlayoutVolume) | 폐기된 인터페이스: 배경 음악 로컬 재생 볼륨 크기 설정. |
| [setBGMPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPublishVolume) | 폐기된 인터페이스: 배경 음악 원격 재생 볼륨 크기 설정. |
| [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback) | 시스템 오디오 수집 활성화. |
| [stopSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSystemAudioLoopback) | 시스템 오디오 수집 비활성화. |
| [setSystemAudioLoopbackVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSystemAudioLoopbackVolume) | 시스템 오디오 수집 볼륨 설정. |
| [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) | 배경 음악 재생 실행. |
| [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) | 배경 음악 재생 정지. |
| [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) | 배경 음악 재생 일시 중지. |
| [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) | 배경 음악 재생 재개. |
| [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) | 배경 음악 파일 총 시간 가져오기. 단위: 밀리초. |
| [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) | 배경 음악 재생 진행률 설정. |
| [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) | 배경 음악 믹싱 재생 시 배경음의 음량 조절에 사용되는 배경 음악의 음량 설정. |
| [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) | 배경 음악의 로컬 재생 볼륨 설정. |
| [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) | 배경 음악의 원격 재생 볼륨 설정. |


### 음향 효과 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [playAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playAudioEffect) | 폐기된 인터페이스: 음향 효과 재생. |
| [setAudioEffectVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioEffectVolume) | 폐기된 인터페이스: 음향 효과 볼륨 설정. |
| [stopAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioEffect) | 폐기된 인터페이스: 음향 효과 중지. |
| [stopAllAudioEffects](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllAudioEffects) | 폐기된 인터페이스: 모든 음향 효과 중지. |
| [setAllAudioEffectsVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllAudioEffectsVolume) | 폐기된 인터페이스: 모든 음향 효과 볼륨 설정. |
| [pauseAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseAudioEffect) | 폐기된 인터페이스: 음향 효과를 일시 중지. |
| [resumeAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeAudioEffect) | 폐기된 인터페이스: 음향 효과 다시 재생. |


### 디바이스 및 네트워크 테스트

| API | 설명 |
|-----|-----|
| [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest) | 네트워크 속도 테스트 시작(통화 품질에 영향을 미칠 수 있으니 영상 통화 중에는 사용하지 마십시오). |
| [stopSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeedTest) | 네트워크 속도 테스트 중지. |
| [startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startCameraDeviceTest) | 카메라 테스트 시작. |
| [stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopCameraDeviceTest) | 카메라 테스트 중지. |
| [startMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startMicDeviceTest) | 마이크 테스트 시작. |
| [stopMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopMicDeviceTest) | 마이크 테스트 중지. |
| [startSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeakerDeviceTest) | 스피커 테스트 시작. |
| [stopSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeakerDeviceTest) | 스피커 테스트 중지. |


### LOG 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [getSDKVersion](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSDKVersion) | SDK 버전 정보 가져오기. |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogLevel) | Log 출력 레벨 설정. |
| [setConsoleEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setConsoleEnabled) |  콘솔 로그 출력 활성화/비활성화. |
| [setLogCompressEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCompressEnabled) | Log의 로컬 압축 활성화/비활성화. |
| [setLogDirPath](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogDirPath) | 로그 저장 경로 설정. |
| [setLogCallback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCallback) | 로그 콜백 설정. |
| [callExperimentalAPI](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#callExperimentalAPI) | 실험용 API  호출. |


### 사용하지 않는 인터페이스 함수

| API | 설명 |
|-----|-----|
| [setMicVolumeOnMixing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMicVolumeOnMixing) | v6.9 버전부터 폐기. |


## TRTCCallback @ TXLiteAVSDK

Tencent Cloud 영상 통화 기능의 콜백 인터페이스 유형.

### 오류 및 경고 이벤트 콜백 API

| API | 설명 |
|-----|-----|
| [onError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onError) | 오류 콜백. SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 맞게 사용자에게 적절한 인터페이스 알림을 제공. |
| [onWarning](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onWarning) | 경고 콜백: 랙 또는 복구 가능한 디코딩 실패 등 심각하지 않은 문제를 알릴 때 사용. |


### 방 이벤트 콜백 API

| API | 설명 |
|-----|-----|
| [onEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) | 방 입장 콜백. |
| [onExitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) | 방 퇴장 이벤트 콜백. |
| [onSwitchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRole) | 역할 전환 이벤트 콜백. |
| [onConnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom) | 크로스 룸 통화(호스트 PK) 요청 결과 콜백. |
| [onDisconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDisconnectOtherRoom) |크로스 룸 통화(호스트 PK) 종료 결과 콜백. |
| [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) | 방 전환.  |


### 사용자 이벤트 콜백 API

| API | 설명 |
|-----|-----|
| [onRemoteUserEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserEnterRoom) | 사용자가 현재 방에 입장함. |
|onRemoteUserLeaveRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserLeaveRoom) | 사용자가 현재 방에서 퇴장함. |
| [onUserVideoAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) | 사용자의 카메라 비디오 활성화 여부. |
| [onUserSubStreamAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserSubStreamAvailable) | 사용자의 화면 공유 활성화 여부. |
| [onUserAudioAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) | 사용자의 오디오 업스트림 활성화 여부. |
| [onFirstVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstVideoFrame) | 로컬 또는 원격 사용자의 첫 번째 프레임 화면 렌더링 시작. |
| [onFirstAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstAudioFrame) | 원격 사용자의 첫 번째 프레임 오디오(로컬 오디오는 공지 안 함) 재생 시작. |
| [onSendFirstLocalVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | 첫 번째 프레임 로컬 비디오 데이터 발송 완료. |
| [onSendFirstLocalAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalAudioFrame) | 첫 번째 프레임 로컬 오디오 데이터 발송 완료. |
| [onUserEnter](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserEnter) | 호스트가 현재 방에 입장함(폐기됨). |
| [onUserExit](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserExit) | 호스트가 현재 방에서 퇴장함(폐기됨). |


### 네트워크 품질 및 기술 메트릭에 대한 통계를 위한 콜백 API

| API | 설명 |
|-----|-----|
| [onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality) | 네트워크 품질: 해당 콜백은 2초에 한 번 트리거되고 현재의 네트워크 업스트림/다운스트림 품질을 통계함. |
| [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) | 기술 메트릭 통계 콜백. |


### 서버 이벤트 콜백 API

| API | 설명 |
|-----|-----|
| [onConnectionLost](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionLost) | SDK와 서버 연결이 끊김. |
| [onTryToReconnect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTryToReconnect) | SDK와 서버 다시 연결 중. |
| [onConnectionRecovery](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionRecovery) | SDK와 서버가 다시 연결됨. |
| [onSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTest) | 폐기 인터페이스: 서버 속도 테스트 콜백. SDK는 여러 서버 IP에 속도 테스트를 진행하며 모든 IP의 속도 테스트 결과는 해당 콜백을 통해 공지됨.|
| [onSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTestResult) | 네트워크 속도 테스트 결과 콜백. |


### 하드웨어 이벤트 콜백 API

| API | 설명 |
|-----|-----|
| [onCameraDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onCameraDidReady) | 카메라 준비 완료. |
| [onMicDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMicDidReady) | 마이크 준비 완료. |
| [onUserVoiceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVoiceVolume) | user ID의 볼륨 및 원격 총 불륨 등 볼륨 크기 알림에 사용되는 콜백. |
| [onDeviceChange](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDeviceChange) | 로컬 디바이스 연결 상태 콜백. |
| [onTestMicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestMicVolume) | 마이크 테스트 볼륨 콜백. |
| [onTestSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestSpeakerVolume) | 스피커 테스트 볼륨 콜백. |
| [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) | 현재 오디오 캡처 디바이스 볼륨 변경 콜백. |
| [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) | 현재 오디오 재생 디바이스 볼륨 변경 콜백. |


### 사용자 정의 메시지 수신 콜백

| API | 설명 |
|-----|-----|
| [onRecvCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvCustomCmdMsg) | 사용자 정의 메세지 수신 콜백 |
| [onMissCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMissCustomCmdMsg) | 사용자 정의 메세지 손실 콜백. |
| [onRecvSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvSEIMsg) | SEI 메세지 수신 콜백. |


### CDN 릴레이 푸시용 콜백 API

| API | 설명 |
|-----|-----|
| [onStartPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishing) | Tencent Cloud 라이브 방송 CDN에 푸시 스트림을 시작하는 콜백으로 TRTCCloud의 startPublishing() 인터페이스에 상응함. |
| [onStopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishing) | Tencent Cloud 라이브 방송 CDN에 푸시 스트림을 중지하는 콜백으로 TRTCCloud의 stopPublishing() 인터페이스에 상응함. |
| [onStartPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishCDNStream) | CDN으로 릴레이 푸시 스트림 활성화 콜백. |
| [onStopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishCDNStream) | CDN으로 릴레이 푸시 스트림 중지 콜백. |
| [onSetMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSetMixTranscodingConfig) | 클라우드 혼합 스트림 트랜스 코딩 매개변수 설정 콜백으로 TRTCCloud의 setMixTranscodingConfig() 인터페이스에 상응함. |

### 시스템 볼륨 수집 콜백
| API | 설명 |
|-----|-----|
| [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError) | 시스템 볼륨 수집 상태 콜백(Mac만 해당됨). |

### 음향 효과 콜백

| API | 설명 |
|-----|-----|
| [onAudioEffectFinished](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioEffectFinished) | 폐기된 인터페이스: 음향 효과 재생 종료 콜백. |

### 화면 공유 콜백

| API | 설명 |
|-----|-----|
| [onScreenCaptureCovered](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureCovered) | 화면 공유 창이 차단되어 캡처가 불가능할 경우 SDK는 해당 콜백을 통해 사용자에게 차단된 창을 제거할 것을 공지. |
| [onScreenCaptureStarted](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStarted) | 화면 공유 시작 시, SDK에서 해당 콜백을 통해 공지. |
| [onScreenCapturePaused](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCapturePaused) | 화면 공유 일시 중지 시, SDK에서 해당 콜백을 통해 공지. |
| [onScreenCaptureResumed](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureResumed) | 화면 공유 복구 시, SDK에서 해당 콜백을 통해 공지. |
| [onScreenCaptureStopped](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStopped) | 화면 공유 중지 시, SDK에서 해당 콜백을 통해 공지. |


### 화면 캡처 콜백

| API | 설명 |
|-----|-----|
| [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) | 화면 캡처 완료 시, SDK에서 해당 콜백을 통해 공지. |


### 배경 오디오 믹싱 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onPlayBGMBegin](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMBegin) | 배경 음악 재생 시작(폐기됨). |
| [onPlayBGMProgress](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMProgress) | 배경 음악 재생 진행률 콜백(폐기됨). |
| [onPlayBGMComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMComplete) | 배경 음악 재생 종료(폐기됨). |


## 주요 클래스의 정의

### 주요 클래스

| 클래스 이름 | 설명 |
|-----|-----|
| [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)| 방 입장 관련 매개변수. |
| [TRTCVideoEncParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVideoEncParam.html) | 비디오 인코딩 매개변수. |
| [TRTCNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCNetworkQosParam.html) | 네트워크 트래픽 제어 관련 매개변수. |
| [TRTCQualityInfo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCQualityInfo.html)| 비디오 품질. |
| [TRTCVolumeInfo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVolumeInfo.html) | 볼륨 크기. |
| [TRTCSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCSpeedTestResult.html)| 네트워크 속도 테스트 결과. |
| [TRTCMixUser](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCMixUser.html)| 클라우드 혼합 스트림의 모든 서브 채널 위치 정보. |
| [TRTCTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCTranscodingConfig.html)| 클라우드 혼합 스트림(트랜스 코딩) 설정. |
| [TRTCPublishCDNParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCPublishCDNParam.html)| CDN 릴레이 푸시 스트림 매개변수. |
| [TRTCAudioRecordingParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCAudioRecordingParams.html)| 녹음 매개변수. |
| [TRTCLocalStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCLocalStatistics.html)| 사용자 로컬 멀티미디어 통계 정보. |
| [TRTCRemoteStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCRemoteStatistics.html) | 원격 구성원의 멀티미디어 통계 정보. |
| [TRTCStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCStatistics.html)| 통계 데이터. |

### 열거 값

| 열거 | 설명 |
|-----|-----|
| [TRTCVideoResolution](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)| 비디오 해상도. |
| [TRTCVideoResolutionMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolutionMode)| 비디오 해상도 모드. |
| [TRTCVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType) | 비디오 스트림 유형. |
| [TRTCQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQuality)| 화질 레벨. |
| [TRTCVideoFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoFillMode)| 영상 화면 채우기 모드. |
| [TRTCBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCBeautyStyle) | 뷰티 필터(피부 보정) 알고리즘. |
| [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)| 응용 시나리오. |
| [TRTCRoleType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCRoleType)| 역할. 라이브 방송 시나리오(TRTCAppSceneLIVE)만 해당. |
| [TRTCQosControlMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQosControlMode)| 트래픽 제어 모드. |
| [TRTCVideoQosPreference](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoQosPreference)| 화질 선호도. |
| [TRTCDeviceState](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceState)| 디바이스 작업. |
| [TRTCDeviceType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceType)| 디바이스 유형. |
| [TRTCWaterMarkSrcType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCWaterMarkSrcType)| 워터마크 이미지의 소스 유형. |
| [TRTCTranscodingConfigMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode)| 혼합 스트림 매개변수 설정 모드. |
