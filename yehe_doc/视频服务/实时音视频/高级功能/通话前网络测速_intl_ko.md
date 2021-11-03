일반 사용자가 네트워크 품질을 평가하기 어렵기 때문에 영상 통화 전에 네트워크 테스트를 해보는 것을 권장합니다. 속도 테스트를 통해 네트워크 품질을 보다 직관적으로 평가할 수 있습니다.

## 주의 사항

- 영상 통화 중에는 테스트하지 마십시오. 통화 품질에 영향이 미칠 수 있습니다.
- 속도 테스트 자체가 일정량의 트래픽을 소모하기 때문에 매우 적은 양의 추가 트래픽 비용이 발생합니다(기본적으로 무시할 수 있음).

## 지원 플랫폼

| iOS | Android | Mac OS | Windows | Electron| Web |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003; | &#10003; 참고：[Web 튜토리얼](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)  |

## 속도 테스트 원리

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- 속도 테스트의 원리는 SDK가 감지 패킷 배치를 서버 노드로 보낸 다음 반환된 패킷의 품질을 계산하고 속도 테스트 결과를 콜백 인터페이스를 통해 알려주는 것입니다.
- 속도 테스트 결과는 SDK의 이후 서버 선택 정책을 최적화하는 데 사용됩니다. 따라서 사용자가 최초 통화 전 먼저 속도 테스트를 진행하는 것을 권장하며, 이는 최적의 서버를 선택하는 데 도움이 됩니다. 또한 테스트 결과가 매우 이상적이지 않는 경우 시각화된 UI를 통해 사용자에게 더 나은 네트워크를 선택하도록 안내할 수 있습니다.
- SDK에서 동시에 연결 가능한 클라우드 서버는 일반적으로 3개 이상의 노드를 가지고 있으며, 테스트 과정에서 하나 하나 직렬 연결하여 테스트 속도 결과 콜백 값이 여러 번 나뉘어 반환됩니다.
- 속도 테스트 결과 ([TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult))는 다음 필드를 포함합니다.
<table>
<tr><th>필드</th><th>의미</th><th>의미 설명</th>
</tr><tr>
<td>ip</td>
<td>서버 IP</td>
<td>속도 테스트 결과는 여러 번 콜백되며, 각각 다른 IP 주소에 상응합니다.</td>
</tr><tr>
<td>quality</td>
<td>네트워크 품질 평가</td>
<td>평가 알고리즘에 의해 계산된 네트워크 품질은 loss가 낮을수록 rtt가 작아지고 점수가 높아집니다.</td>
</tr><tr>
<td>upLostRate</td>
<td>업스트림 패킷 손실률</td>
<td>범위는 [0-1.0]입니다. 예를 들어 0.3은 서버로 전송되는 10개의 패킷 중 3개의 패킷이 도중 손실될 수 있음을 의미합니다.</td>
</tr><tr>
<td>downLostRate</td>
<td>다운스트림 패킷 손실률</td>
<td>범위는 [0-1.0]입니다. 예를 들어 0.2는 서버에서 수신되는 10개의 패킷 중 2개의 패킷이 도중 손실될 수 있음을 의미합니다.</td>
</tr><tr>
<td>rtt</td>
<td>네트워크 딜레이</td>
<td>SDK와 서버 사이에 소요되는 시간을 나타냅니다. 값이 작을수록 좋습니다. 정상 값은 10ms~100ms입니다.</td>
</tr></table>

## 속도 테스트 방법

TRTCCloud의 `startSpeedTest` 기능을 통해 속도 테스트 기능을 실행할 수 있으며, 속도 테스트 결과는 콜백 함수를 통해 1~2초에 한 번씩 콜백됩니다. 모든 콜백에는 SDK에서 클라우드 서버 노드까지의 속도 테스트 결과가 포함되어 있으며 콜백 횟수는 SDK에서 총 몇 대의 클라우드 서버에 액세스하는지에 따라 달라집니다.


<dx-codeblock>
::: Objective-C Objective-C
// 네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고).
// 로그인 후 테스트 시작 예시
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    [trtcCloud startSpeedTest:SDKAppID
                       userId:userId
                      userSig:userSig
                   completion:^(TRTCSpeedTestResult *result, NSInteger completedCount, NSInteger totalCount) {
                       NSLog(@"속도 테스트 (제 %d회/총 %d회) %@", (int)completedCount, (int)totalCount, result);
                   }];
}
:::
::: Java Java
//네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고).
// 로그인 후 테스트 시작 예시
public void onLogin(String userId, String userSig) 
{
	// sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    trtcCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 속도 테스트 결과 수신. TRTCCloudListener를 상속하여 다음 메소드 구현.
void onSpeedTest(TRTCCloudDef.TRTCSpeedTestResult currentResult, int finishedCount, int totalCount)
{
    // SDK는 여러 서버 IP에 대해 속도 테스트를 진행하며, IP별로 테스트 결과를 콜백함
}
:::
::: C++ C++
// 네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고).
// 로그인 후 테스트 시작 예시
void onLogin(const char* userId, const char* userSig)
{
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    trtcCloud->startSpeedTest(sdkAppID, userId, userSig);
}

// 속도 테스트 결과 수신
void TRTCCloudCallbackImpl::onSpeedTest(
             const TRTCSpeedTestResult& currentResult, uint32_t finishedCount, uint32_t totalCount)
{
    // SDK는 여러 서버 IP에 대해 속도 테스트를 진행하며, IP별로 테스트 결과를 콜백함
}
:::
::: C# C#
// 네트워크 속도 테스트 실행 샘플 코드. sdkAppId, UserSig 필요(획득 방법은 기본 기능 참고).
// 로그인 후 테스트 시작 예시
private void onLogin(string userId, string userSig)
{
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    mTRTCCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 속도 테스트 결과 수신
public void onSpeedTest(TRTCSpeedTestResult currentResult, uint finishedCount, uint totalCount)
{
    // SDK는 여러 서버 IP에 대해 속도 테스트를 진행하며, IP별로 테스트 결과를 콜백함
}
:::
</dx-codeblock>



