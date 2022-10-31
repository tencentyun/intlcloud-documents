## 컴포넌트 개요

TUIRoom은 UI가 있는 오픈 소스 오디오/비디오 컴포넌트입니다. TUIRoom을 통합하면 오디오/비디오 룸, 화면 공유, 채팅 및 기타 비즈니스 기능을 빠르게 런칭할 수 있습니다. Electron TUIRoom의 기본 기능은 다음과 같습니다.

>? TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/a98627586f82847a061a3695ad15ad26.png)

온라인 체험 링크: [Mac OS](https://web.sdk.qcloud.com/trtc/electron/download/solution/TUIRoom-Electron/TUIRoom-Electron-mac-latest.zip) 및 [Windows](https://web.sdk.qcloud.com/trtc/electron/download/solution/TUIRoom-Electron/TUIRoom-Electron-windows-latest.zip)를 다운로드하여 TUIRoom Electron의 더 많은 기능을 체험할 수 있습니다.
[Github](https://github.com/tencentyun/TUIRoom)을 클릭하여 TUIRoom 코드를 다운로드할 수 있으며, [TUIRoom Electron Demo 프로젝트 빠른 실행](https://github.com/tencentyun/TUIRoom/tree/main/Electron) 문서를 참고하여 TUIRoom Electron 데모 프로젝트를 빠르게 실행할 수도 있습니다.
이 문서는 TUIRoom Electron 컴포넌트를 기존 프로젝트에 통합하는 방법을 보여줍니다.

## 컴포넌트 통합
TUIRoom 컴포넌트는 Vue3 + TS + Pinia + Element Plus + SCSS를 사용하여 개발되었으므로 프로젝트는 Electron + Vue3 + TS를 기반으로 해야 합니다.

[](id:step1)
### 1단계: Tencent Cloud TRTC 및 IM 서비스 활성화
TUIRoom은 Tencent Cloud의 TRTC 및 IM 서비스를 기반으로 개발되었습니다.

1. **Tencent Real-Time Communication(TRTC) 애플리케이션 생성**
	- 아직 Tencent Cloud 계정이 없다면 먼저 [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)를 생성하고 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)을 완료하십시오.
	- [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 **애플리케이션 관리 > 애플리케이션 생성**을 클릭하여 새로운 애플리케이션을 생성합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b0f61355af812d8ae822a5df2252d709.png)
2. **TRTC 키 정보 가져오기**
  1. 생성된 애플리케이션을 **애플리케이션 목록 > 애플리케이션 정보**에서 찾아 클릭하여 SDKAppID를 확인합니다. 비즈니스 격리에 사용되는 TRTC 애플리케이션 ID입니다. 즉, SDKAppID 값이 다른 호출은 상호 연결될 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3e70316dabad631ddebb156033a77798.png)
  2. **애플리케이션 관리 > 퀵 스타트** 탭을 선택하여 애플리케이션의 secretKey를 봅니다. TRTC의 승인된 사용을 위한 인증 자격 UserSig를 생성하기 위해 SDKAppID와 함께 사용해야 하는 TRTC 애플리케이션 키입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2323fa87ff3308e2eaa95e66d9be6726.png)
