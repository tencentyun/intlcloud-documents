본 문서에서는 Tencent Cloud TRTC Electron SDK를 귀하의 프로젝트에 빠르게 통합하는 방법을 소개합니다.

## 지원 플랫폼
-  Windows(PC)
-  Mac

## TRTC Electron SDK 통합

#### 1단계: Node.js 설치
**Windows 설치 가이드**
1. Windows 운영 체제에 따라 최신 버전 [Node.js](https://nodejs.org/en/download) 설치 패키지 `Windows Installer (.msi) 64-bit`를 다운로드합니다.
2. 응용 프로그램 목록의 Node.js command prompt를 열어 명령 프롬프트를 실행한 후, 이후 단계의 각 명령어를 입력하는 데 사용합니다.
![](https://main.qcloudimg.com/raw/a29b4681c1ed6ce57d66b5a79bda5e94.png)

**Mac OS 설치 가이드**
1. 터미널(Terminal) 창을 열어 다음 명령어를 실행해 Homebrew를 설치합니다. Homebrew를 이미 설치한 경우 본 단계를 생략합니다.
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2. 다음 명령어를 실행하여 Node.js를 설치합니다. (10.0 이상의 버전 필수)
```shell
$ brew install node
```
3. Homebrew 기본 주소를 사용한 Node.js 설치가 조금 늦을 경우 국내 이미지 주소로 교환하는 것을 권장합니다.
```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
```

#### 2단계: Electron 설치
명령 프롬프트에 다음 명령어를 실행하여 Electron을 설치합니다. (4.0.0 버전 권장)
```shell
$ npm install electron@latest --save-dev
```

#### 3단계: Electron 버전의 TRTC SDK 설치
1. Electron 프로젝트에 npm 명령어를 사용하여 SDK 패키지를 설치합니다.
```shell
$ npm install trtc-electron-sdk@latest --save
```

>?TRTC Electron SDK 최신 버전은 [trtc-electron-sdk](https://www.npmjs.com/package/trtc-electron-sdk)에서 다운로드할 수 있습니다.
2. 프로젝트 스크립트에 모듈을 불러와 사용합니다.
```javascript
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
// SDK 버전 획득
this.rtcCloud.getSDKVersion();
```
	v7.0.149부터 TRTC Electron SDK에 trtc.d.ts 파일이 추가되었으며, TypeScript 개발자에게 편리합니다.
```
// ES Module 결합 모드(esModuleInterop=true) 활성화
import * as trtc_namespace from 'trtc-electron-sdk';
const TRTCCloud = require('trtc-electron-sdk');
const rtcCloud: trtc_namespace.TRTCCloud = new TRTCCloud();
// SDK 버전 획득
rtcCloud.getSDKVersion();
```

## 실행 가능한 프로그램 패키징

#### 1단계: 패키징 툴 설치
1. 패키징 툴 `electron-builder`(권장)를 사용하여 패키징합니다. 다음 명령어를 실행하여 `electron-builder`를 설치할 수 있습니다
```bash
$ npm install electron-builder@latest --save-dev
```
2. Electron 버전의 TRTC SDK(즉, `trtc_electron_sdk.node` 파일)를 정확하게 패키징하기 위해 다음 명령어를 실행하여 `native-ext-loader` 툴을 설치해야 합니다.
```bash
$ npm install native-ext-loader@latest --save-dev
```

####  2단계: webpack.config.js 설정 수정
`webpack.config.js`에는 프로젝트 구축 설정 정보가 포함되어 있으며, `webpack.config.js` 파일은 다음 위치에 있습니다.
- 일반적으로 `webpack.config.js`는 프로젝트 기본 디렉터리에 있습니다.
- `create-react-app`을 사용하여 프로젝트를 생성한 경우, 구성 파일은 `node_modules/react-scripts/config/webpack.config.js`에 있습니다.
- `vue-cli`를 사용하여 프로젝트를 생성한 경우 `vue.config.js` 설정의 `configureWebpack` 속성에 webpack 설정이 있습니다.
- 프로젝트 파일을 사용자 정의한 경우 webpack 설정을 자체적으로 찾아야 합니다.


1. `module.exports` 전, 먼저 코드 구축 과정에서 각각의 타깃 플랫폼 특징에 따라 정확하게 패키징할 수 있도록 `webpack.config.js`가 구축 시 `--target_platform`의 명령 라인 매개변수를 수신하기 위해 다음 코드를 추가합니다.
```js
const os = require('os');
const targetPlatform = (function(){
		let target = os.platform();
		for (let i=0; i<process.argv.length; i++) {
			if (process.argv[i].includes('--target_platform=')) {
				target = process.argv[i].replace('--target_platform=', '');
				break;
			}
		}
		if (!['win32', 'darwin'].includes) target = os.platform();
		return target;
})();
```

>os.platform() 리턴 결과에서"darwin"은 Mac을, "win32"은 Windows(64비트 또는 32비트)를 의미합니다.
2. `rules` 선택 항목에서 다음 설정을 추가하여 `targetPlatform` 변수가 `rewritePath`를 각각의 타깃 플랫폼에 따라 설정을 전환할 수 있도록 합니다.
```js
rules: [
  { 
			test: /\.node$/, 
			loader: 'native-ext-loader', 
			options: { 
				rewritePath: targetPlatform === 'win32' ? './resources' : '../Resources' 
			} 
		},
]
```
	해당 설정의 의미는 다음과 같습니다.
	- Windows에서 `.exe` 파일 패키징 시, `native-ext-loader`가 `[응용 프로그램 기본 루트 디렉터리]/resources`로 TRTC SDK를 로딩하도록 합니다.
	- Mac에서 `.dmg`패키징 시, `native-ext-loader`를 `[응용 프로그램 기본 루트 디렉터리]/Contents/Frameworsk/../Resources`로 TRTC SDK를 로딩합니다.

`package.json` 스크립트 구축 중, `--target_platform` 매개변수를 추가한 후 다음 단계를 진행합니다.

####  3단계: package.json 설정 수정
`package.json`은 디렉터리 기본 루트에 있으며, 프로젝트 패키징에 필요한 정보가 포함되어 있습니다. 기본적으로 `package.json` 경로를 수정해야만 원활하게 패키징할 수 있으며, 다음 절차에 따라 해당 문서를 수정할 수 있습니다. 

1. `main` 설정을 수정합니다.

```javascript
// 여러 상황에서 main 파일명은 임의 설정이 가능합니다. 예시: TRTCSimpleDemo를 다음과 같이 설정 가능합니다.
"main": "main.electron.js",
  
// 단, create-react-app 스캐폴드를 사용하여 생성한 프로젝트의 경우 main 파일을 반드시 다음과 같이 설정해야 합니다.
"main": "public/electron.js",
```
2. 다음 `build` 설정을 복사하여 `package.json` 파일에 추가합니다. 이는 `electron-builder`로, 읽을 수 있는 설정 정보가 있어야 합니다.

```json
"build": {
  "appId": "[appId는 사용자 정의]",
  "directories": {
    "output": "./bin"
  },
  "win": {
    "extraFiles": [
      {
        "from": "node_modules/trtc-electron-sdk/build/Release/",
        "to": "./resources",
        "filter": ["**/*"]
      }
    ]
  },
  "mac": {
    "extraFiles": [
      { 
        "from": "node_modules/trtc-electron-sdk/build/Release/trtc_electron_sdk.node", 
        "to": "./Resources" 
      }
    ]
  }
},
```

3. `scripts` 노드에 다음 구축 및 패키징 명령어 스크립트를 추가합니다.
 본 문서에서는 `create-react-app`과 `vue-cli` 프로젝트를 예시로 하며, 기타 툴에서 생성하는 프로젝트는 해당 설정을 참고할 수 있습니다.

```json
// create-react-app 프로젝트는 해당 설정을 사용합니다.
"scripts": {
  "build:mac": "react-scripts build --target_platform=darwin",
  "build:win": "react-scripts build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}

// vue-cli 프로젝트는 해당 설정을 사용합니다.
"scripts": {
  "build:mac": "vue-cli-service build --target_platform=darwin",
  "build:win": "vue-cli-service build --target_platform=win32",
  "compile:mac": "node_modules/.bin/electron-builder --mac",
  "compile:win64": "node_modules/.bin/electron-builder --win --x64",
  "pack:mac": "npm run build:mac && npm run compile:mac",
  "pack:win64": "npm run build:win && npm run compile:win64"
}
```

>? 
>-  `main` : Electron의 게이트 파일은 일반적으로 자유롭게 설정 가능합니다. 단, 프로젝트를 `create-react-app` 스캐폴드를 사용하여 생성한 경우, 게이트 파일은 반드시 `public/electron.js`로 설정해야 합니다.
>-   `build.win.extraFiles`: Windows 프로그램 패키징 시, `electron-builder`는 `from`에서 지정하는 디렉터리의 모든 파일을 bin/win-unpacked/resources(모두 소문자)에 복사합니다.
>-   `build.mac.extraFiles`: Mac 프로그램 패키징 시, `electron-builder`는 `from`에서 지정하는 `trtc_electron_sdk.node` 파일을 bin/mac/your-app-name.app/Contents/Resources(첫 글자 대문자)에 복사합니다.
>-   `build.directories.output`: 패키징 파일 출력 경로입니다. 예를 들어 해당 설정으로 `bin` 디렉터리에 출력된다면 실제 필요에 따라 수정할 수 있습니다.
>-   `build.scripts.build:mac`: Mac 플랫폼 타깃의 구축 스크립트
>-   `build.scripts.build:win`: Windows 플랫폼 타깃의 구축 스크립트
>-   `build.scripts.compile:mac`: Mac용 .dmg 설치 파일로 컴파일링
>-   `build.scripts.compile:win64`: Windows용 .exe 설치 파일로 컴파일링
>-   `build.scripts.pack:mac`: 먼저 build:mac 구축 코드를 호출하고, 다시 compile:mac을 호출해 .dmg 설치 파일로 패키징
>-   `build.scripts.pack:win64`: 먼저build:win 구축 코드를 호출하고, 다시 pack:win64를 호출해 .exe 설차 파일로 패키징

#### 4단계: 패키징 명령어 실행
- Mac용 .dmg 설치 파일 패키징
```bash
$ cd [프로젝트 디렉터리]
$ npm run pack:mac
```
	실행 완료 후 패키징 툴에서 `bin/your-app-name-0.1.0.dmg` 설치 파일을 생성하며, 해당 파일을 선택하여 배포하십시오.
- Windows용 .exe 설치 파일 패키징
```bash
$ cd [프로젝트 디렉터리]
$ npm run pack:win64
```
	실행 완료 후 패키징 툴에서 `bin/your-app-name Setup 0.1.0.exe` 설치 파일을 생성하며, 해당 파일을 선택하여 배포하십시오.

>!TRTC Electron SDK는 현재 플랫폼 간 패키징(예: Mac에서 Windows용 .exe 파일을 패키징, 또는 Windows에서 Mac용 .dmg 파일 패키징)을 지원하지 않습니다. 현재 플랫폼 간 패키징 솔루션을 연구개발 중에 있으니 참고 부탁드립니다.

## FAQ

### 1. 방화벽에 어떤 제한이 있습니까?

SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하여 UDP를 차단하는 기업용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참조하십시오.