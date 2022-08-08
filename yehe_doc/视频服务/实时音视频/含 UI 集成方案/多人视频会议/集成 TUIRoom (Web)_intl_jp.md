## コンポーネントの説明

TUIRoomは、UIを含むオープンソースオーディオビデオコンポーネントです。TUIRoomを統合することにより、ビジネスにおいて、オーディオビデオルーム、画面共有、チャットなどの機能を速やかにオンラインにすることができます。Web端末TUIRoomコンポーネントの基本機能は次のとおりです。

>?TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期してアクティブ化することができます。 IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブ化すると、関連するIM SDKの体験版がデフォルトでアクティブ化されます。これは100 DAUのみをサポートします。

![](https://qcloudimg.tencent-cloud.cn/raw/d3778fc1655141b5a53e65c5ba4cfa08.png)


[TUIRoomオンラインリンク](https://web.sdk.qcloud.com/component/tuiroom/index.html)をクリックすると、TUIRoomのその他の機能を体験することができます。
[Github](https://github.com/tencentyun/TUIRoom)をクリックしてTUIRoomのコードをダウンロードし、[TUIRoom Webデモプロジェクトクイックスタート](https://github.com/tencentyun/TUIRoom/tree/main/Electron)のドキュメントを参照し、TUIRoom Webデモプロジェクトをクイックスタートすることができます。
現在の業務でWeb端末のTUIRoomコンポーネントを統合する必要がある場合は、こちらのドキュメントをご参照ください。

## コンポーネントの統合
TUIRoomコンポーネントはVue3 + TS + Pinia + Element Plus + SCSSを使用して開発されています。プロジェクトの統合には、Vue3 + TSの技術スタックを使用する必要があります。

[](id:step1)

### ステップ1： Tencent Cloud TRTCおよびIMサービスのアクティブ化
TUIRoomは、Tencent Cloud TRTCとIMサービスをベースに開発されています。

1. **TRTCアプリケーションの作成**
	- Tencent Cloudアカウントがない場合は、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)を行ってください。
	- [TRTCコンソール](https://console.cloud.tencent.com/trtc) で、**アプリケーション管理>アプリケーションの作成** をクリックし、新たなアプリケーションを作成します。
![](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)
2. **TRTCアプリケーションおよびキー情報の取得**
  1. **アプリケーション管理 > アプリケーション情報**でSDKAppID の情報を取得します。SDKAppIDはTRTCのアプリケーションIDです。業務の分離、すなわち異なるSDKAppIDの通話が互いに接続できないようにするために用いられます。
![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)

  2. **アプリケーション管理 > クイックマスター**でアプリケーションのsecretKey情報を取得します。SecretKeyはTRTCのアプリケーションキーです。SDKAppIDとペアで使用する必要があり、TRTCサービスを正当に使用するための認証用証明書UserSigの発行に用いられます。
![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)

3. **UserSigの発行**
    UserSigとは、悪意ある攻撃者によるクラウドサービスの使用権の盗用を防ぐために、Tencent Cloudによって設計された、セキュリティ保護された署名です。TUIRoomの初期化にはUserSigパラメータの提供が必要です。
	- デバッグスタート段階でuserSigを発行する方法については、[デバッグスタート段階でのUserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
	- 本番環境でuserSigを発行する方法については、[本番環境でのUserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。


[](id:step2)
### ステップ2：TUIRoomコンポーネントのダウンロードとコピー
1. [Github](https://github.com/tencentyun/TUIRoom)をクリックし、TUIRoomリポジトリのコードをクローンまたはダウンロードします。
2. ビジネスサイドで既存のVue3 + TSプロジェクトを開き、ViteとWebpackのパッケージ方式をサポートします。Vue3 + TSのプロジェクトがない場合、以下のいずれかの方法を選択して、テンプレートプロジェクトを生成することができます。
<dx-tabs>
::: Vue3 + Vite + TSのテンプレートプロジェクトの生成
```bash
npm create vite@latest TUIRoom-demo -- --template vue
```
>! テンプレートプロジェクトスクリプトの生成を実行する場合、ステップ1で直接リターンし、ステップ2でVueを選択し、ステップ3でvue-tsを選択します。

Vue3 + Vite + TSテンプレートプロジェクトの生成に成功したら、以下のスクリプトを実行します。
```
cd TUIRoom-demo
npm install
npm run dev
```
:::
::: Vue3 + Webpack + TSテンプレートプロジェクトの生成
```bash
// vue-cliをインストールします。Vue CLI 4.xはNode.jsのv10以上のバージョンが必要なのでご注意ください
npm install -g @vue/cli
::: Vue3 + Webpack + TSテンプレートプロジェクトの作成
vue create TUIRoom-demo
```
<dx-alert infotype="notice">テンプレートプロジェクトスクリプトの生成を実行する場合、テンプレートの生成方式としてManually select featuresを選択し、残りの設定オプションは画像を参照します。</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/800412fb72b8e092f41fd06d5272601b.png)

Vue3 + Webpack + TSテンプレートプロジェクトの生成に成功したら、以下のスクリプトを実行します。
```
cd TUIRoom-demo
npm run serve
```
:::
</dx-tabs>
3. `TUIRoom/Web/src/TUIRoom`フォルダを既存プロジェクトのsrc/ディレクトリにコピーします。

[](id:step3)
### ステップ3：TUIRoomコンポーネントのインポート

1. ページ内にTUIRoomコンポーネントをインポートします。例えば、`App.vue`コンポーネントにTUIRoomコンポーネントをインポートします。
	- TUIRoomコンポーネントはユーザーをキャスターロールと一般メンバーロールに区分します。コンポーネントは外部に対し[init](#init)、[createRoom](#createroom)、[enterRoom](#enterroom)のメソッドを提供します。
	- キャスターと一般メンバーは[init](#init)メソッドによってTUIRoomコンポーネントに対し、アプリケーションとユーザーデータの初期化を行うことができます。キャスターは[createRoom](#createroom) メソッドによってルームを作成し入室することができます。一般メンバーは[enterRoom](#enterroom)メソッドによって、キャスターが作成したルームに入室することができます。
```javascript
<template>
	<room ref="TUIRoomRef"></room>
</template>

<script setup lang="ts">
	import { ref, onMounted } from 'vue';
	// TUIRoomコンポーネントをインポートします。インポートパスが正しいかどうかよく確認してください
	import Room from './TUIRoom/index.vue';
	// TUIRoomコンポーネント要素を取得し、TUIRoomコンポーネントの呼び出しメソッドに用います
	const TUIRoomRef = ref();

	 onMounted(async () => {
		// TUIRoomコンポーネントを初期化します
		// キャスターはルームを作成する前にTUIRoomコンポーネントを初期化する必要があります
		// 一般メンバーは入室前にTUIRoomコンポーネントを初期化する必要があります
		await TUIRoomRef.value.init({
			// sdkAppIdを取得します。ステップ1をご参照ください
			sdkAppId: 0,
			業務// ユーザーの業務における固有の表示IDです
			userId: '',
			// ローカル開発デバッグの場合はhttps://console.cloud.tencent.com/trtc/usersigtoolページでuserSigをすぐに発行できます。userSigとuserIdは対になる関係であることに注意してください
			userSig: '',
			// ユーザーが業務で使用するニックネーム
			userName: '',
			// ユーザーが業務で使用するプロフィール画像リンク
			userAvatar: '',
			// ユーザーが画面共有に用いる固有のIdであり、shareUserId = `share_${userId}`である必要があります。画面共有機能が必要なければ渡さなくても結構です
			shareUserId: '',
			// 本文ステップ1 > ステップ3を参照し、sdkAppIdとshareUserIdを使用してshareUserSigを発行してください 
			shareUserSig: '',
		})
		 // デフォルトではルーム作成が実行されます。実際の統合では必要に応じ、タイミングを見てhandleCreateRoomメソッドを実行することができます
		await handleCreateRoom();
	})

	// キャスターがルームを作成します。このメソッドはルーム作成時にのみ呼び出します
	async function handleCreateRoom() {
		// roomIdはユーザーが入室するルームナンバーです。roomIdのタイプはnumberである必要があります
		// roomModeには'FreeSpeech'(自由発言モード) と'ApplySpeech'(挙手発言モード)の2種類があります。デフォルトでは'FreeSpeech'です。現在は自由発言モードのみサポートされていますのでご注意ください
		// roomParamはユーザーの入室時のデフォルト動作(デフォルトでマイクをオンにするかどうか、デフォルトでカメラをオンにするかどうか、デフォルトのメディアデバイスId)を指定するものです
		const roomId = 123456;
		const roomMode = 'FreeSpeech';
		const roomParam = {
			isOpenCamera: true,
			isOpenMicrophone: true,
		}
		await TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
	}

	// 一般メンバーが入室します。このメソッドは一般メンバーが作成済みのルームに入室する際にのみ呼び出します
	async function handleEnterRoom() {
		// roomIdはユーザーが入室するルームナンバーです。roomIdのタイプはnumberである必要があります
		// roomParamはユーザーの入室時のデフォルト動作(デフォルトでマイクをオンにするかどうか、デフォルトでカメラをオンにするかどうか、デフォルトのメディアデバイスId)を指定するものです
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

<dx-alert infotype="notice">ページ内で上記のコードをコピーした後、TUIRoomインターフェースのパラメータを実際のデータに変更する必要があります。</dx-alert>

[](id:step4)
### ステップ4：本番環境の設定
TUIRoomコンポーネントをインポートした後、プロジェクトが正常に実行されることを確認するため、次の設定を行います。

<dx-tabs>
::: Vue3 + Vite + TSプロジェクトの開発環境の設定

1. **依存のインストール**
	- 開発環境の依存をインストールします。
```bash
npm install sass typescript unplugin-auto-import unplugin-vue-components -S -D
```
  - 本番環境の依存をインストールします。
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Piniaの登録**
TUIRoomはPiniaを使用してルームデータの管理を行うため、プロジェクトのエントリーファイルでPiniaの登録を行う必要があります。プロジェクトのエントリーファイルは`src/main.ts`ファイルです。
```javascript
// src/main.tsファイル
import { createPinia } from 'pinia';

const app = createApp(App);
// Piniaの登録
app.use(createPinia()); 
app.mount('#app');
```
3. **element-plusを必要に応じてインポートするよう設定**
  - TUIRoomはelement-plus UIコンポーネントを使用します。すべてのelement-plusコンポーネントをインポートしてしまわないように、`vite.config.ts`で、element-plusコンポーネントを必要に応じてロードするように設定しておく必要があります。
<dx-alert infotype="notice">以下の設定項目は増分設定です。すでに存在するVite設定項目を削除しないでください。</dx-alert>

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
  - また、element-plusに付帯するUIコンポーネントがスタイルを正常に表示できるようにするため、エントリーファイル`src/main.ts`でelement-plusコンポーネントスタイルをロードする必要があります。
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```
:::
::: Vue3+Webpack+Tsプロジェクトの開発環境の設定
1. **依存のインストール**
  - 開発環境の依存をインストールします。
```bash
npm install sass sass-loader typescript unplugin-auto-import unplugin-vue-components unplugin-element-plus @types/events -S -D
```
  - 本番環境の依存をインストールします。
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Piniaの登録**
TUIRoomはPiniaを使用してルームデータの管理を行うため、プロジェクトのエントリーファイルでPiniaの登録を行う必要があります。プロジェクトのエントリーファイルは`src/main.ts`ファイルです。
```javascript
// src/main.tsファイル
import { createPinia } from 'pinia';

const app = createApp(App);
// Piniaの登録
app.use(createPinia()); 
app.mount('#app');
```
3. **element-plusを必要に応じてインポートするよう設定**
  - TUIRoomはelement-plus UIコンポーネントを使用します。すべてのelement-plusコンポーネントをインポートしてしまわないように、`vue.config.js`で、element-plusコンポーネントを必要に応じてロードするように設定しておく必要があります。
>! 以下の設定項目は増分設定です。すでに存在するvue.config.js設定項目を削除しないでください。

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
      // 必要に応じてインポート時のテーマカラーをカスタマイズ
      ElementPlus({
        useSource: true
      })
    ]
  }
})

```
  - また、element-plusに付帯するUIコンポーネントがスタイルを正常に表示できるようにするため、エントリーファイル`src/main.ts`でelement-plusコンポーネントスタイルをロードする必要があります。
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```
4. **ts宣言ファイルの設定**
 `src/shims-vue.d.ts`ファイルに以下の設定を追加します。
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
### ステップ5：開発環境の実行
コンソールの実行開発環境でスクリプトを実行し、TUIRoomの含まれるページをブラウザで開くと、そのページでTUIRoomコンポーネントを使用することができます。

- [ステップ2](#step2)のスクリプトを使用してVue + Vite + TSプロジェクトを生成する場合は、次の事項を行う必要があります。

1. 開発環境コマンドを実行します。
```bash
npm run dev
```
2. ブラウザでページ`http://localhost:3000/`を開きます。
>! TUIRoomはelement-plusコンポーネントを必要に応じてインポートするため、開発環境のルーティングページでの初回ロード時に反応がやや遅くなりますが、必要なelement-plusのロードが完了すると正常に使用できるようになります。element-plusの必要に応じてのロードがパッケージ化後のページロードに影響することはありません。

3. TUIRoomコンポーネント機能を体験します。

- [ステップ2](#step2)のスクリプトを使用してVue + Webpack + TSプロジェクトを生成する場合は、次の事項を行う必要があります。
1. 開発環境コマンドを実行します
```bash
npm run serve
```

2. ブラウザで`http://localhost:8080/`のページを開きます
> ! 実行中、src/TUIRoomディレクトリでeslintエラーが発生した場合、.eslintignoreファイルに/src/TUIRoomのパスを追加すると、eslintチェックをブロックできます。

3. TUIRoomコンポーネント機能を体験します

## 付録：TUIRoom API
### TUIRoomインターフェース
#### init

TUIRoomデータを初期化します。TUIRoomを使用するすべてのユーザーはinitメソッドを呼び出す必要があります。
```javascript
TUIRoomRef.value.init(roomData);
```

パラメータは下表に示すとおりです。

| パラメータ                  | タイプ   | 意味                                                         |
| --------------------- | ------ | ------------------------------------------------------------ |
| roomData              | object |                                                              |
| roomData.sdkAppId     | number | お客様のSDKAppId                                              |
| roomData.userId       | string | ユーザーの固有ID                                                |
| roomData.userSig      | string | ユーザーのUserSig                                               |
| roomData.userName     | string | ユーザーのニックネーム                                                   |
| roomData.userAvatar   | string | ユーザーのプロフィール画像                                                   |
| roomData.shareUserId  | string | 任意入力。ユーザーが画面共有を行う際のUserIdであり、shareUserId = `share_${userId}`である必要があります。画面共有機能がなければ渡さなくても結構です |
| roomData.shareUserSig | string | 任意入力。ユーザーが画面共有を行う際のUserSig                           |


#### createRoom

キャスターがルームを作成します。
```javascript
TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
```

パラメータは下表に示すとおりです。

| パラメータ                          | タイプ   | 意味                                                         |
| ----------------------------- | ------ | ------------------------------------------------------------ |
| roomId                        | number | ルームID                                                      |
| roomMode                      | string | ルームモード。'FreeSpeech'（自由発言モード）と'ApplySpeech'（挙手発言モード）があり、デフォルトでは'FreeSpeech'です。現在は自由発言モードのみサポートされていますのでご注意ください |
| roomParam                     | Object | 任意入力                                                       |
| roomParam.isOpenCamera        | string | 任意入力。入室時にカメラをオンにするかどうか。デフォルトではオフ                       |
| roomParam.isOpenMicrophone    | string | 任意入力。入室時にマイクをオンにするかどうか。デフォルトではオフ                       |
| roomParam.defaultCameraId     | string | 任意入力。デフォルトのカメラデバイスID                                    |
| roomParam.defaultMicrophoneId | string | 任意入力。デフォルトのマイクデバイスID                                    |
| roomParam.defaultSpeakerId    | String | 任意入力。デフォルトのスピーカーデバイスID                                    |

#### enterRoom
一般メンバーが入室します。
```javascript
TUIRoomRef.value.enterRoom(roomId, roomParam);
```

パラメータは下表に示すとおりです。

| パラメータ                          | タイプ   | 意味                                   |
| ----------------------------- | ------ | -------------------------------------- |
| roomId                        | number | ルームID                                |
| roomParam                     | Object | 任意入力                                 |
| roomParam.isOpenCamera        | string | 任意入力。入室時にカメラをオンにするかどうか。デフォルトではオフ |
| roomParam.isOpenMicrophone    | string | 任意入力。入室時にマイクをオンにするかどうか。デフォルトではオフ |
| roomParam.defaultCameraId     | string | 任意入力。デフォルトではカメラデバイスID              |
| roomParam.defaultMicrophoneId | string | 任意入力。デフォルトではマイクデバイスID              |
| roomParam.defaultSpeakerId    | String | 任意入力。デフォルトではスピーカーデバイスID              |


### TUIRoomイベント

#### onRoomCreate
ルーム作成のコールバックです。
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-create="handleRoomCreate"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいかどうかよく確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomCreate(info) {
    if (info.code === 0) {
      console.log('ルーム作成成功')
    }
  }
</script>
```

#### onRoomEnter

入室コールバックです。
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-enter="handleRoomEnter"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいかどうかよく確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomEnter(info) {
    if (info.code === 0) {
      console.log('入室成功')
    }
  }
</script>
```

#### onRoomDestory

キャスターのルーム破棄通知。
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-destory="handleRoomDestory"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいかどうかよく確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomDestory(info) {
    if (info.code === 0) {
      console.log('キャスターが破棄に成功')
    }
  }
</script>
```

#### onRoomExit
一般メンバーのルーム退出通知。

```javascript
<template>
  <room ref="TUIRoomRef" @on-room-exit="handleRoomExit"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいかどうかよく確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomExit(info) {
    if (info.code === 0) {
      console.log('一般メンバーのルーム退出成功')
    }
  }
</script>
```

#### onKickOff

一般メンバーがキャスターにルームからキックアウトされたときの通知です。

```javascript
<template>
  <room ref="TUIRoomRef" @on-kick-off="handleKickOff"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいかどうかよく確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleKickOff(info) {
    if (info.code === 0) {
      console.log('一般メンバーがキャスターにルームからキックアウト')
    }
  }
</script>
```
