Tencent Cloud TRTC는 화면 공유 기능을 지원합니다. Windows 플랫폼에서는 메인 채널 공유와 서브 채널 공유, 두 가지 화면 공유 방법을 지원합니다.
- **서브 채널 공유**
TRTC에서는 화면 공유를 위해 비디오 스트림의 업스트림 채널을 단독으로 활성화할 수 있으며, 이를 '서브 채널(**substream**)'이라고 부릅니다. 서브 채널 공유란 호스트가 카메라 화면과 스크린 화면, 두 채널의 화면을 동시에 업스트림하는 것입니다. 이는 VooV Meeting의 사용 방법으로, `startScreenCapture` 인터페이스 호출 시 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeSub`로 지정하여 해당 모드를 활성화할 수 있습니다. 해당 채널 화면 시청 시 전용 `startRemoteSubStreamView` 인터페이스가 필요합니다.

- **메인 채널 공유**
TRTC에서 일반적으로 카메라 데이터가 지나가는 터널을 '메인 채널(**bigstream**)'이라고 하며, 메인 채널 공유란 카메라 터널을 통한 화면 공유입니다. 해당 모드에서 호스트가 보유한 비디오 스트림 업스트림 채널은 1개이며, 상호 배제 관계인 카메라 화면과 스크린 화면 중 하나를 업스트림합니다. `startScreenCapture` 인터페이스 호출 시 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeBig`으로 지정해 해당 모드를 활성화할 수 있습니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows | Electron| Chrome 브라우저|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003;  |  &#10003;  |   &#10003; |   &#10003; | &#10003;  |&#10003; |

## 종속된 API

| API 기능 | C++ 버전 |  C# 버전 | Electron 버전 |
|---------|---------|---------|---------|
|공유 타깃 선택| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) |
|화면 공유 시작| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a984f461eebe77819f40c4129fc5a71bb) | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) |
|화면 공유 일시 중지| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) |
|화면 공유 재개| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture)|
|화면 공유 종료| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) |


## 공유 타깃 획득
`getScreenCaptureSources`를 통해 공유 가능한 창 리스트를 열거할 수 있으며, 리스트는 매개변수 sourceInfoList를 통해 반환됩니다.
>? Windows의 데스크톱 화면도 하나의 창이며, 데스크톱 창(Desktop)이라고 부릅니다. 듀얼 모니터를 사용하는 경우 모니터마다 해당하는 데스크톱 창이 있습니다. 따라서 getScreenCaptureSources가 반환하는 창 리스트에도 Desktop 창이 있을 수 있습니다.

sourceInfoList의 모든 sourceInfo는 공유할 수 있는 타깃이며, 해당 필드 설명은 다음과 같습니다.

| 필드 | 유형 | 의미|
|-------|--------| ---------------|
| type |TRTCScreenCaptureSourceType| 수집 소스 유형, 지정 유형은 창 또는 화면|
| sourceId | HWND| 수집 소스 ID<li>창에서 해당 필드는 창 핸들을 의미</li><li>화면에서 해당 필드는 화면 ID를 의미</li> |
| sourceName| string | 창 이름, 화면일 경우 Screen0 Screen1... 반환 |
| thumbWidth| int32 | 창 썸네일 너비 |
| thumbHeight| int32 | 창 썸네일 높이 |
| thumbBGRA| buffer | 창 썸네일의 바이너리 buffer |
| iconWidth | int32 | 창 아이콘의 너비 |
| iconHeight| int32 | 창 아이콘의 높이 |
| iconBGRA | buffer | 창 아이콘의 바이너리 buffer |

위 정보에 따라, 공유 가능한 타깃을 나열하여 사용자가 선택할 수 있는 간단한 리스트 페이지를 구현할 수 있습니다(다음 이미지 참고).



## 공유 타깃 선택
TRTC SDK는 3가지 공유 모드를 지원합니다. `selectScreenCaptureTarget`을 통해 지정할 수 있습니다.

- **전체 화면 공유**:
전체 화면 창을 공유하는 것으로, 멀티 모니터 화면 분할을 지원합니다. sourceInfoList의 type이 `TRTCScreenCaptureSourceTypeScreen`인 source 매개변수를 지정하고 captureRect를 { 0, 0, 0, 0 }으로 설정해야 합니다.

- **지정 구역 공유**:
화면의 특정 구역을 공유하는 것으로, 사용자가 지정한 구역의 위치 좌표가 필요합니다. sourceInfoList의 type이 `TRTCScreenCaptureSourceTypeScreen`인 source 매개변수를 지정하고 captureRect를 NULL로 설정하지 말아야 합니다. 예: { 100, 100, 300, 300 }

