## コンポーネントの説明

TUIRoomは、UIを含むオープンソースのオーディオビデオコンポーネントであり、TUIRoomの統合により、業務にオーディオビデオルーム、画面共有、チャットなどの機能を速やかに立ち上げることができます。Web側のTUIRoomの基本機能は下図のとおりです。

>?TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブにすると、デフォルトでは、100DAUまでサポートするIM SDK体験版もアクティブになります。

![](https://qcloudimg.tencent-cloud.cn/raw/357aa08b7c0d291993a9f4803453e9f0.png)

[TUIRoomオンラインリンク](https://web.sdk.qcloud.com/component/tuiroom/index.html)をクリックすると、TUIRoomのその他の機能を体験できます。
[Github](https://github.com/tencentyun/TUIRoom)をクリックしてTUIRoomコードをダウンロードし、[TUIRoom Webデモプロジェクトのクイックスタート](https://github.com/tencentyun/TUIRoom/tree/main/Web)ドキュメントを参照してTUIRoom Webデモプロジェクトをクイックスタートできます。
Web側のTUIRoomコンポーネントを既存のビジネスに統合する場合は、このドキュメントをご参照ください。

## コンポーネントの統合
TUIRoomコンポーネントは、Vue3+TS+Pinia+Element Plus+SCSSを使用して開発されており、インポート先のプロジェクトにはVue3+TSテクノロジースタックが必要です。

[](id:step1)
### ステップ1：Tencent Cloud TRTCとInstant Messagingサービスを有効化します
TUIRoomは、Tencent Cloud TRTCとInstant Messagingサービスをベースに開発されたものです。

ステップ1. **TRTCアプリケーションを作成します**
  - Tencent Cloudアカウントをお持ちでない場合は、[Tencent Cloudアカウントに登録](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)をお願いします。
  - [TRTCコンソール](https://console.cloud.tencent.com/trtc) で、**アプリケーション管理>アプリケーションの作成** をクリックし、新たなアプリケーションを作成します。
![](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)
2. **TRTCキー情報およびキー情報の取得**
  1. **アプリケーション管理>アプリケーション情報**でSDKAppID情報を取得します。SDKAppIDは、TRTCのアプリケーションIDであり、サービス分離のために使用され、すなわち、異なるSDKAppIDによる通話が相互に通じません。
![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)
  2. **アプリケーション管理>クイックマスター**でアプリケーションのsecretKey情報を取得します。SecretKeyはTRTCのアプリケーションキーであり、SDKAppIDとペアで使用してください。TRTCサービスを正当に使用するための認証用チケットUserSigをチェックアウトします。
![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)
3. **UserSigの発行**
    UserSigとは、悪意ある攻撃者によるクラウドサービスの使用権の盗用を防ぐために、Tencent Cloudによって設計されたセキュリティ保護された署名です。TUIRoomを初期化するには、UserSigパラメータを提供してください。
	- デバッグのクイックスタートフェーズにおいてuserSigを発行する方法については、[デバッグのクイックスタートフェーズにおけるUserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166#how-do-i-calculate-.3Ccode.3Eusersig.3C.2Fcode.3E-during-debugging-and-running.3F)をご参照ください。
	- 本番環境でのuserSigの発行方法については、[本番稼働フェーズでのUserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166#how-do-i-calculate-.3Ccode.3Eusersig.3C.2Fcode.3E-during-production.3F)をご参照ください。

[](id:step2)

### ステップ2：TUIRoomコンポーネントのダウンロードとコピー
1. [Github](https://github.com/tencentyun/TUIRoom)をクリックして、TUIRoomウェアハウスコードをクローンまたはダウンロードします。
2. ビジネス側の既存のVue3+TSプロジェクトを開き、Vue3+TSプロジェクトが存在しない場合は、次のスクリプトを使用してVue 3.0+VITE+TSのテンプレートプロジェクトを生成します。
```bash
npm create vite@latest TUIRoom-demo -- --template vue
```
>! テンプレートプロジェクト生成用スクリプトを実行する際には、まず直接エンターキーを押し、次に「Vue」を選択し、最後に「vue-ts」を選択します。

テンプレートプロジェクトが正常に生成されたら、次のスクリプトを実行します。
```
cd TUIRoom-demo
npm install
npm run dev
```
3.`TUIRoom/Web/src/TUIRoom`フォルダを既存のプロジェクトsrc/ディレクトリにコピーします。

[](id:step3)

### ステップ3：TUIRoomコンポーネントのインポート

1. ページでTUIRoomコンポーネントを参照します。例：TUIRoomコンポーネントを`App.vue`コンポーネントにインポートします。
	- TUIRoomコンポーネントは、ユーザーをキャスターロールと一般メンバーロールに分けます。コンポーネントは外部に[init](#init)、[createRoom](#createroom)、[enterRoom](#enterroom)の各メソッドを提供します。
	- キャスターと一般メンバーは[init](#init)メソッドを使用してTUIRoomコンポーネントの適用とユーザーデータを初期化できます。キャスターは[createRoom](#createroom)メソッドを使用してルームを作成して参加します。一般メンバーは[enterRoom](#enterroom)メソッドを使用してキャスターが作成したルームに参加できます。
```javascript
<template>
	<room ref="TUIRoomRef"></room>
</template>

<script setup lang="ts">
	import { ref, onMounted } from 'vue';
	// TUIRoomコンポーネントをインポートします。インポートパスが正しいことを確認してください。
	import Room from './TUIRoom/index.vue';
	// TUIRoomコンポーネントのメソッドを呼び出すために、TUIRoomコンポーネント要素を取得します
	const TUIRoomRef = ref();

	 onMounted(async () => {
		// TUIRoomコンポーネントの初期化
		// キャスターはルームを作成する前にTUIRoomコンポーネントを初期化してください
		// 一般メンバーは、ルームに参加する前にTUIRoomコンポーネントを初期化してください
		await TUIRoomRef.value.init({
			// sdkAppIdを取得するにはステップ1をご参照ください 
			sdkAppId: 0,
			// ビジネスにおけるユーザーの一意の識別ID
			userId: '',
			// ローカル開発デバッグは、userSigをhttps://console.cloud.tencent.com/trtc/usersigtoolページにすばやく生成します。userSigとuserIdは1対1で対応していることに注意してください
			userSig: '',
			// ユーザーがビジネスで使用するニックネーム
			userName: '',
			// ユーザーがビジネスで使用するアバターへのリンク
			userAvatar: '',
			// 画面共有のためにユーザーが使用する一意のID。shareUserId=`share_${userId}`が必要です。画面共有機能が要求されない場合は渡す必要がありません
			shareUserId: '',
			// このドキュメントのステップ1>3を参照し、sdkAppIdとshareUserIdを使用してshareUserSigを発行してください 
			shareUserSig: '',
		})
		 // デフォルトではルームの作成が実行され、実際のインポートはオンデマンドでhandleCreateRoomメソッドが実行されます
		await handleCreateRoom();
	})

	// キャスターがルームを作成します。このメソッドはルームが作成されたときにのみ呼び出されます
	async function handleCreateRoom() {
		// roomIdはユーザーが参加するルーム番号です。roomIdタイプはnumber型が必要です
		// roomModeは、'FreeSpeech'（自由発言モード）と'ApplySpeech'（举手発言モード）の2モードを含み、デフォルトは'FreeSpeech'です。現在、自由発言モードだけをサポートします
		// roomParamは、ユーザがルームに参加したときのデフォルトの動作を指定します（デフォルトでマイクをオンにするかどうか、デフォルトでカメラをオンにするかどうか、デフォルトのメディアデバイスID）
		const roomId = 123456;
		const roomMode = 'FreeSpeech';
		const roomParam = {
			isOpenCamera: true,
			isOpenMicrophone: true,
		}
		await TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
	}

	// 一般メンバーがルームに参加します。このメソッドは作成されたルームに一般メンバーが参加するときに呼び出されます
	async function handleEnterRoom() {
		// roomIdはユーザーが参加するルーム番号です。roomIdタイプはnumber型が必要です
		// roomParamは、ユーザがルームに参加したときのデフォルトの動作を指定します（デフォルトでマイクをオンにするかどうか、デフォルトでカメラをオンにするかどうか、デフォルトのメディアデバイスID）
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

>! ページで上記のコードをコピーした後、TUIRoomインターフェースのパラメータを実際のデータに変更する必要があります。

### ステップ4：開発環境の設定

TUIRoomコンポーネントがインポートされたら、プロジェクトが正常に機能するように、次の設定を行ってください

1. **依存関係のインストール**
	- 開発環境の依存関係をインストールします。
```bash
npm install sass typescript unplugin-auto-import unplugin-vue-components -S -D
```
  - 本番環境の依存関係をインストールします。
```bash
npm install element-plus events mitt pinia rtc-beauty-plugin tim-js-sdk trtc-js-sdk tsignaling -S
```
2. **Piniaの登録**
TUIRoomはPiniaを使用してルームのデータ管理を行います。Piniaをプロジェクトエントリファイルに登録してください。プロジェクトエントリファイルは`src/main.ts`ファイルです。
```javascript
// src/main.tsファイル
import { createPinia } from 'pinia';

const app = createApp(App);
// pinia登録
app.use(createPinia()); 
app.mount('#app');
```
3. **svg-iconコンポーネントのSVGアイコンロードを設定します**
TUIRoomはすべてのアイコンリソース（SVGファイル）を`src/TUIRoom/assets/icons/svg`ディレクトリに配置するので、`vite.config.ts`ファイルでSVGアイコンのロード方法を設定してください。
>! 次のコンフィグレーション項目は、増分コンフィグレーションです。既存のViteコンフィグレーション項目は削除しないでください。

```javascript
// vite.config.ts
import { createSvg } from './src/TUIRoom/assets/icons/index';

export default defineConfig({
	// ...
	plugins: [
		// ...
		createSvg('./src/TUIRoom/assets/icons/svg/'),
	],
	// ...
});
```
4. **element-plusをオンデマンドでインポートするための設定**
	- TUIRoomはelement-plus UIコンポーネントを使用します。すべてのelement-plusコンポーネントがインポートされないようにするには、`vite.config.ts`でelement-plusコンポーネントをオンデマンドでロードするように設定してください。
>! 次のコンフィグレーション項目は、増分コンフィグレーションです。既存のViteコンフィグレーション項目は削除しないでください。

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

  - また、UI付きのelement-plus コンポーネントがスタイルを正しく表示するためには、エントリファイル`src/main.ts`にelement-plusコンポーネントスタイルをロードしてください。
```
// src/main.ts
import 'element-plus/theme-chalk/el-message.css';
import 'element-plus/theme-chalk/el-message-box.css';
```

[](id:step5)
### ステップ5：開発環境の実行
コンソールで開発環境実行スクリプトを実行し、ブラウザを使用してTUIRoomを含むページを開くと、ページ内でTUIRoomコンポーネントを使用できます。

[ステップ2](#step2)のスクリプトを使用してVue+TSプロジェクトを生成するする場合は、次の手順を実行してください。

1. 開発環境コマンドを実行します。
```bash
npm run dev
```
2. ブラウザでページ`http://localhost:3000/`を開きます。
>! TUIRoomはオンデマンドでelement-plusコンポーネントをインポートするため、開発環境のルーティングページが最初にロードされたときの反応が遅くなり、element-plusがオンデマンドでロードされるのを待つと正常に機能するようになります。element-plusのオンデマンドロードは、パッケージング後のページロードには影響しません。
3. TUIRoomコンポーネント機能を体験します。



## 付録：TUIRoom API
### TUIRoomインターフェース

#### init

TUIRoomデータを初期化します。TUIRoomを使用するすべてのユーザーはinitメソッドを呼び出してください。
```javascript
TUIRoomRef.value.init(roomData);
```

パラメータは下表に示すとおりです：

| パラメータ     | タイプ     | 意味         |
| --------------------- | ------ | ------------------------------------------------------------ |
| roomData              | object |                                                              |
| roomData.sdkAppId     | number | お客様のSDKAppId                                              |
| roomData.userId       | string | ユーザーの唯一ID                                                |
| roomData.userSig      | string | ユーザーのUserSig                                               |
| roomData.userName     | string | ユーザーのニックネーム                                                   |
| roomData.userAvatar   | string | ユーザーのプロフィール写真                                                   |
| roomData.shareUserId  | string | 非必須。ユーザーが画面共有を行うUserIdです。shareUserId=`share_${userId}`が要求され、画面共有機能がない場合は渡されません |
| roomData.shareUserSig | string | 非必須。ユーザーが画面共有を行うUserSig                           |


#### createRoom

キャスターがルームを作成します。
```javascript
TUIRoomRef.value.createRoom(roomId, roomMode, roomParam);
```

パラメータは下表に示すとおりです：

| パラメータ     | タイプ     | 意味         |
| ----------------------------- | ------ | ------------------------------------------------------------ |
| roomId                        | number | ルームID                                                      |
| roomMode                      | string | ルームモードです。'FreeSpeech'（自由発言モード）と'ApplySpeech'（举手発言モード）を含み、デフォルトは'FreeSpeech'です。現在、自由発言モードだけをサポートします |
| roomParam                     | Object | 非必須                                                       |
| roomParam.isOpenCamera        | string | 非必須。入室はカメラをオンにするかどうか。デフォルトはオフです                       |
| roomParam.isOpenMicrophone    | string | 非必須。入室はマイクをオンにするかどうか。デフォルトはオフです                       |
| roomParam.defaultCameraId     | string | 非必須。デフォルトはカメラ装置のID                                    |
| roomParam.defaultMicrophoneId | string | 非必須。デフォルトはマイク装置のID                                    |
| roomParam.defaultSpeakerId    | String | 非必須。デフォルトはスピーカー装置のID                                    |

#### enterRoom
一般メンバーがルームに参加します。
```javascript
TUIRoomRef.value.enterRoom(roomId, roomParam);
```

パラメータは下表に示すとおりです：

| パラメータ     | タイプ     | 意味         |
| ----------------------------- | ------ | -------------------------------------- |
| roomId                        | number | ルームID                                                      |
| roomParam                     | Object | 非必須                                                       |
| roomParam.isOpenCamera        | string | 非必須。入室はカメラをオンにするかどうか。デフォルトはオフです                       |
| roomParam.isOpenMicrophone    | string | 非必須。入室はマイクをオンにするかどうか。デフォルトはオフです                       |
| roomParam.defaultCameraId     | string | 非必須。デフォルトはカメラ装置のID                                    |
| roomParam.defaultMicrophoneId | string | 非必須。デフォルトはマイク装置のID                                    |
| roomParam.defaultSpeakerId    | String | 非必須。デフォルトはスピーカー装置のID                                    |


### TUIRoomイベント

#### onRoomCreate
ルーム作成のコールバック。
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-create="handleRoomCreate"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいことを確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomCreate(info) {
    if （info.code === 0) {
      console.log('ルーム作成成功')
    }
  }
</script>
```

#### onRoomEnter

入室コールバック。
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-enter="handleRoomEnter"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいことを確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomEnter(info) {
    if （info.code === 0) {
      console.log('入室成功')
    }
  }
</script>
```

#### onRoomDestory

キャスターがルームを廃棄する通知。
```javascript
<template>
  <room ref="TUIRoomRef" @on-room-destory="handleRoomDestory"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいことを確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomDestory(info) {
    if （info.code === 0) {
      console.log('キャスターが廃棄することに成功しました')
    }
  }
</script>
```

#### onRoomExit
一般メンバーが退室する通知。

```javascript
<template>
  <room ref="TUIRoomRef" @on-room-exit="handleRoomExit"></room>
</template>

<script setup lang="ts">
  // TUIRoomコンポーネントをインポートします。インポートパスが正しいことを確認してください
  import Room from './TUIRoom/index.vue';
  
  function handleRoomExit(info) {
    if （info.code === 0) {
      console.log('一般メンバーが退室することに成功しました')
    }
  }
</script>
```

