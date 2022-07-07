본 문서에서는 화면을 공유하는 방법을 설명합니다. 현재 TRTC 룸은 한 번에 하나의 화면 공유 스트림만 가질 수 있습니다.

TRTC는 Electron의 메인 스트림 및 서브 스트림 모드에서 화면 공유를 지원합니다.

- **서브 스트림 공유**
TRTC에서는 ‘**substream**’이라고 하는 전용 스트림을 통해 화면을 공유할 수 있습니다. 서브 스트림 공유에서 앵커는 카메라 비디오와 화면 공유 이미지를 동시에 게시합니다. 이것은 VooV Meeting에서 사용하는 체계입니다. `startScreenCapture` API를 호출할 때 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeSub`로 설정하여 서브 스트림 공유를 활성화할 수 있습니다.

- **메인 스트림 공유**
TRTC에서 일반적으로 카메라 데이터가 지나가는 터널을 '메인 스트림(**bigstream**)'이라고 하며, 메인 스트림 공유란 카메라 터널을 통한 화면 공유입니다. 해당 모드에서 호스트가 보유한 비디오 스트림 업스트림 채널은 1개이며, 상호 배제 관계인 카메라 화면과 스크린 화면 중 하나를 업스트림합니다. `startScreenCapture` 인터페이스 호출 시 `TRTCVideoStreamType` 매개변수를 `TRTCVideoStreamTypeBig`으로 지정해 해당 모드를 활성화할 수 있습니다.

[](id:step1)
## 1단계: 공유 소스 가져오기
`getScreenCaptureSources`를 통해 공유 가능한 창 리스트를 열거할 수 있으며, 리스트는 매개변수 sourceInfoList를 통해 반환됩니다.
>? Electron의 데스크톱 화면도 하나의 창이며, 데스크톱 창(Desktop)이라고 부릅니다. 듀얼 모니터를 사용하는 경우 모니터마다 해당하는 데스크톱 창이 있습니다. 따라서 getScreenCaptureSources가 반환하는 창 리스트에도 Desktop 창이 있을 수 있습니다.

획득한 창 정보를 기반으로 아래와 같이 사용자가 선택할 수 있는 공유 가능한 소스 목록을 UI에 표시할 수 있습니다.


```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources
const screenList = rtcCloud.getScreenCaptureSources();
```

[](id:step2)
## 2단계: 화면 공유 시작
 - [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget)을 호출하여 공유 소스를 선택할 수 있습니다.
 - 공유 타깃 선택 후 [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) API를 호출하여 화면 공유를 시작할 수 있습니다.
 - 화면 공유 중 [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget)을 호출하여 공유 소스를 변경할 수 있습니다.
 - [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture)와 [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture)의 차이점은 전자가 화면 캡처를 pause하고 일시 중지하는 순간 이미지를 표시한다는 것입니다. 원격 사용자는 화면 캡처가 resume될 때까지 일시 중지하기 전에 비디오의 마지막 프레임을 봅니다.

```javascript
import TRTCCloud, { 
	Rect, TRTCScreenCaptureProperty, TRTCVideoStreamType, TRTCVideoEncParam,
	TRTCVideoResolution, TRTCVideoResolutionMode
} from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources
const screenList = rtcCloud.getScreenCaptureSources();
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/Rect.html
const captureRect = new Rect(0, 0, 0, 0);
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCScreenCaptureProperty.html
const property = new TRTCScreenCaptureProperty(
	true, true, true, 0, 0, false
);
if (screenList.length > 0) {
	rtcCloud.selectScreenCaptureTarget(screenList[0], captureRect, property)
}

const screenshareDom = document.querySelector('screen-dom');
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVideoEncParam.html
const encParam = new TRTCVideoEncParam(
	TRTCVideoResolution.TRTCVideoResolution_1920_1080,
	TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape,
	15,
	2000,
	0,
	false
); 
rtcCloud.startScreenCapture(screenshareDom, TRTCVideoStreamType.TRTCVideoStreamTypeSub, encParam);
```

[](id:step3)
## 3단계: 화질 설정
`startScreenCapture` API의 세 번째 매개변수(`encParam`)를 사용하여 해상도, 비트 레이트 및 프레임 레이트를 포함하여 화면 공유의 비디오 품질을 설정할 수 있습니다([2단계](#step2) 참고). 다음 설정을 권장합니다:

| 해상도 레벨 | 해상도 | 프레임 레이트 | 비트 레이트 |
|:-------------:|:---------:|:---------:| :---------: |
| 초고화질(HD+) | 1920 × 1080 | 10 | 2000 kbps |
|  고화질(HD) | 1280 × 720 | 10 | 600kbps |
| 표준 화질(SD) | 960 × 720 | 10 | 400 kbps |

[](id:step4)
## 4단계: 화면 공유 보기
방에 있는 사용자가 화면 공유를 시작하면 서브 스트림을 통해 화면이 공유되고 방에 있는 다른 사용자는 [onUserSubStreamAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserSubStreamAvailable)을 통해 알림을 받습니다.
공유 화면을 보고 싶은 사용자는 [startRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) API를 통해 원격 사용자의 서브 스트림 이미지 렌더링을 시작할 수 있습니다.

```javascript
import TRTCCloud, { 
	TRTCVideoStreamType
} from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();

const remoteDom = document.querySelector('.remote-user');
function onUserSubStreamAvailable(userId, available) {
	if (available === 1) {
		rtcCloud.startRemoteView(userId, remoteDom, TRTCVideoStreamType.TRTCVideoStreamTypeSub);
	} else {
		rtcCloud.stopRemoteView(userId, TRTCVideoStreamType.TRTCVideoStreamTypeSub);
	}
}

rtcCloud.on('onUserSubStreamAvailable', onUserSubStreamAvailable);
```

## FAQ
#### 1. 방에서는 동시에 몇 개 채널의 화면을 공유할 수 있습니까?
현재 하나의 TRTC 멀티미디어 방에서는 한 채널의 화면만 공유할 수 있습니다.

#### 2. 지정 창 공유(SourceTypeWindow) 시 창의 크기가 달라질 경우 비디오 스트리밍의 해상도도 변경됩니까?
기본적으로 SDK 내부에서는 공유한 창의 크기에 따라 자동으로 코드 매개변수를 조정합니다.
고정 해상도가 필요한 경우 setSubStreamEncoderParam 인터페이스를 호출하여 화면 공유 코딩 매개변수를 설정하거나 startScreenCapture 호출 시 해당 코딩 매개변수를 지정해야 합니다.