- **지정 창 공유**:
타깃 창의 콘텐츠를 공유하는 것으로, 사용자가 공유할 창을 선택해야 합니다. sourceInfoList의 type이 `TRTCScreenCaptureSourceTypeWindow`인 source 매개변수를 지정하고 captureRect를 { 0, 0, 0, 0 }으로 설정해야 합니다.


>? 추가 매개변수 2개:
> - 매개변수 captureMouse는 마우스 포인터의 캡처 여부를 지정할 때 사용합니다.
> - 매개변수 highlightWindow는 현재 공유 중인 창의 하이라이트 여부, 캡처한 아이콘이 가려졌을 때 사용자에게 가림 제거 알림 여부를 지정할 때 사용합니다. 이 부분의 UI 특수효과는 SDK 내부에서 구현합니다.


## 화면 공유 시작

 - 공유 타깃 선택 후 `startScreenCapture` 인터페이스를 사용하여 화면 공유를 실행할 수 있습니다.
 - 공유 중에도 `selectScreenCaptureTarget`을 호출하여 공유 타깃을 변경할 수 있습니다.
 - `pauseScreenCapture`와 `stopScreenCapture`의 차이는 pause의 화면 콘텐츠 수집 중지 여부와 중지된 순간의 화면 연동입니다. 따라서 원격에서는 resume될 때까지 마지막 프레임만 보게 됩니다.

```C++
    /**
    * \brief 7.5 [화면 공유] 화면 공유 실행
    * \param: rendHwnd - 미리보기 화면을 처리하는 HWND
    */
    void startScreenCapture(HWND rendHwnd);

    /**
    * \brief 7.6 [화면 공유] 화면 공유 일시 중지
    */
    void pauseScreenCapture();

    /**
    * \brief 7.7 [화면 공유] 화면 공유 재개
    */
    void resumeScreenCapture();

    /**
    * \brief 7.8 [화면 공유] 화면 공유 비활성화
    */
    void stopScreenCapture();
```

## 화질 설정
`setSubStreamEncoderParam` 인터페이스에서 해상도, 비트 레이트, 프레임 레이트 등 공유 화면의 화질을 설정할 수 있습니다. 다음 값을 참고하십시오.

| 해상도 레벨 | 해상도 | 프레임 레이트 | 비트 레이트 |
|:-------------:|:---------:|:---------:| :---------: |
| 초고화질(HD+) | 1920 × 1080 | 10 | 800 kbps |
|  고화질(HD) | 1280 × 720 | 10 | 600kbps |
| 표준 화질(SD) | 960 × 720 | 10 | 400 kbps |

## 공유 화면 시청
- **Mac/Window 공유 화면 시청**
  방 안에 있는 Mac/Windows 사용자가 화면 공유를 실행하면 서브스트림을 통해 공유가 시작됩니다. 방 안의 다른 사용자는 TRTCCloudDelegate의 [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) 이벤트를 통해 이 공지를 수신합니다.
  공유 화면을 시청하려면 [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) 인터페이스를 통해 원격 사용자의 서브스트림 화면을 렌더링할 수 있습니다.

- **Android/iOS 공유 화면 시청**
  사용자가 Android/iOS를 통해 화면 공유를 실행하면 메인스트림을 통해 공유가 시작됩니다. 방 안의 다른 사용자는 TRTCCloudDelegate의 [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트를 통해 이 공지를 수신합니다.
  공유 화면을 시청하려면 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) 인터페이스를 통해 원격 사용자의 메인스트림 화면을 렌더링할 수 있습니다.

```C++
//예시 코드: 공유 화면 시청
void CTRTCCloudSDK::onUserSubStreamAvailable(const char * userId, bool available)
{
	    LINFO(L"onUserSubStreamAvailable userId[%s] available[%d]\n", UTF82Wide(userId).c_str(), available);
	   if (available)  {
	         startRemoteSubStreamView(userId, hWnd);
	   } else {
	         stopRemoteSubStreamView(userId);
	   }
}
```

## FAQ
 **한 개의 방에서 동시에 몇 개 채널의 화면을 공유할 수 있나요?**
현재 하나의 TRTC 멀티미디어 방에서는 한 채널의 화면만 공유할 수 있습니다.

 **지정 창 공유(SourceTypeWindow) 시 창의 크기가 달라질 경우 비디오 스트림의 해상도도 변경되나요?**
기본적으로 SDK 내부에서는 공유한 창의 크기에 따라 자동으로 코드 매개변수를 조정합니다.
고정 해상도가 필요한 경우 setSubStreamEncoderParam 인터페이스를 호출하여 화면 공유 코딩 매개변수를 설정하거나 startScreenCapture 호출 시 해당 코딩 매개변수를 지정해야 합니다.
