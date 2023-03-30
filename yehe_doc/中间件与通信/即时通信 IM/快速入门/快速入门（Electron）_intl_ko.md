````javascript
본문은 IM Demo(Electron)를 빠르게 실행하는 방법과 Electron SDK를 통합하는 방법을 설명합니다.

## 환경 요건

| 플랫폼     | 버전                |
| -------- | ------------------- |
| Electron | 13.1.5 이상 버전. |
| Node.js  | v14.2.0             |

## 플랫폼 지원

현재 Macos 및 Windows 2가지 플랫폼을 지원합니다.

## DEMO 체험

통합하기 전에 [DEMO](https://intl.cloud.tencent.com/document/product/1047/34279)를 사용하여 IM Electron SDK의 기능을 빠르게 이해할 수 있습니다.

## 전제 조건

[Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계

[](id:step1)

### 1단계: 애플리케이션 생성

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
  > ?이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
  > 동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
2. **애플리케이션 생성**을 클릭하고 **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력한 후 **확인**을 클릭합니다.
    ![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID 정보를 저장하십시오. 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 태그, 생성 시간 및 만료 시간을 확인할 수 있습니다.
   ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 생성된 애플리케이션을 클릭한 후, 왼쪽 사이드바의 **보조 툴** > **UserSig 툴**을 클릭하여, UserID 및 UserSig를 생성하고, 로그인에 사용할 UserSig를 복사합니다.
    ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)

### 2단계: Electron SDK를 통합하기 위한 적절한 방법 선택

Tencent Cloud IM은 두 가지 통합 체계를 제공합니다. 가장 적합한 체계를 선택할 수 있습니다.

| 통합 방법  | 적용 가능한 시나리오                                                                                                                                                                |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEMO 사용 | IM Demo에는 모든 채팅 기능이 포함되어 있으며 오픈 소스 코드를 제공합니다. 채팅 시나리오를 구현하려면 Demo를 사용하여 2차 개발을 진행할 수 있습니다. [Demo](https://intl.cloud.tencent.com/document/product/1047/34279)에서 체험해 보십시오. |
| 자체 구현    | Demo가 UI 요구 사항을 충족하지 않는 경우 이 방법을 사용할 수 있습니다.                                                                                                                |

IM SDK의 API 이해를 돕기 위해, [API 문서](https://comm.qq.com/im/doc/electron/zh/)를 제공합니다.

[](id:step3)

### 3단계: Demo 사용

1. IM Electron Demo 소스 코드를 로컬에 클론합니다.
  ```javascript
  git clone https://github.com/TencentCloud/tc-chat-demo-electron.git
  ```
2. 프로젝트 종속성을 설치합니다.
  ```javascript
  // 프로젝트의 루트 디렉터리
  npm install

  // 렌더링 프로세스 디렉터리
  cd src/client
  npm install
  ```
3. 프로젝트를 실행합니다.
```javascript
// 프로젝트의 루트 디렉터리
npm start
```
4. 프로젝트를 패키징합니다.
  ```javascript
  // mac 패키징
  npm run build:mac
  // windows 패키징
  npm run build:windows
  ```

>? demo에서 메인 프로세스 디렉터리 `src/app/main.js`와 렌더링 프로세스 디렉터리는 `src/client`입니다. 실행 중 문제가 발생하면 먼저 문제 해결을 위한 FAQ를 참고하십시오.

[](id:step4)

### 4단계: 자체 구현

**Electron SDK 설치**
다음 명령을 사용하여 최신 버전의 Electron SDK를 설치합니다
다음 명령을 실행합니다.

```
npm install im_electron_sdk
```

**SDK 초기화**

1. `TimMain`에 `sdkAppID`를 전달합니다.
```javascript
// 메인 프로세스
const TimMain = require('im_electron_sdk/dist/main')

const sdkappid = 0;// IM 콘솔에서 신청할 수 있습니다
const tim = new TimMain({
  sdkappid:sdkappid
})
```
2. `TIMInit`를 호출하여 SDK를 초기화합니다.
```javascript
//렌더링 프로세스
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
// 컴포넌트 초기화
timRender.TIMInit()
```
3. 테스트 사용자로 로그인합니다.
로그인 확인을 위해 콘솔에서 처음 생성한 테스트 계정으로 로그인합니다.
`timRender.TIMLogin` 메소드를 호출하여 테스트 사용자로 로그인합니다.
반환된 `code`가 0이면 로그인에 성공한 것입니다.
```javascript
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
let {code} = await timRender.TIMLogin({
  userID:"userID",
  userSig:"userSig" // userSig 생성 참고
})
```

>? 이 계정은 개발 테스트 전용이며, 애플리케이션이 런칭되기 전에 정확한 `UserSig` 배포 방법은 `UserSig` 계산 코드를 서버에 통합하고 APP 지향 API를 제공하는 것입니다. `UserSig`가 필요한 경우 APP은 동적 `UserSig`에 대한 요청을 비즈니스 서버에 보낼 수 있습니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

**메시지 보내기**
다음 샘플은 문자 메시지를 보내는 방법을 보여줍니다. 반환된 `code`가 0이면 메시지가 성공적으로 전송된 것입니다.
코드 예시:

```javascript
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
let param:MsgSendMessageParamsV2 = {    // param of TIMMsgSendMessage
    conv_id: "conv_id",
    conv_type: 1,
    params: {
        message_elem_array: [{
            elem_type: 1,
            text_elem_content:'Hello Tencent!',

        }],
        message_sender: "senderID",
    },
    callback: (data) => {}
  }
let {code} = await timRender.TIMMsgSendMessageV2(param);
```

>? 메시지 전송에 실패한 경우, sdkAppID가 낯선 사람에게 메시지 전송을 지원하지 않기 때문일 수 있습니다. 이 경우 테스트를 위해 콘솔에서 [친구 관계 체인 확인 비활성화](https://console.cloud.tencent.com/im/login-message)할 수 있습니다.

**대화 목록 가져오기**
이전 단계에서 테스트 메시지를 보내면 다른 테스트 계정에 로그인하여 대화 목록을 가져올 수 있습니다.
일반 응용 시나리오는 다음과 같습니다.
응용 프로그램 시작 시 대화 목록을 가져오고 지속적인 연결을 수신하여 대화 목록을 실시간으로 업데이트합니다.

```javascript
let param:getConvList = {
            userData:userData,
        }
let data:commonResult<convInfo[]> = await timRenderInstance.TIMConvGetConvList(param)
```

이 때 이전 단계에서 다른 테스트 계정에서 보낸 메시지를 볼 수 있습니다.

**메시지 수신**
일반 응용 시나리오는 다음과 같습니다.

1. 인터페이스는 새로운 대화가 시작되면 먼저 일정량의 메시지 기록을 한꺼번에 요청하여 메시지 기록 목록을 보여 줍니다.
2. 긴 링크를 수신하여 실시간으로 새로운 메시지를 수신하여 메시지 기록 목록에 추가합니다.

일회성 요청 메시지 기록 리스트

```javascript
let param:MsgGetMsgListParams = {
        conv_id: conv_id,
        conv_type: conv_type,
        params: {
            msg_getmsglist_param_last_msg: msg,
            msg_getmsglist_param_count: 20,
            msg_getmsglist_param_is_remble: true,
        },
        user_data: user_data
    }
    let msgList:commonResult<Json_value_msg[]> = await timRenderInstance.TIMMsgGetMsgList(param);
```

실시간으로 새 메시지 수신
다음은 callback 바인딩에 대한 샘플 코드입니다.

```javascript
let param : TIMRecvNewMsgCallbackParams = {
            callback: (...args)=>{},
            user_data: user_data
        }
timRenderInstance.TIMAddRecvNewMsgCallback(param);
```

이제 IM 모듈 개발을 완료했으며, 메시지를 주고받거나 다른 대화에 들어갈 수 있습니다.
그룹, 사용자 프로필, 관계 체인, 오프라인 푸시 및 로컬 검색과 같은 더 많은 기능을 개발할 수 있습니다.
자세한 내용은 [API 문서](https://comm.qq.com/im/doc/electron/zh/Callback/readme.html)를 참고하십시오.

## FAQ

#### 어떤 플랫폼이 지원됩니까?

현재 Macos 및 Windows 2가지 플랫폼을 지원합니다.

#### 에러 코드를 쿼리하는 방법은 무엇입니까?

IM SDK의 API 레이어 에러 코드는 [에러 코드](https://intl.cloud.tencent.com/document/product/1047/34348)를 참고하십시오.

#### 개발 환경 설치 중에 `npm ERR! gyp ERR! stack TypeError: Cannot assign to read only property 'cflags' of object '#<Object>'` 오류가 보고되면 어떻게 해야 합니까?

node 버전을 16.18.1로 다운그레이드합니다.

#### 개발 환경 설치 문제 `gypgyp ERR!ERR` 오류를 해결하는 방법은 무엇입니까?

[gypgyp ERR!ERR! ](https://stackoverflow.com/questions/57879150/how-can-i-solve-error-gypgyp-errerr-find-vsfind-vs-msvs-version-not-set-from-c)를 참고하십시오.

#### `npm install` 실행 시 `npm ERR! Fix the upstream dependency conflict, or retry` 오류가 보고되면 어떻게 해야 하나요?

npmV7 이전 버전에서는 설치 중에 발생하는 종속성 충돌이 자동으로 무시됩니다. 계속 설치를 진행합니다.
npmV7 이상 버전에서는 종속성 충돌이 자동으로 무시되지 않으며, 이를 무시하려면 수동으로 명령을 입력해야 합니다.
종속성 충돌을 무시하는 명령은 다음과 같습니다.
<dx-codeblock>
:::  sh
npm install --force
:::
</dx-codeblock>


#### `npm run start` 실행 시 `Error: error:0308010C:digital envelope routines::unsupported` 오류가 보고되면 어떻게 해야 하나요?

node 버전을 16.18.1로 다운그레이드합니다.

#### Mac 클라이언트 Demo에서 `npm run start`를 실행할 때 화면이 흰색으로 바뀌면 어떻게 해야 하나요?

Mac에서 `npm run start`를 실행하면 흰색 화면이 나오는 이유는 아직 렌더링 프로세스의 코드가 build 완료되지 않았고, 메인 프로세스가 오픈한 포트 3000번이 빈 페이지이기 때문입니다. 렌더링 프로세스의 코드 build 완료 후 창을 새로고침하면 문제가 해결될 수 있습니다. 또는 `cd src/client && npm run dev:react`, `npm run dev:electron`을 실행하여 렌더링 프로세스와 메인 프로세스를 각각 시작합니다.

#### `vue-cli-plugin-electron-builder`로 빌드된 프로젝트에서 `native modules`을 어떻게 사용합니까?

`vue-cli-plugin-electron-builder`로 빌드된 프로젝트에서 `native modules` 사용과 관련된 문제는 [No native build was found for platform = xxx](https://github.com/nklayman/vue-cli-plugin-electron-builder/issues/1492)를 참고하십시오.

#### `webpack`으로 빌드한 프로젝트에서 `native modules`을 어떻게 사용하나요?

webpack으로 빌드한 프로젝트에서 native modules를 사용하는 것과 관련된 문제는 [Windows 환경 FAQ](https://blog.csdn.net/Yoryky/article/details/106780254)를 참고하십시오.

#### `Dynamic Linking Error` 오류가 보고되면 어떻게 해야 합니까?

Dynamic Linking Error. electron-builder 구성

``` javascript
   extraFiles:[
    {
      "from": "./node_modules/im_electron_sdk/lib/",
      "to": "./Resources",
      "filter": [
        "**/*"
      ]
    }
  ]
```xxxxxxxxxx    extraFiles:[    {      "from": "./node_modules/im_electron_sdk/lib/",      "to": "./Resources",      "filter": [        "**/*"      ]    }  ]javascript
````
