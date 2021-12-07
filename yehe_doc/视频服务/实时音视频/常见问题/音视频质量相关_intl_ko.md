## 1. 비디오 문제

[](id:v1)
### TRTC 비디오 화면에 검은 띠가 나타났습니다. 어떻게 제거합니까?
TRTCVideoFillMode_Fill(채우기)을 설정하면 됩니다. TRTC 비디오 렌더링 모드는 채우기와 적용으로 나뉘며, 로컬 렌더링 화면은 setLocalViewFillMode()를 통해 설정할 수 있습니다. 원격 렌더링 화면은 setRemoteViewFillMode를 통해 설정할 수 있습니다.
- TRTCVideoFillMode_Fill: 이미지 전체 화면. 윈도우를 초과한 비디오 부분이 잘려 나가 화면이 완전히 표시되지 않을 수 있습니다.
- TRTCVideoFillMode_Fit: 이미지 긴 변 전체 화면. 짧은 변 부분이 검은색으로 채워지며 화면은 완전히 표시됩니다.

[](idv2:)
### TRTC에 랙이 발생하면 어떻게 해결해야 합니까?
TRTC 콘솔의 **[모니터링 대시보드](https://console.cloud.tencent.com/trtc/monitor)** 페이지에서 ​해당 RoomID, UserID를 통해 통화 품질을 확인할 수 있습니다.
- 수신자 시점에서 발신자와 수신자의 상황을 확인합니다.
- 발신자와 수신자의 패킷 손실률이 높은지 확인합니다. 패킷 손실률이 너무 높은 경우 일반적으로 네트워크가 불안정하여 랙이 발생합니다.
- 프레임 레이트와 CPU 이용률을 확인합니다. 프레임 레이트가 낮거나 CPU 이용률이 너무 높은 경우 랙 현상이 발생합니다.

[](id:v3)
### TRTC 화질이 좋지 않습니다. 흐릿하고 모자이크 현상 등이 발생합니다. 어떻게 해결해야 합니까?
- 해상도는 주로 비트 레이트와 관련이 있습니다. SDK 비트 레이트가 낮게 설정되어 있는지 확인하십시오. 해상도가 높은데 비트 레이트가 낮은 경우 모자이크 현상이 쉽게 나타날 수 있습니다.
- TRTC는 클라우드 QOS 트래픽 제어 정책을 통해 네트워크 상태에 따라 비트 레이트와 해상도를 동적으로 조정합니다. 네트워크 상태가 좋지 않은 경우 비트 레이트가 낮아져 해상도가 떨어질 수 있습니다.
- 방 입장 시 사용한 VideoCall 모드가 Live 모드인지 확인합니다. 통화 VideoCall 모드는 저지연성과 원활한 통화에 중점을 두므로 네트워크가 약한 경우 화질을 포기하고 원활한 통화 상태를 확보합니다. 화질이 더 중요한 경우 Live 모드 사용을 권장합니다.

[](id:v4)
### TRTC에서 로컬 화면과 원격 화면의 좌우가 상반됩니까?
로컬 기본 캡처 화면은 이미지입니다. 앱에서 [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) 인터페이스를 통해 설정할 수 있으며, 해당 인터페이스는 로컬 카메라 미리보기 화면의 이미지 모드만을 변경합니다. 또한 setVideoEncoderMirror 인터페이스를 통해 인코더에서 출력된 화면 이미지 모드를 설정할 수 있으며, 해당 인터페이스는 로컬 카메라의 미리보기 화면은 변경하지 않습니다. 단, 사용자가 보게 되는 (및 서버 녹화) 화면 효과는 변경합니다. 웹에서는 [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) 인터페이스를 통해 mirror 매개변수를 수정하여 설정할 수 있습니다.

[](id:v5)
### TRTC에서 비디오 코딩 출력 방향을 설정했는데 적용되지 않은 이유는 무엇입니까?
setGSensorMode()를 TRTCGSensorMode_Disable로 설정하고 중력 센서를 차단해야 합니다. 그렇지 않으면 setVideoEncoderRotation 호출 후 원격 사용자가 보게 되는 화면이 변하지 않습니다.

[](id:v6)
### TRTC에 정상적인 업스트림 데이터가 있는데 릴레이 풀 스트림에 실패하며 화면이 보이지 않는 이유는 무엇입니까?
**[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>기능 설정**에서 자동 릴레이 푸시 스트림을 활성화했는지 확인합니다.

[](id:v7)
### 미리보기/재생 화면이 회전하는 이유는 무엇입니까?
- **TRTCSDK 카메라를 사용하여 수집**:
  - SDK 버전을 최신 버전으로 업데이트할 것을 권장합니다.
  - 특수 장치인 경우 로컬 미리보기 화면 렌더링 각도 인터페이스 `setLocalViewRotation`, 원격 비디오 화면 렌더링 각도 인터페이스 `setRemoteViewRotation`, 인코더 출력 화면 렌더링 각도 인터페이스 `setVideoEncoderRotation`을 사용하여 조정할 수 있습니다. 구체적인 인터페이스 사용 설명은 [비디오 화면 회전](https://intl.cloud.tencent.com/document/product/647/35154)을 참고하십시오.
- **사용자 정의 비디오를 사용하여 수집**:
  - SDK 버전을 최신 버전으로 업데이트할 것을 권장합니다.
  - 수집하고자 하는 비디오 화면의 각도가 올바른지 확인합니다.
  - 비디오 데이터를 TRTCSDK에 채우고, `TRTCCloudDef.TRTCVideoFrame`의 회전 각도 설정 여부를 확인합니다.
  - 특수 장치인 경우 로컬 미리보기 화면 렌더링 각도 인터페이스 `setLocalViewRotation`, 원격 비디오 화면 렌더링 각도 인터페이스 `setRemoteViewRotation`, 인코더 출력 화면 렌더링 각도 인터페이스 `setVideoEncoderRotation`을 사용하여 조정할 수 있습니다. 구체적인 인터페이스 사용 설명은 [비디오 화면 회전](https://intl.cloud.tencent.com/document/product/647/35154)을 참고하십시오.

[](id:v8)
### 비디오에 이미지 문제가 생기는 이유는 무엇입니까?
전면 카메라로 영상 통화를 할 경우 이미지 효과가 있어 로컬 미리보기와 원격 시청자 화면이 좌우 반전됩니다.

[](id:v9)
### 가로 화면으로 푸시 스트림하는 방법은 무엇입니까?
TV 또는 기타 장치를 사용하여 시나리오 필요에 따라 가로 화면으로에 푸시 스트림할 수 있습니다.

[](id:v10)
### 라이브 방송에 검은색 화면이 나오는 이유는 무엇입니까?
- 재생 실패 또는 디코딩 실패입니다. 재생 실패 해결 방법을 참고하십시오.
- Metadata 문제일 수 있습니다. 예를 들어 Metadata에 오디오 스트림 정보만 있지만 실제 데이터에는 오디오와 비디오가 모두 포함되어 있는 경우 또는 초기 데이터에는 오디오만 있지만 일정 시간 재생 후 비디오 정보가 추가되는 경우에 발생할 수 있습니다. 이 경우 일반적으로 소스 스트림의 Metadata 정보를 수정할 것을 권장합니다.
- 비디오 인코딩 데이터에는 화면 정보가 존재하지 않으며, SEI와 같은 프레임만 있을 경우 복호화 시 화면이 나오지 않고 자연스럽게 검은 화면이 나옵니다. 일반적으로 사용자 정의 비디오 데이터입니다.

[](id:v11)
### 라이브 방송에 재생 화면 흐려짐과 그린 스크린이 발생하는 이유는 무엇입니까?
- 일반적으로 I 프레임의 손실로 인해 발생합니다. P 및 B 프레임의 디코딩은 I 프레임에 의존하기 때문에 I 프레임이 손실되면 P 및 B 프레임의 디코딩이 실패하여 화면이 흐려지고 그린 스크린이 나타납니다. 이 경우 먼저 ffplay, VLC 및 Potplayer와 같은 다른 플레이어를 사용하여 동일한 스트림을 동시에 재생합니다. 플레이어의 화면이 흐리거나 그린 스크린이 나타나면 일반적으로 멀티미디어 소스 스트림에 문제가 있는 것입니다. 소스 스트림을 확인해야 합니다.
- Metadata 변경이 원인일 수 있습니다. 대부분의 플레이어는 일반적으로 디코딩을 시작하기 전에 metadata를 리졸브하여 디코딩 매개변수를 설정합니다. 예를 들어 화면이 변경되면 해상도가 변경되었지만 플레이어의 디코딩 매개변수가 재설정되지 않은 경우 화면 흐림, 그린 스크린이 발생할 수 있습니다. 이 경우 가장 좋은 방법은 푸시 스트림에서 라이브 방송 중에 인코딩 매개변수를 변경하지 않아 metadata 정보가 수정되지 않도록 하는 것입니다.
- 하드웨어 코덱과의 호환성 문제일 수 있습니다. 일반적으로 Android 기기에서 발생하며, 일부 Android 기기는 하드웨어 코덱 구현성 및 호환성이 좋지 않습니다. 이 경우 가장 좋은 방법은 소프트웨어 버전 및 디코딩을 변경하여 비교해보는 것입니다.
- 푸시 스트림과 재생의 색상 형식 불일치 문제일 수 있습니다. 예를 들어 푸시 스트림이 NV12를 사용하고 재생이 I420을 지원하는 경우 디코딩 중 색상 형식의 불일치로 인해 화면이 흐릿해지거나 그린 스크린으로 표시됩니다. 이 경우 푸시/풀 스트림의 색상 형식을 통일합니다.



## 2. 오디오 문제

[](id:a1)
###  TRTC의 통화와 동시에 VOD 플레이어 TXVodPlayer를 사용하여 재생했는데 소리가 작은 이유는 무엇입니까?
setSystemVolumeType 인터페이스를 통해 통화 시 사용하는 시스템 음량 유형을 설정합니다. 미디어 음량 모드 TRTCSystemVolumeTypeMedia로 설정하면 해결됩니다.

[](id:a2)
### 미디어 음량과 통화 음량은 어떻게 선택합니까?
setSystemVolumeType 인터페이스를 통해 통화 음량 및 미디어 음량을 선택할 수 있습니다.
- TRTCAudioVolumeTypeAuto: 기본 유형, 마이크 연결 통화 음량, 마이크 꺼짐 미디어 음량.
- TRTCAudioVolumeTypeVOIP: 통화 음량 사용.
- TRTCAudioVolumeTypeMedia: 미디어 음량 사용.


[](id:a4)
### 소리가 작을 경우 어떻게 해결합니까?
- **모든 시청자가 듣는 소리가 작다면** 업스트림 요인입니다.
  - Windows 및 mac의 [setCurrentDeviceVolume](http://doc.qcloudtrtc.com/group__ITXDeviceManager__csharp.html#a1c9517a8a6a23558b4bd40c41eb97ee5), 모든 플랫폼의 [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a53681962139b81140f2d66abc4ea6a0f) 인터페이스의 volume 값이 50 미만인지 확인하고 음량을 적절히 높일 수 있습니다.
  - 3A에서 처리한 AGC 자동 게인이 활성화되어 있는지 확인합니다.
  - 블루투스 헤드셋 문제인지 확인합니다.
- **일부 시청자의 오디오만 작다면** 다운스트림 요인입니다.
  - [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a9b8946403b8b3ac8e11f3a78e9d531ca), [setCurrentDeviceVolume](http://doc.qcloudtrtc.com/group__ITXDeviceManager__csharp.html#a1c9517a8a6a23558b4bd40c41eb97ee5) 인터페이스의 volume 값이 50 미만인지 확인하고 적절하게 음량을 높일 수 있습니다.
  - setAudioRoute API를 호출하여 핸드셋 재생으로 전환하지 않았는지 확인합니다.

[](id:a5)
### 계속 오디오 랙이 발생하는 이유는 무엇입니까?
[모니터링 대시보드](https://console.cloud.tencent.com/trtc/monitor)를 열고 오디오 탭에서 확인합니다.
- 수신측과 발신측 ‘디바이스 상태’의 CPU가 90%를 초과하는 경우, 다른 백그라운드 프로그램을 종료할 것을 권장합니다.
- 오디오 업스트림 및 다운스트림에 명백한 패킷 손실이 있는 경우 rtt 값이 크게 변동하여 현재 사용자의 네트워크 품질이 좋지 않음을 나타내며 안정적인 네트워크로 전환할 것을 권장합니다.

[](id:a6)
### 에코가 발생하는 이유는 무엇입니까?
수/발신자의 장치가 너무 가까우면 이는 정상적인 현상입니다. 더 멀리 떨어져서 테스트하시기 바랍니다. 3A 처리의 AEC 에코 제거가 실수로 해제되었는지 확인합니다.

[](id:a7)
### 음질이 좋지 않거나 볼륨이 일정하지 않은 이유는 무엇입니까?
외부에서 사운드 카드를 연결한 상태에서 인이어 모니터링을 켰을 경우 마이크가 연결되었을 때 이런 문제가 발생합니다. 일반적으로 사운드 카드에는 인이어 모니터링 기능이 있기 때문에 사운드 카드 연결 시 인이어 모니터링을 끌 것을 권장합니다.

[](id:a8)
### Web 통화 중에 에코, 잡음, 소음이 발생하거나 소리가 작습니다.
통화 수/발신자의 디바이스가 너무 가까이 있는 경우는 정상적인 현상이므로 더 멀리 떨어져서 테스트하시기 바랍니다. 다른 단말에서 Web 오디오에 에코, 소음, 잡음 등이 들리는 경우 Web의 3A 처리가 적용되지 않은 것을 의미합니다. 사용자 정의 수집에 브라우저의 기본 [getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia) API를 사용하는 경우 3A 매개변수를 수동으로 설정해야 합니다.
- echoCancellation: 에코 제거 스위치.
- noiseSuppression: 소음 억제 스위치.
- autoGainControl: 자동 게인 제어. 자세한 내용은 [미디어 추적 제한](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints)을 참고하십시오.

[TRTC.createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream) 인터페이스로 수집하는 경우 3A 매개변수를 수동으로 설정할 필요 없이 SDK가 기본적으로 3A를 활성화합니다.

## 3. 기타 문제

[](id:q1)
### TRTC는 어떻게 네트워크 상태를 모니터링하여 신호 강약 표시 기능을 나타냅니까?
onNetworkQuality()를 사용하여 현재 네트워크의 업스트림과 다운스트림 품질을 수신할 수 있습니다. [공식 Demo](https://github.com/tencentyun/TRTCSDK)를 참고하여 신호 강도 기능을 실행하십시오.

[](id:q2)
### 디바이스 카메라 또는 마이크 사용 중 등 이상 현상이 나타나는 이유는 무엇입니까?
exitRoom() 인터페이스를 호출하면 방 나가기 관련 로직이 실행됩니다. 예를 들어 멀티미디어 디바이스 리소스 및 코덱 리소스 릴리스 등의 하드웨어 디바이스의 릴리스는 비동기화 작업이며, SDK는 리소스 릴리스 완료 후 TRTCCloudListener의 onExitRoom() 콜백을 통해 어퍼 클래스에 알립니다. enterRoom()을 다시 호출하거나 기타 멀티미디어 SDK로 전환하려면, onExitRoom()의 콜백 이후 다시 관련 작업을 진행할 수 있습니다.

[](id:q3)
### 카메라 작동에 성공했는지 어떻게 판단합니까?
onCameraDidReady 콜백을 통해 콜백이 수신되면 카메라 준비가 완료되었다는 것을 의미합니다.

[](id:q4)
### 마이크 작동에 성공했는지 어떻게 판단합니까?
onMicDidReady 콜백을 통해 콜백이 수신되면 마이크 준비가 완료되었다는 것을 의미합니다.

[](id:q5)
### 카메라 켜기 실패의 이유는 무엇입니까?
- 카메라 권한 허용 여부를 확인합니다. 
- 장치가 TV, 셋톱박스 등인 경우 사용되는 카메라는 외부 카메라입니다. 현재 TRTCSDK는 외부 카메라 인식을 지원합니다. 따라서 카메라 커넥터와 장치가 잘 접촉되어 있는지 확인해야 합니다.

[](id:q6)
### TRTC에는 어떤 기술적 통계 지표가 있습니까?
> ! 이 시나리오는 iOS/Mac, Android 및 Windows 플랫폼에 적용할 수 있습니다.

SDK는 2초마다 기술 지표를 반환하는 onStatistics(TRTCStatistics statics) 콜백 메소드를 제공하며, appCpu(App의 CPU 사용량), systemCpu(현재 시스템의 CPU 사용량), rtt(딜레이), upLoss(업스트림 패킷 손실률), downLoss(다운스트림 패킷 손실률) 및 로컬 및 원격 참석자의 멀티미디어 통계 정보가 포함됩니다. 매개변수에 대한 유형 설명은 [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatisic__ios.html#interfaceTRTCStatistics)를 참고하십시오.

