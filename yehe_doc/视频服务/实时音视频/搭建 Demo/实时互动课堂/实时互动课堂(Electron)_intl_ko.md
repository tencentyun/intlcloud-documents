## Demo 체험
<input type="button" value="Windows 버전" style="height: 30px;width: 150px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;margin-right:10px;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-windows-latest.zip')" />

<input type="button" value="MacOS 버전" style="height: 30px;width: 150px;margin-top: 5px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-mac-latest.zip')" />

## 효과
App 설치 패키지를 다운로드 및 설치하여 실시간 인터랙션 수업의 기능 및 효과를 경험해 볼 수 있습니다. 기본적인 음성 및 영상 통화, 화면 공유, 화이트보드, 문자 채팅 등 기본 기능 뿐만 아니라, 전체 음소거, 손 들기, 발언 요청, 출석 체크 등의 고급 기능을 구현합니다.


## 실시간 인터랙션 수업 소스 코드 실행
[](id:step1)
### 1단계: 애플리케이션 생성 및 SDKAppID와 키 획득
이전에 Tencent Cloud TRTC 애플리케이션을 생성한 적이 있는 경우 이 단계를 건너뛰고 이전에 생성된 애플리케이션의 SDKAppID 및 키를 사용할 수 있습니다.

1. TRTC 콘솔에 로그인하고 **개발 지원** > **[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택한 후, **애플리케이션 생성** 탭에서 'TestTRTC'와 같은 애플리케이션 이름을 입력하고, **생성** 버튼을 클릭합니다.  
![](https://qcloudimg.tencent-cloud.cn/raw/dfb1acca0137cd30d5168c3d9d72aa13.png)
2. **소스 코드 다운로드** 탭을 건너뛰고 **다음 단계** 버튼을 클릭하여 **설정 수정** 탭으로 이동한 후 페이지에 표시되는 SDKAppID와 키를 기록합니다. 다음 단계에서 사용하게 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ca5da75be8285ead342e06971229680e.png)

[](id:step2)
### 2단계: IM 설정
>? 실시간 인터랙션 수업은 기본 PaaS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

1. **관련 클라우드 서비스** 메뉴로 이동한 후, 아래 이미지의 **IM 애플리케이션**을 클릭하면 IM 애플리케이션 관리 페이지로 리디렉션됩니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/14e4c3b097ecadb046330975dbec6bd0.png)

2. 아래 이미지와 같이 방금 생성한 애플리케이션을 찾아 클릭하여 애플리케이션 관리 페이지로 이동합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/50aa612285befcfa14562923622cad6d.png)

3. 아래 이미지와 같이 **기능 설정** > **로그인 및 메시지** 메뉴를 열고 **로그인 설정** 섹션의 **편집** 링크를 클릭하여 **Web 동시 로그인 개수**를 2 이상으로 설정합니다(현재 이 애플리케이션은 최대 2개의 Web IM 인스턴스 동시 로그인이 필요합니다. 향후 추가 사용을 위해 더 높게 설정할 수 있습니다).

   ![](https://qcloudimg.tencent-cloud.cn/raw/2385858860a8f12091eab619b313eaec.png)


[](id:step3)
### 3단계: 실행 환경 준비
이 코드 프로젝트의 실행은 node.js와 yarn에 종속됩니다.

1. **node.js 설치:**
[node.js](https://nodejs.org/en/download/) 버전 14.16.0 이상 사용을 권장하며, 설치 완료 후 명령 라인 터미널에서 다음 명령어를 실행하여 node.js 버전을 확인합니다.
```
node --version
```
2. **yarn 설치:**
 - node.js 버전이 16.10 미만인 경우 명령 라인 터미널에서 다음 명령어를 실행하여 [yarn](https://yarnpkg.com/getting-started/install)을 설치합니다.
```
npm i -g corepack
```
 - node.js 버전이 16.10 이상인 경우 명령 라인 터미널에서 다음 명령어를 실행하여 yarn을 설치합니다.
```
corepack enable
```
>!Window 10, 11에서 권한이 부족하다는 오류 메시지가 나오면 관리자 신분으로 cmd에서  실행해 보시기 바랍니다.



[](id:step4)
### 4단계: 코드 프로젝트 클론

[코드 다운로드](https://github.com/TencentCloud/trtc-education-electron) 및 압축 해제 후 코드 디렉터리 `trtc-education-electron`에 들어가거나 [git](https://git-scm.com/downloads) 툴을 사용하여 코드 프로젝트를 복제합니다. git 툴을 사용하여 코드 프로젝트를 복제하려면 명령 라인 터미널에서 다음 명령을 실행하십시오.

```
git clone https://github.com/TencentCloud/trtc-education-electron.git

cd trtc-education-electron
```

[](id:step5)
### 5단계: SDKAppID와 키 설정
1. `src/main/config/generateUserSig.js` 파일을 찾아 엽니다.
2. `generateUserSig.js` 파일에서 관련 매개변수를 설정하여 실명 인증을 위한 사용자 서명 UserSig를 생성합니다.
   - SDKAPPID: 기본값은 0이며, [1단계](#step1) 애플리케이션 생성의 키로 설정하십시오.
   - SECRETKEY: 기본값은 빈 문자열이며, [1단계](#step1) 애플리케이션 생성의 키로 설정하십시오.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:step6)
### 6단계: 개발 모드 실행
명령 라인 터미널에서 코드 디렉터리 `trtc-education-electron`으로 이동하여 다음 명령을 실행합니다.
```
yarn

yarn start
```
>!
>- 처음으로 yarn 명령어를 실행하여 종속을 설치할 때 Window10, Window11에서 권한이 부족하다는 오류 메시지가 나오면 cmd에서 관리자 신분으로 한 번 실행해 보시기 바랍니다. 그 후 cmd 또는 Visual Studio Code, WebStorm 등과 같은 통합 개발 툴의 터미널에서 일반 사용자로 실행할 수 있습니다.
>- 종속성 설치 중 Electron 다운로드 속도 저하 또는 랙 발생 등의 문제가 발생하면 [문의하기](https://intl.cloud.tencent.com/contact-us)를 참고하여 해결할 수 있습니다.

[](id:step7)
### 7단계: 설치 패키지 구축, 실행
명령 라인 터미널에서 코드 디렉터리 `trtc-education-electron`으로 이동하고 다음 명령을 실행하여 설치 패키지를 구축합니다. 구축된 설치 패키지는 `trtc-education-electron/build/release` 디렉터리에 있으며 설치 및 실행할 수 있습니다.

```
yarn package
```

>!Mac 설치 패키지는 Mac 컴퓨터로, Windows 설치 패키지는 Windows 컴퓨터로만 구축할 수 있습니다.


## 기술 컨설팅
자세한 내용은 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하거나 colleenyu@tencent.com으로 이메일을 보내주십시오.

## 참고 문서

- [SDK API 매뉴얼](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK 업데이트 로그](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demo 소스 코드](https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTCSimpleDemo)
- [API Example 소스 코드](https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example)
- [Electron FAQ](https://intl.cloud.tencent.com/document/product/647/43093)
