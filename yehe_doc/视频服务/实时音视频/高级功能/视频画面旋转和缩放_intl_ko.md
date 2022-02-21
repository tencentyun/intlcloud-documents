## 개요

실시간 커뮤니케이션(TRTC)은 모바일 라이브 방송의 천편일률적인 세로 화면 환경과 달리, 가로 및 세로 화면 환경 모두를 고려해야하므로 가로 및 세로 화면에 대한 수많은 처리 로직이 필요합니다. 본 문서에서는 주로 다음과 같은 내용에 대해 소개합니다.
- 세로 화면 모드는 어떻게 구현하나요? 예를 들면 WeChat의 영상 통화가 바로 전형적인 세로 화면 모드라고 할 수 있습니다.
- 가로 화면 모드는 어떻게 구현하나요? 예시: 그룹 멀티미디어 인터랙션 App(Xiaoyu Yilian 등)은 일반적으로 가로 화면입니다.
- 사용자 정의로 로컬 화면과 원격 화면의 회전 방향 및 채우기 모드 제어하는 방법.

![](https://main.qcloudimg.com/raw/1b4452db22edfe88646cd35888794d44.jpg)

## 플랫폼 지원

| iOS | Android | Mac OS | Windows | Electron|web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003;  |  &#10003; |  &#10003; |  &#10003;  |&#10003;  |  × |


## 세로 화면 모드
WeChat 영상 통화와 같은 세로 화면 모드를 구현하기 위해서는 다음과 같은 2가지 작업을 수행해야 합니다.

[](id:step1)
### 1.  App의 UI 인터페이스를 세로로 설정
<dx-tabs>
::: iOS 플랫폼
XCode의 [General]>[Deployment Info]>[Device Orientation]에서 직접 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

Appdelegate의 `supportedInterfaceOrientationsForWindow` 방법을 구현하는 경우에도 동일한 목표를 달성할 수 있습니다.

<dx-codeblock>
::: ObjectiveC ObjectiveC
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
:::
</dx-codeblock>
>?CSDN의 [iOS 가로 세로 화면 회전 및 기본 적응 방법](https://blog.csdn.net/DreamcoffeeZS/article/details/79037207)에서는 iOS플랫폼의 화면 방향에 대한 개발 경험을 자세히 소개하고 있습니다.
:::
::: Android 플랫폼
Activity의 `screenOrientation` 속성을 portrait로 지정하면 해당 인터페이스를 세로 화면 모드로 설정할 수 있습니다.
<dx-codeblock>
::: xml 
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:step2)
### 2. SDK 설정을 통한 세로 화면 해상도 사용
TRTCCloud의 setVideoEncoderParam 인터페이스를 사용하여 영상 인코딩 매개변수를 설정하는 경우, resMode를 `TRTCVideoResolutionModePortrait`로 지정하십시오.
예시 코드는 다음과 같습니다. [](id:example_code)
<dx-codeblock>
::: iOS 플랫폼 ObjectiveC
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; //해상도 모드를 세로 화면 모드로 설정

[trtc setVideoEncoderParam: encParam];
:::
::: Android 플랫폼 java
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT; //해상도 모드를 세로 화면 모드로 설정
trtc.setVideoEncoderParam(encParams);
:::
</dx-codeblock>

## 가로 화면 모드
App이 수평 화면 환경에서 구현되도록 하려면 수직 화면 모드와 유사한 작업을 수행해야 하는데, 첫 번째와 두 번째 단계에서 매개변수를 적절하게 조정할 수 있습니다.
특히 [2단계](#step2)에서 TRTCVideoEncParam의 resMode값은 다음과 같이 지정하십시오.
- iOS플랫폼에서는 `TRTCVideoResolutionModeLandscape`로 지정해야 합니다.
- Android플랫폼에서는 `TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE`로 지정해야 합니다.

## 사용자 정의 제어

TRTC SDK 자체적으로 로컬 및 원격 화면의 회전 방향과 채우기 모드를 제어하기 위한 많은 인터페이스 함수를 제공합니다.

| 인터페이스 함수 | 기능의 역할 |  비고 |
|---------|---------| ----- |
| setLocalViewRotation | 로컬 프리뷰 화면의 시계 방향 회전 각도| 시계 방향으로 90도, 180도, 270도 3가지 방향의 회전 지원  |
| setLocalViewFillMode | 로컬 프리뷰 화면의 채우기 모드 | 검은 테두리 자르기 또는 남기기|
| setRemoteViewRotation | 원격 영상 화면의 시계 방향 회전 각도 | 시계 방향으로 90도, 180도, 270도 3가지 방향의 회전 지원  |
| setRemoteViewFillMode | 원격 영상 화면의 채우기 모드 | 검은 테두리 자르기 또는 남기기|
| setVideoEncoderRotation | 인코더 출력 화면의 시계 방향 회전 각도 설정 | 시계 방향으로 90도, 180도, 270도 3가지 방향의 회전 지원|

![](https://main.qcloudimg.com/raw/f965d6d603f95862d73525469637b437.jpg)


## GSensorMode
화면 회전이 녹화 및 CDN 릴레이 라이브 방송의 다양한 적응 문제와 연관되어 있다는 점을 고려하여 TRTC SDK는 간단한 중력 감지 적응 기능만을 제공하므로 사용자는 TRTCCloud의 `setGSensorMode` 인터페이스를 통해 작동시킬 수 있습니다. 

해당 기능은 현재 180도 상하 회전 자체 적응만 지원합니다. 즉, 사용자의 휴대폰을 상하로 180도 뒤집어도 상대방이 보는 화면 방향은 그대로 유지됩니다(90도, 270도 회전의 자체 적응 기능은 아직 지원하지 않습니다). 또한 이러한 자체 적응은 인코더의 방향 조정을 기반으로 구현되므로 녹화된 영상, 그리고 H5에서 보이는 영상 화면 역시 기존 방향을 유지할 수 있습니다.

>!G-센서 자체 적응의 또 다른 구현 방식은 영상의 개별 프레임마다 현재 영상의 중력 방향 정보를 가지게 한 뒤 원격 사용자의 위치에서 렌더링 방향을 자체 적응으로 조정하도록 하는 것인데, 이 방식은 추가적인 트랜스 코딩을 진행해야만 녹화된 영상의 방향을 원하는 방향으로 맞출 수 있기 때문에 권장하지 않습니다.
