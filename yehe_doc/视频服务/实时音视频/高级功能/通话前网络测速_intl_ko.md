
일반 사용자가 네트워크 품질을 평가하기 어렵기 때문에 영상 통화 전에 네트워크 테스트를 해보는 것을 권장합니다. 속도 테스트를 통해 네트워크 품질을 보다 직관적으로 평가할 수 있습니다.

## 주의 사항

- 영상 통화 중에는 테스트하지 마십시오. 통화 품질에 영향이 미칠 수 있습니다.
- 속도 테스트 자체가 일정량의 트래픽을 소모하기 때문에 매우 적은 양의 추가 트래픽 비용이 발생합니다(기본적으로 무시할 수 있음).

## 지원 플랫폼

| iOS | Android | Mac OS | Windows | Electron| Web |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003;    | &#10003;(참고: [Web 튜토리얼](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html))  |

## 속도 테스트 원리

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- 속도 테스트의 원리는 SDK가 감지 패킷 배치를 서버 노드로 보낸 다음 반환된 패킷의 품질을 계산하고 속도 테스트 결과를 콜백 인터페이스를 통해 알려주는 것입니다.
- 속도 테스트 결과는 SDK의 이후 서버 선택 정책을 최적화하는 데 사용됩니다. 따라서 사용자가 최초 통화 전 먼저 속도 테스트를 진행하는 것을 권장하며, 이는 최적의 서버를 선택하는 데 도움이 됩니다. 또한 테스트 결과가 매우 이상적이지 않는 경우 시각화된 UI를 통해 사용자에게 더 나은 네트워크를 선택하도록 안내할 수 있습니다.
- 속도 테스트 결과 ([TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult))는 다음 필드를 포함합니다.
<table>
<tr><th>필드</th><th>의미</th><th>의미 설명</th>
</tr><tr>
<td>success</td>
<td>성공 여부</td>
<td>테스트 성공 여부</td>
</tr><tr>
<td>errMsg</td>
<td>오류 정보</td>
<td>대역폭 테스트에 대한 자세한 오류 정보</td>
</tr><tr>
<td>ip</td>
<td>서버 IP</td>
<td>속도 테스트 서버의 IP</td>
</tr><tr>
<td><a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga25f9ccb045890cb18a5f647ef3c1f974">quality</a></td>
<td>네트워크 품질 평가</td>
<td>평가 알고리즘에 의해 계산된 네트워크 품질은 loss가 낮을수록 rtt가 작아지고 점수가 높아집니다.</td>
</tr><tr>
<td>upLostRate</td>
<td>업스트림 패킷 손실률</td>
<td>범위는 [0 - 1.0]입니다. 예를 들어 0.3은 서버로 전송되는 10개의 패킷 중 3개의 패킷이 도중 손실될 수 있음을 의미합니다.</td>
</tr><tr>
<td>downLostRate</td>
<td>다운스트림 패킷 손실률</td>
<td>범위는 [0 - 1.0]입니다. 예를 들어 0.2는 서버에서 수신되는 10개의 패킷 중 2개의 패킷이 도중 손실될 수 있음을 의미합니다.</td>
</tr><tr>
<td>rtt</td>
<td>네트워크 딜레이</td>
<td>SDK와 서버 사이에 소요되는 시간을 나타냅니다. 값이 작을수록 좋습니다. 정상 값은 10ms - 100ms입니다.</td>
</tr><tr>
<td>availableUpBandwidth</td>
<td>업스트림 대역폭</td>
<td>예상 업스트림 대역폭. 단위: kbps, -1: 잘못된 값.</td>
</tr><tr>
<td>availableDownBandwidth</td>
<td>다운스트림 대역폭</td>
<td>예상 다운스트림 대역폭. 단위: kbps, -1: 잘못된 값.</td>
</tr></table>

## 속도 테스트 방법

TRTCCloud의 `startSpeedTest` 기능을 통해 속도 측정 기능을 실행할 수 있습니다. 속도 측정 결과는 콜백 함수를 통해 반환됩니다.

<dx-codeblock>
::: Objective-C ObjectiveC
// 네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고)
// 로그인 후 테스트 시작 예시
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    TRTCSpeedTestParams *params;
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    params.sdkAppID = sdkAppId;
    params.userID = userId;
    params.userSig = userSig;
    // 예상 업스트림 대역폭(kbps, 값 범위: 10 ~ 5000, 0일 때 테스트되지 않음)
    params.expectedUpBandwidth = 5000;
    // 예상 다운스트림 대역폭(kbps, 값 범위: 10 ~ 5000, 0일 때 테스트되지 않음)
    params.expectedDownBandwidth = 5000;
    [trtcCloud startSpeedTest:params];
}
- (void)onSpeedTestResult:(TRTCSpeedTestResult *)result {
    // 속도 측정이 완료된 후 속도 측정 결과 콜백
}
:::
::: Java Java
//네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고)
// 로그인 후 테스트 시작 예시
public void onLogin(String userId, String userSig) 
{
  TRTCCloudDef.TRTCSpeedTestParams params = new TRTCCloudDef.TRTCSpeedTestParams();
  params.sdkAppId = GenerateTestUserSig.SDKAPPID;
  params.userId = mEtUserId.getText().toString();
  params.userSig = GenerateTestUserSig.genTestUserSig(params.userId);
  params.expectedUpBandwidth = Integer.parseInt(expectUpBandwidthStr);
  params.expectedDownBandwidth = Integer.parseInt(expectDownBandwidthStr);
	// sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    trtcCloud.startSpeedTest(params);
}

