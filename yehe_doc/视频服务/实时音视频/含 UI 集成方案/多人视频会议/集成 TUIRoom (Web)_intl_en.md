## Overview

`TUIRoom` is an open-source audio/video component that comes with UI elements. It allows you to quickly integrate conference capabilities including screen sharing and chat into your project.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports up to 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

![](https://qcloudimg.tencent-cloud.cn/raw/d3778fc1655141b5a53e65c5ba4cfa08.png)


Click [here](https://web.sdk.qcloud.com/component/tuiroom/index.html) to try out more features of `TUIRoom`.
Click [here](https://github.com/tencentyun/TUIRoom) to download the `TUIRoom` code and refer to [this document](https://github.com/tencentyun/TUIRoom/tree/main/Web) to run the `TUIRoom` web demo.
This document shows you how to integrate the `TUIRoom` web component into your existing project.

## Integration
The `TUIRoom` component is developed using Vue 3 + TypeScript + Pinia + Element Plus + SCSS, so your project must be based on Vue 3 + TypeScript.

[](id:step1)

### Step 1. Activate the TRTC service
`TUIRoom` is based on TRTC and IM.

1. **Create a TRTC application**
	- If you don’t have a Tencent Cloud account yet, [sign up](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327) for one first.
	- In the [TRTC console](https://console.cloud.tencent.com/trtc), click **Application Management** on the left sidebar and then click **Create Application**.
![](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)
2. **Get the SDKAppID and key**
  1. On the **Application Management** page, find the application you created, and click **Application Info** to view its `SDKAppID` (different applications cannot communicate with each other).
![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)

  2. Select the **Quick Start** tab to view the application's secret key. Each `SDKAppID` corresponds to a secret key. They are used to generate the signature (`UserSig`) required to legitimately use TRTC services.
![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)

3. **Generate UserSig**
    `UserSig` is a security signature designed by Tencent Cloud to prevent attackers from accessing your Tencent Cloud account. It is required when you initialize the `TUIRoom` component.
	- [How do I calculate UserSig for debugging?](https://intl.cloud.tencent.com/document/product/647/35166#how-do-i-calculate-.3Ccode.3Eusersig.3C.2Fcode.3E-during-debugging-and-running.3F)
	- [How do I calculate UserSig for production?](https://intl.cloud.tencent.com/document/product/647/35166#how-do-i-calculate-.3Ccode.3Eusersig.3C.2Fcode.3E-during-production.3F)


[](id:step2)
### Step 2. Download and copy the `TUIRoom` component
1. Click [here](https://github.com/tencentyun/TUIRoom) to clone or download the `TUIRoom` repository code.
2. Open your Vue3 + TypeScript project. You can use the build tool Vite or Webpack. If you don’t have a Vue3 + TypeScript project, create a template using either of the following two methods:
<dx-tabs>
::: Create a Vue3 + Vite + TypeScript template
```bash
npm create vite@latest TUIRoom-demo -- --template vue
```
<dx-alert infotype="notice">During the creation process, press Enter first, select "Vue", and then select "vue-ts".</dx-alert>

After the template is generated, run the script below:

```
cd TUIRoom-demo
npm install
npm run dev
```
:::
::: Create a Vue3 + Webpack + Typescript template
```bash
// Install Vue CLI. If you use Vue CLI 4.x, your Node.js version must be v10 or later.
npm install -g @vue/cli
// Create a Vue3 + Webpack + TypeScript template
vue create TUIRoom-demo
```
<dx-alert infotype="notice">Select "Manually select features" as the template generation mode. For other settings, refer to the figure below:</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/800412fb72b8e092f41fd06d5272601b.png)

After the template is generated, run the script below:
```
cd TUIRoom-demo
npm run serve
```
:::
</dx-tabs>
3. Copy the `TUIRoom/Web/src/TUIRoom` folder to the project's `src/` directory.

[](id:step3)
### Step 3. Import the `TUIRoom` component

1. Import the `TUIRoom` component into your webpage, such as `App.vue`.
	- The `TUIRoom` component classifies users as hosts and members and offers APIs including [init](#init), [createRoom](#createroom), and [enterRoom](#enterroom).
	- Hosts and members can call [init](#init) to initialize application and user data. Hosts can call [createRoom](#createroom) to create and enter rooms. Members can call [enterRoom]( #enterroom) to join the rooms created by hosts.
```javascript
<template>
	<room ref="TUIRoomRef"></room>
</template>

<script setup lang="ts">
	import { ref, onMounted } from 'vue';
	// Import the `TUIRoom` component. Be sure to use the correct import path.
	import Room from './TUIRoom/index.vue';
	// Get the `TUIRoom` component elements used to call the component’s APIs
	const TUIRoomRef = ref();

	 onMounted(async () => {
		// Initialize the `TUIRoom` component
		// A host needs to initialize the `TUIRoom` component before creating a room
		// A member needs to initialize the `TUIRoom` component before entering a room
		await TUIRoomRef.value.init({
			// Get the `SDKAppID` (see step 1)
			sdkAppId: 0,
			// The user's unique ID in your business
			userId: '',
			// For local development and debugging, you can quickly generate a `userSig` at https://console.cloud.tencent.com/trtc/usersigtool. Note that `userSig` and `userId` have a one-to-one correspondence.
			userSig: '',
			// The user's username in your business
			userName: '',
			// The URL of the user's profile photo in your business
			userAvatar: '',
			// The user's unique ID used for screen sharing. It must be in the format of `share_${userId}`. You don’t need to pass this parameter if you don’t need the screen sharing feature.
			shareUserId: '',
			// Refer to steps 1-3 above and use the `SDKAppID` and `shareUserId` to generate `shareUserSig` 
			shareUserSig: '',
		})
		 // By default, a room is created at this point. During actual implementation, you can specify when to call handleCreateRoom()
		await handleCreateRoom();
	})

	// The host creates a room. Call this API only when you need to create a room.
	async function handleCreateRoom() {
		// `roomId` is the ID of the room to enter, which must be a number.
		// The valid values of `roomMode` are `FreeSpeech` (free speech mode) and `ApplySpeech` (request-to-speak mode). The default value is `FreeSpeech`, which is the only supported mode currently.
		// `roomParam` specifies whether to turn on the mic/camera upon room entry, as well as the default media device ID to use
		const roomId = 123456;
		const roomMode = 'FreeSpeech';
		const roomParam = {
			isOpenCamera: true,
			isOpenMicrophone: true,
		}
		await TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
	}

	// The member enters a room. This API is called by a member to join an existing room.
	async function handleEnterRoom() {
		// `roomId` is the ID of the room entered by the user, which must be a number.
		// `roomParam` specifies whether to turn on the mic/camera upon room entry, as well as the default media device ID to use
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

>! Copy the above code to your webpage and replace the parameter values for the APIs with the actual values.

[](id:step4)
### Step 4. Configure the development environment
After the `TUIRoom` component is imported, in order to ensure that the project can run normally, the following configurations are required:

<dx-tabs>
::: Set up the Vue3 + Vite + TypeScript development environment

1. **Install dependencies**
	- Install development environment dependencies:
```bash
npm install sass typescript unplugin-auto-import unplugin-vue-components -S -D
```
	- Install production environment dependencies:
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Register Pinia**
`TUIRoom` uses Pinia for room data management. You need to register Pinia in the project entry file `src/main.ts`.
```javascript
// `src/main.ts` file
import { createPinia } from 'pinia';

const app = createApp(App);
// Register Pinia
app.use(createPinia()); 
app.mount('#app');
```
3. **Import Element Plus components**
  - `TUIRoom` uses Element Plus UI components, which you need to import in `vite.config.ts`. You can import only the components you need.
<dx-alert infotype="notice">Add the code in the file. Do not delete the existing configuration.</dx-alert>

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
  - Meanwhile, in order to ensure that Element Plus UI components can display styles properly, you need to load Element Plus component styles in the entry file `src/main.ts`.
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```
:::
::: Set up the Vue3 + Webpack + TypeScript environment
1. **Install dependencies**
  - Install development environment dependencies:
```bash
npm install sass sass-loader typescript unplugin-auto-import unplugin-vue-components unplugin-element-plus @types/events -S -D
```
  - Install production environment dependencies:
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Register Pinia**
`TUIRoom` uses Pinia for room data management. You need to register Pinia in the project entry file `src/main.ts`.
```javascript
// `src/main.ts` file
import { createPinia } from 'pinia';

const app = createApp(App);
// Register Pinia
app.use(createPinia()); 
app.mount('#app');
```
3. **Import Element Plus components**
  - `TUIRoom` uses Element Plus UI components, which you need to import in `vue.config.js`. You can manually import only the components you need.

<dx-alert infotype="notice">Add the code in the file. Do not delete the existing configuration.</dx-alert>

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
      // Specify the theme color when importing the components
      ElementPlus({
        useSource: true
      })
    ]
  }
})

```
  - Meanwhile, in order to ensure that Element Plus UI components can display styles properly, you need to load Element Plus component styles in the entry file `src/main.ts`.
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```
4. **Configure the TS file**
 Add the following configuration to `src/shims-vue.d.ts`:
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
### Step 5. Run your project in the development environment
In the console, execute the development environment script. Then, open the page integrated with the `TUIRoom` component with a browser.

- **If you used the script in [step 2](#step2) to create a Vue + Vite + TypeScript project**, follow the steps below:

1. Run the development environment command.
```bash
npm run dev
```
2. Open `http://localhost:3000/` in a browser.
>! Because Element Plus components are imported manually, it may take a relatively long time for the page to load in the development environment for the first time. This will not be an issue after packaging.

3. Try out the features of the `TUIRoom` component.

- **If you used the script in [step 2](#step2) to create a Vue + Webpack + TypeScript project**, follow the steps below:
1. Run the development environment command.
```bash
npm run serve
```

2. Open `http://localhost:8080/` in a browser.
>! If an ESLint error occurs in the `src/TUIRoom` directory, you can disable ESLint by adding `/src/TUIRoom` to the `.eslintignore` file.

3. Try out the features of the `TUIRoom` componen


[](id:step6)
### Step 6. Commercial Scenario Deployment

1.Package dist file

```bash
npm run build
```

>? Note: Please check the package.json file for the actual packaging command

2.Deploy the dist file to the server

>?Note：Commercial Scenario requires the use of https domain name
![](https://qcloudimg.tencent-cloud.cn/raw/53efdc1d1692a21946cb6c94ddea40e5.png)






## Appendix: TUIRoom APIs
### TUIRoom APIs
#### init

This API is used to initialize `TUIRoom` data. All users using `TUIRoom` need to call this API first.
```javascript
TUIRoomRef.value.init(roomData);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| --------------------- | ------ | ------------------------------------------------------------ |
| roomData              | object |                                                              |
| roomData.sdkAppId     | number | The SDKAppID.                                              |
| roomData.userId       | string | The unique user ID.                                                |
| roomData.userSig      | string | The UserSig.                                               |
| roomData.userName     | string | The username.                                                   |
| roomData.userAvatar   | string | The user profile photo.                                                   |
| roomData.shareUserId  | string | The `UserId` used for screen sharing, which must be in the format of `share_${userId}`. You don’t need to pass this parameter if you don’t need the screen sharing feature. |
| roomData.shareUserSig | string | `UserSig` used for screen sharing, which is optional.                           |


#### createRoom

This API is used by a host to create a room.
```javascript
TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ----------------------------- | ------ | ------------------------------------------------------------ |
| roomId                        | number | The room ID.                                                      |
| roomMode                      | string | The speech mode, including `FreeSpeech` (free speech) and `ApplySpeech` (request-to-speak). The default value is `FreeSpeech`, which is the only supported mode currently. |
| roomParam                     | Object | Optional                                                       |
| roomParam.isOpenCamera        | string | Whether to turn on the camera upon room entry. This parameter is optional and the default is no.                       |
| roomParam.isOpenMicrophone    | string | Whether to turn on the mic upon room entry. This parameter is optional and the default is no.                       |
| roomParam.defaultCameraId     | string | The ID of the default camera, which is optional.                                    |
| roomParam.defaultMicrophoneId | string | The ID of the default mic, which is optional.                                    |
| roomParam.defaultSpeakerId    | String | The ID of the default speaker, which is optional.                                    |

#### enterRoom
This API is used by a member to enter a room.
```javascript
TUIRoomRef.value.enterRoom(roomId, roomParam);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----------------------------- | ------ | -------------------------------------- |
| roomId                        | number | The Room ID.                                                      |
| roomParam                     | Object | Optional                                                       |
| roomParam.isOpenCamera        | string | Whether to turn on the camera upon room entry. This parameter is optional and the default is no.                       |
| roomParam.isOpenMicrophone    | string | Whether to turn on the mic upon room entry. This parameter is optional and the default is no.                       |
| roomParam.defaultCameraId     | string | The ID of the default camera, which is optional.                                    |
| roomParam.defaultMicrophoneId | string | The ID of the default mic, which is optional.                                    |
| roomParam.defaultSpeakerId    | String | The ID of the default speaker, which is optional.                                    |


### TUIRoom events

#### onRoomCreate
A room was created.
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-create="handleRoomCreate"></room>
</template>

<script setup lang="ts">
  // Import the `TUIRoom` component. Be sure to use the correct import path.
  import Room from './TUIRoom/index.vue';
  
  function handleRoomCreate(info) {
    if (info.code === 0) {
      console.log('Room created successfully')
    }
  }
</script>
```

#### onRoomEnter

A member entered the room.
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-enter="handleRoomEnter"></room>
</template>

<script setup lang="ts">
  // Import the `TUIRoom` component. Be sure to use the correct import path.
  import Room from './TUIRoom/index.vue';
  
  function handleRoomEnter(info) {
    if (info.code === 0) {
      console.log('Entered room successfully')
    }
  }
</script>
```

#### onRoomDestory

The host closed the room.
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-destory="handleRoomDestory"></room>
</template>

<script setup lang="ts">
  // Import the `TUIRoom` component. Be sure to use the correct import path.
  import Room from './TUIRoom/index.vue';
  
  function handleRoomDestory(info) {
    if (info.code === 0) {
      console.log('The host closed the room successfully')
    }
  }
</script>
```

#### onRoomExit
A member exited the room.

```javascript
<template>
  <room ref="TUIRoomRef" @on-room-exit="handleRoomExit"></room>
</template>

<script setup lang="ts">
  // Import the `TUIRoom` component. Be sure to use the correct import path.
  import Room from './TUIRoom/index.vue';
  
  function handleRoomExit(info) {
    if (info.code === 0) {
      console.log('The member exited the room successfully')
    }
  }
</script>
```

#### onKickOff

A member was removed from the room by the host.

```javascript
<template>
  <room ref="TUIRoomRef" @on-kick-off="handleKickOff"></room>
</template>

<script setup lang="ts">
  // Import the `TUIRoom` component. Be sure to use the correct import path.
  import Room from './TUIRoom/index.vue';
  
  function handleKickOff(info) {
    if (info.code === 0) {
      console.log('The member was removed from the room by the host')
    }
  }
</script>
```
