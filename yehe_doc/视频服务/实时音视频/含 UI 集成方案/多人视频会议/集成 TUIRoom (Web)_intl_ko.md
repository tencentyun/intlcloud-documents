## 컴포넌트 개요

TUIRoom은 UI가 있는 오픈 소스 오디오/비디오 컴포넌트입니다. TUIRoom을 통합하면 오디오/비디오 룸, 화면 공유, 채팅 및 기타 비즈니스 기능을 빠르게 런칭할 수 있습니다. Web TUIRoom의 기본 기능은 다음과 같습니다.

>?TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/d3778fc1655141b5a53e65c5ba4cfa08.png)


[TUIRoom 온라인 링크](https://web.sdk.qcloud.com/component/tuiroom/index.html)를 클릭하여 TUIRoom의 더 많은 기능을 경험할 수 있습니다.
[Github](https://github.com/tencentyun/TUIRoom)를 클릭하여 TUIRoom 코드를 다운로드할 수 있으며, [TUIRoom Web Demo 프로젝트 빠른 실행](https://github.com/tencentyun/TUIRoom/tree/main/Web) 문서를 참고하여 TUIRoom Web 데모 프로젝트를 실행할 수 있습니다.
Web TUIRoom 컴포넌트를 기존 비즈니스에 통합하려면 이 문서를 참고하십시오.

## 컴포넌트 통합
TUIRoom 컴포넌트는 Vue3 + TS + Pinia + Element Plus + SCSS를 사용하여 개발되며 Vue3 + TS 기술 스택을 사용하려면 액세스 프로젝트가 필요합니다.

[](id:step1)

### 1단계: Tencent Cloud TRTC 및 IM 서비스 활성화
TUIRoom은 Tencent Cloud의 TRTC 및 IM 서비스를 기반으로 개발되었습니다.

1. **Tencent Real-Time Communication(TRTC) 애플리케이션 생성**
	- Tencent Cloud 계정이 없으시다면 [Tencent Cloud 계정을 등록](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)하시기 바랍니다.
	- [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 **애플리케이션 관리 > 애플리케이션 생성**을 클릭하여 새로운 애플리케이션을 생성합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)
2. **TRTC 키 정보 가져오기**
  1. 생성된 애플리케이션을 **애플리케이션 목록 > 애플리케이션 정보**에서 찾아 클릭하여 SDKAppID를 확인합니다. 비즈니스 격리에 사용되는 TRTC 애플리케이션 ID입니다. 즉, SDKAppID 값이 다른 호출은 상호 연결될 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)

  2. **애플리케이션 관리 > 퀵 스타트** 탭을 선택하여 애플리케이션의 secretKey를 봅니다. TRTC의 승인된 사용을 위한 인증 자격 UserSig를 생성하기 위해 SDKAppID와 함께 사용해야 하는 TRTC 애플리케이션 키입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)

