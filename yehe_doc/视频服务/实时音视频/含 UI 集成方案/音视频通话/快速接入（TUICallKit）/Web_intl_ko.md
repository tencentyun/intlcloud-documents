본문에서는 TUICallKit 컴포넌트를 빠르게 통합하는 방법을 설명합니다. 다음 주요 단계를 완료하고 완전한 UI로 영상 통화 기능을 얻을 수 있습니다.

컴포넌트를 사용해 보려면 [TUICallKit 기본 demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)를 참고하십시오.

통합하기 전에 데스크탑 브라우저가 오디오/비디오 서비스를 지원하는지 확인하십시오. 자세한 내용은 [환경 요구 사항](https://www.tencentcloud.com/document/product/647/50993#1b83cb8f-4c54-43f3-863d-579786ab78bc)을 참고하십시오.

[](id:step1)
##  1단계: 서비스 활성화

TUICallKit은 Tencent Cloud의 두 가지 유료 PaaS 서비스 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448) 및 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)을 기반으로 하는 오디오/비디오 통신 컴포넌트입니다. 아래 단계에 따라 관련 서비스를 활성화하고 60일 무료 베타 서비스를 체험할 수 있습니다.

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하고 **애플리케이션 생성**을 클릭하고 팝업 대화 상자에 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/ce2e34f7cd1cd14679fc5decffb469af.png)

2. 방금 생성한 애플리케이션을 클릭하여 **기본 구성** 페이지로 이동하고 페이지 오른쪽 하단에서 **Tencent TRTC 서비스 활성화**의 **무료 체험**을 클릭하여 TUICallKit의 7일 무료 베타 서비스를 활성화합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

