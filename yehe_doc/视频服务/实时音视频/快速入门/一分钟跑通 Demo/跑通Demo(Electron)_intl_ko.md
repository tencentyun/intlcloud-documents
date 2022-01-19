본 문서에서는 Tencent Cloud TRTC Demo(Electron)를 빠르게 실행하는 방법을 소개합니다.

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계

[](id:step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔 로그인 후, **개발 지원**>**[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. **애플리케이션 생성**을 클릭하고 `TestTRTC`와 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 생성된 경우 **기존 애플리케이션 선택**을 클릭합니다.
3. 실제 비즈니스 요구에 따라 태그를 추가하거나 편집하고 **생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)

>?
>- 애플리케이션 이름은 숫자, 중국어, 영어, 언더바만 포함할 수 있으며 15자를 초과할 수 없습니다.
>- 태그는 Tencent Cloud에서 다양한 리소스를 식별하고 구성하는 데 사용됩니다. 예를 들어, 기업이 여러 사업부를 가지고 있고, 각 부서에는 하나 이상의 TRTC 애플리케이션이 있을 수 있는데, 이 경우 기업은 TRTC 애플리케이션에 태그를 추가하여 부서 정보를 표시할 수 있습니다. 태그는 필수 사항이 아니며, 실제 비즈니스 니즈에 따라 추가하거나 편집할 수 있습니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 수요에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 **다운로드 완료, 다음 단계**를 클릭합니다.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Electron/js/GenerateTestUserSig.js` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
<ul>
 <li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
 <li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
 <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

**파일 디렉터리 설명:**
```bash
.
|---README.md                             README 파일, 자세히 읽어 주십시오.
|---main.electron.js                      Electron 메인 파일
|---public                                정적 파일 저장
|---babel.config.js
|---package.json
|---vue.config.js                         vue-cli 프로그래밍 파일
|---src                                   소스 코드 디렉터리
| |---app.vue
| |---common.css
| |---main.js
| |---components                          UI 구성 요소 디렉터리
| | |---main-menu.vue
| | |---nav-bar.vue
| | |---show-screen-capture.vue
| |---common                              툴 함수, 공용 라이브러리
| | |---live-room-service.js
| | |---log.js                            로그 툴
| | |---mtah5.js                          
| | |---routes.js
| | |---rand.js
| |---pages                               페이지 디렉터리
| | |---index.vue                         메인 페이지
| | |---trtc                              화상 회의 관련 페이지
| | | |---trtc-room.vue                   화상 회의룸 페이지
| | | |---trtc-index.vue                  화상 회의 게이트 페이지
| | |---404.vue
| | |---live                              라이브 방송 페이지
| | | |---live-index.vue                  라이브 방송 게이트 페이지
| | | |---live-room-audience.vue          관중석 페이지
| | | |---live-room-anchor.vue            호스트 룸 페이지
| |---debug                               주의! 배포 시, 해당 폴더 내 서명 로직을 서버로 이동해 주십시오.
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

[](id:step4)

### 4단계: 컴파일 실행
<dx-tabs>
::: Windows 플랫폼
1.  Node 최신 버전을 설치합니다. 64비트 `.msi` 파일을 권장합니다. [Node 다운로드 주소](https://nodejs.org/en/download/).
2.  `win + r`을 눌러 cmd를 입력해 관리자 권한으로 명령 프롬프트를 실행하고 디렉터리를 [프로젝트 디렉터리](#projectFolder)로 지정한 후 다음 명령어를 실행합니다.
```shell
$ npm install
```![설치](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)

4.  npm 종속 패키지의 설치가 모두 완료된 후, 명령 프롬프트에 다음 명령어를 실행하여 Demo를 실행합니다.
​```shell
$ npm run start  # 처음 실행 시 잠시 기다리면 창에 UI가 나타납니다.
​```![demo 실행](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

:::
::: MacOS 플랫폼
1.  터미널(Terminal) 또는 cmd 창을 열어 다음 명령어를 실행해 Homebrew를 설치합니다. Homebrew를 이미 설치한 경우 본 단계를 생략합니다.
​```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2.  다음 명령어를 실행하여 Node.js를 설치합니다.
```shell
$ brew install node
```

3.  Homebrew의 기본 주소를 사용한 Node.js 설치 속도가 느린 경우, 중국 내 이미지 주소로의 전환을 고려해볼 수 있습니다.
 ```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
 ```

4.  cd 명령어를 통해 프로젝트 디렉터리를 지정하고 다음 명령어를 실행합니다.
```shell
$ npm install 
​```![](https://main.qcloudimg.com/raw/8bcc95adad07ff37e7f0a27893b8b7cf.png)

5.  npm 종속 패키지의 설치가 모두 완료된 후, 명령 프롬프트에 다음 명령어를 실행하여 Demo를 실행합니다.
​```shell
$ npm run start # 처음 실행 시 잠시 기다리면 창에 UI가 나타납니다.
​```![mac에서 프로젝트 실행](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
:::
</dx-tabs>
    
### 프로젝트 주요 명령어

| 명령어 | 설명 |
|--|--|
| npm run start | 개발 환경으로 Demo 실행 |
| npm run pack:mac | Mac용 .dmg 설치 파일 패키징 |
| npm run pack:win64 | Windows 64비트용 .exe 설치 파일 패키징 |

## FAQ

### 1. 키 조회 시 공개키와 프라이빗 키 정보만 획득할 수 있습니다. 키는 어떻게 획득합니까?

TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트를 진행하지 않을 경우 [기존 버전 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있습니다.

**업데이트 작업:**
1.  [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2.  왼쪽 사이드바에서 **애플리케이션 관리**를 선택한 후 대상 애플리케이션이 속한 행의 **애플리케이션 정보**를 클릭합니다.
3.  **퀵 스타트** 탭을 선택하고 **2단계: UserSig 발급 키 획득** 섹션에서 **업데이트**를 클릭합니다.

### 2. 2대의 디바이스에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇입니까?

2대의 디바이스가 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 디바이스에서 동시에 사용할 수 없습니다.

![](https://main.qcloudimg.com/raw/9a03335e435de0f12e2a26882f53db02.png)

### 3. 방화벽에 어떤 제한이 있습니까?

SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.

>? 더 많은 FAQ는 [Electron 관련 FAQ](https://intl.cloud.tencent.com/document/product/647/43093)를 참고하십시오.

## 기술 컨설팅
더 자세한 내용은 [고객센터](https://intl.cloud.tencent.com/contact-us)를 통해 문의하시기 바랍니다.


## 참고 문서

- [SDK API 매뉴얼](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK 업데이트 로그](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demo 소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCSimpleDemo)
- [API Example 소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example)
- [Electron FAQ](https://intl.cloud.tencent.com/document/product/647/43093)

```