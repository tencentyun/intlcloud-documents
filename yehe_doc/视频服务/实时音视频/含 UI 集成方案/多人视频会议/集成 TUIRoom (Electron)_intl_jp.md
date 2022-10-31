## コンポーネントの説明

TUIRoomは、UIを含むオープンソースオーディオビデオコンポーネントです。TUIRoomを統合することにより、ビジネスにおいて、オーディオビデオルーム、画面共有、チャットなどの機能を速やかにオンラインにすることができます。Electron端末のTUIRoomの基本機能は下図のとおりです。

>? TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期してアクティブ化することができます。 IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブ化すると、関連するIM SDKの体験版がデフォルトでアクティブ化されます。これは100 DAUのみをサポートします。

![](https://qcloudimg.tencent-cloud.cn/raw/a98627586f82847a061a3695ad15ad26.png)

オンライン体験リンク[Mac OS版](https://web.sdk.qcloud.com/trtc/electron/download/solution/TUIRoom-Electron/TUIRoom-Electron-mac-latest.zip)および[Windows版](https://web.sdk.qcloud.com/trtc/electron/download/solution/TUIRoom-Electron/TUIRoom-Electron-windows-latest.zip)をクリックしてダウンロードすると、TUIRoom Electronのより多くの機能を体験することができます。
[Github](https://github.com/tencentyun/TUIRoom)をクリックしてTUIRoomのコードをダウンロードし、[TUIRoom Electronデモプロジェクトクイックスタート](https://github.com/tencentyun/TUIRoom/tree/main/Electron)のドキュメントを参照し、TUIRoom Electronデモプロジェクトをクイックスタートすることもできます。
現在の業務でElectron端末のTUIRoomコンポーネントを統合する必要がある場合は、こちらのドキュメントをご参照ください。

## コンポーネントの統合
TUIRoomコンポーネントはVue3 + TS + Pinia + Element Plus + SCSSを使用して開発されています。プロジェクトの統合には、Electron + Vue3 + TSの技術スタックを使用する必要があります。

[](id:step1)
### ステップ1： Tencent Cloud TRTCおよびIMサービスのアクティブ化
TUIRoomは、Tencent Cloud TRTCとIMサービスをベースに開発されています。

1. **TRTCアプリケーションの作成**
	- Tencent Cloudアカウントをまだお持ちでない場合は、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了してください。
	- [TRTCコンソール](https://console.cloud.tencent.com/trtc) で、**アプリケーション管理>アプリケーションの作成** をクリックし、新たなアプリケーションを作成します。
![](https://qcloudimg.tencent-cloud.cn/raw/b0f61355af812d8ae822a5df2252d709.png)
2. **TRTCアプリケーションおよびキー情報の取得**
  1. **アプリケーション管理 > アプリケーション情報**でSDKAppID の情報を取得します。SDKAppIDはTRTCのアプリケーションIDです。業務の分離、すなわち異なるSDKAppIDの通話が互いに接続できないようにするために用いられます。
![](https://qcloudimg.tencent-cloud.cn/raw/3e70316dabad631ddebb156033a77798.png)
  2. **アプリケーション管理 > クイックマスター**でアプリケーションのsecretKey情報を取得します。SecretKeyはTRTCのアプリケーションキーです。SDKAppIDとペアで使用する必要があり、TRTCサービスを正当に使用するための認証用証明書UserSigの発行に用いられます。
![](https://qcloudimg.tencent-cloud.cn/raw/2323fa87ff3308e2eaa95e66d9be6726.png)
3. **UserSigの発行**
    UserSigとは、悪意ある攻撃者によるクラウドサービスの使用権の盗用を防ぐために、Tencent Cloudによって設計された、セキュリティ保護された署名です。TUIRoomの初期化にはUserSigパラメータの提供が必要です。
	- デバッグスタート段階でuserSigを発行する方法については、[デバッグスタート段階でのUserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
	- 本番環境でuserSigを発行する方法については、[本番環境でのUserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
[](id:step2)

### ステップ2：TUIRoomコンポーネントのダウンロードとコピー
1. 業務側にすでにあるElectron + Vue3 + TSプロジェクトを開きます。Electron + Vue3 + TSプロジェクトがない場合は、このテンプレート[Github](https://github.com/electron-vite/electron-vite-vue/tree/v1.0.0)によってElectron + Vue3 + TSのテンプレートプロジェクトを生成することができます。
>! 
>- このドキュメントで説明する統合手順はelectron-vite-vueテンプレートプロジェクトのバージョン1.0.0をベースにしています。
>- electron-vite-vueテンプレートプロジェクトの最新バージョンではディレクトリ構造が調整されています。最新バージョンを使用される場合は、このドキュメントを参照してご自身でディレクトリの調整と設定を行うことができます。

2. テンプレートプロジェクトの生成に成功後、次のスクリプトを実行します。
```bash
cd electron-vite-vue
npm install
npm run dev
```
3. [Github](https://github.com/tencentyun/TUIRoom)をクリックし、TUIRoomリポジトリコードをクローンまたはダウンロードし、`TUIRoom/Electron/packages/renderer/src/TUIRoom`フォルダを既存のプロジェクトの`packages/renderer/src/`ディレクトリ下にコピーします。

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
			// 本文ステップ1 > 第3段階を参照し、sdkAppIdとshareUserIdを使用してshareUserSigを発行してください 
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

>! ページ内で上記のコードをコピーした後、TUIRoomインターフェースのパラメータを実際のデータに変更する必要があります。

[](id:step4)
### ステップ4：本番環境の設定

TUIRoomコンポーネントをインポートした後、プロジェクトが正常に実行されることを確認するため、次の設定を行います。

1. **依存のインストール**
 - 開発環境の依存をインストールします。
```bash
npm install sass typescript unplugin-auto-import unplugin-vue-components -S -D
```
 - 本番環境の依存をインストールします。
```bash
npm install element-plus events mitt pinia trtc-electron-sdk tim-js-sdk tsignaling -S
```
2. **Piniaの登録**
TUIRoomはPiniaを使用してルームデータの管理を行うため、プロジェクトのエントリーファイルでPiniaの登録を行う必要があります。プロジェクトのエントリーファイルは`packages/renderer/src/main.ts`ファイルです。
```javascript
// src/main.tsファイル
import { createPinia } from 'pinia';

const app = createApp(App);
// Piniaの登録
createApp(App)
  .use(createPinia())
  .mount('#app')
  .$nextTick(window.removeLoading)
```
3. **element-plusを必要に応じてインポートするよう設定**
	- TUIRoomはelement-plus UIコンポーネントを使用します。すべてのelement-plusコンポーネントをインポートしてしまわないように、`packages/renderer/vite.config.ts`で、element-plusコンポーネントを必要に応じてロードするように設定しておく必要があります。
>! 以下の設定項目は増分設定です。すでに存在するVite設定項目を削除しないでください。

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
	- また、element-plusに付帯するUIコンポーネントがスタイルを正常に表示できるようにするため、エントリーファイル`packages/renderer/src/main.ts`でelement-plusコンポーネントスタイルをロードする必要があります。
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css'
import 'element-plus/theme-chalk/el-message-box.css'
```
4. **trtc-electron-sdkのインポート**
UIレイヤーでimport方式により`trtc-electron-sdk`をインポートするためには、コードスタイルを統一します。これを行わない場合はrequire方式でのインポートが必要になります。`packages/renderer/vite.config.ts`での設定が必要です。
>! 以下の設定項目でresolveの内容を置き換えます。
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
5. **env.d.tsファイル設定**

    - env.d.tsファイル設定は`packages/renderer/src/env.d.ts`で行う必要があります。

>! 以下の設定項目は増分設定です。すでに存在するenv.d.tsファイル設定を削除しないでください。

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
6. **プロジェクト内にimport動的ロードが存在する場合は、アーキテクチャ設定を変更し、esモジュールをパッケージ化して生成する必要があります**
    - esモジュールをパッケージ化して生成するには、`packages/renderer/vite.config.ts`内で設定を行う必要があります。
>! プロジェクト内にimport動的ロードが存在しない場合は、この設定を行わないでください。以下の設定項目は増分設定です。すでに存在するVite設定項目を削除しないでください。

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
### ステップ5：開発環境の実行
コンソールの実行開発環境でスクリプトを実行し、TUIRoomの含まれるページをブラウザで開くと、そのページでTUIRoomコンポーネントを使用することができます。
[ステップ2](#step2)のスクリプトを使用してElectron + Vue3 + TSプロジェクトを作成する場合は、次の事項を行う必要があります。

1. 開発環境コマンドを実行します。
```bash
npm run dev
```
>! TUIRoomはelement-plusコンポーネントを必要に応じてインポートするため、開発環境のルーティングページでの初回ロード時に反応がやや遅くなりますが、必要なelement-plusのロードが完了すると正常に使用できるようになります。element-plusの必要に応じてのロードがパッケージ化後のページロードに影響することはありません。
2. TUIRoomコンポーネント機能を体験します。

[](id:step6)
### ステップ6：インストールパッケージの作成、実行

コマンドライン端末で、次のコマンドを実行してインストールパッケージを作成します。作成したインストールパッケージは`release`ディレクトリにあり、インストールの実行が可能です。

```
npm run build
```

>! Mac PCを使用したMacインストールパッケージの作成、Windows PCを使用したWindowsインストールパッケージの作成のみ可能です。

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
| roomData.shareUserId  | string | 任意入力。ユーザーが画面共有を行う際のUserIdであり、`shareUserId = share_${userId}`である必要があります。画面共有機能がなければ渡さなくても結構です |
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