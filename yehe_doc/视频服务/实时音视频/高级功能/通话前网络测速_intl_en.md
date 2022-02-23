
It is difficult for ordinary users to measure network quality. Before calls are made, we recommend that you test the network speed to get more accurate results on network quality.

## Notes

- To ensure call quality, do not run the test during a video call.
- Speed testing consumes traffic and consequently generates a small traffic fee (almost negligible).

## Supported Platforms

| iOS | Android | Mac OS | Windows | Electron| Web |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003; | &#10003; (Reference: [Guide for Web](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html))|

## How Speed Testing Works

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- During speed testing, the SDK sends a batch of probe packets to the server node, measures the quality of return packets, and returns the testing result via a callback API.
- The testing result can be used to optimize the SDK's server selection policy, so you are advised to run the test before the first call, which will help the SDK select the optimal server. If the result is unsatisfactory, you can show a UI message asking users to change to a better network.
- The test result ([TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult)) includes the following parameters:
<table>
<tr><th>Parameter</th><th>Type</th><th>Description</th>
</tr><tr>
<td>success</td>
<td>Success result</td>
<td>Whether the test is successful.</td>
</tr><tr>
<td>errMsg</td>
<td>Error message</td>
<td>Error message of bandwidth test.</td>
</tr><tr>
<td>ip</td>
<td>Server address</td>
<td>Testing server IP</td>
</tr><tr>
<td><a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga25f9ccb045890cb18a5f647ef3c1f974">quality</a></td>
<td>Network quality score</td>
<td>Network quality measured by the SDK. Lower packet loss and shorter RTT result in a higher network quality score.</td>
</tr><tr>
<td>upLostRate</td>
<td>Upstream packet loss rate</td>
<td>Value range: 0-1.0. `0.3` indicates that for every 10 data packets sent to the server, 3 may be lost.</td>
</tr><tr>
<td>downLostRate</td>
<td>Downstream packet loss rate</td>
<td>Value range: 0-1.0. `0.2` indicates that for every 10 data packets received from the server, 2 may be lost.</td>
</tr><tr>
<td>rtt</td>
<td>Latency</td>
<td>The time it takes for data to travel from the SDK to the server and back again. The shorter the RTT, the better. The normal range of RTT is 10-100 ms.</td>
</tr><tr>
<td>availableUpBandwidth</td>
<td>Upstream bandwidth</td>
<td>Estimated upstream bandwidth in Kbps. -1 indicates an invalid value.</td>
</tr><tr>
<td>availableDownBandwidth</td>
<td>Downstream bandwidth</td>
<td>Estimated downstream bandwidth in Kbps. -1 indicates an invalid value.</td>
</tr></table>

## How to Test Speed

The speed test feature can be started through the `startSpeedTest` function of `TRTCCloud`. The speed test result will be called back through the callback function.

<dx-codeblock>
::: Objective-C ObjectiveC
// Sample code for starting speed testing. `sdkAppId` and `UserSig` are required. For how to get them, see Basic Features.
// The example below starts after login.
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    TRTCSpeedTestParams *params;
    // `sdkAppID` is the actual application ID obtained from the console.
    params.sdkAppID = sdkAppId;
    params.userID = userId;
    params.userSig = userSig;
    // Expected upstream bandwidth in Kbps. Value range: 10–5000. 0 indicates not to test
    params.expectedUpBandwidth = 5000;
    // Expected downstream bandwidth in Kbps. Value range: 10–5000. 0 indicates not to test
    params.expectedDownBandwidth = 5000;
    [trtcCloud startSpeedTest:params];
}
- (void)onSpeedTestResult:(TRTCSpeedTestResult *)result {
    // The speed test result will be called back after the test is completed
}
:::
::: Java Java
// Sample code for starting speed testing. `sdkAppId` and `UserSig` are required. For how to get them, see Basic Features.
// The example below starts after login.
public void onLogin(String userId, String userSig) 
{
  TRTCCloudDef.TRTCSpeedTestParams params = new TRTCCloudDef.TRTCSpeedTestParams();
  params.sdkAppId = GenerateTestUserSig.SDKAPPID;
  params.userId = mEtUserId.getText().toString();
  params.userSig = GenerateTestUserSig.genTestUserSig(params.userId);
  params.expectedUpBandwidth = Integer.parseInt(expectUpBandwidthStr);
  params.expectedDownBandwidth = Integer.parseInt(expectDownBandwidthStr);
	// `sdkAppID` is the actual application ID obtained from the console.
    trtcCloud.startSpeedTest(params);
}

