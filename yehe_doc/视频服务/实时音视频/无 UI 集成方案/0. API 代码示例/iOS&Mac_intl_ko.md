본문에서는 Tencent Cloud TRTC-API-Example(iOS&Mac)을 빠르게 실행하는 방법을 설명합니다.

## 환경 요건
- Xcode 11.0 이상 버전
- 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- Qt Creator 4.13.3(Mac) 또는 이후 버전.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있어야 합니다.

## 작업 단계

### 1단계: 애플리케이션 생성

1. TRTC 콘솔에 로그인하고 [[애플리케이션 관리](https://console.tencentcloud.com/trtc/app)]를 선택합니다.

2. [애플리케이션 생성]을 클릭하고 `APIExample`과 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 있는 경우, [기존 애플리케이션 선택]을 선택하고 [다음]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### 2단계: 다운로드 예시 코드

1. UI 없음을 선택하고 Github로 이동하여 플랫폼에 대한 샘플 코드를 다운로드합니다.
2. 다운로드가 완료되면 [다음]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### 3단계: 프로젝트 구성
1. 데모 프로젝트를 실행 중인 경우 [테스트]를 선택합니다. SDKAppID와 Secret key를 기록해 둡니다.
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 이전에 다운로드한 파일을 엽니다. 콘솔의 지시에 따라 SDKAppID와 Secret key를 수정하고 [다음]을 클릭합니다.

>?
>- 본문에서 설명하는 UserSig를 생성하는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 쉽게 디컴파일되고 역전될 수 있으며, 키가 공개되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 로컬 TRTC-API-Example의 로컬 실행 및 디버깅에만 적합합니다**.
>- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

### 4단계: 데모 컴파일 및 실행
Xcode(11.0 또는 이후 버전)를 사용하여 소스 코드 디렉터리에서 TRTC-API-Example-OC.xcworkspace 프로젝트를 열고, TRTC-API-Example 프로젝트를 컴파일 및 실행합니다.


## FAQ

### 1. 2대의 모바일에서 동시에 프로젝트를 실행하였는데 서로의 화면이 보이지 않는 이유는 무엇입니까?
2대의 모바일에서 프로젝트를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 단말에서 동시에 사용할 수 없습니다.

### 2. 방화벽에 어떤 제한이 있습니까?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 공용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [방화벽 제한 대응 관련 질문](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하여 진단 및 해결하십시오.
