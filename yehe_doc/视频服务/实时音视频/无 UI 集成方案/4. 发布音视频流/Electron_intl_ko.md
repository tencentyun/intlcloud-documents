본 문서는 앵커가 오디오/비디오 스트림을 게시하는 방법을 설명합니다. ‘게시’는 마이크와 카메라를 켜서 오디오를 듣고 비디오를 방의 다른 사용자에게 표시하는 것을 의미합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)
## 호출 가이드

[](id:step1)
### 1단계: 필수 단계 수행
[iOS](https://intl.cloud.tencent.com/document/product/647/35097)에 안내된 대로 SDK를 가져오기 및 구성합니다.

[](id:step2)
### 2단계: 카메라 미리보기 활성화
**startLocalPreview** API를 호출하여 카메라 미리보기를 활성화하면 SDK가 카메라 권한에 대해 시스템에 적용됩니다. 카메라 이미지는 권한이 부여된 후에만 캡처할 수 있습니다.

로컬 비디오 이미지의 렌더링 매개변수를 설정하려면 **setLocalRenderParams** API를 호출하여 로컬 미리보기의 렌더링 매개변수를 설정할 수 있습니다. 미리보기가 활성화된 후 미리보기 매개변수를 설정하면 화면 떨림이 발생할 수 있으므로 미리보기 매개변수를 설정하려면 미리보기를 활성화하기 전에 이 API를 호출하는 것이 좋습니다.

```javascript
// 로컬 비디오 이미지의 미리보기 모드 설정: 수평 미러링을 활성화하고 비디오 이미지의 채우기 모드를 설정합니다
import TRTCCloud, { 
	TRTCRenderParams, TRTCVideoRotation,
	TRTCVideoFillMode, TRTCVideoMirrorType
} from 'trtc-electron-sdk';

const param = new TRTCRenderParams(
	TRTCVideoRotation.TRTCVideoRotation0,
	TRTCVideoFillMode.TRTCVideoFillMode_Fill,
	TRTCVideoMirrorType.TRTCVideoMirrorType_Auto
);
const rtcCloud = new TRTCCloud();
rtcCloud.setLocalRenderParams(param);
const cameraVideoDom = document.querySelector('.camera-dom');
rtcCloud.startLocalPreview(cameraVideoDom);
```

[](id:step3)
### 3단계: 마이크 캡처 활성화
**startLocalAudio**를 호출하여 마이크 캡처를 시작할 수 있습니다. 이 API를 사용하려면 'quality' 매개변수를 사용하여 캡처 모드를 결정해야 합니다. 매개변수 이름이 quality이지만 정확히는 scene을 의미합니다. 높은 품질이 반드시 좋은 것은 아니며 비즈니스 시나리오에 따라 적절한 품질을 설정해야 합니다.

- **SPEECH**
이 모드에서 SDK 오디오 모듈은 오디오 신호를 캡처하고 가능한 한 환경 소음을 필터링하는 데 전념합니다. 또한 이 모드의 오디오 데이터는 열악한 네트워크 품질에 대한 내성이 가장 높습니다. 따라서 ‘화상 통화’ 및 ‘온라인 회의’와 같이 음성 통신을 강조하는 시나리오에 특히 적합합니다.
- **MUSIC**
이 모드에서 SDK는 높은 오디오 처리 대역폭과 스테레오 모드를 사용하여 캡처 품질을 최대화하고 오디오 DSP 모듈을 가장 낮은 수준으로 조정하여 가능한 최고의 오디오 품질을 제공합니다. 따라서 앵커가 전문 사운드 카드를 사용하여 음악을 라이브 스트리밍하는 경우 특히 ‘음악 라이브 스트리밍’ 시나리오에 적합합니다.
- **DEFAULT**
이 모드에서 SDK는 스마트 인식 알고리즘을 사용하여 현재 환경을 인식하고 그에 따라 가장 적합한 처리 모드를 선택합니다. 그러나 아무리 좋은 인식 알고리즘이라도 때로는 부정확할 수 있습니다. 제품 포지셔닝에 대해 잘 알고 있다면 SPEECH 또는 MUSIC을 선택하여 더 나은 오디오 커뮤니케이션이나 음악 품질을 즐길 것을 권장합니다.

```javascript
import { TRTCAudioQuality } from 'trtc-electron-sdk';
// 마이크 캡처를 활성화하고 quality를 SPEECH로 설정합니다(노이즈 억제가 높고 네트워크 상태가 좋지 않음)
rtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualitySpeech);

// 마이크 캡처를 활성화하고 quality를 MUSIC으로 설정합니다(최소 오디오 품질 손실로 Hi-Fi 오디오를 캡처하며 전문 사운드 카드와 함께 사용하는 것이 좋습니다)
rtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualityMusic);
```

[](id:step4)
### 4단계: TRTC 방 입장
[방 입장](https://intl.cloud.tencent.com/document/product/647/48049)의 안내에 따라 현재 사용자가 TRTC 방에 입장하도록 합니다. SDK는 방에 성공적으로 입장하면 원격 사용자에게 오디오 스트림을 게시하기 시작합니다.

>! 물론 방에 입장(enterRoom)한 후 카메라 미리보기 및 마이크 캡처를 활성화할 수 있습니다. 그러나 라이브 스트리밍 시나리오에서는 앵커가 마이크를 테스트하고 뷰티 필터를 조정하는 데 일정 시간이 필요합니다. 따라서 먼저 카메라와 마이크를 켜고 방에 들어가는 것이 더 일반적입니다.

```javascript
import { TRTCParams, TRTCRoleType, TRTCAppScene } from 'trtc-electron-sdk';

// TRTC 방 입장 매개변수를 어셈블합니다. TRTCParams의 필드 값을 고유한 매개변수 값으로 교체합니다.
// Please replace each field in TRTCParams with your own parameters
const param = new TRTCParams();
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = TRTCRoleType.TRTCRoleAnchor;

// 시나리오가 ‘라이브 스트리밍’인 경우 애플리케이션 시나리오를 TRTC_APP_SCENE_LIVE로 설정합니다
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
rtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```

