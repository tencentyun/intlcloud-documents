## TRTCCloud

### 기본 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sharedInstance.html) | TRTCCloud 싱글톤을 생성합니다. |
| [destroySharedInstance](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/destroySharedInstance.html) | TRTCCloud 싱글톤을 폐기합니다. |
| [registerListener](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/registerListener.html) | 이벤트 리스너를 등록합니다. |
| [unRegisterListener](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/unRegisterListener.html) | 이벤트 리스너를 등록 취소합니다. |

### 방 관련 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enterRoom.html) | 방에 들어갑니다. 방이 없으면 시스템에서 자동으로 방을 만듭니다.           |
| [exitRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/exitRoom.html) | 방을 나갑니다.                                                   |
| [switchRole](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/switchRole.html) | 역할을 전환합니다. 이 API는 라이브 스트리밍 시나리오(TRTC_APP_SCENE_LIVE 및 TRTC_APP_SCENE_VOICE_CHATROOM)에서만 작동합니다. |
| [setDefaultStreamRecvMode](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setDefaultStreamRecvMode.html) | 오디오/비디오 데이터 수신 모드를 설정합니다. 이 모드는 입장하기 전에 설정해야 적용됩니다.           |
| [connectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/connectOtherRoom.html) | 크로스 룸 호출을 요청합니다(호스트 PK).          |
| [disconnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/disconnectOtherRoom.html) | 크로스 룸 통화를 종료합니다.          |
| [switchRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/switchRoom.html) | 방을 바꿉니다.         |



### CDN 관련 인터페이스 함수

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishing.html) | Tencent Cloud의 라이브 스트리밍 CDN에 푸시하기 시작합니다.      |
| [stopPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishing.html) | Tencent Cloud의 라이브 스트리밍 CDN에 대한 푸시를 중지합니다.      |
| [startPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishCDNStream.html) | Tencent Cloud가 아닌 공급업체의 라이브 스트리밍 CDN으로 중계를 시작합니다.      |
| [stopPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishCDNStream.html) | Tencent Cloud가 아닌 공급업체의 라이브 스트리밍 CDN 중계를 중지합니다.     |
| [setMixTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setMixTranscodingConfig.html) | On-Cloud MixTranscoding 매개변수를 설정합니다.      |


### 비디오 관련 인터페이스 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalPreview](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startLocalPreview.html) | 로컬 비디오의 미리보기를 활성화합니다.                                     |
| [stopLocalPreview](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalPreview.html) | 로컬 비디오 캡처 및 미리 보기를 중지합니다.                                     |
| [muteLocalVideo](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteLocalVideo.html) | 로컬 비디오 데이터 푸시를 일시 중지/재개합니다.                                |
| [startRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startRemoteView.html) | 원격 사용자의 이미지 표시를 시작합니다.                                       |
| [stopRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopRemoteView.html) | 원격 사용자의 비디오 이미지 표시를 중지하고 사용자의 비디오 스트림을 가져옵니다.   |
| [stopAllRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopAllRemoteView.html) | 모든 사용자의 비디오 이미지 표시 및 비디오 스트림 가져오기를 중지합니다. |
| [muteRemoteVideoStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteRemoteVideoStream.html) | 지정된 원격 비디오 스트림 수신을 일시 중지/재개합니다.                              |
| [muteAllRemoteVideoStreams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteAllRemoteVideoStreams.html) | 모든 원격 비디오 스트림 수신을 일시 중지/재개합니다.                                |
| [setVideoEncoderParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderParam.html) | 비디오 인코더 매개변수를 설정합니다.                                     |
| [setNetworkQosParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setNetworkQosParam.html) | QoS 제어 매개변수를 설정합니다.                                       |
| [setLocalRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLocalRenderParams.html) | 로컬 이미지의 렌더링 모드를 설정합니다. |
| [setRemoteRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setRemoteRenderParams.html) | 원격 이미지 매개변수를 설정합니다. |
| [setVideoEncoderRotation](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderRotation.html) | 인코딩된 비디오 이미지, 즉 원격 사용자에게 제공되고 서버에서 녹화한 이미지의 회전을 설정합니다. |
| [setVideoEncoderMirror](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderMirror.html) | 인코딩된 이미지의 미러 모드를 설정합니다. |
| [setGSensorMode](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setGSensorMode.html) | G-센서의 적응 모드를 설정합니다. |
| [enableEncSmallVideoStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enableEncSmallVideoStream.html) | 이중 채널(큰 이미지 및 작은 이미지) 인코딩 모드를 활성화합니다. |
| [setRemoteVideoStreamType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setRemoteVideoStreamType.html) | 지정된 사용자의 작은 이미지와 큰 이미지 사이를 전환합니다.                          |
| [snapshotVideo](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/snapshotVideo.html) | 비디오 스크린샷을 찍습니다. |


