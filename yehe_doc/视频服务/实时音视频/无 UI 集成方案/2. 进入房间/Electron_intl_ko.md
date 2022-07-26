본 문서는 TRTC 방에 들어가는 방법을 설명합니다. 오디오/비디오 방에 입장한 후에만 사용자는 방에 있는 다른 사용자의 오디오/비디오 스트림을 구독하거나 사용자 자신의 오디오/비디오 스트림을 다른 사용자에게 게시할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

## 호출 가이드

[](id:step1)
### 1단계: SDK 가져오기
[iOS](https://intl.cloud.tencent.com/document/product/647/35097)에 안내된 대로 SDK를 가져옵니다.

[](id:step2)
### 2단계: SDK 인스턴스 생성

```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
```

[](id:step3)
### 3단계: SDK 이벤트 수신 대기
이벤트 콜백 API를 설정하여 SDK 동작 중 오류, 알람, 트래픽 통계, 네트워크 품질 정보 및 다양한 오디오/비디오 이벤트를 들을 수 있습니다.

```javascript
function onError(errCode, errMsg) {
  // errorCode는 https://cloud.tencent.com/document/product/647/32257#.E9.94.99.E8.AF.AF.E7.A0.81.E8.A1.A8을 참고하십시오.
  console.log(errCode, errMsg);
}

function onWarning(warningCode, warningMsg) {
  // warningCode는 https://cloud.tencent.com/document/product/647/32257#.E8.AD.A6.E5.91.8A.E7.A0.81.E8.A1.A8을 참고하십시오.
  console.log(warningCode, warningMsg);
}

rtcCloud.on('onError', onError);
rtcCloud.on('onWarning', onWarning);
```

[](id:step4)
### 4단계: 방 입장 매개변수 TRTCParams 준비
enterRoom API를 호출할 때 'TRTCParams' 및 'TRTCAppScene'이라는 두 가지 주요 매개변수를 입력해야 합니다.

#### 매개변수1: TRTCAppScene
이 매개변수는 응용 시나리오를 **라이브 스트리밍** 또는 **실시간 통화**로 지정하는 데 사용됩니다.
- **실시간 통화:** 'TRTCAppSceneVideoCall'과 'TRTCAppSceneAudioCall'의 두 가지 옵션이 있으며 각각 영상 통화와 음성 통화입니다. 이 모드는 일대일 음성/영상 통화 또는 최대 300명의 참석자를 위한 온라인 회의에 적합합니다.
- **온라인 라이브 스트리밍:** 비디오 라이브 스트리밍과 오디오 라이브 스트리밍인 'TRTCAppSceneLIVE'와 'TRTCAppSceneVoiceChatRoom'의 두 가지 옵션이 있습니다. 이 모드는 최대 10만명의 사용자에게 라이브 스트리밍에 적합합니다. 그러나 방의 사용자(**anchor** 또는 **audience**)에 대한 TRTCParams 매개변수에 **role** 필드를 지정해야 합니다

#### 매개변수2: TRTCParams
TRTCParams는 많은 필드로 구성됩니다. 그러나 일반적으로 다음 필드를 설정하는 방법에만 주의하면 됩니다:

| 매개변수 | 설명 | 비고 | 데이터 유형 | 샘플 값 |
|---------|---------|---------|---------|---------|
| SDKAppID | 애플리케이션 ID | <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 볼 수 있습니다. 존재하지 않는 경우 ‘애플리케이션 생성’을 클릭하여 애플리케이션을 생성합니다. | 숫자 | 1400000123 |
| userId | 사용자 ID | 사용자 이름. 영어 대문자 및 소문자(a-z, A-Z), 숫자(0-9), 밑줄 및 하이픈만 포함할 수 있습니다. TRTC에서는 하나의 userId가 두 개의 다른 장치에서 동시에 같은 방에 들어갈 수 없습니다. | 문자열 | ‘denny’ 또는 ‘123321’|
| userSig | 방 입장 서명 | [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)의 안내에 따라 SDKAppID와 userId를 기반으로 userSig를 계산할 수 있습니다. | 문자열 | eJyrVareCeYrSy1SslI... |
| roomId | 방 ID | 숫자 유형의 방 ID입니다. 문자열 형식의 방 ID를 사용하려면 roomId 필드 대신 **strRoomId** 필드만 사용하십시오. strRoomId와 roomId는 함께 사용할 수 없기 때문입니다. | 숫자 | 29834 |
| strRoomId | 방 ID | 문자열 유형의 방 ID입니다. strRoomId와 roomId를 혼동하지 마십시오. TRTC 백엔드에서는 ‘123’과 123을 서로 다른 방으로 간주합니다.  | 숫자 | 29834 |
| role | 역할 | ‘앵커’와 ‘시청자’의 두 가지 역할이 있습니다. 이 필드는 TRTCAppScene이 `TRTCAppSceneLIVE` 또는 `TRTCAppSceneVoiceChatRoom` 라이브 스트리밍 시나리오로 설정된 경우에만 필요합니다. | 열거 | TRTCRoleAnchor 또는 TRTCRoleAudience   |

>!
>- TRTC에서 하나의 userId는 두 개의 다른 장치에서 동시에 같은 방에 들어갈 수 없습니다. 그렇지 않으면 충돌이 발생합니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

[](id:step5)
### 5단계: 방 입장(enterRoom)
[4단계](#step4)에서 설명한 두 개의 매개변수 TRTCAppScene과 TRTCParams를 준비한 후 enterRoom API 함수를 호출하여 방에 들어갈 수 있습니다.

```javascript
import { TRTCParams, TRTCRoleType, TRTCAppScene } from 'trtc-electron-sdk';

const param = new TRTCParams();
param.sdkAppId = 1400000123;
param.userId = "denny";  
param.roomId = 123321;
param.userSig = "xxx";
param.role = TRTCRoleType.TRTCRoleAnchor;

// 시나리오가 ‘라이브 스트리밍’인 경우 애플리케이션 시나리오를 TRTC_APP_SCENE_LIVE로 설정합니다
rtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```

**이벤트 콜백:**
- 방 입장이 성공하면 SDK는 onEnterRoom(result) 이벤트를 다시 호출합니다. 여기서 result는 0보다 큰 값으로 방 입장 소요 시간(밀리초)을 나타냅니다.
- 방 입장이 실패하면 SDK는 onEnterRoom(result) 이벤트도 다시 호출하지만 'result' 값은 방 입장 실패에 대한 오류 코드를 나타내는 음수가 됩니다.

```javascript
function onEnterRoom(result) {
  // onEnterRoom 은 https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom을 참고하십시오.
  if (result > 0) {
    console.log('Enter room succeed');
  } else {
    // 방 입장 오류 코드는 https://intl.cloud.tencent.com/document/product/647/35124를 참고하십시오.
    console.log('Enter room failed');
  }
  
}

rtcCloud.on('onEnterRoom', onEnterRoom);
```
