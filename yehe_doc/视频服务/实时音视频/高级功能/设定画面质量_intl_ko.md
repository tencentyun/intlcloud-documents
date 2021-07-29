## 콘텐츠 소개

TRTCCloud에서 다음 방식을 통해 화질을 조정할 수 있습니다.
- [TRTCCloud.enterRoom]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)의 TRTCAppScene 매개변수: 응용 시나리오 선택에 사용합니다.
- [TRTCCloud.setVideoEncoderParam]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e): 인코딩 매개변수 설정에 사용합니다.
- [TRTCCloud.setNetworkQosParam]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9): 네트워크 제어 정책 설정에 사용합니다.

본 문서에서는 위의 매개변수를 설정하여 귀하의 프로젝트 수요에 맞게 TRTC SDK의 화질 효과를 조정하는 방법을 소개합니다.
다음 Demo를 참고할 수 있습니다.
- [iOS: LivePushViewController.swift]
- [Android: LivePushActivity.java](https://github.com/tencentyun/TRTCSDK/blob/0123787812e04d3acb44eed06ec9803df363c580/Android/TRTCSimpleDemo/live/src/main/java/com/tencent/live/LivePushActivity.java)
- [Windows: TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp)

## 지원 플랫폼

| iOS | Android | Mac OS | Windows |  Web | Electron|Flutter |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; | &#10003;   | &#10003;  |  &#10003;   | &#10003;  |&#10003;  |&#10003;  |

Web에서의 화면 품질 설정에 대한 자세한 방법은 [설정 가이드](https://www.qcloudtrtc.com/trtc-web-sdk/docs/api/tutorial-04-advanced-set-video-profile.html)를 참조하십시오.

## TRTCAppScene

- **VideoCall** 
영상 통화 시나리오, 즉 대부분 2명 이상의 영상 통화를 사용하는 시나리오에서는 내부 인코더와 네트워크 프로토콜 최적화가 원활성에 치우쳐져 있으며, 통화 딜레이 및 랙 발생률을 낮춥니다.

- **LIVE** 
라이브 방송 시나리오, 즉 대부분 1인 라이브 방송에 사용하고 가끔 다중 사용자 비디오 인터랙션을 사용하는 시나리오에서는 내부 인코더와 네트워크 프로토콜 최적화가 성능 및 호환성에 치우쳐져 있으며, 성능과 해상도가 더욱 좋습니다.	


## TRTCVideoEncParam

### 권장 설정

| 응용 시나리오 | videoResolution |  videoFps | videoBitrate |
|:-------------:|:-------------:|:-------------:|:-------------:|
| 영상 통화(휴대폰) | 640x360 | 15 | 550kbps |
| 화상 회의(메인 화면 @ Mac Win) | 1280x720 | 15 | 1200kbps |
| 화상 회의(메인 화면 @ 휴대폰) | 640x360 | 15 | 900kbps|
| 화상 회의(소형 화면) | 320x180 | 15 | 250kbps |
| 온라인 교육(교사 @ Mac Win) | 960x540 | 15 | 850kbps |
| 온라인 교육(교사 @ iPad) | 640x360 | 15 |  550kbps |
| 온라인 교육(학생) | 320x180 | 15 | 250kbps |

### 필드 상세 정보

- **(TRTCVideoResolution) videoResolution**
인코딩 해상도입니다. 예를 들어 640 x 360은 인코딩된 화면의 너비(픽셀) x 높이(픽셀)이며, TRTCVideoResolution 열거 값 정의에서 너비 >= 높이의 가로 모드(Landscape) 해상도만 정의했습니다. 세로 모드 해상도를 사용하고 싶은 경우 resMode를 Portrait으로 설정해야 합니다.
 >!많은 하드웨어 인코더/디코더가 16배수 픽셀의 너비만 지원하여 SDK에서 실제로 인코딩한 해상도가 사용자 정의한 매개변수 설정을 완벽하게 따르지 않을 수 있으며 자동으로 16배수로 수정됩니다. 예를 들어 640 x 360의 해상도는 SDK 내부에서 640 x 368로 적용될 수 있습니다.

- **(TRTCVideoResolutionMode) resMode**
가로 모드 또는 세로 모드 해상도입니다. TRTCVideoResolution에 가로 모드만 정의되어 있으므로 360 x 640의 세로 모드 해상도를 사용할 경우 resMode를 TRTCVideoResolutionModePortrait으로 설정해야 합니다. 일반적으로 PC 및 Mac에서는 가로 모드(Landscape) 해상도를 사용하며, 휴대폰에서는 세로 모드(Portrait) 해상도를 사용합니다.

- **(int) videoFps**
  프레임 레이트(FPS)는 초당 얼마나 많은 화면을 코딩하는지를 나타냅니다. 권장 값은 15FPS로, 충분히 원활하게 재생될 뿐 아니라 초당 프레임 수가 많다고 해서 단일 화면의 선명도가 떨어지지도 않습니다.
	

 원활도에 대한 수요가 높은 경우 20FPS 또는 25FPS로 설정할 수 있습니다. 영화에서 일반적으로 사용하는 프레임 레이트도 24FPS이므로 25FPS 이상으로 설정하지 마십시오.

- **(int) videoBitrate**
비디오 비트 레이트(Bitrate), 즉 인코더에서 초당 몇 Kbit를 출력하여 인코딩하는지를 이진법 데이터로 표시합니다. videoBitrate를 800kbps로 설정하면 인코더가 초당 800kbit의 비디오 데이터를 생성하며, 해당 데이터를 1개 파일로 저장하는 경우 파일 크기는 800kbit, 즉 100KB = 0.1M가 됩니다.

 비디오 비트 레이트는 높을수록 좋은 것이 아닙니다. 비트레이트와 해상도 사이에는 비교적 적합한 매핑 관계가 있으며, 다음을 참고하십시오.

### 해상도와 비트 레이트 참고표

| 해상도 정의 | 너비와 높이 비율 | 권장 비트 레이트 | 최대 설정 |
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

## TRTCNetworkQosParam
### QosPreference

네트워크 대역폭이 비교적 넉넉해 해상도와 원활도를 모두 높일 수 있으나 사용자의 네트워크가 이상적이지 못할 경우 TRTCNetworkQosParam의 preference 매개변수를 지정하여 해상도와 원활도 중 어떤 것을 우선적으로 보장할지 선택할 수 있습니다. 

- **원활 우선(TRTCVideoQosPreferenceSmooth)**
사용자가 네트워크 신호가 약한 환경인 경우 화면이 흐릿하게 변하고 모자이크가 비교적 많이 나타나지만 원활하게 재생되거나 약간의 랙만 발생합니다.

- **선명 우선(TRTCVideoQosPreferenceClear)**
사용자가 네트워크 신호가 약한 환경인 경우 화면의 해상도를 최대한 보장하지만 랙이 쉽게 발생할 수 있습니다.

### ControlMode

controlMode 매개변수는 **TRTCQosControlModeServer**로 선택하면 됩니다. TRTCQosControlModeClient는 Tencent Cloud R&D팀의 내부 디버깅용으로, 사용하지 마십시오.

## 일반적인 오해
**1. 해상도가 높을수록 좋지 않나요?**
높은 해상도는 높은 비트 레이트가 보장되어야 합니다. 해상도를 1280 x 720로 선택하였으나 비트레이트는 200kbps로 지정하는 경우 화면에 대량의 모자이크가 발생합니다. [해상도와 비트레이트 참고표](https://intl.cloud.tencent.com/document/product/647/35153)를 참고하여 설정하기를 권장합니다.

**2. 프레임 레이트가 높을수록 좋지 않나요?**
카메라가 수집하는 화면은 빛 노출 단계에서 모든 실질적 물체 전체를 반사하므로 프레임 레이트가 높을수록 원활하다 느끼는 것은 아니며, 이 점이 게임에서의 FPS와는 다른 점입니다. 게임과는 반대로 프레임 레이트가 너무 높으면 프레임별 화면의 화질이 떨어지게 되며 카메라 노출 시간이 감소하여 효과가 더욱 낮아집니다.

**3. 비트 레이트가 높을수록 좋지 않나요?**
높은 비트 레이트는 높은 해상도가 매칭되어야 합니다. 320 x 240의 해상도에서 1000kbps의 비트레이트는 낭비입니다. [해상도와 비트레이트 참고표](https://intl.cloud.tencent.com/document/product/647/35153)를 참고하여 설정하기를 권장합니다.

**4. Wi-Fi 시 아주 높은 해상도와 비트 레이트로 설정할 수 있나요?**
Wi-Fi 네트워크 속도가 항상 일정하고 변하지 않는 것은 아닙니다. 무선 라우터가 비교적 멀리 있거나 라우터 채널이 점유된 경우 인터넷 속도가 4G보다 느릴 수 있습니다.
이러한 경우를 위해 TRTC SDK는 속도 테스트 기능을 제공하며, 영상 통화 전 먼저 속도를 테스트한 후 평가값에 따라 네트워크 신호가 좋은지 나쁜지를 결정합니다.