3. **UserSig 발급**
    UserSig란 Tencent Cloud가 설계한 일종의 보안 서명으로, 악성 해커가 귀하의 클라우드 서비스 사용권을 도용하는 것을 방지합니다. TUIRoom을 초기화하려면 UserSig 매개변수를 제공해야 합니다.
	- 디버깅 및 실행 중에 UserSig 계산 방법 방법은 [디버깅 및 실행 단계에서 UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.
	- 프로덕션 환경에서 userSig를 발급하는 방법은 [정식 실행 단계에서 UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.
[](id:step2)

### 2단계: TUIRoom 컴포넌트 다운로드 및 복사
1. 기존 Electron + Vue3 + TypeScript 프로젝트를 엽니다. 없는 경우 이 템플릿 [Github](https://github.com/electron-vite/electron-vite-vue/tree/v1.0.0)을 사용하여 Electron + Vue3 + TS 예시를 생성합니다.
>! 
>- 본문에서 설명하는 통합 단계는 electron-vite-vue 템플릿 프로젝트 버전 1.0.0을 기반으로 합니다.
>- electron-vite-vue 템플릿 프로젝트의 최신 버전의 디렉터리 구조가 조정되었습니다. 최신 버전을 사용해야 하는 경우 본 문서를 참고하여 디렉터리 및 구성을 조정할 수 있습니다.

2. 템플릿 프로젝트가 성공적으로 생성되면 다음 스크립트를 실행합니다.
```bash
cd electron-vite-vue
npm install
npm run dev
```
3. [TUIRoom 코드](https://github.com/tencentyun/TUIRoom)를 복제하거나 다운로드하고 `TUIRoom/Electron/packages/renderer/src/TUIRoom` 폴더를 프로젝트의 `packages/renderer/src/`에 복사합니다.

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

1. **종속성 설치**
 - 개발 환경 종속성을 설치합니다.
```bash
npm install sass typescript unplugin-auto-import unplugin-vue-components -S -D
```
 - 프로덕션 환경 종속성을 설치합니다.
```bash
npm install element-plus events mitt pinia trtc-electron-sdk tim-js-sdk tsignaling -S
```
2. **Pinia 등록**
TUIRoom은 방 데이터 관리를 위해 Pinia를 사용합니다. 프로젝트 엔트리 파일 `packages/renderer/src/main.ts`에 Pinia를 등록해야 합니다.
```javascript
// src/main.ts 파일
import { createPinia } from 'pinia';

const app = createApp(App);
// Pinia 등록
createApp(App)
  .use(createPinia())
  .mount('#app')
  .$nextTick(window.removeLoading)
```
3. **element-plus 컴포넌트의 주문형 가져오기 구성**
	- TUIRoom은 element-plus UI 컴포넌트를 사용합니다. 모든 element-plus 컴포넌트를 가져오지 않으려면 요청 시 로딩하도록 `packages/renderer/vite.config.ts`에서 구성해야 합니다.
>! 다음 구성 항목이 새로 추가되었습니다. 기존 Vite 구성 항목을 삭제하지 마십시오.

```javascript
// vite.config.ts
import AutoImport from 'unplugin-auto-import/vite';
import Components from 'unplugin-vue-components/vite';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';
const path = require('path');

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
        additionalData: `
          @use '${path.resolve(__dirname, 'src/TUIRoom/assets/style/element.scss')}' as *;
        `,
      },
    },
  },
});
```
	- 한편, element-plus UI 컴포넌트가 스타일을 제대로 표시할 수 있도록 하려면 엔트리 파일 `packages/renderer/src/main.ts`에 element-plus 컴포넌트 스타일을 로딩해야 합니다.
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css'
import 'element-plus/theme-chalk/el-message-box.css'
```
4. **trtc-electron-sdk 가져오기**
UI 레이어에서 import 문을 사용하여 `trtc-electron-sdk`를 가져오려면 `packages/renderer/vite.config.ts`를 다음과 같이 구성해야 합니다(그렇지 않으면 require 문을 사용해야 함).
>! resolve의 구성을 다음으로 바꿉니다.
```javascript
// vite.config.ts

export default defineConfig({
	// ...
	plugins: [
    resolve(
      {
        "trtc-electron-sdk": `
          const TRTCCloud = require("trtc-electron-sdk");
          const TRTCParams = TRTCCloud.TRTCParams;
          const TRTCAppScene = TRTCCloud.TRTCAppScene;
          const TRTCVideoStreamType = TRTCCloud.TRTCVideoStreamType;
          const TRTCScreenCaptureSourceType = TRTCCloud.TRTCScreenCaptureSourceType;
          const TRTCVideoEncParam = TRTCCloud.TRTCVideoEncParam;
          const Rect = TRTCCloud.Rect;
          const TRTCAudioQuality = TRTCCloud.TRTCAudioQuality;
          const TRTCScreenCaptureSourceInfo = TRTCCloud.TRTCScreenCaptureSourceInfo;
          const TRTCDeviceInfo = TRTCCloud.TRTCDeviceInfo;
          const TRTCVideoQosPreference = TRTCCloud.TRTCVideoQosPreference;
          const TRTCQualityInfo = TRTCCloud.TRTCQualityInfo;
          const TRTCStatistics = TRTCCloud.TRTCStatistics;
          const TRTCVolumeInfo = TRTCCloud.TRTCVolumeInfo;
          const TRTCDeviceType = TRTCCloud.TRTCDeviceType;
          const TRTCDeviceState = TRTCCloud.TRTCDeviceState;
          const TRTCBeautyStyle = TRTCCloud.TRTCBeautyStyle;
          const TRTCVideoResolution = TRTCCloud.TRTCVideoResolution;
          const TRTCVideoResolutionMode = TRTCCloud.TRTCVideoResolutionMode;
          const TRTCVideoMirrorType = TRTCCloud.TRTCVideoMirrorType;
          const TRTCVideoRotation = TRTCCloud.TRTCVideoRotation;
          const TRTCVideoFillMode = TRTCCloud.TRTCVideoFillMode;
          export { 
            TRTCParams,
            TRTCAppScene,
            TRTCVideoStreamType,
            TRTCScreenCaptureSourceType,
            TRTCVideoEncParam,
            Rect,
            TRTCAudioQuality,
            TRTCScreenCaptureSourceInfo,
            TRTCDeviceInfo,
            TRTCVideoQosPreference,
            TRTCQualityInfo,
            TRTCStatistics,
            TRTCVolumeInfo,
            TRTCDeviceType,
            TRTCDeviceState,
            TRTCBeautyStyle,
            TRTCVideoResolution,
            TRTCVideoResolutionMode,
            TRTCVideoMirrorType,
            TRTCVideoRotation,
            TRTCVideoFillMode,
          };
          export default TRTCCloud.default;
        `,
      }
    ),
    ]
	// ...
});
```
5. **env.d.ts 구성**

    - `packages/renderer/src/env.d.ts`에서 env.d.ts 파일을 다음과 같이 구성합니다.

>! env.d.ts에 아래 코드를 추가하십시오. 파일에서 기존 구성을 삭제하지 마십시오.

```javascript
// env.d.ts

declare module 'tsignaling/tsignaling-js' {
  import TSignaling from 'tsignaling/tsignaling-js';
  export default TSignaling;
}

declare module 'tim-js-sdk' {
  import TIM from 'tim-js-sdk';
  export default TIM;
}

```
6. **프로젝트에 동적 import가 있는 경우 es 모듈을 생성하기 위해 빌드 구성을 수정해야 합니다.**
    - `packages/renderer/vite.config.ts`의 구성을 다음과 같이 수정합니다.
>! 파일에 아래 코드를 추가합니다. 기존 Vite 구성을 삭제하지 마십시오. 프로젝트에 동적 impor가 없는 경우 이 단계를 건너뛰십시오!

```javascript
// vite.config.ts

export default defineConfig({
	// ...
	build: {
        rollupOptions: {
          output: {
              format: 'es'
          }
        }
    },
});
```

[](id:step5)
### 5단계: 개발 환경 실행
콘솔에서 스크립트를 실행하여 개발 환경을 실행합니다. 그런 다음 사용할 브라우저에서 TUIRoom 컴포넌트가 포함된 페이지를 엽니다.
[2단계](#step2)의 스크립트를 사용하여 Electron + Vue3 + TS 프로젝트를 생성하는 경우 다음을 수행해야 합니다.

1. 개발 환경 명령어를 실행합니다.
```bash
npm run dev
```
>! TUIRoom은 element-plus 컴포넌트를 온디맨드로 불러오기 때문에 개발 환경 라우팅 페이지가 처음 로드될 때 반응이 느려지고 element-plus 컴포넌트가 온디맨드로 로딩된 후 정상적으로 사용할 수 있습니다. 이 로딩은 패키징 후 페이지 로딩에 영향을 미치지 않습니다.
2. TUIRoom 컴포넌트의 기능을 사용해 보십시오.

[](id:step6)
### 6단계: 설치 프로그램 생성 및 실행

터미널 창에서 다음 명령을 실행하여 `release` 디렉터리에 설치 프로그램을 생성합니다.

```
npm run build
```

>! Mac 설치 패키지는 Mac 컴퓨터로, Windows 설치 패키지는 Windows 컴퓨터로만 구축할 수 있습니다.

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
| roomData.shareUserId  | string | 선택 사항, 화면 공유에 사용되는 UserId, `shareUserId = share_${userId}`여야 하며, 화면 공유 기능이 없는 경우 불필요 |
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

| 매개변수                          | 유형   | 의미                                                         |
| ----------------------------- | ------ | -------------------------------------- |
| roomId                        | number | 방 ID                                |
| roomParam                     | Object | 선택 사항                                 |
| roomParam.isOpenCamera        | string | 선택 사항, 방에 입장할 때 카메라 켜기 여부, 기본값은 No                       |
| roomParam.isOpenMicrophone    | string | 선택 사항, 방 입장 시 마이크 켜기 여부, 기본값은 No                       |
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
    if （info.code === 0) {
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
    if （info.code === 0) {
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
    if （info.code === 0) {
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
    if （info.code === 0) {
      console.log(‘참석자 방 퇴장 완료’)
    }
  }
</script>
```