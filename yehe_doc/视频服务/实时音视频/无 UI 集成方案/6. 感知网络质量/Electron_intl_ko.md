본 문서는 현재의 네트워크 상태를 평가하는 방법을 설명합니다.

네트워크 상태가 좋지 않은 경우(예: 엘리베이터에 있을 때) WeChat에서 화상 통화를 하면 WeChat은 ‘현재 네트워크 품질이 좋지 않습니다’라는 메시지를 표시합니다. 이 문서에서는 이러한 상호 작용을 구현하기 위해 TRTC를 사용하는 방법을 설명합니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/22766930827983b14cf0875776233eeb.jpg" width=800>

## 호출 가이드

TRTC는 2초에 한 번씩 현재 네트워크 품질을 보고하는 **onNetworkQuality** 콜백 이벤트를 제공합니다. 여기에는 localQuality와 remoteQuality의 두 매개변수가 포함됩니다.
- **localQuality**: Excellent, Good, Poor, Bad, VeryBad 및 Down의 6가지 수준으로 현재 네트워크 품질을 나타냅니다.
- **remoteQuality**: 원격 사용자의 네트워크 품질을 나타내는 배열입니다. 이 배열에서 각 요소는 원격 사용자의 네트워크 품질을 나타냅니다.

| Quality | 이름 | 설명 |
|---------|---------|---------|
| 0 | Unknown | 알 수 없음 |
| 1 | Excellent | 현재 네트워크 상태 우수 |
| 2 | Good | 현재 네트워크 상태 좋음 |
| 3 | Poor | 현재 네트워크 상태 문제 없음 |
| 4 | Bad | 현재 네트워크 상태가 좋지 않아 랙 및 통화 지연이 발생할 수 있음 |
| 5 | VeryBad | 현재 네트워크 상태는 매우 열악하여 TRTC는 연결을 유지할 수 있을 뿐 통신 품질을 보장할 수 없음 |
| 6 | Down | 현재 네트워크 상태는 TRTC의 최소 요구 사항을 충족할 수 없으며 정상적인 음성/영상 통화가 불가능함 |

TRTC의[onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality)를 수신 대기하고 UI에 해당 프롬프트를 표시하기만 하면 됩니다.

```javascript
import TRTCCloud, { TRTCQuality } from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();

function onNetworkQuality(localQuality, remoteQuality) {
  switch(localQuality.quality) {
    case TRTCQuality.TRTCQuality_Unknown:
      console.log('SDK has not yet sensed the current network quality.');
      break;
    case TRTCQuality.TRTCQuality_Excellent:
      console.log('The current network is very good.');
      break;
    case TRTCQuality.TRTCQuality_Good:
      console.log('The current network is good.');
      break;
    case TRTCQuality.TRTCQuality_Poor:
      console.log('The current network quality barely meets the demand.');
      break;
    case TRTCQuality.TRTCQuality_Bad:
      console.log('The current network is poor, and there may be significant freezes and call delays.');
      break;
    case TRTCQuality.TRTCQuality_Vbad:
      console.log('The current network is very poor, the communication quality cannot be guaranteed.');
      break;
    case TRTCQuality.TRTCQuality_Down:
      console.log('The current network does not meet the minimum requirements.');
      break;
    default:
      break;
  }
  for (let i = 0; i < remoteQuality.length; i++) {
    console.log(`remote user: ${remoteQuality[i].userId}, quality: ${remoteQuality[i].quality}`);
  }
}

rtcCloud.on('onNetworkQuality', onNetworkQuality);
```
