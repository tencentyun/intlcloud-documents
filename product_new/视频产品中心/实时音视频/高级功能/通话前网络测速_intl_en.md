It is difficult for ordinary users to evaluate the network quality. It is recommended that you test the network before a video call is made, so that you can evaluate the network quality more intuitively.

## Precautions

- Do not test during a video call so as to avoid affecting the call quality.
- The speed test will consume a certain amount of traffic and generate an extremely small amount of extra traffic fees as a result (which basically can be ignored).

## Supported Platforms

| iOS | Android | macOS | Windows | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | ×  | ×  |

## How Speed Test Works

![](https://main.qcloudimg.com/raw/fda70080f1d1267452ebc721e83e1392.png)

- The speed test works in the following way: the SDK sends a batch of probe packets to the server node, measures the quality of the return packets, and notifies of the speed test results through the callback API.

- The speed test result will be used to optimize the SDK's subsequent selection policy. It is recommended to perform the speed test before users place the first call, which will help select the optimal server. If the test result is not satisfactory, you can use a noticeable UI prompt to remind the user to select a better network.

- Because generally more than three CVM nodes can be connected to by the SDK simultaneously, the test process is performed on the nodes in series one by one, and the return values of the speed test results will be returned in multiple callbacks.

- The speed test result (`TRTCSpeedTestResult`) contains the following fields:

| Field | Meaning | Description |
|:-------:|:-------:| :----------|
| ip | Server IP | Multiple speed test results will be called back, and each of them corresponds to a different IP address |
| quality | Network quality score | Network quality, which is tested and calculated based on the evaluation algorithm. The smaller the loss and round-trip time (RTT), the higher the network quality score |
| upLostRate | Upstreaming packet loss rate | Value range: [0–1.0]. For example, 0.3 indicates that 3 data packets may be lost in every 10 packets sent to the server |
| downLostRate | Downstreaming packet loss rate | Value range: [0–1.0]. For example, 0.2 indicates that 2 data packets may be lost in every 10 packets received from the server |
| rtt | Network delay | This is the round-trip time between the SDK and server. The smaller the value, the better. Normal value range: 10–100 ms |

## How to Test Speed

The speed test feature can be started through the `startSpeedTest` function of TRTCCloud. The speed test result will be called back once every 1–2 seconds through the callback function. Each callback contains a speed test result from the SDK to a CVM node. The number of callbacks is subject to the number of CVM instances the SDK accesses.

- **Objective-C**

``` Objective-C
// The sample code for starting the network speed test requires `sdkAppId` and `UserSig` (for more information on how to get them, please see the basic features)
// Here uses starting the test after login as an example
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    // `sdkAppID` is the `AppID` of the actual application obtained in the console
    [trtcCloud startSpeedTest:SDKAppID
                       userId:userId
                      userSig:userSig
                   completion:^(TRTCSpeedTestResult *result, NSInteger completedCount, NSInteger totalCount) {
                       NSLog(@"Speed test (test %d of %d) %@", (int)completedCount, (int)totalCount, result);
                   }];
}
```

- **Java**

``` java
// The sample code for starting the network speed test requires `sdkAppId` and `UserSig` (for more information on how to get them, please see the basic features)
// Here uses starting the test after login as an example
public void onLogin(String userId, String userSig) 
{
	// `sdkAppID` is the `AppID` of the actual application obtained in the console
    trtcCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// Listen on the speed result. Inherit `TRTCCloudListener` and implement the following method
void onSpeedTest(TRTCCloudDef.TRTCSpeedTestResult currentResult, int finishedCount, int totalCount)
{
    // The SDK performs speed test on multiple server IPs and calls back the test result of one IP each time
}
```

- **C++**

``` C++
// The sample code for starting the network speed test requires `sdkAppId` and `UserSig` (for more information on how to get them, please see the basic features)
// Here uses starting the test after login as an example
void onLogin(const char* userId, const char* userSig)
{
    // `sdkAppID` is the `AppID` of the actual application obtained in the console
    trtcCloud->startSpeedTest(sdkAppID, userId, userSig);
}

// Listen on the speed result
void TRTCCloudCallbackImpl::onSpeedTest(
             const TRTCSpeedTestResult& currentResult, uint32_t finishedCount, uint32_t totalCount)
{
    // The SDK performs speed test on multiple server IPs and calls back the test result of one IP each time
}
```

* **C#**

```c#
// The sample code for starting the network speed test requires `sdkAppId` and `UserSig` (for more information on how to get them, please see the basic features)
// Here uses starting the test after login as an example
private void onLogin(string userId, string userSig)
{
    // `sdkAppID` is the `AppID` of the actual application obtained in the console
    mTRTCCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// Listen on the speed result
public void onSpeedTest(TRTCSpeedTestResult currentResult, uint finishedCount, uint totalCount)
{
    // The SDK performs speed test on multiple server IPs and calls back the test result of one IP each time
}
```




