일반 사용자는 네트워크 품질을 평가하기가 매우 어렵습니다. 영상 통화 전 먼저 네트워크 테스트 진행을 권장하며, 속도 테스트를 통해 더 직관적으로 네트워크 품질을 평가할 수 있습니다.

## 주의 사항

- 영상 통화 중에는 테스트하지 마십시오. 통화 품질에 영향이 미칠 수 있습니다.
- 속도 테스트는 일정의 트래픽이 소모됩니다. 따라서 별도로 극소량의 트래픽 비용(기본적으로 생략 가능)이 발생합니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows | Electron | web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003; |  &#10003; | &#10003; | &#10003; | &#10003; |  &#10003  |

## 속도 테스트의 원리

![](https://main.qcloudimg.com/raw/0d95dc823a809d33bd02b5c7c693918c.jpg)

- 속도 테스트는 SDK에서 서버 노드로 감지 패킷을 발송한 후 패킷 반환 품질을 통계하는 원리로, 속도 테스트 결과는 콜백 인터페이스를 통해 통지합니다.

- 속도 테스트 결과는 SDK의 이후 서버 선택 정책을 최적화하는 데 사용됩니다. 따라서 사용자가 최초 통화 전 먼저 속도 테스트를 진행하는 것을 권장하며, 이는 최적의 서버를 선택하는 데 도움이 됩니다. 또한 테스트 결과가 매우 이상적이지 않는 경우 시각화된 UI를 통해 사용자에게 더 나은 네트워크를 선택하도록 안내할 수 있습니다.

- SDK에서 동시에 연결 가능한 클라우드 서버는 일반적으로 3개 이상의 노드를 가지고 있으며, 테스트 과정에서 하나 하나 직렬 연결하여 테스트 속도 결과 콜백 값이 여러 번 나뉘어 반환됩니다.

- 테스트 결과(`TRTCSpeedTestResult`)에는 다음과 같은 몇 가지 필드가 포함되어 있습니다.

| 필드 | 의미 |   의미 설명|
|:-------:|:-------:| :----------|
| ip | 서버 IP | 속도 테스트 결과는 여러 번 콜백되며, 해당 콜백별로 서로 다른 IP 주소입니다. |
| quality | 네트워크 품질 평점 | 평가 알고리즘을 통해 계산한 네트워크 품질입니다. loss가 적고 rtt가 작을수록 점수는 높아집니다. |
| upLostRate | 업스트림 패킷 손실률 | 범위는 [0 - 1.0]입니다. 예를 들어 0.3인 경우 서버로 10개의 데이터 패킷을 보낼 때 3개가 도중에 손실될 수 있다는 의미입니다. |
| downLostRate | 다운스트림 패킷 손실률 |  범위는 [0 - 1.0]입니다. 예를 들어 0.2인 경우 서버에서 10개의 데이터 패킷을 수신할 때 2개가 도중에 손실될 수 있다는 의미입니다. |
| rtt | 네트워크 딜레이 | SDK와 서버를 1회 왕복 시 소모되는 시간입니다. 해당 값은 작을수록 좋으며, 정상값은 10ms ~ 100ms 사이입니다.|

## 테스트 방법

TRTCCloud의 `startSpeedTest` 기능을 통해 속도 테스트 기능을 실행할 수 있으며, 속도 테스트 결과는 콜백 함수를 통해 1~2초에 한 번씩 콜백됩니다. 모든 콜백에는 SDK에서 클라우드 서버 노드까지의 속도 테스트 결과가 포함되어 있으며 콜백 횟수는 SDK에서 총 몇 대의 클라우드 서버에 액세스하는지에 따라 달라집니다.


```Objective-C Objective-C
// 네트워크 속도 테스트 실행 예시 코드이며, sdkAppId와 UserSig 필요(획득 방법은 기본 기능 참조)
// 로그인 후 테스트를 시작한 경우 예시
- (void)onLogin:(NSString *)userId userSig:(NSString *)userSid 
{
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    [trtcCloud startSpeedTest:SDKAppID
                       userId:userId
                      userSig:userSig
                   completion:^(TRTCSpeedTestResult *result, NSInteger completedCount, NSInteger totalCount) {
                       NSLog(@"속도 테스트(%d회/총 %d회) %@", (int)completedCount, (int)totalCount, result);
                   }];
}
```
``` Java Java
// 네트워크 속도 테스트 실행 예시 코드이며, sdkAppId와 UserSig 필요(획득 방법은 기본 기능 참조)
// 로그인 후 테스트를 시작한 경우 예시
public void onLogin(String userId, String userSig) 
{
	// sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    trtcCloud.startSpeedTest(sdkAppID, userId, userSig);
}

// 속도 테스트 결과 수신으로, TRTCCloudListener를 상속하여 다음 방법을 구현
void onSpeedTest(TRTCCloudDef.TRTCSpeedTestResult currentResult, int finishedCount, int totalCount)
{
    // SDK는 여러 서버 IP에 대해 속도 테스트를 진행하며, IP별로 테스트 결과를 콜백함
}
```
``` C++ C++
// 네트워크 속도 테스트 실행 예시 코드이며, sdkAppId와 UserSig 필요(획득 방법은 기본 기능 참조)
 // 로그인 후 테스트를 시작한 경우 예시
void onLogin(const char* userId, const char* userSig)
{
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    trtcCloud->startSpeedTest(sdkAppID, userId, userSig);
}

 // 테스트 결과 수신
void TRTCCloudCallbackImpl::onSpeedTest(
             const TRTCSpeedTestResult& currentResult, uint32_t finishedCount, uint32_t totalCount)
{
    // SDK는 여러 서버 IP에 대해 속도 테스트를 진행하며, IP별로 테스트 결과를 콜백함
}
```
``` C# C#
 // 네트워크 속도 테스트 실행 예시 코드이며, sdkAppId와 UserSig 필요(획득 방법은 기본 기능 참조)
 // 로그인 후 테스트를 시작한 경우 예시
private void onLogin(string userId, string userSig)
{
    // sdkAppID는 콘솔에서 획득한 실제 애플리케이션 AppID
    mTRTCCloud.startSpeedTest(sdkAppID, userId, userSig);
}

 // 테스트 결과 수신
public void onSpeedTest(TRTCSpeedTestResult currentResult, uint finishedCount, uint totalCount)
{
    // SDK는 여러 서버 IP에 대해 속도 테스트를 진행하며, IP별로 테스트 결과를 콜백함
}
```


