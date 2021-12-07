## 효과
당사 App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 실시간 음성 및 영상 통화의 효과를 체험할 수 있습니다.
<table>
<tr>
   <th>발신자</th>
   <th>수신자</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>



>! 음성 및 영상 통화 기능을 빠르게 구현할 수 있도록 TUICalling 컴포넌트를 최적화하였습니다. 통화 UI는 TUICalling 컴포넌트 내부에 구현되어 있으므로 UI에 신경을 쓸 필요가 없습니다.

[](id:ui)

## App 실행 및 체험

[](id:ui.step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, **개발 지원>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. 애플리케이션 이름(예: `TestVideoCall`)을 입력한 후 **생성**을 클릭합니다.
3. **다운로드 완료, 다음 단계**를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!본 기능은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.


[](id:ui.step2)
### 2단계: App 소스 코드 다운로드
[TUICalling](https://github.com/tencentyun/TUICalling)에서 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:ui.step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2 `iOS/Example/Debug/GenerateTestUserSig.swift` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.swift` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)
### 4단계: App 실행

Xcode(11.0 및 이후 버전) 소스 코드 프로젝트 `TUICalling/Example/TUICallingApp.xcworkspace`를 열고 **실행**을 클릭하여 이 App에 대한 디버깅을 시작합니다.



## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 호출할 userId를 입력하고 검색을 클릭합니다.
3. **호출**을 클릭하고 **영상 통화**를 선택합니다. **수신자가 애플리케이션 로그인 상태가 아니면 호출에 실패할 수 있으니 확인하시기 바랍니다.**<br>

### 사용자 B
1. 사용자 이름을 입력하고 로그인합니다. **사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 메인 페이지로 이동하여 전화 수신을 기다립니다.



[](id:model)
## 연결 프로세스

[소스 코드](https://github.com/tencentyun/TUICalling/tree/master/Android/Source/src/main/java/com/tencent/liteav/trtccalling) 폴더 `Source`에는 세 개의 하위 폴더 ui, model 및 Service가 있으며, Service 폴더에는 Tencent Cloud가 외부에 공개한 오픈 소스 컴포넌트 TUICallingManager가 포함되어 있습니다.  `TUICallingManager.h`  파일에서 이 컴포넌트가 제공하는 인터페이스 함수를 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0de26d679e6e0dc1d9aeadb6dbf6f8aa.png)


오픈 소스 컴포넌트 TUICalling의 TUICallingManager를 사용하면, 복잡한 호출 UI 인터페이스 및 로직을 직접 구현하지 않고도 음성 및 영상 통화 기능을 쉽게 구현할 수 있습니다.

[](id:model.step1)
### 1단계: SDK 통합

통화 컴포넌트 TRTCCalling은 TRTC SDK와 IM SDK에 종속되어 있습니다. 아래 절차에 따라 두 가지 SDK를 프로젝트에 통합할 수 있습니다.

- **방법1: cocoapods 라이브러리를 통한 종속**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod ’TXLiteAVSDK_TRTC’ 
:::
</dx-codeblock>
>?두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK) 및 [IM](https://github.com/tencentyun/TIMSDK)의 Github 첫 페이지에서 획득할 수 있습니다.
- **방법2: 로컬을 통한 종속**
개발 환경에서 cocoapods 라이브러리 액세스가 느릴 경우, ZIP 패키지를 다운로드하고 통합 가이드 문서에 따라 수동으로 프로그램에 통합할 수 있습니다.
<table>
<tr>
<th>SDK</th>
<th>다운로드 페이지</th>
<th>통합 가이드</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드 문서</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">통합 가이드 문서</a></td>
</tr>
</table>

[](id:model.step2)
### 2단계: 권한 설정

info.plist 파일에 `Privacy - Camera Usage Description`, `Privacy - Microphone Usage Description`을 추가해 카메라 및 마이크 권한을 신청해야 합니다.

[](id:model.step3)
### 3단계: TUICalling 컴포넌트 가져오기
**cocoapods를 통해 컴포넌트 가져오기**. 구체적인 단계는 다음과 같습니다.
1. 프로젝트 디렉터리의 `Source`, `Resources`, `TXAppBasic` 폴더 및, `TUICalling.podspec` 파일을 각 프로그램 디렉터리로 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
<dx-codeblock>
::: swift
 pod 'TXAppBasic', :path => "../TXAppBasic/"
 pod ’TXLiteAVSDK_TRTC’
 pod 'TUICalling', :path => "../", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)

### 4단계: 컴포넌트 초기화 및 로그인

1. `TUICallingManager.sharedInstance()` 를 호출하여 컴포넌트를 초기화합니다.
2. `TUILogin.`init`(sdkAppID)`를 호출하여 로그인을 초기화합니다.
3. `TUILogin.login(userId, userSig)`을 호출해 컴포넌트에 로그인합니다. 주요 매개변수는 다음 테이블을 참고하십시오.
<table>
<tr><th>매개변수 이름</th><th>역할</th></tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 계산 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참고하십시오.</td>
</tr></table>

<dx-codeblock>
::: swift
	 // 컴포넌트 초기화
	 TUICallingManager.sharedInstance();
   // 로그인
	 TUILogin.`init`(sdkAppID)
   TUILogin.login(userId, userSig) {
       print("login success")
   } fail: { code, errorDes in
       print("login failed, code:\(code), error: \(errorDes ?? "nil")")
   }
:::
</dx-codeblock>

[](id:model.step5)

### 5단계: 음성 및 영상 통화 구현

1. 발신자: TUICallingManager의 `call();` 메소드를 호출하여 통화를 요청하고, 사용자 ID 배열(userids) 및 통화 유형(type)을 전송합니다. 통화 유형 매개변수 `.audio`(음성 통화) 또는 `.video`(영상 통화) 또한 전송합니다. 사용자 ID 배열(userids)에 userID가 하나만 있으면 1:1 통화이며, 사용자 ID 배열(userids)에 userID가 여러 개(>=2) 있으면 다중 사용자 통화입니다.
2. 수신자: 수신자가 로그인 상태인 경우 해당 인터페이스가 자동으로 실행됩니다. 오프라인 통화 요청 수신 구현 방법은 [오프라인 수신](#model.offline)을 참고하십시오.

<dx-codeblock>
::: swift
// 1. 리스너 등록
TUICallingManager.shareInstance().setCallingListener(listener: TUICallingListerner())

// 2. 페이지 사용자 정의 여부를 설정합니다(기본값: 비활성화).
TUICallingManager.shareInstance().enableCustomViewRoute(enable: true)

// 3. 리스너 콜백 메소드 구현
public func shouldShowOnCallView() -> Bool {
    return true;
}

public func callStart(userIDs: [String], type: TUICallingType, role: TUICallingRole, viewController: UIViewController?) {         if let vc = viewController {
        callingVC = vc;
        vc.modalPresentationStyle = .fullScreen
            
        if var topController = UIApplication.shared.keyWindow?.rootViewController {
            while let presentedViewController = topController.presentedViewController {
                topController = presentedViewController
            }
                
            if let navigationVC = topController as? UINavigationController {
                if navigationVC.viewControllers.contains(self) {
                    present(vc, animated: false, completion: nil)
                } else {
                    navigationVC.popToRootViewController(animated: false)
                    navigationVC.pushViewController(self, animated: false)
                    navigationVC.present(vc, animated: false, completion: nil)
                }
            } else {
                topController.present(vc, animated: false, completion: nil)
            }
        }
    }
}

public func callEnd(userIDs: [String], type: TUICallingType, role: TUICallingRole, totalTime: Float) {
    callingVC.dismiss(animated: true, completion: nil)
}
    
public func onCallEvent(event: TUICallingEvent, type: TUICallingType, role: TUICallingRole, message: String) {
       	
}
// 4. 통화 발신
TUICallingManager.shareInstance().call(userIDs, .video)
:::
</dx-codeblock>

[](id:model.offline)


### 6단계: 오프라인 통화 구현

>?온라인 고객서비스 등 오프라인 수신 기능이 필요 없는 시나리오인 경우, [1단계](#model.step1) - [5단계](#model.step5)만 진행합니다. 소셜 시나리오에서는 오프라인 수신을 권장합니다.

IM SDK는 오프라인 푸시를 지원합니다. 사용 가능 기준을 충족하려면 해당하는 설정을 완료해야 합니다.

1. Apple 푸시 인증서를 신청합니다. 자세한 방법은 [Apple 푸시 인증서 신청](https://intl.cloud.tencent.com/zh/document/product/1047/34346)을 참고하십시오.
2. 백그라운드 및 클라이언트에 오프라인 푸시를 설정합니다. 자세한 방법은 [오프라인 푸시(iOS)](https://intl.cloud.tencent.com/document/product/1047/39157)를 참고하십시오.
3. 현재 TRTCCallingImpl의 sendModel 신호 발송 함수 중 오프라인 발송 함수가 통합되어 있습니다. App의 오프라인 푸시를 설정하면 메시지 오프라인 푸시가 가능합니다.

[](id:api)

## 컴포넌트 API 리스트

TUICalling 컴포넌트의 API 리스트는 다음과 같습니다.

| 인터페이스 함수        | 인터페이스 기능                                                 |
| --------------- | --------------------------------------------------------- |
| call            | C2C 통화 초대         |
| receiveAPNSCalled          | 초대된 사용자 통화 수신                                      |
| setCallingListener          | 리스너 설정                                     |
| setCallingBell          | 벨소리 설정(30초 이내 권장)                                                 |
| enableMuteMode | 음소거 모드 활성화    |
| enableCustomViewRoute      | 사용자 정의 뷰 활성화. 활성화 후 발신/수신 시작 콜백 중 CallingView 인스턴스가 수신되며 개발자가 직접 표시 방법을 결정합니다. 주의: 전체 화면 또는 비례 화면으로 표시해야 합니다. 그렇지 않으면 이상 경고가 표시됩니다.            |