3. 같은 페이지에서 **SDKAppID**와 **Key**를 찾아 기록해둡니다. 나중에 사용하게 됩니다.
	![img](https://qcloudimg.tencent-cloud.cn/raw/8349ac97b261279606316331488784c3.png)
	- SDKAppID: 비즈니스 격리에 사용되는 IM 애플리케이션 ID. 즉, SDKAppID 값이 다른 호출은 상호 연결할 수 없습니다.
	- Secretkey: IM의 승인된 사용을 위한 인증 자격 증명 UserSig를 생성하기 위해 SDKAppID와 함께 사용해야 하는 IM 애플리케이션 키입니다. 5단계에서 사용됩니다.

[](id:step2)
## 2단계: TUICallKit 컴포넌트 가져오기

1. [GitHub](https://github.com/tencentyun/TUICallKit/tree/main/Web)에서 TUICallKit 소스 코드를 다운로드하고 `TUICallKit/Web` 폴더를 프로젝트의 `src/components` 폴더에 복사합니다.
![img](https://qcloudimg.tencent-cloud.cn/image/document/b90fbef92c17090688ebc0c9b4577037.png)

1. 폴더를 입력하고 필요한 종속성을 설치합니다.
```shell
cd ./src/components/TUICallKit/Web 
yarn                                  // yarn이 현재 환경에 설치되어 있지 않으면 npm install -g yarn을 실행하여 설치할 수 있습니다
```

[](id:step3)
## 3단계: UserSig 생성

UserSig가 생성된 경우 이 단계를 건너뛰고 [4단계](#step4)로 진행할 수 있습니다.

1. [IM 콘솔](https://console.tencentcloud.com/im)에서 SDKAppID 및 Key를 얻을 수 있는 초기화 매개변수를 설정합니다. 대상 애플리케이션의 카드를 클릭하여 기본 구성 페이지로 이동합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/95ab37db3b8c371d7fa86af24b5a6aad.png)

2. 기본 정보 섹션에서 키 표시를 클릭하고 키 정보를 `TUICallKit/Web/demos/basic/public/debug/GenerateTestUserSig.js` 파일에 복사하여 저장합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/8cbbf4515e40f0e3bc0062b2c17a635e.png)

3. 4단계에서 `GenerateTestUserSig.js`의 `genTestUserSig(userID)` 함수를 사용하여 userSig를 계산할 수 있습니다.
```javascript
import * as GenerateTestUserSig from "../public/debug/GenerateTestUserSig.js";
const { userSig } = GenerateTestUserSig.genTestUserSig(userID);
```

4. Vite를 스타트업으로 사용하는 경우 [vite에서 가져오기 문제](https://www.tencentcloud.com/document/product/647/50993#f020d04e-5439-4679-bc6e-716f7329b60a)에 주의하십시오.

>! 릴리스하기 전에 이 파일을 삭제해야 합니다. 본문에서 UserSig를 얻는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이는 SECRETKEY를 디컴파일 및 크래킹에 취약하게 만듭니다. 키가 유출되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 로컬에서 실행되는 디버깅에만 적합합니다**. 올바른 UserSig 배포 방법은 UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것입니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 비즈니스 서버에 보낼 수 있습니다. 자세한 내용은 [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385)를 참고하십시오.

[](id:step4)
## 4단계: TUICallKit 컴포넌트 호출

원하는 페이지에서 TUICallKit 컴포넌트를 호출하여 호출 페이지를 표시할 수 있습니다.

1. TUICallKit UI 가져오기
```js
<script lang="ts" setup>
import { TUICallKit } from "./src/components/TUICallKit/Web";
</script>
  
<template>
  <div class="call-kit-container">
    <TUICallKit />
  </div>
</template>
  
<style scoped>
.call-kit-container {
  width: 50rem;
  height: 35rem;
  border-radius: 16px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
}
</style>
```

2. 사용자 로그인 및 전화 걸기
    2.1 [TUIKit](https://www.tencentcloud.com/document/product/1047/50061) 키트를 사용한 경우 다음 코드를 가져와서 TUICallKit을 플러그인으로 선언해야 합니다. 그렇지 않으면 다음 코드를 가져올 필요가 없습니다.
  ```
    import { TUICallKit } from './src/components/TUICallKit/Web/src/index';
    TUIKit.use(TUICallKit);
  ```

  2.2 사용자 로그인을 구현해야 하는 경우 다음 코드를 실행합니다.
  ```
    import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
    TUICallKitServer.init({ SDKAppID, userID, userSig }); 
  ```
>? userSig는 [3단계](#step3)에서 가져올 수 있습니다.

	2.3 호출을 구현해야 하는 경우 다음 코드를 실행합니다.
	```
		import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
		TUICallKitServer.call({ userID, type }); // 일대일 통화
		TUICallKitServer.groupCall({ userIDList, groupID, type }); // 그룹 통화
	```
	상기 단계를 완료하면 첫 번째 전화를 성공적으로 걸 수 있습니다. API 매개변수에 대한 자세한 내용은 [API 문서](https://www.tencentcloud.com/document/product/647/51015)를 참고하십시오.

3. 고급 API
	이 컴포넌트는 현재 통화 상태를 알려주는 데 사용할 수 있는 `beforeCalling` 및 `afterCalling` 콜백을 제공합니다.
	- `beforeCalling`: 통화 전에 반환
	- `afterCalling`: 통화 후에 반환

예를 들어, [TUICallKit/Web/demos/basic/src/App.vue](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/src/App.vue)에 설명된 대로 <`TUICallKit />;` 컴포넌트를 확장 및 축소하는 데 사용할 수 있습니다.
```javascript
function beforeCalling() {
  console.log("이 함수는 통화 전에 실행됩니다");
}
function afterCalling() {
  console.log("이 함수는 통화 후에 실행됩니다");
}
```
```javascript
<TUICallKit :beforeCalling="beforeCalling" :afterCalling="afterCalling"/>
```

## 기타 문서

- [TUICallKit API](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/API.md)
- [TUICallKit 기본 demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [TUICallKit UI 사용자 정의 가이드](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/UI Customization.md)
- [TUICallKit (Web) FAQs](https://www.tencentcloud.com/document/product/647/51024)


## FAQ

### 1. UserSig는 어떻게 생성합니까?

UserSig 배포 방식은 UserSig 계산 코드를 서버에 통합하고 프로젝트 지향 API를 제공하는 것입니다. UserSig가 필요한 경우, 프로젝트에서 동적 UserSig에 대한 요청을 비즈니스 서버에 보낼 수 있습니다. 자세한 내용은 [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385?lang=en&pg=)를 참고하십시오.

### 2. vite에서 가져오기 문제

vite에서 프로젝트를 생성하는 경우 vite는 다른 파일 패키징 방법을 사용하므로 `lib-generate-test-usersig.min.js`를 `index.html`로 가져와야 합니다.
```javascript
// index.html
<script src="/public/debug/lib-generate-test-usersig.min.js"> </script>
```

`GenerateTestUserSig.js`에서 import한 메소드를 주석 처리합니다

```javascript
// import * as LibGenerateTestUserSig from './lib-generate-test-usersig.min.js'
```

### 3. 환경 요구 사항

#### 브라우저 버전 요구 사항

| 운영 체제 | 브라우저 유형                   | 브라우저 최저 버전 요구사항 |
| -------- | ---------------------------- | ------------------ |
|  Mac OS   | 데스크톱 Safari 브라우저         | 11+                |
|  Mac OS   | 데스크톱 Chrome 브라우저         | 56+                |
|  Mac OS   | 데스크톱 Firefox 브라우저        | 56+                |
|  Mac OS  | 데스크톱 Edge 브라우저           | 80+                |
| Windows  | 데스크톱 Chrome 브라우저         | 56+                |
| Windows  | 데스크톱 QQ 브라우저(고속 커널) | 10.4+              |
| Windows  | 데스크톱 Firefox 브라우저        | 56+                |
| Windows  | 데스크톱 Edge 브라우저           | 80+                |

>?브라우저 호환성에 대한 자세한 내용은 [지원되는 브라우저](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)를 참고하십시오. [TRTC 호환성 확인 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 사용하여 온라인 테스트를 실행할 수도 있습니다.

#### 네트워크 환경 요구 사항

TUICallKit 사용 시 방화벽 제한으로 인해 음성 및 영상 통화가 안될 수 있으니 [방화벽 제한 처리](https://www.tencentcloud.com/document/product/647/35164)를 참고하여 해당 포트 및 도메인 이름을 방화벽 얼로우리스트에 추가하시기 바랍니다.

#### 웹사이트 도메인 이름 프로토콜에 대한 요구 사항

보안 및 개인 정보 보호를 위해 HTTPS URL만 본 문서에 연결된 컴포넌트의 모든 기능에 액세스할 수 있습니다. 따라서 프로덕션 환경에서 사용자가 제품 기능을 원활하게 체험할 수 있도록 **https://** 프로토콜 도메인에 귀하의 웹사이트를 배치하십시오.

>! 로컬 개발은 `http://localhost` 또는 `file://` 프로토콜을 통해 액세스할 수 있습니다.

URL 도메인 및 프로토콜 지원은 다음 표 참고:

| 응용 시나리오     | 프로토콜             | 수신(재생) | 발송(푸시) | 화면 공유 | 비고     |
| ------------ | ---------------- | ------------ | ------------ | -------- | ---- |
| 프로덕션 환경     | HTTPS 프로토콜        | 지원         | 지원         | 지원     | 권장 |
| 프로덕션 환경     | HTTP 프로토콜         | 지원         | 미지원       | 미지원   | -    |
| 로컬 디버깅 환경 | http://localhost | 지원         | 지원         | 지원     | 권장 |
| 로컬 디버깅 환경 | http://127.0.0.1 | 지원         | 지원         | 지원     |      -    |
| 로컬 디버깅 환경 | http://[로컬 IP 주소]  | 지원         | 미지원       | 미지원   | -    |
| 로컬 디버깅 환경 | file:///         | 지원         | 지원         | 지원     | -    |