// Listen for the test result. Inherit `TRTCCloudListener` and implement the following method.
void onSpeedTestResult(TRTCCloudDef.TRTCSpeedTestResult result)
{
    // The speed test result will be called back after the test is completed
}
:::
::: C++ C++
// Sample code for starting speed testing. `sdkAppId` and `UserSig` are required. For how to get them, see Basic Features.
// The example below starts after login.
void onLogin(const char* userId, const char* userSig)
{
    TRTCSpeedTestParams params;
    // `sdkAppID` is the actual application ID obtained from the console.
    params.sdkAppID = sdkAppId;
    params.userId = userid;
    param.userSig = userSig;
    // Expected upstream bandwidth in Kbps. Value range: 10–5000. 0 indicates not to test
    param.expectedUpBandwidth = 5000;
    // Expected downstream bandwidth in Kbps. Value range: 10–5000. 0 indicates not to test
    param.expectedDownBandwidth = 5000;
    trtcCloud->startSpeedTest(params);
}

// Listen for the testing result
void TRTCCloudCallbackImpl::onSpeedTestResult(
             const TRTCSpeedTestResult& result)
{
    // The speed test result will be called back after the test is completed
}
:::
::: C# C#
// Sample code for starting speed testing. `sdkAppId` and `UserSig` are required. For how to get them, see Basic Features.
// The example below starts after login.
private void onLogin(string userId, string userSig)
{
    TRTCSpeedTestParams params;
    // `sdkAppID` is the actual application ID obtained from the console.
    params.sdkAppID = sdkAppId;
    params.userId = userid;
    param.userSig = userSig;
    // Expected upstream bandwidth in Kbps. Value range: 10–5000. 0 indicates not to test
    param.expectedUpBandwidth = 5000;
    // Expected downstream bandwidth in Kbps. Value range: 10–5000. 0 indicates not to test
    param.expectedDownBandwidth = 5000;
    mTRTCCloud.startSpeedTest(params);
}

// Listen for the testing result
public void onSpeedTestResult(TRTCSpeedTestResult result)
{
    // The speed test result will be called back after the test is completed
}
:::
</dx-codeblock>

## Speed Test Tool
If you don't want to call an API to test the network speed, you can use the network speed test tool for PC provided by TRTC to quickly get the network quality details.
### Download link
[Mac](https://liteav.sdk.qcloud.com/customer/%E6%B5%8B%E8%AF%95/%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7/trtc-network-tools-latest.dmg) ｜[Windows](https://liteav.sdk.qcloud.com/customer/%E6%B5%8B%E8%AF%95/%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7/trtc-network-tools_Setup_latest.exe)
### Test metrics

| Metric         | Description                                                                                                               |
|--------------|--------------------------------------------------------------------------------------------------------------------|
| WiFi Quality | Wi-Fi signal reception quality                                                                                                  |
| DNS RTT      | Tencent Cloud testing domain DNS round-trip time (RTT)                                                                          |
| MTR          | MTR is a network speed test tool, which can detect the packet loss rate and latency between client and TRTC node and display the details of each hop in the route |
| UDP Loss     | UDP packet loss rate between client and TRTC node                                                                                        |
| UDP RTT      | UDP latency between client and TRTC node                                                                                        |
| Local RTT    | Latency between client and local gateway                                                                                        |
| Upload       | Estimated upstream bandwidth                                                                                                       |
| Download     | Estimated downstream bandwidth                                                                                                       |


### Tool screenshots

Quick test:
![](https://qcloudimg.tencent-cloud.cn/raw/2fff6c178663ae53af68844e63c02048.png)
Continuous test:
![](https://qcloudimg.tencent-cloud.cn/raw/76e0e62a6ea6f92779f37bd7331d0085.png)



