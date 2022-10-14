본문에서는 화면을 공유하는 방법을 설명합니다. 현재 TRTC 룸은 한 번에 하나의 화면 공유 스트림만 가질 수 있습니다.

TRTC는 Windows의 메인 스트림 및 서브 스트림 모드에서 화면 공유를 지원합니다.

- **서브 스트림 공유**
TRTC에서는 화면 공유를 위해 비디오 스트림의 업스트림 채널을 단독으로 활성화할 수 있으며, 이를 '서브 스트림(**substream**)'이라고 부릅니다. 서브 스트림 공유란 호스트가 카메라 화면과 스크린 화면, 두 채널의 화면을 동시에 업스트림하는 것입니다. 이는 VooV Meeting의 사용 방법으로, `startScreenCapture` 인터페이스 호출 시 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeSub`로 지정하여 해당 모드를 활성화할 수 있습니다.

- **메인 스트림 공유**
TRTC에서 일반적으로 카메라 데이터가 지나가는 터널을 '메인 스트림(**bigstream**)'이라고 하며, 메인 스트림 공유란 카메라 터널을 통한 화면 공유입니다. 해당 모드에서 호스트가 보유한 비디오 스트림 업스트림 채널은 1개이며, 상호 배제 관계인 카메라 화면과 스크린 화면 중 하나를 업스트림합니다. `startScreenCapture` 인터페이스 호출 시 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeBig`으로 지정해 해당 모드를 활성화할 수 있습니다.

## 종속된 API

| API 기능 | C++ 버전 |  C# 버전 | Electron 버전 |
|---------|---------|---------|---------|
|공유 타깃 선택| selectScreenCaptureTarget | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) |
|화면 공유 시작| startScreenCapture | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) |
|화면 공유 일시 중지| pauseScreenCapture | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) |
|화면 공유 재개| resumeScreenCapture | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture)|
|화면 공유 종료| stopScreenCapture | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) |


## 공유 타깃 획득
`getScreenCaptureSources`를 통해 공유 가능한 창 리스트를 열거할 수 있으며, 리스트는 매개변수 sourceInfoList를 통해 반환됩니다.
>? Windows의 데스크톱 화면도 하나의 창이며, 데스크톱 창(Desktop)이라고 부릅니다. 듀얼 모니터를 사용하는 경우 모니터마다 해당하는 데스크톱 창이 있습니다. 따라서 getScreenCaptureSources가 반환하는 창 리스트에도 Desktop 창이 있을 수 있습니다.

획득한 창 정보를 기반으로 아래와 같이 사용자가 선택할 수 있는 공유 가능한 소스 목록을 UI에 표시할 수 있습니다.

## 화면 공유 시작

 - 공유 타깃 선택 후 `startScreenCapture` 인터페이스를 사용하여 화면 공유를 실행할 수 있습니다.
 - 공유 중에도 `selectScreenCaptureTarget`을 호출하여 공유 타깃을 변경할 수 있습니다.
 - `pauseScreenCapture`와 `stopScreenCapture`의 차이는 pause의 화면 콘텐츠 수집 중지 여부와 중지된 순간의 화면 연동입니다. 따라서 원격에서는 resume될 때까지 마지막 프레임만 보게 됩니다.


## 화질 설정
`setSubStreamEncoderParam` 인터페이스에서 해상도, 비트 레이트, 프레임 레이트 등 공유 화면의 화질을 설정할 수 있습니다. 다음 값을 참고하십시오.

| 해상도 레벨 | 해상도 | 프레임 레이트 | 비트 레이트 |
|:-------------:|:---------:|:---------:| :---------: |
| 초고화질(HD+) | 1920 × 1080 | 10 | 800 kbps |
|  고화질(HD) | 1280 × 720 | 10 | 600kbps |
| 표준 화질(SD) | 960 × 720 | 10 | 400 kbps |

## 공유 화면 시청
  방에 있는 사용자가 화면 공유를 시작하면 서브 스트림을 통해 화면이 공유되고 방에 있는 다른 사용자는 ITRTCCloudCallback의 [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html)을 통해 알림을 받습니다.
  공유 화면을 보고 싶은 사용자는 [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html) API를 통해 원격 사용자의 서브 스트림 이미지 렌더링을 시작할 수 있습니다.

```C++
//예시 코드: 공유 화면 시청
void CTRTCCloudSDK::onUserSubStreamAvailable(const char * userId, bool available) {
    LINFO(L"onUserSubStreamAvailable userId[%s] available[%d]\n", UTF82Wide(userId).c_str(), available);
    liteav::ITRTCCloud* trtc_cloud_ = getTRTCShareInstance();
    if (available)  {
        trtc_cloud_->startRemoteView(userId, liteav::TRTCVideoStreamTypeSub, hWnd);
    } else {
        trtc_cloud_->stopRemoteView(userId, liteav::TRTCVideoStreamTypeSub);
    }
}
```

## FAQ
####  1. 방에서는 동시에 몇 개 채널의 화면을 공유할 수 있습니까?
현재 하나의 TRTC 멀티미디어 방에서는 한 채널의 화면만 공유할 수 있습니다.

####  2. 지정 창 공유(SourceTypeWindow) 시 창의 크기가 달라질 경우 비디오 스트리밍의 해상도도 변경됩니까?
기본적으로 SDK 내부에서는 공유한 창의 크기에 따라 자동으로 코드 매개변수를 조정합니다.
고정 해상도가 필요한 경우 setSubStreamEncoderParam 인터페이스를 호출하여 화면 공유 코딩 매개변수를 설정하거나 startScreenCapture 호출 시 해당 코딩 매개변수를 지정해야 합니다.