### 오디오 관련 인터페이스 함수

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startLocalAudio.html) | 로컬 오디오 캡처 및 업스트림 데이터 전송을 활성화합니다.                                   |
| [stopLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalAudio.html) | 로컬 오디오 캡처 및 업스트림 데이터 전송을 비활성화합니다.                                   |
| [muteLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteLocalAudio.html) | 로컬 오디오를 음소거/음소거 해제합니다.                                    |
| [setVideoMuteImage](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoMuteImage.html) | 로컬 비디오 푸시가 일시 중지될 때 푸시될 이미지를 설정합니다.                                    |
| [setAudioRoute](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager/setAudioRoute.html) | 오디오 경로를 설정합니다.                                               |
| [muteRemoteAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteRemoteAudio.html) | 지정된 원격 사용자의 오디오를 음소거/음소거 해제합니다.                          |
| [muteAllRemoteAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteAllRemoteAudio.html) | 모든 사용자를 음소거/음소거 해제합니다.                                |
| [setAudioCaptureVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setAudioCaptureVolume.html) | SDK 캡처 볼륨을 설정합니다.                                          |
| [getAudioCaptureVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioCaptureVolume.html) | SDK 캡처 볼륨을 가져옵니다.                                          |
| [setAudioPlayoutVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setAudioPlayoutVolume.html) | SDK 재생 볼륨을 설정합니다.                                          |
| [getAudioPlayoutVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioPlayoutVolume.html) | SDK 재생 볼륨을 가져옵니다.                                          |
| [enableAudioVolumeEvaluation](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enableAudioVolumeEvaluation.html) | 볼륨 알림을 활성화합니다.                                           |
| [startAudioRecording](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startAudioRecording.html) | 오디오 녹음을 시작합니다.                                                   |
| [stopAudioRecording](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopAudioRecording.html) | 오디오 녹음을 중지합니다.                                                   |
| [setSystemVolumeType](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager/setSystemVolumeType.html) | 통화 중에 사용되는 시스템 볼륨 유형을 설정합니다.                               |


### 기기 관리 API

| API | 설명  |
|-----|-----|
| [getDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getDeviceManager.html) | 장치 관리 모듈을 가져옵니다. 자세한 내용은 [장치 관리 API](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html)를 참고하십시오. |


### 뷰티 필터 관련 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getBeautyManager.html) | 뷰티 필터 관리 객체를 가져옵니다. 자세한 내용은 [뷰티 필터 관리](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html) 문서를 참고하십시오. |
| [setWatermark](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setWatermark.html) | 워터마크를 추가합니다.                                                   |


### 음악 및 음성 효과 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioEffectManager.html) | BGM, 짧은 오디오 효과 및 음성 효과를 관리하는 데 사용되는 오디오 효과 관리 클래스 TXAudioEffectManager를 가져옵니다. 자세한 내용은 [오디오 효과 관리](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html) 문서를 참고하십시오. |

### 서브스트림 관련 인터페이스 함수

| API                                                          | 설명        |
| ------------------------------------------------------------ | -------------- |
| [startScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html) | 화면 공유를 시작합니다. |
| [stopScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopScreenCapture.html) | 화면 공유를 중지합니다. |
| [pauseScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/pauseScreenCapture.html) | 화면 공유를 일시 중지합니다. |
| [resumeScreenCapture](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/resumeScreenCapture.html) | 화면 공유를 재개합니다. |

### 사용자 정의 메시지 발송

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sendCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sendCustomCmdMsg.html) | 채팅방의 모든 사용자에게 사용자 정의 메시지를 보냅니다. |
| [sendSEIMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sendSEIMsg.html) | 비디오 프레임에 소량의 사용자 정의 데이터를 포함합니다.                                           |


### 네트워크 테스트 

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startSpeedTest.html) | 네트워크 속도 테스트를 시작합니다. 이는 화상 통화 품질을 저하시킬 수 있으므로 화상 통화 중에는 피해야 합니다. |
| [stopSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopSpeedTest.html) | 서버 속도 테스트를 중지합니다.                                             |


