This document describes how to assess the current network conditions.

When you have a video call on WeChat under poor network conditions (for example, when you are in an elevator), WeChat displays a message indicating the current network quality is poor. This document describes how to use TRTC to implement a similar interaction in your own application.

<img src="https://qcloudimg.tencent-cloud.cn/raw/22766930827983b14cf0875776233eeb.jpg" width=800>

## Call Guide

TRTC provides the **onNetworkQuality** callback to report the current network quality once every two seconds. It contains two parameters: `localQuality` and `remoteQuality`.
- **localQuality** indicates your current network quality, which has six levels: `Excellent`, `Good`, `Poor`, `Bad`, `VeryBad`, and `Down`.
- **remoteQuality** is an array indicating the network quality of remote users. In this array, each element represents the network quality of a remote user.

| Quality | Name | Description |
|---------|---------|---------|
| 0 | Unknown | Unknown |
| 1 | Excellent | The current network is excellent. |
| 2 | Good | The current network is good. |
| 3 | Poor | The current network is fine. |
| 4 | Bad | The current network is poor. There may be obvious stuttering and delay. |
| 5 | VeryBad | The current network is very poor. TRTC can sustain the connection but cannot guarantee the communication quality. |
| 6 | Down | The current network cannot meet the minimum requirements of TRTC, and it is impossible to have a normal audio/video call. |

You only need to listen for [onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality) of TRTC and display the corresponding prompt on the UI.

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
