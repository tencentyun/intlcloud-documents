このドキュメントでは、主に現在のネットワーク品質の検出方法を紹介します。

WeChatビデオ通話を使用しているときに、ネットワーク環境が悪い場合（たとえば、エレベーターに入った後）、WeChatビデオ通話のインターフェースで「現在のネットワーク品質が悪い」と表示されます。このドキュメントでは、主にTRTCを介して同じインタラクションを実行する方法について説明します。

<img src="https://qcloudimg.tencent-cloud.cn/raw/22766930827983b14cf0875776233eeb.jpg" width=800>

## 呼び出しガイド

TRTCは、**onNetworkQuality**と呼ばれるコールバックイベントを提供します。このイベントは、現在のネットワーク品質を2秒ごとに報告します。そのパラメーターには、localQualityとremoteQualityの2つの部分が含まれます：
- **localQuality** ：それぞれExcellent、Good、Poor、Bad、VeryBadとDownの6つのレベルに分けて、現在のネットワーク品質を表します。
- **remoteQuality**：リモートユーザーのネットワーク品質を表します。これはプライムグループであり、プライムグループのそれぞれの要素はリモートユーザーのそれぞれのネットワーク品質を表します。

| Quality | 名称 | 説明 |
|---------|---------|---------|
| 0 | Unknown | 検出されていません |
| 1 | Excellent | 現在のネットワークは非常に良い |
| 2 | Good | 現在のネットワークは比較的良い |
| 3 | Poor | 現在のネットワークは一般です |
| 4 | Bad | 現在のネットワークは悪い。明らかなラグや通話の遅延が発生する可能性があります|
| 5 | VeryBad | 現在のネットワークは非常に悪い。TRTCは接続をほぼ維持できませんが、通信品質を保証することはできません|
| 6 | Down | 現在のネットワークはTRTCの最小要件を満たしていないため、通常のオーディオビデオ通話を行うことはできません。|

TRTCの[onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality)を監視し、インターフェースで対応するプロンプトを表示するだけでよい。

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