// 속도 테스트 결과 수신. TRTCCloudListener를 상속하여 다음 메소드 구현
void onSpeedTestResult(TRTCCloudDef.TRTCSpeedTestResult result)
{
    // 속도 측정이 완료된 후 속도 측정 결과 콜백
}
:::
::: C++ C++
// 네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고)
// 로그인 후 테스트 시작 예시
void onLogin(const char* userId, const char* userSig)
{
    TRTCSpeedTestParams params;
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    params.sdkAppID = sdkAppId;
    params.userId   = userid;
    param.userSig = userSig;
    // 예상 업스트림 대역폭(kbps, 값 범위: 10 ~ 5000, 0일 때 테스트되지 않음)
    param.expectedUpBandwidth = 5000;
    // 예상 다운스트림 대역폭(kbps, 값 범위: 10 ~ 5000, 0일 때 테스트되지 않음)
    param.expectedDownBandwidth = 5000;
    trtcCloud->startSpeedTest(params);
}

// 속도 테스트 결과 수신
void TRTCCloudCallbackImpl::onSpeedTestResult(
             const TRTCSpeedTestResult& result)
{
    // 속도 측정이 완료된 후 속도 측정 결과 콜백
}
:::
::: C# C#
// 네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고).
// 로그인 후 테스트 시작 예시
private void onLogin(string userId, string userSig)
{
    TRTCSpeedTestParams params;
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    params.sdkAppID = sdkAppId;
    params.userId   = userid;
    param.userSig = userSig;
    // 예상 업스트림 대역폭(kbps, 값 범위: 10 ~ 5000, 0일 때 테스트되지 않음)
    param.expectedUpBandwidth = 5000;
    // 예상 다운스트림 대역폭(kbps, 값 범위: 10 ~ 5000, 0일 때 테스트되지 않음)
    param.expectedDownBandwidth = 5000;
    mTRTCCloud.startSpeedTest(params);
}

// 속도 테스트 결과 수신
public void onSpeedTestResult(TRTCSpeedTestResult result)
{
    // 속도 측정이 완료된 후 속도 측정 결과 콜백
}
:::
</dx-codeblock>

## 속도 측정 툴
인터페이스를 호출하여 네트워크 속도를 측정하고 싶지 않은 경우, TRTC는 데스크톱에서 네트워크 속도 측정 툴 프로그램을 제공하여 상세한 네트워크 품질 정보를 빠르게 얻을 수 있도록 도와줍니다.
### 다운로드 링크
[Mac](https://liteav.sdk.qcloud.com/customer/%E6%B5%8B%E8%AF%95/%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7/trtc-network-tools-latest.dmg) ｜[Windows](https://liteav.sdk.qcloud.com/customer/%E6%B5%8B%E8%AF%95/%E6%B5%8B%E8%AF%95%E5%B7%A5%E5%85%B7/trtc-network-tools_Setup_latest.exe)
### 테스트 지표

| 지표         | 의미                                                                                                               |
|--------------|--------------------------------------------------------------------------------------------------------------------|
| WiFi Quality | Wi-Fi 신호 품질                                                                                                  |
| DNS RTT      | Tencent Cloud의 속도 테스트 리졸브 소요 시간                                                                          |
| MTR          | MTR은 클라이언트에서 TRTC 노드까지의 패킷 손실률 및 지연을 감지할 수 있는 네트워크 테스트 툴이며 라우팅의 각 홉에 대한 특정 정보 확인 가능 |
| UDP Loss     | 클라이언트에서 TRTC 노드로의 UDP 패킷 손실률                                                                                        |
| UDP RTT      | 클라이언트에서 TRTC 노드까지의 UDP 딜레이                                                                                        |
| Local RTT    | 클라이언트에서 로컬 게이트웨이로의 딜레이                                                                                        |
| Upload       | 업스트림 예상 대역폭                                                                                                       |
| Download     | 다운스트림 예상 대역폭                                                                                                       |


### 툴 화면 캡처

빠른 테스트:
![](https://qcloudimg.tencent-cloud.cn/raw/e1d7e4b4bfcd1c7c3916e56095b8ba24.png)
지속적인 테스트:
![](https://qcloudimg.tencent-cloud.cn/raw/76e0e62a6ea6f92779f37bd7331d0085.png)