### Log 관련 인터페이스 함수

| API                                                          | 설명                       |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getSDKVersion.html) | SDK 버전을 가져옵니다.         |
| [setLogLevel](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogLevel.html) | Log 출력 수준을 설정합니다.         |
| [setLogDirPath](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogDirPath.html) | 로그를 저장할 경로를 변경합니다.         |
| [setLogCompressEnabled](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogCompressEnabled.html) | 로컬 Log 압축을 활성화/비활성화합니다.         |
| [setConsoleEnabled](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setConsoleEnabled.html) | 콘솔 로그 인쇄를 활성화/비활성화합니다.  |


## TRTCCloudListener

TRTC 화상 통화 기능을 위한 콜백 API.

### 오류 및 경고 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onError) | 오류 콜백. 이는 SDK에 복구할 수 없는 오류가 발생했음을 나타냅니다. 이러한 오류를 청취해야 하며 필요한 경우 UI 메시지를 사용자에게 표시해야 합니다. |
| [onWarning](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onWarning) | 경고 콜백. 이는 지연 또는 복구 가능한 디코딩 실패와 같은 심각하지 않은 문제에 대해 경고합니다. |


### 방 이벤트 콜백 API

| API                                                          | 설명                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onEnterRoom) | 방 입장 콜백.                  |
| [onExitRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onExitRoom) | 방 종료 콜백.                |
| [onSwitchRole](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSwitchRole) | 역할 전환 콜백.                |
| [onConnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onConnectOtherRoom) | 크로스 룸 호출 요청 결과의 콜백(호스트 PK).         |
| [onDisConnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onDisConnectOtherRoom) | 크로스 룸 호출 종료 결과의 콜백(호스트 PK).        |
| [onSwitchRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSwitchRoom) | 방 전환 결과의 콜백(switchRoom).               |

### 사용자 이벤트 콜백 API

| API                                                          | 설명                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRemoteUserEnterRoom) | 사용자 입장 콜백.                |
| [onRemoteUserLeaveRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRemoteUserLeaveRoom) | 사용자 퇴장 콜백.                |
| [onUserVideoAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserVideoAvailable) | 원격 사용자에게 재생 가능한 기본 이미지(일반적으로 카메라의 이미지)가 있는지 여부에 대한 콜백. |
| [onUserSubStreamAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserSubStreamAvailable) | 원격 사용자에게 재생 가능한 서브스트림 이미지(일반적으로 화면 공유 이미지)가 있는지 여부에 대한 콜백. |
| [onUserAudioAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserAudioAvailable) | 원격 사용자의 재생 가능한 오디오 존재 여부 콜백.        |
| [onFirstVideoFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onFirstVideoFrame) | 로컬 사용자 또는 원격 사용자의 첫 번째 비디오 프레임 렌더링 콜백.           |
| [onFirstAudioFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onFirstAudioFrame) | 원격 사용자의 첫 번째 오디오 프레임 재생의 콜백. 로컬 오디오에 대한 알림이 전송되지 않습니다.   |
| [onSendFirstLocalVideoFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSendFirstLocalVideoFrame) | 첫 번째 로컬 비디오 프레임 발송 완료 콜백.    |
| [onSendFirstLocalAudioFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSendFirstLocalAudioFrame) | 첫 번째 로컬 오디오 프레임 발송 완료 콜백.       |

### 배경 음악 재생을 위한 콜백 API

배경 음악 재생을 위한 콜백 API.

| API                                                          | 설명                  |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMusicObserverStart) | 음악 재생 시작 콜백. |
| [onMusicObserverPlayProgress](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMusicObserverPlayProgress) | 음악 재생 진행 콜백. |
| [onMusicObserverComplete](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMusicObserverComplete) | 음악 재생 종료 콜백. |

### 네트워크 품질 및 기술 메트릭에 대한 통계를 위한 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onNetworkQuality) | 네트워크 품질의 콜백. 이 콜백은 현재 업스트림 및 다운스트림 데이터 전송 품질에 대한 통계를 수집하기 위해 2초마다 트리거됩니다. |
| [onStatistics](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStatistics) | 기술 지표에 대한 통계 콜백.                          |


### 서버 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onConnectionLost) | 서버에서 SDK 연결 해제 콜백.                |
| [onTryToReconnect](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onTryToReconnect) | 서버에 다시 연결을 시도하는 SDK의 콜백.                |
| [onConnectionRecovery](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onConnectionRecovery) | SDK 서버 재연결 콜백.         |
| [onSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSpeedTest) | 서버 속도 테스트 결과의 콜백. SDK는 여러 서버 주소의 속도를 테스트하고 각 테스트의 결과는 이 콜백을 통해 반환됩니다. |


