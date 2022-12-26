본문은 Tencent Cloud TRTC Demo(Windows C++)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- Microsoft Visual Studio 2017 이상 버전, Microsoft Visual Studio 2019 사용 권장
- [QT](https://download.qt.io/archive/qt/5.14/5.14.2/) 개발 환경(QT 5.14.x 버전)을 다운로드하여 설치합니다.
- [.vsix](https://download.qt.io/official_releases/vsaddin/2.7.2/) 플러그 인 파일을 다운로드 및 설치합니다. 공식 홈페이지 파일명에 따라 해당 플러그 인 버전을 찾아 설치할 수 있습니다.
- VS를 열어 툴바에서 `QT VS Tools -> Qt Options -> Qt Versions`를 찾은 다음, 자체 Qt 컴파일러 msvc를 추가합니다.
- `SDK/CPlusPlus/Win64/lib`의 모든 `.dll` 파일을 프로그램 디렉터리에 있는 `debug`/`release` 폴더에 복사해야 합니다.
>! 'debug/release' 폴더는 VS의 환경이 구성된 후 자동으로 생성됩니다. 32비트 프로그램인 경우 `SDK/CPlusPlus/Win64/lib` 아래의 `.dll`을 모두 `debug` / `release` 폴더에 복사해야 합니다.


## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있어야 합니다.

## 작업 단계

### 1단계: 애플리케이션 생성

1. TRTC 콘솔에 로그인하고 왼쪽 사이드바에서 [[애플리케이션 관리](https://console.tencentcloud.com/trtc/app)]를 선택합니다.

2. [애플리케이션 생성]을 클릭하고 `APIExample`과 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 있는 경우 [기존 애플리케이션 선택]을 선택하고 [다음]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### 2단계: 샘플 코드 다운로드

1. UI 없음을 선택하고 Github로 이동하여 플랫폼에 대한 샘플 코드를 다운로드합니다.
2. [다음]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### 3단계: 프로젝트 구성
1. 데모 프로젝트를 실행 중인 경우 [테스트]를 선택합니다. SDKAppID와 Secret key를 기록해 둡니다.
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 이전에 다운로드한 파일을 엽니다. 콘솔의 지시에 따라 SDKAppID와 Secret key를 수정하고 [다음]을 클릭합니다.

>?
>- 이 문서에서 설명하는 UserSig를 생성하는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 쉽게 디컴파일되고 역전될 수 있으며, 키가 공개되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 TRTC-API-Example의 로컬 실행 및 디버깅에만 적합합니다**.
>- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

### 4단계: 데모 컴파일 및 실행
Microsoft Visual Studio(Microsoft Visual Studio 2019 권장)로 TRTC-API-Example-Qt 디렉터리의 `QTDemo.sln`을 열고 QT 환경을 설정(QT 5.14 권장)하고 프로젝트를 [실행]합니다.


## FAQ

### 1. Demo가 두 대의 기기에서 실행되고 있는데 왜 서로의 이미지를 표시할 수 없습니까?
두 기기가 서로 다른 UserID를 사용하는지 확인하십시오. TRTC를 사용하면 SDKAppID가 다른 경우를 제외하고 동일한 UserID를 두 장치에서 동시에 사용할 수 없습니다.


### 2. 방화벽에 어떤 제한이 있습니까?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [방화벽 제한](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.
