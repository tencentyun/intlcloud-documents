## 콘텐츠 소개

휴대폰 라이브 방송의 천편일률적인 세로 모드 체험과는 달리 TRTC는 가로 모드와 세로 모드의 두 가지 시나리오에서 모두 사용 가능합니다. 따라서 대부분의 가로 모드 프로세스 로직에 대한 대응이 필요하며, 본 문서에서는 주로 다음과 같은 내용을 소개합니다.
- 세로 모드 구현 방법. 예를 들어 WeChat 영상 통화가 전형적인 세로 모드입니다.
- 가로 모드 구현 방법. 예를 들어 다중 사용자 화상 회의 App(예: XYLink)은 대부분 가로 모드를 사용합니다.
- 로컬 화면 및 원격 화면 회전 방향과 화면 맞춤 모드를 사용자 정의 제어하는 방법

![](https://main.qcloudimg.com/raw/1b4452db22edfe88646cd35888794d44.jpg)

## 플랫폼 지원

| iOS | Android | Mac OS | Windows | Electron|WeChat 미니프로그램 | Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003;  |  &#10003; |  &#10003; |  &#10003;  |&#10003;  |  ×  |  × |


## 세로 모드
WeChat 영상 통화와 같은 모드를 구현하기 위해서는 다음 두 작업을 실행해야 합니다.

**1. App의 UI 인터페이스를 세로 모드로 설정**
iOS 플랫폼은 직접 XCode의 [General]>[Deployment Info]>[Device Orientation]에서 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

Appdelegate의 `supportedInterfaceOrientationsForWindow` 방법을 이용해 동일한 효과를 구현할 수도 있습니다.
``` ObjectiveC
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
```

Android 플랫폼에서는 activity의 `screenOrientation` 속성을 portrait으로 지정하여 인터페이스를 세로 모드로 지정할 수 있습니다.
```xml
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
```

**2. SDK에서 세로 모드 해상도 사용 설정**
TRTCCloud의 setVideoEncoderParam 인터페이스를 이용해 비디오 인코딩 매개변수를 설정할 때 resMode를 `TRTCVideoResolutionModePortrait`으로 설정합니다.

iOS 예시 코드는 다음과 같습니다.
``` ObjectiveC
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; //해상도 모드를 세로 모드로 설정

[trtc setVideoEncoderParam: encParam];
```

## 가로 모드

App에서 가로 모드를 사용하고 싶은 경우 세로 모드 사용 방법과 비슷합니다. 1단계와 2단계에서 매개변수를 상응하게 조정하면 됩니다.
특히 2단계에서 TRTCVideoEncParam의 resMode를 `TRTCVideoResolutionModeLandscape` (Android 플랫폼: TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE)로 지정하면 됩니다.

## 사용자 정의 제어

TRTC SDK는 자체적으로 많은 인터페이스 함수를 제공하여 로컬 및 원격 화면의 회전 방향과 화면 맞춤 모드를 제어할 수 있습니다.

| 인터페이스 함수 | 기능 작용 |  비고 |  
|---------|---------| ----- |
| setLocalViewRotation | 로컬 미리보기 화면의 시계 방향 회전 각도| 시계 방향으로 90°, 180°, 270°의 세 가지 각도 회전 지원  | 
| setLocalViewFillMode | 로컬 미리보기 화면의 화면 맞춤 모드 | 채우기 또는 맞추기|
| setRemoteViewRotation | 원격 비디오 화면의 시계 방향 회전 각도 | 시계 방향으로 90°, 180°, 270°의 세 가지 각도 회전 지원  |
| setRemoteViewFillMode | 원격 비디오 화면의 화면 맞춤 모드 | 채우기 또는 맞추기|
| setVideoEncoderRotation | 인코더가 출력하면 화면의 시계 방향 회전 각도 설정 | 시계 방향으로 90°, 180°, 270°의 세 가지 각도 회전 지원|

![](https://main.qcloudimg.com/raw/f965d6d603f95862d73525469637b437.jpg)


## GSensorMode
화면 회전으로 인한 녹화 및 CDN 릴레이 라이브 방송과의 여러 호환 문제를 고려하여, TRTC SDK는 간단한 중력 센서 자가 적응 기능을 제공합니다. TRTCCloud의 `setGSensorMode` 인터페이스를 통해 활성화할 수 있습니다.

해당 기능은 현재 180° 상하 회전 자가 적응만 제공하며, 사용자가 휴대폰을 180° 회전해도 상대방이 보는 화면 방향은 변경되지 않습니다. 현재 90° 또는 270° 회전 자가 적응은 지원하지 않습니다. 해당 기능은 인코더의 방향 조정을 기반으로 구현되므로 녹화되는 비디오 및 미니프로그램, H5에서 보는 비디오 화면 또한 기본 화면 방향에서 변경되지 않습니다.

>!중력 센서 자가 적응 기능을 구현할 수 있는 또 다른 방법은 모든 프레임의 비디오 정보 안에 현재 비디오의 중력 방향을 포함시킨 후 원격 사용자 측의 자가 적응 방향으로 렌더링하여 조정하는 방법입니다. 그러나 해당 방법은 별도의 트랜스 코딩 리소스를 불러와야만 녹화된 비디오 방향을 원하는 비디오 방향으로 통일할 수 있는 문제가 있어 권장하지는 않습니다.





