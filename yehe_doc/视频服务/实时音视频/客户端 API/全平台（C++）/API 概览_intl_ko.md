## C++ 전체 플랫폼 인터페이스 소개
8.0 버전부터 기존 Windows(C++) 인터페이스를 기반으로 Windows, iOS, Mac, Android 플랫폼에 적용되는 새로운 C++ 인터페이스를 제공합니다.
C++ 인터페이스 통합 방법에 대한 자세한 내용은 각 플랫폼의 통합 가이드를 참조하십시오.  
- [iOS C++ 인터페이스 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35092)  
- [Android C++ 인터페이스 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35093)  
- [Mac C++ 인터페이스 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35094)  
- [Windows 통합 가이드](https://intl.cloud.tencent.com/document/product/647/35095)  

>?
>- 현재 C++ 인터페이스는 라이트 버전(TRTC)에서만 제공됩니다.  
>- TRTC 헤더 파일은 Windows 플랫폼에서 'trtc' 네임스페이스를 자동으로 사용하고 있으므로 다시 지정할 필요가 없습니다.

## ITRTCCloud @ TXLiteAVSDK
### ITRTCCloudCallback 콜백 설정

| API | 설명 |
|-----|-----|
| [addCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | 콜백 인터페이스 [ITRTCCloudCallback](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#classtrtc_1_1ITRTCCloudCallback) 설정 |
| [removeCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | 이벤트 콜백 삭제 |



### 방 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) | 방 입장 |
| [exitRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | 방 퇴장 |
| [switchRole](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | 역할 전환. 라이브 방송 시나리오(TRTCAppSceneLIVE 및 TRTCAppSceneVoiceChatRoom)에만 적용됩니다. |
| [connectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae472af11c30db29fcd21ea01854ab32f) | 크로스 룸 통화 요청(호스트 PK) |
| [disconnectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | 크로스 룸 마이크 연결 해제 |
| [setDefaultStreamRecvMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | 멀티미디어 데이터 수신 모드 설정. 방 입장 전 설정해야만 적용됩니다. |
| [createSubCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | 서브 TRTCCloud 인스턴스 생성 |
| [destroySubCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0555e9e9d9d02c8c116946915f969d18) | 서브 TRTCCloud 인스턴스 폐기 |
| [switchRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | 방 전환 |


### CDN 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac2f616263c108bf6ac5ef2b66b83a380) | Tencent Cloud 라이브 방송 CDN에 스트림 푸시 시작 |
| [stopPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Tencent Cloud 라이브 방송 CDN에 스트림 푸시 중지 |
| [startPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | 다른 업체 클라우드의 라이브 방송 CDN에 스트림 공유 시작 |
| [stopPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Tencent Cloud가 아닌 주소에 스트림 공유 중지 |
| [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | 클라우드의 혼합 스트림 트랜스 코딩 매개변수 설정 |


### 비디오 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df) | 로컬 비디오 화면 미리보기(Windows 및 Mac 버전) 활성화 |
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df2) | 로컬 비디오 화면 미리보기(iOS 및 Android 버전) 활성화. enterRoom 전 해당 함수를 호출하면 SDK가 카메라만 활성화하며, enterRoom을 호출해야만 스트림을 푸시하기 시작합니다. enterRoom 후 해당 함수를 호출하면 SDK가 카메라를 활성화하고 자동으로 비디오 스트림을 푸시하기 시작합니다. 카메라 화면 첫 프레임의 렌더링이 시작되면 사용자는 [ITRTCCloudCallback](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#classtrtc_1_1ITRTCCloudCallback)의 onFirstVideoFrame(null) 콜백을 수신합니다. |
| [updateLocalView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6db572d1e387b21328c6c78de561838c) | 로컬 비디오 화면 미리보기 창 새로고침 |
| [stopLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | 로컬 비디오 수집 및 미리보기 중지 |
| [muteLocalVideo](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6070313a28d3302c94ad807c636eb60f) | 로컬 비디오 데이터 전송 일시 중지/다시 시작 |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a25f09552efac99d88a7aad53960146d7) | 지정 사용자의 원격 화면 풀링 및 표시 활성화 |
| [updateRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9f774f9abb7970fb32c3172fa3229fd2) | 원격 비디오 렌더링 창 새로고침 |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | 원격 비디오 화면 표시를 중지하고 해당 원격 사용자의 비디오 데이터 스트림을 다시 풀링하지 않습니다. |
| [stopAllRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | 모든 원격 비디오 화면 표시를 중지하고 원격 사용자의 비디오 데이터 스트림을 다시 풀링하지 않습니다. |
| [muteRemoteVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a22155f6fe17dde77a16c273e0d5a02a3) | 지정 원격 비디오 스트림 수신 일시 중지/다시 시작 |
| [muteAllRemoteVideoStreams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | 모든 원격 비디오 스트림 수신 일시 중지/다시 시작 |
| [setVideoEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa2bc2739031035b40e8f2a76184c20d9) | 비디오 인코더 관련 매개변수 설정 |
| [setNetworkQosParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a374f1000d443de80d70747cba876f879) | 네트워크 트래픽 제어 관련 매개변수 설정 |
| [setLocalRenderParams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | 로컬 이미지(메인 스트림)의 렌더링 매개변수 설정 |
| [setVideoEncoderRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | 비디오 인코딩이 출력되는 화면 방향 설정. 원격 사용자가 시청하는 화면과 서버가 녹화하는 화면 방향을 설정합니다. |
| [setVideoEncoderMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | 인코더의 출력 화면 이미지 모드 설정 |
| [setRemoteRenderParams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | 원격 이미지의 렌더링 모드 설정 |
| [enableSmallVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a80648f76afbda35c9bf5d96701c62a9e) | 크고 작은 화면의 듀얼 채널 인코딩 모드 활성화 |
| [setRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abd330074a9e99cb9c75d42ef3d1d63a0) | 지정 userId의 화면 선택(큰 화면/작은 화면) |
| [snapshotVideo](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | 비디오 화면 캡처 |


### 오디오 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | 로컬 오디오 수집 및 업스트림 활성화 |
| [stopLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | 로컬 오디오 수집 및 업스트림 비활성화 |
| [muteLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | 로컬 오디오 음소거/음소거 취소 |
| [muteRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | 지정 원격 사용자 오디오 음소거/음소거 취소 |
| [muteAllRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | 모든 사용자 오디오 음소거/음소거 취소 |
| [setRemoteAudioVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | 특정 원격 사용자의 재생 음량 설정 |
| [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | SDK 수집 음량 설정 |
| [getAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | SDK 수집 음량 획득 |
| [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | SDK 재생 음량 설정 |
| [getAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | SDK 재생 음량 획득 |
| [enableAudioVolumeEvaluation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | 음량 크기 표시 활성화 또는 비활성화 |
| [startAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a15b74c793aea807ef9142230c088473b) | 녹음 시작 |
| [stopAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | 녹음 중지 |
| [startLocalRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | 로컬 녹음 시작 |
| [stopLocalRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | 로컬 녹음 중지 |


### 디바이스 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [getDeviceManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | 디바이스 관리 모듈 획득 |


### 뷰티 필터 특수 효과 및 이미지 워터마크

| API | 설명 |
|-----|-----|
| [setBeautyStyle](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | 뷰티 필터, 미색, 안색 보정 효과 레벨 설정 |
| [setWaterMark](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | 워터마크 설정 |


### 음향 특수 효과 및 보이스 특수 효과

| API | 설명 |
|-----|-----|
| [getAudioEffectManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) |음향 효과 관리 유형 ITXAudioEffectManager 획득 |
| [startSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6a651a786871927917b087ae7094c8a) | 시스템 오디오 수집 활성화 |
| [stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | 시스템 오디오 수집 비활성화 |
| [setSystemAudioLoopbackVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | 시스템 오디오 수집 음량 설정 |


### 화면 공유 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0f8b23d8c48b9a056ca0e61ddcc894f) | 화면 공유 시작 |
| [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | 화면 수집 중지 |
| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | 화면 공유 일시 중지 |
| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | 화면 공유 다시 시작 |
| [getScreenCaptureSources](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3777e1506f1aa806bee116e7117993b5) | 공유 가능한 화면 창 열거. startScreenCapture 전 호출을 권장합니다. |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a) | 화면 공유 매개변수 설정. 해당 방법은 화면 공유 중에도 호출할 수 있습니다. |
| [setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abdc3d6339afd741bd8d3ed88ea551282) | 화면 공유 인코더 매개변수 설정 |
| [setSubStreamMixVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | 화면 공유 믹싱 음량 크기 설정 |
| [addExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0edaac7111c63d9a00b7749ee0c7b137) | 지정 창을 화면 공유 제외 리스트에 추가. 제외 리스트에 추가된 창은 공유되지 않습니다. |
| [removeExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a39db493034f2898788898e6669168c61) | 지정 창을 화면 공유 제외 리스트에서 제거 |
| [removeAllExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | 모든 창을 화면 공유 제외 리스트에서 제거 |
| [addIncludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a76c684e860bca4e48f06269261d73fc0) | 지정 창을 화면 공유 리스트에 추가. 공유 리스트에 추가된 창이 창 수집 구역에 있는 경우 공유됩니다. |
| [removeIncludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae9e324dac071b6d2bbc7b6e2a676ea05) | 지정 창을 화면 공유 리스트에서 제거 |
| [removeAllIncludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | 모든 창을 화면 공유 리스트에서 제거 |


### 사용자 정의 수집 및 렌더링

| API | 설명 |
|-----|-----|
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3278ac2b7b2e093ef22332cff3e6d97f) | 사용자 정의 비디오 수집 모드 활성화 |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629) | 사용자가 수집한 비디오 데이터를 SDK에 전송 |
| [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | 사용자 정의 오디오 수집 모드 활성화. 해당 모드를 활성화하면 SDK에서 기존의 오디오 수집 프로세스 실행이 중지되고 인코딩과 전송 기능만 유지됩니다. 사용자는 수집한 오디오 데이터를 [sendCustomAudioData()](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d)로 SDK에 전송해야 합니다. |
| [sendCustomAudioData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | 사용자가 수집한 오디오 데이터를 SDK에 전송 |
| [enableMixExternalAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | 외부 오디오의 푸시 스트림 혼합 여부 및 혼합 재생 여부 제어 |
| [mixExternalAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f) | 사용자 정의 서브스트림 오디오 데이터를 SDK에 전송 |
| [setLocalVideoRenderCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | 로컬 비디오 사용자 정의 렌더링 설정 |
| [setRemoteVideoRenderCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | 원격 비디오 사용자 정의 렌더링 설정 |
| [setAudioFrameCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | 오디오 데이터 콜백 설정 |
| [generateCustomPTS](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | 사용자 정의 타임스탬프 수집 생성 |


### 사용자 정의 메시지 발송

| API | 설명 |
|-----|-----|
| [sendCustomCmdMsg](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | 방 안에 있는 모든 사용자에게 사용자 정의 메시지 발송 |
| [sendSEIMsg](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | 데이터 양이 적은 사용자 정의 데이터를 비디오 프레임에 삽입 |


### 디바이스 및 네트워크 테스트

| API | 설명 |
|-----|-----|
| [startSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af86b2903b95b6e74f02d701701ce3380) | 네트워크 속도 테스트 실행. 통화 품질에 영향을 미칠 수 있으므로 영상 통화 중에는 테스트를 실행하지 마십시오. |
| [stopSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | 네트워크 속도 테스트 중지 |


### LOG 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [getSDKVersion](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | SDK 버전 정보 획득 |
| [setLogLevel](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Log 출력 레벨 설정 |
| [setConsoleEnabled](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | 콘솔 로그 출력 활성화/비활성화 |
| [setLogCompressEnabled](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | Log 로컬 압축 활성화 또는 비활성화 |
| [setLogDirPath](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | 로그 저장 경로 설정 |
| [setLogCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | 로그 콜백 설정 |
| [showDebugView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | 대시보드 보기 |
| [callExperimentalAPI](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab15fc0877664a8ac257ca4d6e7afc7b0) | 실용적인 API 인터페이스 호출 |


### 사용하지 않는 인터페이스 함수

| API | 설명 |
|-----|-----|
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | 로컬 오디오 수집 및 업스트림 활성화 |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a50ec31c281de91903a1ef492a2ec7997) | 원격 비디오 화면 표시 시작 |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | 원격 비디오 화면 표시를 중지하고 해당 원격 사용자의 비디오 데이터 스트림을 다시 풀링하지 않습니다. |
| [setLocalViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acdfe0dc822f074d5c42dfe308dc313a0) | 로컬 이미지 채우기 모드 설정 |
| [setLocalViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4447783c52960cffbaedb7ccd7c456a2) | 로컬 이미지 시계 방향 회전 각도 설정 |
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5a04c60eb2e9997e745412374b7b8d19) | 로컬 카메라 화면 미리보기 이미지 모드 설정 |
| [setRemoteViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab5be71379d671f77b99cf6ccd86cdbc7) | 원격 이미지 렌더링 모드 설정 |
| [setRemoteViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a385042d69e79468c9ef60dee8ec8cc96) | 원격 이미지 시계 방향 회전 각도 설정 |
| [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5935a852496c1a033576cc6fbf676746) | 원격 사용자의 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 표시 시작 |
| [stopRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a56a7770d90cad9141aecbd70d93af588) | 원격 사용자의 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 표시 중지. v8.0 버전은 사용하지 않습니다. stopRemoteView(userId,streamType) 인터페이스를 사용하십시오. |
| [setRemoteSubStreamViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7832e5870431ccb0e75614b51af51205) | 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 표시 모드 설정 |
| [setRemoteSubStreamViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab63344839afca9bd4a890f6f609fd9e7) | 서브 채널 화면(TRTCVideoStreamTypeSub, 일반적으로 화면 공유에 사용) 시계 방향 회전 각도 설정 |
| [setAudioQuality](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a742eefe8508e744918f704e2fa0d3405) | 오디오 품질 설정 |
| [setPriorRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a074579fcbcd5f4639ab40a2d5884fa3f) | 시청자 측에서 우선 선택한 비디오 품질로 설정 |
| [getCameraDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ace7e563213b43c1763b1eb60d5b2e8c5) | 카메라 디바이스 리스트 획득 |
| [setCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af5ce3a160a7f0dc889322983f5cfa68a) | 사용할 카메라 설정 |
| [getCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0f4a19bdc82b81dd1e0a8ac8b735261a) | 현재 사용 중인 카메라 획득 |
| [getMicDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab85ff9472d499bd740f953ccff549147) | 마이크 디바이스 리스트 획득 |
| [getCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5a17cc110f2b9c146df4498aa35eebc6) | 현재 선택한 마이크 획득 |
| [setCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aded68bf47cb1e381961b0b69dde8931b) | 사용할 마이크 설정 |
| [getCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#addb5ea84bf67a3fdd49eee30e66f4826) | 현재 시스템의 마이크 디바이스 음량 획득 |
| [setCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaa35154699a59962bc065519e79761fa) | 현재 시스템의 마이크 디바이스 음량 설정 |
| [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a44453f04c53f19f65ca362a1cb55963b) | 현재 시스템의 마이크 디바이스 음소거 여부 설정 |
| [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac7df6f29e11ded5faf7996334d4af61b) | 현재 시스템의 마이크 디바이스 음소거 여부 획득 |
| [getSpeakerDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20fa0073543ed1bd1df5dbb825b408bf) | 스피커 디바이스 리스트 획득 |
| [getCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0ac0ecdbf0d077563fd6d2fb1ee65bee) | 현재 스피커 디바이스 획득 |
| [setCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a768367aba35b104f8529740b86802b73) | 사용할 스피커 설정 |
| [getCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#accb2d6bc752f550b968462ba5a5c0538) | 현재 시스템의 스피커 디바이스 음량 획득 |
| [setCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae99882060b048467a0f39f13b168775f) | 현재 시스템의 스피커 디바이스 음량 설정 |
| [setCurrentSpeakerDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad8c3800ba3e2101ff63de7117dc729f3) | 현재 시스템의 스피커 디바이스 음소거 여부 설정 |
| [getCurrentSpeakerDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4ec49fc0c07c04031d328db5814793f) | 현재 시스템의 스피커 디바이스 음소거 여부 획득 |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | 카메라 테스트 시작 |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | 카메라 테스트 시작 |
| [stopCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3cb3fd62d04b5975c9c50210e98f0a2d) | 카메라 테스트 중지. v8.0 버전은 사용하지 않습니다. ITXDeviceManager::stopCameraDeviceTest 인터페이스를 사용하십시오. |
| [startMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aca6add13bdd6535bed6d28407b5468af) | 마이크 테스트 시작 |
| [stopMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a29c2a5a42f65108074174e0bc58c0aee) | 마이크 테스트 중지. v8.0 버전은 사용하지 않습니다. ITXDeviceManager::stopMicDeviceTest 인터페이스를 사용하십시오. |
| [startSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af60f0db87d1f7001860f1bf330eeee3c) | 스피커 테스트 시작 |
| [stopSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4b7a172067664fe50015c758e02a822) | 스피커 테스트 중지. v8.0 버전은 사용하지 않습니다. ITXDeviceManager::stopSpeakerDeviceTest 인터페이스를 사용하십시오. |
| [setMicVolumeOnMixing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4e3fb7ca730f15b6ab201e73e21f1260) | 마이크 음량 설정 |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0f8b23d8c48b9a056ca0e61ddcc894f2) | 화면 공유 시작 |
| [playBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a815aa5a969dcb0617e02f955a9ee7cd4) | 배경 음악 재생 |
| [stopBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8eec0a8a7edf45d3b49b897286154b4f) | 배경 음악 재생 중지 |
| [pauseBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed6272ead63eb14b9f64a92a59196c28) | 배경 음악 재생 일시 중지 |
| [resumeBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a221c73557814b71880c9a9323e3f31d2) | 배경 음악 다시 재생 |
| [getBGMDuration](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a487cff035a50da09ab39e87f7488d647) | 음악 파일 총 시간 획득, 단위: 밀리초 |
| [setBGMPosition](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2e2050b96d2b453e0ca83e483efec02c) | BGM 재생 진행률 설정 |
| [setBGMVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab651d0daff2d1b7e25b43606a4776796) | 배경 음악 재생 음량 설정 |
| [setBGMPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9c083e91e2af46503e522443a7b51b32) | 배경 음악 로컬 재생 음량 설정 |
| [setBGMPublishVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af193ff23e008485cf949d761028ce6e9) | 배경 음악 원격 재생 음량 설정 |
| [playAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4db6f176c155c0f83d11eb302f6e1dab) | 음향 효과 재생 |
| [setAudioEffectVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a401d82c610be2136896c0f60621d66cf) | 음향 효과 음량 설정 |
| [stopAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a254acc2f0fe96ffcce33629eb4309877) | 음향 효과 중지 |
| [stopAllAudioEffects](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a07a2dfd7ce4e76b28172d73ee8405dbe) | 모든 음향 효과 중지 |
| [setAllAudioEffectsVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a06219d65076c6c7024fab30d2516b167) | 모든 음향 효과 음량 설정 |
| [pauseAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2b004f3a3a7bdde7b2926930f31afa6c) | 음향 효과 일시 중지 |
| [resumeAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af10583316f15ed709247590a081b2307) | 음향 효과 다시 재생 |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a2) | 화면 공유 매개변수 설정 |
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac9d547341170330a70623299b366c44a) | 사용자 정의 비디오 수집 모드 활성화 |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3a53ae79c1bd28825cb276c7555500fe) | TRTCVideoFrame은 다음과 같은 입력 방식이 권장됩니다(기타 필드 입력 필요 없음). |


