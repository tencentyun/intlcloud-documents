
## TUIKit 소개

TUIKit은 Tencent Cloud IM SDK를 기반으로 하는 UI 컴포넌트 라이브러리로, 세션, 채팅, 관계 체인, 그룹, 음성/영상 통화 등의 기능을 포함한 일부 범용 UI 컴포넌트를 제공합니다.
UI 컴포넌트를 기반으로 블록을 쌓는 것처럼 자신의 비즈니스 로직을 빠르게 구축할 수 있습니다.
TUIKit의 컴포넌트는 UI 기능을 구현하는 동시에 IM SDK에 해당하는 인터페이스를 호출하여 IM 관련 로직과 데이터를 처리하므로 개발자는 UIKit을 사용할 때 자신의 업무에만 집중하거나 필요에 따라 확장할 수 있습니다.
React를 기반으로 개발된 TUIKit API 스타일은 중국 외 고객의 사용 습관에 더 부합하며, 국제화를 지원합니다. 해외 진출 니즈가 있는 경우 권장합니다.

## Example App
체험 가능한 온라인 [demo](https://web.sdk.qcloud.com/im/demo/intl/index.html)를 제공합니다. 또한 github에서 오픈 소스 코드 [chat-uikit-react](https://github.com/TencentCloud/chat-uikit-react)를 얻으실 수 있습니다.

## 개발 환경 요구사항
- React ≥ v18.0
- TypeScript
- node（12.13.0 ≤ node 버전 ≤ 17.0.0, Node.js의 공식 LTS 버전 16.17.0 권장）
- npm(사용 중인 node 버전과 일치하는 버전 사용)

## 데모 실행

### 1단계: 소스 코드 다운로드
```
# Run the code in CLI
$ git clone https://github.com/TencentCloud/chat-uikit-react
# Go to the project  
$ cd chat-uikit-react
# Install dependencies of the demo and build chat-uikit-react
$ npm install && npm run build
$ cd examples/sample-chat && npm install
```

>! `examples/sample-chat` 프로젝트의 종속성 패키지 `@tencentcloud/chat-uikit-react`는 로컬 패키지입니다. 따라서 `chat-uikit-react` 루트 디렉터리에서 `npm run build` 또는 `npm run start`를 실행해야 합니다. `npm run start` 명령은 `npm run rollup -c -w`를 시작하고 `examples/sample-chat` 프로젝트는 수정된 컴포넌트 라이브러리를 실시간으로 로딩합니다. 컴포넌트 라이브러리를 개발하거나 수정하려면 `npm run start` 명령을 사용하는 것이 좋습니다.


### 2단계: demo 구성
1. `examples/sample-chat` 프로젝트를 열고 `./examples/sample-chat/src/debug/GenerateTestUserSig.js` 경로를 통해 `GenerateTestUserSig.js` 파일을 찾습니다.
2. `GenerateTestUserSig.js` 파일에서 `SDKAPPID`와 `SECRETKEY`를 설정하고 [IM 콘솔](https://console.cloud.tencent.com/im)에서 해당 값을 얻을 수 있습니다. 대상 애플리케이션 카드를 클릭하여 기본 구성 페이지로 이동합니다. 예시:
3. **상기 이미지**에서 **복사** 아이콘을 클릭하고 복사된 값을 사용하여 `GenerateTestUserSig.js` 파일의 원본 `SDKAPPID` 및 `SECRETKEY`를 대체합니다.
>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다.**
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.
   [](id:2-4)
4. 애플리케이션의 계정 관리 페이지로 이동하여, 계정을 생성하고 userID를 가져와 메시지 전송 테스트 사용자로 사용합니다.

### 3단계: 프로젝트 실행
```
# Launch the project
$ cd examples/sample-chat
$ npm run start
```

### 4단계: 첫 번째 메시지 전송
1. 프로젝트가 성공적으로 실행된 후 ‘+’ 아이콘을 클릭하여 대화를 생성합니다.
2. 입력란에 다른 사용자의 userID를 검색합니다([2.4단계](#2-4) 참고).
3. 대화를 시작하려면 사용자의 프로필 사진을 클릭합니다.
4. 입력란에 메시지를 입력하고 "Enter"키를 누르면 전송됩니다.

## FAQ

#### UserSig는 무엇입니까?

UserSig는 IM 로그인 비밀번호입니다. UserID 등의 정보를 암호화하여 생성된 암호문입니다.

#### UserSig는 어떻게 생성합니까?

UserSig 배포 방식은 UserSig 계산 코드를 서버에 통합하고 프로젝트 지향 API를 제공하는 것입니다. UserSig가 필요한 경우, 프로젝트에서 동적 UserSig에 대한 요청을 비즈니스 서버에 보낼 수 있습니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385#GeneratingdynamicUserSig)를 참고하십시오.

> !본문의 샘플 코드에서 UserSig을 가져오는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일 및 리버스 엔지니어링에 취약합니다. SECRETKEY가 노출되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서, **이 방법은 로컬 데모 프로젝트 및 기능 디버깅에만 적합합니다**. 올바른 UserSig 배포 방법은 상기 설명을 참고하십시오.

## 관련 문서

- [SDK API 매뉴얼](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK 업데이트 로그](https://intl.cloud.tencent.com/document/product/1047/34281)