3. **UserSig 발급**
    UserSig란 Tencent Cloud가 설계한 일종의 보안 서명으로, 악성 해커가 귀하의 클라우드 서비스 사용권을 도용하는 것을 방지합니다. TUIRoom을 초기화하려면 UserSig 매개변수를 제공해야 합니다.
	- 디버깅 및 실행 중에 UserSig 계산 방법 방법은 [디버깅 및 실행 단계에서 UserSig를 계산하는 방법은 무엇입니까?](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.
	- 프로덕션 환경에서 userSig를 발급하는 방법은 [정식 실행 단계에서 UserSig는 어떻게 계산하나요?](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.


[](id:step2)
### 2단계: TUIRoom 컴포넌트 다운로드 및 복사
1. [Github](https://github.com/tencentyun/TUIRoom)을 클릭하여 TUIRoom 저장소 코드를 클론 또는 다운로드합니다.
2. 기존 Vue3 + TS 프로젝트를 엽니다. Vite 및 Webpack 패키징 사용을 지원합니다. Vue3 + TS 프로젝트가 없는 경우 다음 방법 중 하나를 선택하여 템플릿 프로젝트를 생성할 수 있습니다.
<dx-tabs>
::: Vue3 + Vite + TS 템플릿 프로젝트 생성
```bash
npm create vite@latest TUIRoom-demo -- --template vue
```
<dx-alert infotype="notice">생성 과정에서 먼저 엔터 키를 누르고 Vue를 선택한 다음 vue-ts를 선택합니다.</dx-alert>

Vue3 + Vite + TS 템플릿 프로젝트 생성 완료 후 다음 스크립트를 실행합니다.
```
cd TUIRoom-demo
npm install
npm run dev
```
:::
::: Vue3 + Webpack + TS 템플릿 프로젝트 생성
```bash
// vue-cli를 설치, Vue CLI 4.x는 Node.js가 v10 이상이어야 함
npm install -g @vue/cli
// Vue3 + Webpack + TS 템플릿 프로젝트 생성
vue create TUIRoom-demo
```
<dx-alert infotype="notice">템플릿 생성 모드로 Manually select features를 선택합니다. 기타 설정은 아래 이미지를 참고하십시오.</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/800412fb72b8e092f41fd06d5272601b.png)

Vue3 + Webpack + TS 템플릿 프로젝트 생성 완료 후 다음 스크립트를 실행합니다.
```
cd TUIRoom-demo
npm run serve
```
:::
</dx-tabs>
3. `TUIRoom/Web/src/TUIRoom` 폴더를 프로젝트의 src/ 디렉터리에 복사합니다.

[](id:step3)
### 3단계: TUIRoom 컴포넌트 레퍼런스

1. TUIRoom 컴포넌트를 'App.vue' 컴포넌트와 같은 페이지로 가져옵니다.
	- TUIRoom 컴포넌트는 사용자를 호스트 및 참석자 역할로 나눕니다. [init](#init), [createRoom](#createroom), [enterRoom](#enterroom) 메소드를 제공합니다.
	- 호스트와 참석자는 [init](#init) 메소드를 통해 TUIRoom 컴포넌트에 애플리케이션 및 사용자 데이터를 초기화할 수 있습니다. 호스트는 [createRoom](#createroom) 메소드를 통해 방을 만들고 입장할 수 있습니다. 참석자는 [enterRoom](#enterroom) 메소드를 통해 호스트가 만든 방에 참여할 수 있습니다.
```javascript
<template>
	<room ref="TUIRoomRef"></room>
</template>

<script setup lang="ts">
	import { ref, onMounted } from 'vue';
	// TUIRoom 컴포넌트를 가져옵니다. 올바른 가져오기 경로를 사용해야 함
	import Room from './TUIRoom/index.vue';
	// 컴포넌트의 메소드를 호출하는 데 사용되는 TUIRoom 컴포넌트 요소 가져오기
	const TUIRoomRef = ref();

	 onMounted(async () => {
		// TUIRoom 컴포넌트 초기화
		// 호스트는 방을 만들기 전에 TUIRoom 컴포넌트를 초기화해야 함
		// 참석자는 방에 들어가기 전에 TUIRoom 컴포넌트를 초기화해야 함
		await TUIRoomRef.value.init({
			// sdkAppId 가져오기(1단계 참고)
			sdkAppId: 0,
			// 귀하의 비즈니스에서 사용자의 고유 Id
			userId: '',
			// 로컬 개발 및 디버깅을 위해 https://console.cloud.tencent.com/trtc/usersigtool 에서 userSig를 빠르게 생성할 수 있습니다. userSig 와 userId는 일대일 대응 관계임
			userSig: '',
			// 귀하의 비즈니스에서 사용자의 사용자 이름
			userName: '',
			// 비즈니스에 있는 사용자의 프로필 사진에 연결
			userAvatar: '',
			// 화면 공유에 사용되는 사용자의 고유 Id입니다. shareUserId = `share_${userId}`여야 합니다. 화면 공유 기능이 필요하지 않은 경우 이 매개변수 불필요
			shareUserId: '',
			// 이 문서의 1단계 > 3단계를 참고하여 sdkAppId 및 shareUserId 를 사용하여 shareUserSig 발행 
			shareUserSig: '',
		})
		 // 기본적으로 방이 생성됩니다. 실제 연결 시 필요에 따라 handleCreateRoom 메소드를 실행할 수 있음
		await handleCreateRoom();
	})

	// 호스트가 방을 만듭니다. 이 메소드는 방을 생성할 때만 호출됨
	async function handleCreateRoom() {
		// roomId는 사용자가 입력한 roomId로 숫자여야 함
		// roomMode에는 ‘FreeSpeech’(자유롭게 말하기) 및 ‘ApplySpeech’(손 들고 말하기) 포함, 기본값은 ‘FreeSpeech’이며 현재 유일하게 지원되는 모드임
		// roomParam은 방에 들어가는 사용자의 기본 동작을 지정함(기본적으로 마이크를 켤지 여부, 기본적으로 카메라를 켤지 여부, 기본 미디어 장치 Id)
		const roomId = 123456;
		const roomMode = 'FreeSpeech';
		const roomParam = {
			isOpenCamera: true,
			isOpenMicrophone: true,
		}
		await TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
	}

	// 참석자 방 입장. 이 메소드는 참석자가 생성된 방에 들어갈 때 호출됨
	async function handleEnterRoom() {
		// roomId는 사용자가 입력한 roomId로 숫자여야 함
		// roomParam은 방에 들어가는 사용자의 기본 동작을 지정함(기본적으로 마이크를 켤지 여부, 기본적으로 카메라를 켤지 여부, 기본 미디어 장치 Id)
		const roomId = 123456;
		const roomParam = {
			isOpenCamera: true,
			isOpenMicrophone: true,
		}
		await TUIRoomRef.value.enterRoom(roomId, roomParam);
	}
</script>

<style>
html, body {
	width: 100%;
	height: 100%;
	margin: 0;
}

#app {
	width: 100%;
	height: 100%;
}
</style>
```

>! 페이지에 위의 코드를 복사하여 TUIRoom API의 매개변수를 실제 값으로 바꿉니다.

[](id:step4)
### 4단계: 개발 환경 구성
TUIRoom 컴포넌트를 가져온 후 프로젝트가 정상적으로 실행되도록 하려면 다음 구성이 필요합니다.

<dx-tabs>
::: Vue3 + Vite + TS 프로젝트 개발 환경 구성

1. **종속성 설치**
  - 개발 환경 종속성을 설치합니다.
```bash
npm install sass typescript unplugin-auto-import unplugin-vue-components -S -D
```
  - 프로덕션 환경 종속성을 설치합니다.
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Pinia 등록**
TUIRoom은 방 데이터 관리를 위해 Pinia를 사용합니다. 프로젝트 엔트리 파일 `src/main.ts`에 Pinia를 등록해야 합니다.
```javascript
// src/main.ts 파일
import { createPinia } from 'pinia';

const app = createApp(App);
// pinia 등록
app.use(createPinia()); 
app.mount('#app');
```
3. **element-plus 컴포넌트의 주문형 가져오기 구성**
  - TUIRoom은 element-plus UI 컴포넌트를 사용합니다. 모든 element-plus 컴포넌트를 가져오지 않으려면 요청 시 로딩하도록 `vite.config.ts`에서 구성해야 합니다.
	

<dx-alert infotype="notice">파일에 코드를 추가합니다. 기존 Vite 구성을 삭제하지 마십시오.</dx-alert>

```javascript
// vite.config.ts
import AutoImport from 'unplugin-auto-import/vite';
import Components from 'unplugin-vue-components/vite';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';

export default defineConfig({
	// ...
	plugins: [
		AutoImport({
			resolvers: [ElementPlusResolver()],
		}),
		Components({
			resolvers: [ElementPlusResolver({
				importStyle: 'sass',
			})],
		}),
	],
	css: {
		preprocessorOptions: {
			scss: {
				// ...
				additionalData: `
					@use "./src/TUIRoom/assets/style/element.scss" as *;
				`,
			},
		},
	},
});
```
  - 한편, element-plus UI 컴포넌트가 스타일을 제대로 표시할 수 있도록 하려면 엔트리 파일 `src/main.ts`에 element-plus 컴포넌트 스타일을 로딩해야 합니다.
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```
:::
::: Vue3 + Webpack + TS 프로젝트 개발 환경 구성
1. **종속성 설치**
  - 개발 환경 종속성을 설치합니다.
```bash
npm install sass sass-loader typescript unplugin-auto-import unplugin-vue-components unplugin-element-plus @types/events -S -D
```
  - 프로덕션 환경 종속성을 설치합니다.
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Pinia 등록**
TUIRoom은 방 데이터 관리를 위해 Pinia를 사용합니다. 프로젝트 엔트리 파일 `src/main.ts`에 Pinia를 등록해야 합니다.
```javascript
// src/main.ts 파일
import { createPinia } from 'pinia';

const app = createApp(App);
// pinia 등록
app.use(createPinia()); 
app.mount('#app');
```
3. **element-plus 컴포넌트의 주문형 가져오기 구성**
  - TUIRoom은 element-plus UI 컴포넌트를 사용합니다. 모든 element-plus 컴포넌트를 가져오지 않으려면 요청 시 로딩하도록 `vue.config.js`에서 구성해야 합니다.
<dx-alert infotype="notice">파일에 코드를 추가합니다. 기존 vue.config.js 구성을 삭제하지 마십시오.</dx-alert>

```javascript
// vue.config.js
const { defineConfig } = require('@vue/cli-service')
const AutoImport = require('unplugin-auto-import/webpack')
const Components = require('unplugin-vue-components/webpack')
const { ElementPlusResolver } = require('unplugin-vue-components/resolvers')
const ElementPlus = require('unplugin-element-plus/webpack')

module.exports = defineConfig({
  transpileDependencies: true,
  css: {
    loaderOptions: {
      scss: {
        additionalData: '@use "./src/TUIRoom/assets/style/element.scss" as *;'
      }
    }
  },
  configureWebpack: {
    plugins: [
      AutoImport({
        resolvers: [ElementPlusResolver({ importStyle: 'sass' })]
      }),
      Components({
        resolvers: [ElementPlusResolver({ importStyle: 'sass' })]
      }),
      // 주문형으로 가져올 때 테마 색상 사용자 지정
      ElementPlus({
        useSource: true
      })
    ]
  }
})

```
  - 한편, element-plus UI 컴포넌트가 스타일을 제대로 표시할 수 있도록 하려면 엔트리 파일 `src/main.ts`에 element-plus 컴포넌트 스타일을 로딩해야 합니다.
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```
4. **ts 선언 파일 구성**
 `src/shims-vue.d.ts` 파일에 다음 구성을 추가합니다.
```
declare module 'tsignaling/tsignaling-js' {
  import TSignaling from 'tsignaling/tsignaling-js';
  export default TSignaling;
}

declare module 'tim-js-sdk' {
  import TIM from 'tim-js-sdk';
  export default TIM;
}

declare const Aegis: any;
```
:::
</dx-tabs>

[](id:step5)
### 5단계: 개발 환경 실행
콘솔에서 스크립트를 실행하여 개발 환경을 실행합니다. 그런 다음 사용할 브라우저에서 TUIRoom 컴포넌트가 포함된 페이지를 엽니다.

- **[2단계](#step2)의 스크립트를 사용하여 Vue + Vite + TS 프로젝트를 생성하는 경우** 다음을 수행해야 합니다.

1. 개발 환경 명령어를 실행합니다.
```bash
npm run dev
```
2. 브라우저에서 `http://localhost:3000/`에 접속합니다.
>! TUIRoom은 element-plus 컴포넌트를 온디맨드로 불러오기 때문에 개발 환경 라우팅 페이지가 처음 로드될 때 반응이 느려지고 element-plus 컴포넌트가 온디맨드로 로딩된 후 정상적으로 사용할 수 있습니다. 이 로딩은 패키징 후 페이지 로딩에 영향을 미치지 않습니다.

3. TUIRoom 컴포넌트의 기능을 사용해 보십시오.

- **[2단계](#step2)의 스크립트를 사용하여 Vue + Webpack + TS 프로젝트를 생성하는 경우** 다음을 수행해야 합니다.
1. 개발 환경 명령어를 실행합니다.
```bash
npm run serve
```

2. 브라우저에서 `http://localhost:8080/`에 접속합니다.
> ! 실행 중 src/TUIRoom 디렉터리에 eslint 오류가 있는 경우 .eslintignore 파일에 /src/TUIRoom 경로를 추가하여 eslint 검사를 차단할 수 있습니다.

3. TUIRoom 컴포넌트의 기능을 사용해 보십시오.

### 6단계: 프로덕션 환경 배포

1. dist 파일을 패키징합니다.

```bash
npm run build
```

>? 실제 패키징 명령어는 package.json 파일을 확인하십시오.

2. dist 파일을 서버에 배포합니다.

>! 프로덕션 환경에서는 HTTPS 도메인 이름을 사용해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/53efdc1d1692a21946cb6c94ddea40e5.png)


## 부록: TUIRoom API
### TUIRoom 인터페이스
#### init

이 API는 TUIRoom 데이터를 초기화하는 데 사용됩니다. TUIRoom을 사용하는 사람은 이 init 메소드를 호출해야 합니다.
```javascript
TUIRoomRef.value.init(roomData);
```

매개변수는 다음과 같습니다.

| 매개변수                  | 유형   | 의미                                                         |
| --------------------- | ------ | ------------------------------------------------------------ |
| roomData              | object |                                                              |
| roomData.sdkAppId     | number | 고객 SDKAppId                                              |
| roomData.userId       | string | 사용자 고유 ID                                                |
| roomData.userSig      | string | 사용자 UserSig                                               |
| roomData.userName     | string | 사용자 닉네임                                                   |
| roomData.userAvatar   | string | 사용자 프로필                                                   |
| roomData.shareUserId  | string | 선택 사항, 화면 공유에 사용되는 UserId, shareUserId = `share_${userId}`여야 하며, 화면 공유 기능이 없는 경우 불필요 |
| roomData.shareUserSig | string | 선택 사항, 화면 공유에 사용되는 UserSig                           |


#### createRoom

이 API는 호스트가 방을 만드는 데 사용합니다.
```javascript
TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
```

매개변수는 다음과 같습니다.

| 매개변수                          | 유형   | 의미                                                         |
| ----------------------------- | ------ | ------------------------------------------------------------ |
| roomId                        | number | 방 ID                                                      |
| roomMode                      | string | ‘FreeSpeech’(자유롭게 말하기) 및 ‘ApplySpeech’(손 들고 말하기)를 포함한 방 모드, 기본값은 ‘FreeSpeech’이며 현재 유일하게 지원되는 모드임 |
| roomParam                     | Object | 선택 사항                                                       |
| roomParam.isOpenCamera        | string | 선택 사항, 방에 입장할 때 카메라 켜기 여부, 기본값은 No                       |
| roomParam.isOpenMicrophone    | string | 선택 사항, 방 입장 시 마이크 켜기 여부, 기본값은 No                       |
| roomParam.defaultCameraId     | string | 선택 사항, 기본 카메라의 ID                                    |
| roomParam.defaultMicrophoneId | string | 선택 사항, 기본 마이크의 ID                                    |
| roomParam.defaultSpeakerId    | String | 선택 사항, 기본 스피커의 ID                                    |

#### enterRoom
이 API는 참석자가 방에 입장하는 데 사용됩니다.
```javascript
TUIRoomRef.value.enterRoom(roomId, roomParam);
```

매개변수는 다음과 같습니다.

| 매개변수                          | 유형   | 의미                                   |
| ----------------------------- | ------ | -------------------------------------- |
| roomId                        | number | 방 ID                                |
| roomParam                     | Object | 선택 사항                                 |
| roomParam.isOpenCamera        | string | 선택 사항, 방에 입장할 때 카메라 켜기 여부, 기본값은 No                       |
| roomParam.isOpenMicrophone    | string | 선택 사항, 방 입장 시 마이크 켜기 여부, 기본값은 No |
| roomParam.defaultCameraId     | string | 선택 사항, 기본 카메라의 ID              |
| roomParam.defaultMicrophoneId | string | 선택 사항, 기본 마이크의 ID              |
| roomParam.defaultSpeakerId    | String | 선택 사항, 기본 스피커의 ID              |


### TUIRoom 이벤트

#### onRoomCreate
방 생성 콜백입니다.
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-create="handleRoomCreate"></room>
</template>

<script setup lang="ts">
  // TUIRoom 컴포넌트를 가져옵니다. 올바른 가져오기 경로를 사용해야 함
  import Room from './TUIRoom/index.vue';
  
  function handleRoomCreate(info) {
    if (info.code === 0) {
      console.log(‘방 생성 완료’)
    }
  }
</script>
```

#### onRoomEnter

방 입장 콜백입니다.
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-enter="handleRoomEnter"></room>
</template>

<script setup lang="ts">
  // TUIRoom 컴포넌트를 가져옵니다. 올바른 가져오기 경로를 사용해야 함
  import Room from './TUIRoom/index.vue';
  
  function handleRoomEnter(info) {
    if (info.code === 0) {
      console.log(‘방 입장 완료’)
    }
  }
</script>
```

#### onRoomDestory

호스트가 방을 종료했습니다.
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-destory="handleRoomDestory"></room>
</template>

<script setup lang="ts">
  // TUIRoom 컴포넌트를 가져옵니다. 올바른 가져오기 경로를 사용해야 함
  import Room from './TUIRoom/index.vue';
  
  function handleRoomDestory(info) {
    if (info.code === 0) {
      console.log(‘호스트가 방 종료 완료’)
    }
  }
</script>
```

#### onRoomExit
참석자가 방을 나갔습니다.

```javascript
<template>
  <room ref="TUIRoomRef" @on-room-exit="handleRoomExit"></room>
</template>

<script setup lang="ts">
  // TUIRoom 컴포넌트를 가져옵니다. 올바른 가져오기 경로를 사용해야 함
  import Room from './TUIRoom/index.vue';
  
  function handleRoomExit(info) {
    if (info.code === 0) {
      console.log(‘참석자 방 퇴장 완료’)
    }
  }
</script>
```

#### onKickOff

일반 참석자는 호스트로부터 퇴장 공지를 받습니다.

```javascript
<template>
  <room ref="TUIRoomRef" @on-kick-off="handleKickOff"></room>
</template>

<script setup lang="ts">
  // TUIRoom 컴포넌트를 가져옵니다. 올바른 가져오기 경로를 사용해야 함
  import Room from './TUIRoom/index.vue';
  
  function handleKickOff(info) {
    if (info.code === 0) {
      console.log(‘호스트에 의해 참석자 방 강제 퇴장’)
    }
  }
</script>
```
