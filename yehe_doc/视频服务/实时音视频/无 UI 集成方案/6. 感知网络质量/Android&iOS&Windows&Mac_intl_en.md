This document describes how to assess the current network conditions.

When you have a video call on WeChat under poor network conditions (for example, when you are in an elevator), WeChat displays a message indicating the current network quality is poor. This document describes how to use TRTC to implement a similar interaction in your own application.

![](https://qcloudimg.tencent-cloud.cn/raw/22766930827983b14cf0875776233eeb.jpg)

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
| 4 | Bad | The current network is poor, and there may be obvious stuttering and delay. |
| 5 | VeryBad | The current network is very poor, and TRTC can merely sustain the connection but cannot guarantee the communication quality. |
| 6 | Down | The current network cannot meet the minimum requirements of TRTC, and it is impossible to have a normal audio/video call. |

You only need to listen for `onNetworkQuality` of TRTC and display the corresponding prompt on the UI.

<dx-codeblock>
::: Android  java
// Listen for the `onNetworkQuality` callback to get the change of the current network conditions
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
// Listen for the `onNetworkQuality` callback to get the change of the current network conditions
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
// Listen for the `onNetworkQuality` callback to get the change of the current network conditions
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
