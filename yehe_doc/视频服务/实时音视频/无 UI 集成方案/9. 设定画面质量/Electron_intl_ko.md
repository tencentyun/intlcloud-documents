본문은 영상 통화 또는 라이브 스트리밍 세션의 이미지 화질을 설정하는 방법을 설명합니다. 더 나은 사용자 경험을 제공하기 위해 비디오 화질 및 원활성에 대한 요구 사항에 따라 속성을 설정할 수 있습니다.
비디오 속성에는 해상도, 프레임 레이트 및 비트 레이트가 포함됩니다.

## 개요
Electron SDK에서 다음과 같은 방법으로 이미지 화질을 조정할 수 있습니다.
- [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)의 TRTCAppScene 매개변수: 사용 사례 선택.
- [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam): 인코딩 매개변수 설정.
- [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam): 네트워크 제어 정책 설정.

본문은 TRTC SDK의 비디오 화질이 프로젝트별 요구 사항을 충족하도록 상기 매개변수를 구성하는 방법을 설명합니다.
[Electron API Example: video-quality](https://github.com/tencentyun/TRTCSDK/blob/master/Electron/TRTC-API-Example/assets/code/advanced/video-quality/index.js) Demo를 참고하십시오.

## TRTCAppScene

- **VideoCall:** 대부분의 경우 2명 이상의 사람이 있는 영상 통화 시나리오로서, 내부 인코더 및 네트워크 프로토콜 최적화는 원활성에 중점을 두어 통화 지연 및 랙을 줄입니다.
- **LIVE:** 대부분의 경우 한 사람이 말하거나 공연하고 때로는 여러 사람이 비디오를 통해 서로 상호 작용하는 라이브 스트리밍 시나리오로서, 내부 인코더 및 네트워크 프로토콜 최적화는 성능과 호환성에 중점을 두어 더 나은 성능과 해상도를 제공합니다.	


## TRTCVideoEncParam

### 권장 설정

| 응용 시나리오 | videoResolution |  videoFps | videoBitrate | 
|:-------------:|:-------------:|:-------------:|:-------------:|
| 화상 회의(기본 이미지 @ Mac Win) | 1280x720 | 15 | 1200kbps | 
| 온라인 교육(교사 @ Mac Win) | 960x540 | 15 | 850kbps |

### 필드에 대한 자세한 설명

- **(TRTCVideoResolution) videoResolution**
인코딩된 해상도입니다. 예를 들어, 640 x 360은 인코딩된 비디오 이미지의 너비(픽셀) x 높이(픽셀)를 나타냅니다. TRTCVideoResolution 열거형 정의에서는 가로 해상도 즉, 너비 >= 높이(Landscape)만 정의됩니다. 세로 해상도를 사용하려면 resMode를 Portrait로 설정해야 합니다.
>!많은 하드웨어 코덱은 16으로 나눌 수 있는 픽셀 너비만 지원하므로 SDK로 인코딩된 실제 해상도는 매개변수로 구성된 것과 반드시 정확히 동일하지는 않습니다. 대신 16의 제수에 따라 자동으로 수정됩니다. 예를 들어, 해상도 640 x 360은 SDK 내에서 640 x 368로 조정될 수 있습니다.

- **(TRTCVideoResolutionMode) resMode**
가로 또는 세로 해상도를 결정합니다. TRTCVideoResolution에는 가로 해상도만 정의되어 있으므로 360 x 640과 같은 세로 해상도를 사용하려면 resMode를 TRTCVideoResolutionModePortrait로 지정해야 합니다. 일반적으로 PC와 Mac에서는 가로(Landscape) 해상도를 사용하고 모바일 장치에서는 세로(Portrait) 해상도를 사용합니다.

- **(int) videoFps**
  프레임 레이트(FPS)는 초당 인코딩되는 프레임 수를 나타냅니다. 권장 값은 15 FPS로, 충분히 원활하게 재생될 뿐 아니라 초당 프레임 수가 많다고 해서 단일 화면의 선명도가 떨어지지는 않습니다.
	
 원활성에 대한 요구 사항이 높은 경우 프레임 레이트를 20 FPS 또는 25 FPS로 설정할 수 있습니다. 그러나 영화의 일반 프레임 속도는 24 FPS에 불과하므로 25 FPS 이상의 값을 설정하지 마시기 바랍니다.

- **(int) videoBitrate**
비디오 비트 레이트(Bitrate)입니다. 초당 인코더에서 출력되는 인코딩된 이진 데이터의 Kbit를 나타냅니다. videoBitrate를 800Kbps로 설정하면 인코더가 초당 800Kbit의 비디오 데이터를 생성합니다. 이러한 데이터가 파일로 저장되는 경우 파일 크기는 800Kbit, 즉 100KB 또는 0.1M이 됩니다.

 더 높은 비디오 비트 레이트가 항상 더 좋은 것은 아닙니다. 아래 표와 같이 해상도와 적절한 매칭 관계가 있습니다.
 
### 해상도 및 비트 레이트 참조 테이블

| 해상도 정의 | 종횡비 | 권장 비트 레이트(VideoCall) | 권장 비트 레이트(LIVE) |
|:-------------:|:-------------:|:-------------:|:-------------:|
| TRTCVideoResolution_120_120 | 1:1 |   80kbps | 120kbps|
| TRTCVideoResolution_160_160 | 1:1 | 100kbps | 150kbps|
| TRTCVideoResolution_270_270 | 1:1 | 200kbps | 300kbps|
| TRTCVideoResolution_480_480 | 1:1 | 350kbps | 525kbps|
| TRTCVideoResolution_160_120 | 4:3 | 100kbps | 150kbps|
| TRTCVideoResolution_240_180 | 4:3 | 150kbps | 225kbps|
| TRTCVideoResolution_280_210 | 4:3 | 200kbps | 300kbps|
| TRTCVideoResolution_320_240 | 4:3 | 250kbps | 375kbps|
| TRTCVideoResolution_400_300 | 4:3 | 300kbps | 450kbps|
| TRTCVideoResolution_480_360 | 4:3 | 400kbps | 600kbps|
| TRTCVideoResolution_640_480 | 4:3 | 600kbps | 900kbps|
| TRTCVideoResolution_960_720 | 4:3 | 1000kbps | 1500kbps|
| TRTCVideoResolution_160_90   | 16:9 | 150kbps | 250kbps|
| TRTCVideoResolution_256_144 | 16:9 | 200kbps | 300kbps|
| TRTCVideoResolution_320_180 | 16:9 | 250kbps | 400kbps|
| TRTCVideoResolution_480_270 | 16:9 | 350kbps | 550kbps|
| TRTCVideoResolution_640_360 | 16:9 | 550kbps | 900kbps|
| TRTCVideoResolution_960_540 | 16:9 | 850kbps | 1300kbps|
| TRTCVideoResolution_1280_720 | 16:9 | 1200kbps | 1800kbps|
|TRTCVideoResolution_1920_1080 	| 16:9 | 2000kbps| 3000kbps |

## TRTCNetworkQosParam
### QosPreference

네트워크 대역폭이 비교적 넉넉해 해상도와 원활성을 모두 높일 수 있으나 사용자의 네트워크가 이상적이지 못할 경우 TRTCNetworkQosParam의 preference 매개변수를 지정하여 해상도와 원활성 중 어떤 것을 우선적으로 보장할지 선택할 수 있습니다. 

- **원활성 우선(TRTCVideoQosPreferenceSmooth)**
사용자가 네트워크 신호가 약한 환경인 경우 화면이 흐릿하게 변하고 모자이크가 비교적 많이 나타나지만 원활하게 재생되거나 약간의 랙만 발생합니다.

- **해상도 우선(TRTCVideoQosPreferenceClear)**
사용자가 네트워크 신호가 약한 환경인 경우 화면의 해상도를 최대한 보장하지만 랙이 쉽게 발생할 수 있습니다.

### ControlMode

controlMode 매개변수는 **TRTCQosControlModeServer**를 선택하면 됩니다. TRTCQosControlModeClient는 Tencent Cloud R&D팀의 내부 디버깅용으로, 사용하지 마십시오.

## 일반적인 오해
#### 1. 해상도가 높을수록 더 좋지 않은가요?
해상도가 높을수록 지원을 위해 더 높은 비트 레이트가 필요합니다. 해상도가 1280 x 720이지만 비트 레이트가 200Kbps로 지정되어 있으면 비디오 화질이 저하됩니다. [해상도 및 비트 레이트 참조표](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)를 참고하여 매개변수를 설정하시기 바랍니다.

#### 2. 프레임 레이트가 높을수록 더 좋지 않은가요?
카메라에 포착된 이미지는 노출 단계의 모든 실제 물체에 대한 완전한 매핑이기 때문에 프레임 레이트가 높을수록 비디오 원활성이 더 높은 것은 아닙니다. 게임에서의 FPS 개념과 다릅니다. 반대로 프레임 속도가 너무 높으면 각 비디오 프레임의 품질이 저하되고 카메라의 노출 시간이 줄어들어 이미지 효과가 악화됩니다.

#### 3. 비트 레이트가 높을수록 더 좋지 않은가요?
높은 비트 레이트에는 높은 해상도를 매칭해야 합니다. 320 x 240 해상도의 경우 1000Kbps의 비트 레이트는 낭비입니다. [해상도 및 비트 레이트 참조표](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)를 참고하여 매개변수를 설정하시기 바랍니다.

#### 4. Wi-Fi 네트워크에서 고해상도와 비트 레이트를 설정할 수 있나요?
Wi-Fi 네트워크 속도가 항상 일정하지는 않습니다. 기기가 무선 라우터에서 멀리 떨어져 있거나 라우터 채널이 점유되어 있는 경우 Wi-Fi 네트워크가 4G만큼 빠르지 않을 수 있습니다.
이러한 문제에 대응하기 위해, TRTC SDK는 영상 통화 설정 전에 속도 테스트를 수행하여 점수를 기반으로 네트워크 품질을 확인할 수 있는 속도 테스트 기능을 제공합니다.

