>? **최신 버전의 SDK(v1.1.0.103)의 TUICallEngine API가 일부 변경되었습니다.**
>- maven latest 업데이트 메커니즘으로 인해 Android 프로젝트 빌드 오류가 발생하는 경우 다음 두 가지 방법을 사용하여 문제를 해결해 보십시오.
	  - TUICallKit을 최신 버전으로 업데이트합니다.
	  - tuicallkit/build.gradle에서 tuicallengine 종속성을 1.0의 고정 버전`com.tencent.liteav.tuikit:tuicallengine:1.0.0.53`으로 지정합니다.
>- pod update를 실행할 때 iOS 프로젝트 빌드 오류가 발생하면 다음 두 가지 방법을 사용하여 문제를 해결해 보십시오.
	  - TUICallKit을 최신 버전으로 업데이트합니다.
	  - Podfile에 `pod ‘TUICallEngine’, ‘1.0.0.53’`을 추가합니다.

### Version 1.1.0.103  @ 2022.09.30
- Android&iOS: 그룹 통화에 새로운 구성원을 초대하는 기능을 최적화했습니다.
- Android&iOS: 통화를 하기 전에 녹화, 조정 및 기타 요금이 부과되지 않도록 통화 프로세스를 최적화했습니다.
- Android&iOS: 사용자 정의 오프라인 알림에 대한 지원이 추가되었습니다.
- Android&iOS: 일부 **TUICallEngine** API의 매개변수가 변경되었습니다. 자세한 내용은 [call()](https://www.tencentcloud.com/document/product/647/51006#call), [groupCall()](https://www.tencentcloud.com/document/product/647/51006#groupcall), [inviteUser()](https://www.tencentcloud.com/document/product/647/51006#inviteuser), [onCallReceived()](https://www.tencentcloud.com/document/product/647/51007#oncallreceived)를 참고하십시오.
- Android&iOS: 그룹 통화 중 간헐적으로 발생하는 콜백 오류를 수정했습니다.
- Android&iOS: 반복 로그인 또는 UserSig 만료로 인한 상태 비정상 문제를 수정했습니다.
- iOS: Objective-C와 Swift가 혼합된 언어 TUICallKit 프로젝트 빌드 시, 'init' 호출 시 오류가 발생하는 현상이 수정되었습니다.
- Android: Kotlin 프로젝트에 플로팅 창 기능 통합 시 오류가 발생하는 현상이 수정되었습니다.

### Version 1.0.0.53   @ 2022.08.15

#### 첫 번째 릴리스: 
- Android&iOS: 1v1 및 그룹 음성/영상 통화를 지원합니다.
- Android&iOS: 주요 장치에 대한 오프라인 통화 푸시를 지원합니다.
- Android&iOS: 사용자 정의 프로필 사진 및 대화명을 지원합니다.
- Android&iOS: 플로팅 통화 창을 지원합니다.
- Android&iOS: 사용자 지정 벨소리를 지원합니다.
- Android&iOS: 사용자가 여러 플랫폼에서 로그인한 상태에서의 전화 수신을 지원합니다.