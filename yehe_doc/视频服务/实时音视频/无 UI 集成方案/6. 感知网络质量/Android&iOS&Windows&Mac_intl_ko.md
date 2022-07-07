본 문서는 현재 네트워크 상태를 평가하는 방법을 설명합니다.

네트워크 상태가 좋지 않은 경우(예: 엘리베이터에 있을 때) WeChat에서 화상 통화를 하면 WeChat은 ‘현재 네트워크 품질이 좋지 않습니다’라는 메시지를 표시합니다. 본 문서에서는 이러한 상호 작용을 구현하기 위해 TRTC를 사용하는 방법을 설명합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/22766930827983b14cf0875776233eeb.jpg)

## 호출 가이드
TRTC는 2초에 한 번씩 현재 네트워크 품질을 보고하는 **onNetworkQuality** 콜백 이벤트를 제공합니다. 여기에는 localQuality와 remoteQuality의 두 매개변수가 포함됩니다.
- **localQuality**: Excellent, Good, Poor, Bad, VeryBad 및 Down의 6가지 수준으로 현재 네트워크 품질을 나타냅니다.
- **remoteQuality**: 원격 사용자의 네트워크 품질을 나타내는 배열입니다. 이 배열에서 각 요소는 원격 사용자의 네트워크 품질을 나타냅니다.

| Quality | 이름 | 설명 |
|---------|---------|---------|
| 0 | Unknown | 알 수 없음 |
| 1 | Excellent | 현재 네트워크가 우수함 |
| 2 | Good | 현재 네트워크가 좋음 |
| 3 | Poor | 현재 네트워크에 문제가 없음 |
| 4 | Bad | 현재 네트워크 상태가 좋지 않아 지연 및 통화 지연이 발생할 수 있음 |
| 5 | VeryBad | 현재 네트워크는 매우 열악하고 TRTC는 연결을 유지할 수 있을 뿐 통신 품질을 보장할 수 없음 |
| 6 | Down | 현재 네트워크는 TRTC의 최소 요구 사항을 충족할 수 없으며 정상적인 음성/영상 통화 불가능 |

TRTC의 onNetworkQuality를 수신 대기하고 UI에 해당 프롬프트를 표시하기만 하면 됩니다:

<dx-codeblock>
::: Android  java
// onNetworkQuality 콜백을 수신하여 현재 네트워크 상태의 변경 사항을 가져옴
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
// onNetworkQuality 콜백을 수신하여 현재 네트워크 상태의 변경 사항을 가져옴
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
// onNetworkQuality 콜백을 수신하여 현재 네트워크 상태의 변경 사항을 가져옴
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
