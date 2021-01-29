본 문서에서는 Tencent Cloud TRTC Demo(Electron)를 빠르게 실행하는 방법을 소개합니다.

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 순서

<span id="step1" name="step1"> </span>

### 1단계: 신규 애플리케이션 생성

1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 보조] > [Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 명칭(예: `TestTRTC`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

<span id="step2" name="step2"> </span>

### 2단계: SDK와 Demo 소스 코드 다운로드

1. 커서를 상응하는 카드로 이동 후, [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)를 클릭하여 Github(또는 [ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Electron_latest.zip) 클릭)로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
    ![img](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 볼 수 있습니다.

<span id="step3" name="step3"> </span>

### 3단계: Demo 프로그래밍 파일 설정
1. [2단계[(#step2)에서 다운로드한 소스 패키지를 압축 해제하고, `TRTCSDK/Electron/TRTCSimpleDemo/` 디렉터리를 찾습니다. 해당 디렉터리가 **프로젝트 디렉터리**이고, 다음에서 언급하는 <span id="projectFolder" name="projectFolder">“프로젝트 디렉터리”</span>는 `TRTCSDK/Electron/TRTCSimpleDemo/` 디렉터리를 의미합니다.

2. 프로젝트 디렉터리에서 `debug/gen-test-user-sig.js` 파일을 찾아 열어줍니다.

3. `gen-test-user-sig.js` 파일의 관련 매개변수를 설정합니다.

    -   SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.
    -   SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.
    
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.

5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

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
| | |---log.js 로그 툴
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

<span id="step4"> </span>

### 4단계: 컴파일 실행

#### Windows 플랫폼

1. Node 최신 버전을 설치합니다. 64비트 `.msi` 파일을 권장합니다. [Node 다운로드 주소](https://nodejs.org/en/download/)

2. `win + r`을 눌러 cmd를 입력해 관리자 권한으로 명령 프롬프트를 실행하고 디렉터리를 [프로젝트 디렉터리](#projectFolder)로 지정한 후 다음 명령어를 실행합니다.
	
```shell
$ npm install
```
	
![설치](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)


3. npm 종속 패키지의 설치가 모두 완료된 후, 명령 프롬프트에 다음 명령어를 실행하여 Demo를 실행합니다.

```shell
$ npm run start  # 처음 실행 시 잠시 기다리면 창에 UI가 나타납니다.
```
    
![demo 실행](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

#### Mac OS 플랫폼

1. 터미널(Terminal) 또는 cmd 창을 열어 다음 명령어를 실행해 Homebrew를 설치합니다. Homebrew를 이미 설치한 경우 본 단계를 생략합니다.

```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. 다음 명령어를 실행하여 Node.js를 설치합니다.

```shell
$ brew install node
```

3. cd 명령어를 통해 프로젝트 디렉터리를 지정하고 다음 명령어를 실행합니다.

 ```shell
$ npm install 
 ```
    
    ![mac에 설치](https://main.qcloudimg.com/raw/3f8e92e9c59ff1bdb9fd0b2a0f34852a.png)
    
4. npm 종속 패키지의 설치가 모두 완료된 후, 명령 프롬프트에 다음 명령어를 실행하여 Demo를 실행합니다.

```shell
$ npm run start # 처음 실행 시 잠시 기다리면 창에 UI가 나타납니다.
```
    
![mac에서 프로젝트 실행](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
    
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

1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. 왼쪽 메뉴에서 [Application Management]를 선택한 후 대상 애플리케이션이 속한 행의 [Application Info]를 클릭합니다.
3. [Quick Start] 탭을 선택한 후 [Step 2: obtain the secret key to issue UserSig]의 [업데이트]를 클릭합니다.

### 2. 2대의 디바이스에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇입니까?

2대의 디바이스가 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 디바이스에서 동시에 사용할 수 없습니다.

### 3. 방화벽에 어떤 제한이 있습니까?

SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응]((https://intl.cloud.tencent.com/document/product/647/35164)을 참조하십시오.


