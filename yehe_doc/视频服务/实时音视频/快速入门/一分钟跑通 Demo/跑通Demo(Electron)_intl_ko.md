본 문서에서는 Tencent Cloud TRTC Demo(Electron)를 빠르게 실행하는 방법을 소개합니다.

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 내 TRTC 서비스를 구매할 수 없습니다.

## 작업 순서

[](id:step1)

### 1단계: 신규 애플리케이션 생성

1. TRTC 콘솔에 로그인한 후 [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예: TestTRTC)을 입력한 후 [생성]을 클릭합니다.

[](id:step2)

### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 수요에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:step3)
### 3단계: Demo 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `TRTCSDK/Electron/TRTCSimpleDemo/` 디렉터리를 찾습니다. 해당 디렉터리는 **프로젝트 디렉터리**로, 본 문서에서 지칭하는 <span id="projectFolder"></span>'프로젝트 디렉터리'란 `TRTCSDK/Electron/TRTCSimpleDemo/` 디렉터리를 의미합니다.
2. 프로젝트 디렉터리에서 `debug/gen-test-user-sig.js` 파일을 찾아 엽니다.
3. `gen-test-user-sig.js` 파일의 관련 매개변수를 설정합니다.
<ul>
 <li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
 <li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

**파일 디렉터리 설명:**
```bash
.
|---README.md                             README 파일, 자세히 읽어 주십시오.
|---main.electron.js                      Electron 메인 파일
|---public                                정적 파일 저장
|---babel.config.js
|---package.json
|---vue.config.js                         vue-cli 프로그램 파일
|---src                                   소스 코드 디렉터리
| |---app.vue
| |---common.css
| |---main.js
| |---components                          UI 모듈 디렉터리
| | |---main-menu.vue
| | |---nav-bar.vue
| | |---show-screen-capture.vue
| |---common                              툴 함수, 공용 라이브러리 등
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
| | | |---live-room-audience.vue          시청자 페이지
| | | |---live-room-anchor.vue            호스트 룸 페이지
| |---debug                               주의 사항: 배포 시 해당 폴더 내 서명 로직을 서버로 이동해 주십시오.
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

[](id:step4)

### 4단계: 컴파일 실행
#### Windows 플랫폼
1. Node 최신 버전을 설치합니다. 64bit `.msi` 파일을 권장합니다. [Node 다운로드 주소](https://nodejs.org/en/download/)
2. `win + r`을 눌러 cmd를 입력하고 관리자 권한으로 명령 프롬프트를 실행한 다음, 디렉터리를 [프로젝트 디렉터리](#projectFolder)로 지정한 후 다음 명령어를 실행합니다.
```shell
$ npm install
```
![설치](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)
3. npm 종속 패키지 설치가 모두 완료된 후 명령 프롬프트에서 다음 명령어로 Demo를 실행합니다.
```shell
$ npm run start  # 처음 실행 시 잠시 기다리면 창에 UI가 나타납니다.
```
![demo 실행](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)



#### MacOS 플랫폼
1. 터미널(Terminal) 또는 cmd 창을 열고 다음 명령어를 실행해 Homebrew를 설치합니다. Homebrew를 이미 설치한 경우 본 단계를 생략합니다.
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. 다음 명령어를 실행하여 Node.js를 설치합니다.
```shell
$ brew install node
```
3. Homebrew의 기본 주소를 사용한 Node.js 설치 속도가 느린 경우, 중국 내 이미지 주소로의 전환을 고려해볼 수 있습니다.
 ```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
 ```
4. cd 명령어를 통해 프로젝트 디렉터리를 지정하고 다음 명령어를 실행합니다.
```shell
$ npm install 
```

5. npm 종속 패키지 설치가 모두 완료된 후 명령 프롬프트에서 다음 명령어로 Demo를 실행합니다.
```shell
$ npm run start # 처음 실행 시 잠시 기다리면 창에 UI가 나타납니다.
```

### 프로젝트 주요 명령어

| 명령어 | 설명 |
|--|--|
| npm run start | 개발 환경으로 Demo 실행 |
| npm run pack:mac | Mac용 .dmg 설치 파일 패키징 |
| npm run pack:win64 | Windows 64비트용 .exe 설치 파일 패키징 |

## FAQ

### 1. 키 조회 시 공개키와 개인키 정보만 획득할 수 있습니다. 키는 어떻게 획득하나요?

TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트를 진행하지 않을 경우 [기존 버전 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있습니다.

**업데이트 작업:**
1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. 왼쪽 메뉴에서 [애플리케이션 관리]를 선택한 후 타깃 애플리케이션이 속한 행의 [애플리케이션 정보]를 클릭합니다.
3. [퀵 스타트] 탭을 선택한 후 [2단계: UserSig 발급 키 획득]의 [업데이트]를 클릭합니다.

### 2. 2대의 디바이스에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇인가요?

2대의 디바이스가 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 디바이스에서 동시에 사용할 수 없습니다.

### 3. 방화벽에 어떤 제한이 있나요?

SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참조하십시오.