### 하드웨어 이벤트 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onCameraDidReady) | 준비 중인 카메라의 콜백.                                             |
| [onMicDidReady](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMicDidReady) | 준비 중인 마이크의 콜백.                         |
| [onUserVoiceVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onUserVoiceVolume) | 각 userId의 볼륨과 전체 원격 볼륨을 포함한 볼륨의 콜백. |


### 사용자 정의 메시지 수신 콜백

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onRecvCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRecvCustomCmdMsg) | 사용자 정의 메시지 수신 콜백. |
| [onMissCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onMissCustomCmdMsg) | 사용자 정의 메시지 손실 콜백. |
| [onRecvSEIMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onRecvSEIMsg) | SEI 메시지 수신 콜백. |


### CDN 릴레이 푸시용 콜백 API

| API                                                          | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStartPublishing) | [TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishing.html)의 startPublishing() API에 해당하는 Tencent Cloud의 라이브 스트리밍 CDN으로 푸시 시작 콜백. |
| [onStopPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStopPublishing) | [TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishing.html)의 stopPublishing() API에 해당하는 Tencent Cloud의 라이브 스트리밍 CDN으로 푸시 중지 콜백. |
| [onStartPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStartPublishCDNStream) | CDN으로 릴레이 푸시 시작 완료에 대한 콜백.|
| [onStopPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onStopPublishCDNStream) | CDN에 대한 릴레이 푸시 중지 완료 콜백.|
| [onSetMixTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSetMixTranscodingConfig) | [TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setMixTranscodingConfig.html)의 setMixTranscodingConfig() API에 해당하는 On-Cloud MixTranscoding 매개변수 설정의 콜백. |


### 화면 공유 콜백

| API                                                          | 설명             |
| ------------------------------------------------------------ | ---------------- |
| [onScreenCaptureStarted](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCaptureStarted) | 화면 공유 시작 콜백 |
| [onScreenCapturePaused](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCapturePaused) | pauseScreenCapture() 호출을 통한 일시 중지 화면 공유 콜백. |
| [onScreenCaptureResumed](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCaptureResumed) | resumeScreenCapture() 호출을 통한 화면 공유 재개 콜백. |
| [onScreenCaptureStoped](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onScreenCaptureStoped) | 화면 공유 중지 콜백. |

### 화면 캡처 콜백

| API                                                          | 설명             |
| ------------------------------------------------------------ | ---------------- |
| [onSnapshotComplete](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener.html#onSnapshotComplete) | 스크린샷 완료 콜백. |


## 주요 클래스의 정의

| 클래스                                                         | 설명                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCCloudDef](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCCloudDef-class.html) | 주요 클래스 정의를 위한 변수.                              |
| [TRTCParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCParams-class.html) | 방 입장 매개변수.                              |
| [TRTCSwitchRoomConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCSwitchRoomConfig-class.html) | 방 전환 매개변수.                              |
| [TRTCVideoEncParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCVideoEncParam-class.html) | 비디오 인코딩 매개변수.                              |
| [TRTCNetworkQosParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCNetworkQosParam-class.html) | QoS 제어 매개변수.                      |
| [TRTCRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCRenderParams-class.html) | 원격 이미지 매개변수. |
| [TRTCMixUser](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCMixUser-class.html) | On-Cloud MixTranscoding에서 각 채널의 이미지 위치. |
| [TRTCTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCTranscodingConfig-class.html) | On-Cloud MixTranscoding 구성. |
| [TXVoiceChangerType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TXVoiceChangerType-class.html) | 목소리 변화 유형 정의(소녀, 중년 남성, 메탈, 외국 억양 등). |
| [TXVoiceReverbType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TXVoiceReverbType-class.html) | 리버브 효과 유형의 정의(KTV, 룸, 홀, 로우 앤 딥, 레조넌트 등). |
| [AudioMusicParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/AudioMusicParam-class.html) | 음악 및 음성 효과 설정 API에 대한 매개변수. |
| [TRTCAudioRecordingParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCAudioRecordingParams-class.html) | 오디오 녹음 매개변수. |
| [TRTCPublishCDNParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCPublishCDNParam-class.html) | CDN 릴레이 푸시 매개변수. |
