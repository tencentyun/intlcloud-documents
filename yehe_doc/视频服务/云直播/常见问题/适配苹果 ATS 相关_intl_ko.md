Apple은 WWDC 2016에서 2017년 01월 01일부터 새로 제출하는 앱은 기본적으로 `NSAllowsArbitraryLoads=YES`를 사용하여 ATS 제한을 피할 수 없다고 발표했습니다. Tencent Cloud는 HTTPS를 지원하므로 새로운 버전의 SDK(인터페이스 변동 없음)를 사용하고 기존 비디오 주소의 접두사를 `http://`에서 `https://`로 변경하면 SDK 내부에서 자동으로 적용됩니다.

그러나 HTTPS는 HTTP와 비교했을 때 보안성이 뛰어난 반면(비디오의 경우 특별히 필요하지 않음) 연결 속도 및 CPU 사용률에서 약점을 가지고 있습니다. 새로운 정책 발표 후에도 앱에서 계속 HTTP를 사용하고자 할 경우 Info.plist를 수정하여 `myqcloud.com`을 `NSExceptionDomains`에 추가하는 방법이 있습니다. 구체적인 수정 방법은 다음과 같습니다.  

![](https://main.qcloudimg.com/raw/9cd1a8754cb0b2e7d2d407fec1f82db1.png)

특정 도메인 ATS 비활성화는 Apple 심사에서 통과될 수 있으며, 심사 시 `myqcloud.com`은 비디오 재생에 사용하는 도메인이라는 설명이 필요합니다.
