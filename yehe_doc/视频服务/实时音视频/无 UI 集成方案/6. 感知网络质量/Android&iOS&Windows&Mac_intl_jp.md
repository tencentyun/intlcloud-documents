このドキュメントでは、主に現在のネットワーク品質の検出方法を紹介します。

WeChatビデオ通話を使用しているときに、ネットワーク環境が悪い場合（たとえば、エレベーターに入った後）、WeChatビデオ通話のインターフェースで「現在のネットワーク品質が悪い」と表示されます。このドキュメントでは、主にTRTCを介して同じインタラクションを実行する方法について説明します。

![](https://qcloudimg.tencent-cloud.cn/raw/22766930827983b14cf0875776233eeb.jpg)

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

TRTCのonNetworkQualityを監視し、インターフェースで対応するプロンプトを表示するだけでよい。

<dx-codeblock>
::: Android java
// onNetworkQualityコールバックを監視し、現在のネットワーク状態変化を検知します
@Override
public void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality,
                             ArrayList<TRTCCloudDef.TRTCQuality> remoteQuality)
{
    // Get your local network quality
    switch(localQuality) {
        case TRTCQuality_Unknown:
            Log.d(TAG, "SDK has not yet sensed the current network quality.");
            break;
        case TRTCQuality_Excellent:
            Log.d(TAG, "The current network is very good.");
            break;
        case TRTCQuality_Good:
            Log.d(TAG, "The current network is good.");
            break;
        case TRTCQuality_Poor:
            Log.d(TAG, "The current network quality barely meets the demand.");
            break;
        case TRTCQuality_Bad:
            Log.d(TAG, "The current network is poor, and there may be significant freezes and call delays.");
            break;
        case TRTCQuality_VeryBad:
            Log.d(TAG, "The current network is very poor, the communication quality cannot be guaranteed");
            break;
        case TRTCQuality_Down:
            Log.d(TAG, "The current network does not meet the minimum requirements.");
            break;
        default:
            break;
    }
    // Get the network quality of remote users
    for (TRTCCloudDef.TRTCQuality info : arrayList) {
        Log.d(TAG, "remote user : = " + info.userId + ", quality = " + info.quality);
    }
}
:::
::: iOS&Mac  ObjC
// onNetworkQualityコールバックを監視し、現在のネットワーク状態変化を検知します
- (void)onNetworkQuality:(TRTCQualityInfo *)localQuality remoteQuality:(NSArray<TRTCQualityInfo *> *)remoteQuality {
    // Get your local network quality
    switch(localQuality.quality) {
        case TRTCQuality_Unknown:
            NSLog(@"SDK has not yet sensed the current network quality.");
            break;
        case TRTCQuality_Excellent:
            NSLog(@"The current network is very good.");
            break;
        case TRTCQuality_Good:
            NSLog(@"The current network is good.");
            break;
        case TRTCQuality_Poor:
            NSLog(@"The current network quality barely meets the demand.");
            break;
        case TRTCQuality_Bad:
            NSLog(@"The current network is poor, and there may be significant freezes and call delays.");
            break;
        case TRTCQuality_VeryBad:
           NSLog(@"The current network is very poor, the communication quality cannot be guaranteed");
            break;
        case TRTCQuality_Down:
            NSLog(@"The current network does not meet the minimum requirements.");
            break;
        default:
            break;
    }
    // Get the network quality of remote users
    for (TRTCQualityInfo *info in arrayList) {
        NSLog(@"remote user : = %@, quality = %@", info.userId, @(info.quality));
    }
}
:::
::: Windows  C++
// onNetworkQualityコールバックを監視し、現在のネットワーク状態変化を検知します
void onNetworkQuality(liteav::TRTCQualityInfo local_quality,
    liteav::TRTCQualityInfo* remote_quality, uint32_t remote_quality_count) {
    // Get your local network quality
    switch (local_quality.quality) {
    case TRTCQuality_Unknown:
        printf("SDK has not yet sensed the current network quality.");
        break;
    case TRTCQuality_Excellent:
        printf("The current network is very good.");
        break;
    case TRTCQuality_Good:
        printf("The current network is good.");
        break;
    case TRTCQuality_Poor:
        printf("The current network quality barely meets the demand.");
        break;
    case TRTCQuality_Bad:
        printf("The current network is poor, and there may be significant freezes and call delays.");
        break;
    case TRTCQuality_Vbad:
        printf("The current network is very poor, the communication quality cannot be guaranteed");
        break;
    case TRTCQuality_Down:
        printf("The current network does not meet the minimum requirements.");
        break;
    default:
        break;
    }
    // Get the network quality of remote users
    for (int i = 0; i < remote_quality_count; ++i) {
        printf("remote user : = %s, quality = %d", remote_quality[i].userId, remote_quality[i].quality);
    }
}
:::
</dx-codeblock>
