## TRTCCloud

### 기본 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#sharedInstance) | TRTCCloud 싱글톤을 생성합니다. |
| [destroySharedInstance](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#destroySharedInstance) | TRTCCloud 싱글톤을 폐기합니다. |
| [registerListener](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#registerListener) | 이벤트 리스너를 등록합니다. |
| [unRegisterListener](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#unRegisterListener) | 이벤트 리스너를 등록 취소합니다. |

### 방 관련 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#enterRoom) | 방에 입장합니다. 방이 없으면 시스템에서 방을 자동 생성합니다.           |
| [exitRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#exitRoom) | 방에서 퇴장합니다.                                                   |
| [switchRole](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#switchRole) | 역할을 전환합니다. 이 API는 라이브 스트리밍 시나리오(TRTC_APP_SCENE_LIVE 및 TRTC_APP_SCENE_VOICE_CHATROOM)에서만 작동합니다. |
| [setDefaultStreamRecvMode](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setDefaultStreamRecvMode) | 오디오/비디오 데이터 수신 모드를 설정합니다. 이 모드는 입장하기 전에 설정해야 적용됩니다.           |
| [connectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#connectOtherRoom) | 크로스 룸 호출을 요청합니다(호스트 PK).          |
| [disconnectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#disconnectOtherRoom) | 크로스 룸 통화를 종료합니다.          |
| [switchRoom](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#switchRoom) | 방을 바꿉니다.         |



### CDN 관련 인터페이스 함수

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startPublishing) | Tencent Cloud의 라이브 스트리밍 CDN에 대한 푸시를 시작합니다.      |
| [stopPublishing](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopPublishing) | Tencent Cloud의 라이브 스트리밍 CDN에 대한 푸시를 중지합니다.      |
| [startPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startPublishCDNStream) | 타사 라이브 스트리밍 CDN에 대한 중계를 시작합니다.      |
| [stopPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopPublishCDNStream) | 타사 라이브 스트리밍 CDN에 대한 중계를 중지합니다.     |
| [setMixTranscodingConfig](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setMixTranscodingConfig) | On-Cloud MixTranscoding 매개변수를 설정합니다.      |


### 비디오 관련 인터페이스 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [muteLocalVideo](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteLocalVideo) | 로컬 비디오 데이터 푸시를 일시 중지/재개합니다.                                |
| [startRemoteView](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startRemoteView) | 원격 사용자의 이미지를 표시하기 시작합니다.                                       |
| [stopRemoteView](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopRemoteView) | 원격 사용자의 비디오 이미지 표시를 중지하고 사용자의 비디오 스트림을 가져옵니다.   |
| [muteRemoteVideoStream](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteRemoteVideoStream) | 지정된 원격 비디오 스트림 수신을 일시 중지/재개합니다.                              |
| [muteAllRemoteVideoStreams](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteAllRemoteVideoStreams) | 모든 원격 비디오 스트림 수신을 일시 중지/재개합니다.                                |
| [setVideoEncoderParam](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoEncoderParam) | 비디오 인코더 매개변수를 설정합니다.                                     |
| [setNetworkQosParam](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setNetworkQosParam) | QoS 제어 매개변수를 설정합니다.                                       |
| [setVideoEncoderRotation](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoEncoderRotation) | 인코딩된 비디오 이미지, 즉 원격 사용자에게 제공되고 서버에서 녹화한 이미지의 회전을 설정합니다. |
| [setVideoEncoderMirror](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoEncoderMirror) | 인코딩된 이미지의 미러 모드를 설정합니다. |
| [setGSensorMode](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setGSensorMode) | G-센서의 적응 모드를 설정합니다. 
| [setVideoMuteImage](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setVideoMuteImage) | 로컬 비디오 푸시가 일시 중지될 때 푸시될 이미지를 설정합니다.                                    |

### 오디오 관련 인터페이스 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startLocalAudio) | 로컬 오디오 캡처 및 업스트림 데이터 전송을 활성화합니다.                                   |
| [stopLocalAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopLocalAudio) | 로컬 오디오 캡처 및 업스트림 데이터 전송을 비활성화합니다.                                   |
| [muteLocalAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteLocalAudio) | 로컬 오디오를 음소거/음소거 해제합니다.                                    |
| [setAudioRoute](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_device_manager.default.html#setAudioRoute) | 오디오 경로를 설정합니다.                                               |
| [muteRemoteAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteRemoteAudio) | 지정된 원격 사용자의 오디오를 음소거/음소거 해제합니다.                          |
| [muteAllRemoteAudio](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#muteAllRemoteAudio) | 모든 사용자를 음소거/음소거 해제합니다.                                |
| [setAudioCaptureVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setAudioCaptureVolume) | SDK 캡처 볼륨을 설정합니다.                                          |
| [getAudioCaptureVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getAudioCaptureVolume) | SDK 캡처 볼륨을 가져옵니다.                                          |
| [setAudioPlayoutVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setAudioPlayoutVolume) | SDK 재생 볼륨을 설정합니다.                                          |
| [getAudioPlayoutVolume](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getAudioPlayoutVolume) | SDK 재생 볼륨을 가져옵니다.                                          |
| [enableAudioVolumeEvaluation](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#enableAudioVolumeEvaluation) | 볼륨 알림을 활성화합니다.                                           |
| [startAudioRecording](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startAudioRecording) | 오디오 녹음을 시작합니다.                                                   |
| [stopAudioRecording](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopAudioRecording) | 오디오 녹음을 중지합니다.                                                   |


### 기기 관리 API

| API      | 설명   |
|-----|-----|
| [getDeviceManager](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getDeviceManager) | 장치 관리 모듈을 가져옵니다. 자세한 내용은 [기기 관리 API](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_device_manager.default.html)를 참고하십시오. |


### 뷰티 필터 관련 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getBeautyManager) | 뷰티 필터 관리 개체를 가져옵니다. 자세한 내용은 [뷰티 필터 관리 문서](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_beauty_manager.default.html)를 참고하십시오. |
| [setWatermark](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setWatermark) | 워터마크를 추가합니다.                                                   |


### 음악 및 음성 효과 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getAudioEffectManager) | BGM, 짧은 오디오 효과 및 음성 효과를 관리하는 데 사용되는 오디오 효과 관리 클래스 TXAudioEffectManager를 가져옵니다. 자세한 내용은 [오디오 효과 관리](https://comm.qq.com/trtc-react-native-en/api2/classes/tx_audio_effect_manager.default.html) 문서를 참고하십시오. |

### 네트워크 테스트 

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startSpeedTest) | 네트워크 속도 테스트를 시작합니다(영상 통화 품질을 저하시킬 수 있으므로 영상 통화 중에는 피해야 합니다). |
| [stopSpeedTest](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopSpeedTest) | 서버 속도 테스트를 중지합니다.                                             |


### Log 관련 인터페이스 함수

| API                                                          | 설명                       |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#getSDKVersion) | SDK 버전을 가져옵니다.         |
| [setLogLevel](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setLogLevel) | Log 출력 수준을 설정합니다.         |
| [setLogDirPath](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setLogDirPath) | 로그를 저장할 경로를 변경합니다.         |
| [setLogCompressEnabled](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setLogCompressEnabled) | 로컬 Log 압축을 활성화/비활성화합니다.         |
| [setConsoleEnabled](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setConsoleEnabled) | 콘솔 로그 인쇄를 활성화/비활성화합니다.  |


## TRTCCloudListener

TRTC 화상 통화 기능을 위한 콜백 API

### 오류 및 경고 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onError) | 오류 콜백. 이는 SDK에 복구할 수 없는 오류가 발생했음을 나타냅니다. 이러한 오류를 청취해야 하며 필요한 경우 UI 메시지를 사용자에게 표시해야 합니다. |
| [onWarning](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onWarning) | 경고 콜백. 이는 지연 또는 복구 가능한 디코딩 실패와 같은 심각하지 않은 문제에 대해 경고합니다. |


### 방 이벤트 콜백 API

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onEnterRoom) | 방 입장 콜백.                  |
| [onExitRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onExitRoom) | 방 퇴장 콜백.                |
| [onSwitchRole](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSwitchRole) | 역할 전환 콜백.                |
| [onConnectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectOtherRoom) | 크로스 룸 호출 요청 결과의 콜백(호스트 PK).         |
| [onDisConnectOtherRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onDisConnectOtherRoom) | 크로스 룸 호출 종료 결과의 콜백(호스트 PK).        |
| [onSwitchRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSwitchRoom) | 방 전환 결과의 콜백(switchRoom).               |

### 사용자 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onRemoteUserEnterRoom) | 사용자 항목의 콜백.                |
| [onRemoteUserLeaveRoom](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onRemoteUserLeaveRoom) | 사용자 퇴장 콜백.                |
| [onUserVideoAvailable](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserVideoAvailable) | 원격 사용자에게 재생 가능한 기본 이미지(일반적으로 카메라의 이미지)가 있는지 여부에 대한 콜백. |
| [onUserSubStreamAvailable](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserSubStreamAvailable) | 원격 사용자에게 재생 가능한 서브스트림 이미지(일반적으로 화면 공유 이미지)가 있는지 여부에 대한 콜백. |
| [onUserAudioAvailable](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserAudioAvailable) | 원격 사용자에게 재생 가능한 오디오가 있는지 여부에 대한 콜백.        |
| [onFirstVideoFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onFirstVideoFrame) | 로컬 사용자 또는 원격 사용자의 첫 번째 비디오 프레임을 렌더링하는 콜백.           |
| [onFirstAudioFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onFirstAudioFrame) | 원격 사용자의 첫 번째 오디오 프레임 재생의 콜백(로컬 오디오에 대한 알림은 전송되지 않습니다).   |
| [onSendFirstLocalVideoFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSendFirstLocalVideoFrame) | 첫 번째 로컬 비디오 프레임 발송 완료 콜백.    |
| [onSendFirstLocalAudioFrame](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSendFirstLocalAudioFrame) | 첫 번째 로컬 오디오 프레임 발송 완료 콜백.       |

### 배경 음악 재생을 위한 콜백 API

배경 음악 재생을 위한 콜백 API

| API                                                          | 설명                  |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverStart) | 음악 재생 시작 콜백. |
| [onMusicObserverPlayProgress](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverPlayProgress) | 음악 재생 진행 콜백. |
| [onMusicObserverComplete](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverComplete) | 음악 재생 종료 콜백. |

### 네트워크 품질 및 기술 메트릭에 대한 통계를 위한 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onNetworkQuality) | 네트워크 품질의 콜백. 이 콜백은 현재 업스트림 및 다운스트림 데이터 전송 품질에 대한 통계를 수집하기 위해 2초마다 트리거됩니다. |
| [onStatistics](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStatistics) | 기술 지표에 대한 통계 콜백.                          |


### 서버 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectionLost) | 서버에서 SDK 연결 해제 콜백.                |
| [onTryToReconnect](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onTryToReconnect) | 서버에 다시 연결을 시도하는 SDK의 콜백.                |
| [onConnectionRecovery](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onConnectionRecovery) | SDK를 서버에 재연결하는 콜백.         |
| [onSpeedTest](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSpeedTest) | 서버 속도 테스트 결과의 콜백. SDK는 여러 서버 주소의 속도를 테스트하고 각 테스트의 결과는 이 콜백을 통해 반환됩니다. |


### 하드웨어 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onCameraDidReady) | 준비 중인 카메라의 콜백.                                             |
| [onMicDidReady](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onMicDidReady) | 준비 중인 마이크의 콜백.                         |
| [onUserVoiceVolume](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onUserVoiceVolume) | 각 userId의 볼륨과 전체 원격 볼륨을 포함한 볼륨의 콜백. |

### CDN 릴레이 푸시용 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishing) | [TRTCCloud](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#startPublishing)의 startPublishing() API에 해당하는 Tencent Cloud의 라이브 스트리밍 CDN으로 푸시 시작 콜백. |
| [onStopPublishing](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStopPublishing) | [TRTCCloud](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#stopPublishing)의 stopPublishing() API에 해당하는 Tencent Cloud의 라이브 스트리밍 CDN으로 푸시 중지 콜백. |
| [onStartPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishCDNStream) | CDN으로 릴레이 푸시 시작 완료에 대한 콜백.|
| [onStopPublishCDNStream](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onStopPublishCDNStream) | CDN에 대한 릴레이 푸시 중지 완료 콜백.|
| [onSetMixTranscodingConfig](https://comm.qq.com/trtc-react-native-en/api2/enums/trtc_cloud.TRTCCloudListener.html#onSetMixTranscodingConfig) | [TRTCCloud](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud.default.html#setMixTranscodingConfig)의 setMixTranscodingConfig() API에 해당하는 On-Cloud MixTranscoding 매개변수 설정의 콜백. |

## 주요 클래스의 정의

| 클래스                                                         | 설명                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCCloudDef](https://comm.qq.com/trtc-react-native-en/api2/classes/trtc_cloud_def.TRTCCloudDef.html) | 주요 클래스 정의를 위한 변수.                              |
| [TRTCParams](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCParams) | 방 입장 매개변수.                              |
| [TRTCSwitchRoomConfig](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCSwitchRoomConfig) | 방 전환 매개변수.                              |
| [TRTCVideoEncParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCVideoEncParam) | 비디오 인코딩 매개변수.                              |
| [TRTCNetworkQosParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCNetworkQosParam) | QoS 제어 매개변수.                      |
| [TRTCRenderParams](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCRenderParams) | 원격 이미지 매개변수. |
| [TRTCMixUser](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCMixUser) | On-Cloud MixTranscoding에서 각 채널의 이미지 위치. |
| [TRTCTranscodingConfig](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCTranscodingConfig) | On-Cloud MixTranscoding 구성. |
| [TXVoiceChangerType](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TXVoiceChangerType) | 음성 변조 유형의 정의(소녀, 중년남성, 메탈, 외국 억양 등). |
| [TXVoiceReverbType](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TXVoiceReverbType) | 리버브 효과 유형의 정의(노래방, 룸, 홀, 로우 앤 딥, 레조넌트 등). |
| [AudioMusicParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#AudioMusicParam) | 음악 및 음성 효과 설정 API에 대한 매개변수. |
| [TRTCAudioRecordingParams](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCAudioRecordingParams) | 오디오 녹음 매개변수. |
| [TRTCPublishCDNParam](https://comm.qq.com/trtc-react-native-en/api2/modules/trtc_cloud_def.html#TRTCPublishCDNParam) | CDN 릴레이 푸시 매개변수. |
