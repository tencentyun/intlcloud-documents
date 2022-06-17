본문에서는 Tencent Cloud TRTC Demo(Windows C++/QT)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- Microsoft Visual Studio 2017 이상 버전, Microsoft Visual Studio 2019 사용 권장
- [QT](https://download.qt.io/archive/qt/5.14/5.14.2/) 개발 환경(QT 5.14.x 버전)을 다운로드하여 설치합니다.
- [.vsix](https://download.qt.io/official_releases/vsaddin/2.7.2/) 플러그 인 파일을 다운로드 및 설치합니다. 공식 홈페이지 파일명에 따라 해당 플러그 인 버전을 찾아 설치할 수 있습니다.
- VS를 열어 툴바에서 `QT VS Tools -> Qt Options -> Qt Versions`를 찾은 다음, 자체 Qt 컴파일러 msvc를 추가합니다.
- `SDK/CPlusPlus/Win64/lib`의 모든 `.dll` 파일을 프로그램 디렉터리에 있는 `debug`/`release` 폴더에 복사해야 합니다.
>! 'debug/release' 폴더는 VS의 환경이 구성된 후 자동으로 생성됩니다. 32비트 프로그램인 경우 `SDK/CPlusPlus/Win64/lib` 아래의 `.dll`을 모두 `debug` / `release` 폴더에 복사해야 합니다.


## 전제 조건
[Tencent Cloud 계정 가입](https://intl.cloud.tencent.com/document/product/378/17985)이 완료된 상태여야 합니다. 

## 작업 단계
[](id:step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, **개발 지원** > [**Demo 빠른 실행**](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. **애플리케이션 생성**을 클릭하고 `TestTRTC`와 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 생성된 경우 **기존 애플리케이션 선택**을 클릭합니다.
3. 실제 비즈니스 요구에 따라 태그를 추가하거나 편집하고 **생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)
>?
>- 애플리케이션 이름은 숫자, 중국어, 영어, 언더바만 포함할 수 있으며 15자를 초과할 수 없습니다.
>- 태그는 Tencent Cloud에서 다양한 리소스를 식별하고 구성하는 데 사용됩니다. 예를 들어, 기업이 여러 사업부를 가지고 있고, 각 부서에는 하나 이상의 TRTC 애플리케이션이 있을 수 있는데, 이 경우 기업은 TRTC 애플리케이션에 태그를 추가하여 부서 정보를 표시할 수 있습니다. 태그는 필수 사항이 아니며, 실제 비즈니스 니즈에 따라 추가하거나 편집할 수 있습니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 **다운로드 완료, 다음 단계**를 클릭합니다.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. 다음과 같이 SDKAppID 및 키 정보를 정의하는 파일을 찾아 엽니다.
 <table>
     <tr>
         <th nowrap="nowrap">적용 플랫폼</th>  
         <th nowrap="nowrap">파일의 상대 경로</th>  
     </tr>
     <tr>      
         <td>Windows(C++/QT)</td>   
         <td>Windows/QTDemo/src/Util/defs.h</td>   
     </tr>
 </table>
3. `defs.h` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAppID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul>
  <img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png">
4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:step4)
### 4단계: 컴파일 실행
- **방법1:** QtCreator를 사용하여 소스 디렉터리에서 `QTDemo\QTDemo.pro` 프로젝트 파일을 열고 QTDemo 프로젝트를 컴파일 및 실행합니다.
- **방법2:** QT 개발 플러그 인이 설치된 상태로 Visual Studio를 시작하고(VS2015 이상 권장) 메뉴에서 `Qt VS Tools > Open Qt Project File(.pro)...`를 선택하여 소스 코드 디렉터리에서 `QTDemo\QTDemo.pro` 프로젝트 파일을 열고 QTDemo 프로젝트를 컴파일 및 실행합니다.

## FAQ

### 1. 키 조회 시 공개키와 프라이빗 키 정보만 획득할 수 있습니다. 키는 어떻게 획득합니까?
TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트를 진행하지 않을 경우 [이전 버전 서명 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있으며, 이미 업데이트한 경우 필요에 따라 기존/신규 알고리즘을 전환할 수 있습니다.

업데이트/전환 작업:
 1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
 2. 왼쪽 사이드바에서 **애플리케이션 관리**를 선택한 후 대상 애플리케이션이 속한 행의 **애플리케이션 정보**를 클릭합니다.
 3. **퀵 스타트** 탭을 선택하고 **2단계: UserSig 발급 키 획득**에서 **업데이트**, **비대칭 암호화** 또는 **HMAC-SHA256**을 클릭합니다.
  - 업데이트
  - 기존 버전 알고리즘 ECDSA-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - 신규 버전 알고리즘 HMAC-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. 2대의 디바이스에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇입니까?
2대의 디바이스가 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 디바이스에서 동시에 사용할 수 없습니다.

### 3. 방화벽에 어떤 제한이 있습니까?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.
