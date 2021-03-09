본 문서에서는 Tencent Cloud TRTC Demo(Windows)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
### Windows(C++) 개발 환경
- Microsoft Visual Studio 2015 이상 버전, Microsoft Visual Studio 2015 사용 권장 
- Windows SDK 8.0 이상 버전, Windows SDK 8.1 사용 권장

### Windows(C#) 개발 환경
- Microsoft Visual Studio 2015 이상 버전, Microsoft Visual Studio 2017 사용 권장
- .Net Framework 4.0 이상 버전, .Net Framework 4.0 사용 권장

### Windows(QT) 개발 환경
- Microsoft Visual Studio 2015 이상 버전, Microsoft Visual Studio 2015 사용 권장
- [.vsix](https://download.qt.io/official_releases/vsaddin/) 플러그 인 파일을 다운로드 및 설치합니다. 홈페이지에서 해당 플러그 인 버전을 찾아 설치하면 됩니다.
- VS를 열고 툴 란에서 `QT VS Tools -> Qt Options -> Qt Versions`를 찾아 Qt 인코더 msvc를 추가합니다.
- `SDK/CPlusPlus/Win32/lib`의 모든 `.dll` 파일을 프로그램 디렉터리에 있는 `debug`/`release` 폴더에 복사해야 합니다.
>! `debug/release` 폴더는 모두 VS에서 환경 설정 완료 후 자동으로 생성됩니다.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 내 TRTC 서비스를 구매할 수 없습니다.

## 작업 순서
<span id="step1"></span>
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)를 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 명칭(예: `TestTRTC`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

<span id="step2"></span>
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 커서를 상응하는 카드로 이동한 후, [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Windows)를 클릭하여 Github(또는 [ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip?_ga=1.195966252.185644906.1567570704) 클릭)로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
 ![](https://main.qcloudimg.com/raw/73b9bfa89b42acbc166074a29f20be47.png)
2. 다운로드 완료 후, TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 조회할 수 있습니다.

<span id="step3"></span>
### 3단계: Demo 프로그램 파일 설정
1. [2단계](#step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `GenerateTestUserSig` 파일을 찾아 엽니다.
 <table>
     <tr>
         <th nowrap="nowrap">적용 플랫폼</th>  
         <th nowrap="nowrap">파일의 상대 경로</th>  
     </tr>
   <tr>      
         <td>Windows(C++)</td>   
       <td>Windows/DuilibDemo/GenerateTestUserSig.h</td>   
     </tr> 
   <tr>
       <td>Windows(C#)</td>   
       <td>Windows/CSharpDemo/GenerateTestUserSig.cs</td>
     </tr> 
 </table>
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
  <img src="https://main.qcloudimg.com/raw/6a95980aa101276c8bf8340cf0a5d99f/%E8%B7%91%E9%80%9ADemo(Windows)0-%E8%BF%94%E8%BF%98.png">
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서의 SECRETKEY는 디컴파일로 크래킹되기 쉬워, 일단 키가 유출되면 해커가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>정확한 UserSig 발급 방식은 UserSig 계산 코드를 귀하의 서버에 통합하여 App 지향의 인터페이스를 제공하는 것입니다. UserSig가 필요한 경우 귀하의 App이 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

<span id="step4"></span>
### 4단계: 컴파일 실행
- **Windows(C++):**
Visual Studio(VS2015 권장)를 사용해 소스 디렉터리의 `DuilibDemo\TRTCDuilibDemo.sln` 프로그램 파일을 엽니다. Release/X86 구축 플랫폼을 선택하여 Demo 프로그램을 컴파일링 및 실행하시길 권장합니다.
- **Windows(C#):**
Visual Studio(VS2017 권장)를 사용해 소스 디렉터리의 `CSharpDemo\TRTCCSharpDemo.sln` 프로그램 파일을 엽니다. Release/X86 구축 플랫폼을 선택하여 Demo 프로그램을 컴파일링 및 실행하시길 권장합니다.
- **Windows(QT):** 
Visual Studio(VS2015 이상 권장)를 사용하여 소스 코드 디렉터리의
QTDemo\QTDemo.pro 프로그램 파일을 열고 QTDemo 프로그램을 컴파일링 및 실행합니다.

## FAQ

### 1. 키 조회 시 공개키와 개인키 정보만 획득할 수 있습니다. 키는 어떻게 획득하나요?
TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트를 진행하지 않을 경우 [기존 버전 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있으며, 이미 업데이트한 경우 필요에 따라 기존/신규 알고리즘을 전환할 수 있습니다.

업데이트/전환 작업:
 1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
 2. 왼쪽 메뉴에서 [애플리케이션 관리]를 선택한 후 타깃 애플리케이션 라인에서 [애플리케이션 정보]를 클릭합니다.
 3. [퀵 스타트] 탭을 선택한 후 [2단계: UserSig 발급 키 획득]의 [업데이트], [비대칭 암호화] 또는 [HMAC-SHA256]을 클릭합니다.
  - 업데이트:
  - 기존 버전 알고리즘 ECDSA-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/96a974bcc25d0fab17db839be12fdb5e/%E8%B7%91%E9%80%9ADemo(Windows)2-%E8%BF%94%E8%BF%98.png)
  - 신규 버전 알고리즘 HMAC-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/c3d53c405bb074ef4758cb12aa01e024/%E8%B7%91%E9%80%9ADemo(Windows)3-%E8%BF%94%E8%BF%98.png)

### 2. 2대의 디바이스에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇인가요?
2대의 디바이스가 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 디바이스에서 동시에 사용할 수 없습니다.

### 3. 방화벽에 어떤 제한이 있나요?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 공용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참조하십시오.
