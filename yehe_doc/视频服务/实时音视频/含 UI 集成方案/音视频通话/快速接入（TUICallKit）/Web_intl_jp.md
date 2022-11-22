ここでは、最短の時間でTUICallKitコンポーネントの統合を完了する方法についてご説明します。このドキュメントに沿って操作することで、次の重要手順を完了し、最終的にUIを完備したビデオ通話機能を手にすることができます。

コンポーネントの効果を体験したい場合は、[TUICallKit demoクイックスタート](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)をご参照ください。

アクセスの前に、デスクトップブラウザがオーディオビデオサービスをサポートしているかどうかをご確認ください。詳細な要件については[環境要件](https://www.tencentcloud.com/document/product/647/50993#1b83cb8f-4c54-43f3-863d-579786ab78bc)をご参照ください。

[](id:step1)
##  ステップ1：サービスのアクティブ化

TUICallKitはTencent Cloudの[IM](https://intl.cloud.tencent.com/document/product/1047/35448)と、[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)という2つの有料PaaSサービスをベースに構築したオーディオビデオ通信コンポーネントです。以下の手順で関連のサービスをアクティブ化し、60日間の無料トライアルサービスを体験することができます。

1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、**新しいアプリケーションの作成**をクリックし、ポップアップしたダイアログボックスにアプリケーション名を入力して**OK**をクリックします。
![img](https://qcloudimg.tencent-cloud.cn/raw/ce2e34f7cd1cd14679fc5decffb469af.png)

2. 作成したアプリケーションをクリックし、**基本設定**ページに進み、ページ右下隅の**TRTCサービスのアクティブ化**機能エリアで**無料体験**をクリックすると、TUICallKitの7日間無料トライアルサービスをアクティブ化することができます。
![img](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

3. 同じページで**SDKAppID**と**キー**を見つけて記録します。これらは後ほど使用します。
	![img](https://qcloudimg.tencent-cloud.cn/raw/8349ac97b261279606316331488784c3.png)
	- SDKAppID：IMのアプリケーションIDです。業務の分離、すなわち異なるSDKAppIDの通話が互いに接続できないようにするために用いられます。
	- Secretkey：IMのアプリケーションキーです。SDKAppIDとペアで使用する必要があり、IMサービスを正当に使用するための認証用証明書UserSigの発行に用いられます。このKeyは次のステップ5で使用します。

[](id:step2)
## ステップ2：TUICallKitコンポーネントのインポート

1. [GitHub](https://github.com/tencentyun/TUICallKit/tree/main/Web)からTUICallKitソースコードをダウンロードします。`TUICallKit/Web`フォルダをコピーして自身のプロジェクトの`src/components`フォルダに置きます。例えば次のようになります。
![img](https://qcloudimg.tencent-cloud.cn/image/document/b90fbef92c17090688ebc0c9b4577037.png)

1. このフォルダに進み、実行に必要な依存をインストールします
```shell
cd ./src/components/TUICallKit/Web 
yarn                                  // 現在の環境にyarnパッケージ管理ツールがインストールされていない場合は、npm install -g yarnを使用してインストールできます
```

[](id:step3)
## ステップ3：UserSigの生成

UserSigを生成済みの場合は、この手順をスキップして[ステップ4](#step4)に進んでください

1. 初期化設定の関連パラメータのうち、SDKAppIDやキーなどの情報は[IMコンソール](https://console.cloud.tencent.com/im)から取得できます。対象のアプリケーションカードをクリックして、アプリケーションの基本設定ページに進みます。例えば次のようになります。
![img](https://qcloudimg.tencent-cloud.cn/raw/95ab37db3b8c371d7fa86af24b5a6aad.png)

2. 基本情報エリアで、クリックしてキーを表示し、キー情報をコピーして`TUICallKit/Web/demos/basic/public/debug/GenerateTestUserSig.js`ファイルに保存します。
![img](https://qcloudimg.tencent-cloud.cn/raw/8cbbf4515e40f0e3bc0062b2c17a635e.png)

3. ステップ4では、`GenerateTestUserSig.js`の`genTestUserSig(userID)`関数を使用してuserSigを計算することができます。例えば次のようになります。
```javascript
import * as GenerateTestUserSig from "../public/debug/GenerateTestUserSig.js";
const { userSig } = GenerateTestUserSig.genTestUserSig(userID);
```

4. viteを起動ツールとして使用する場合は、[viteのインポートの問題](https://www.tencentcloud.com/document/product/647/50993#f020d04e-5439-4679-bc6e-716f7329b60a)にもご注意ください。

>! 公開前にこのファイルは必ず削除してください。ここで言及するUserSigの取得方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのクイックスタート機能デバッグにのみ適しています**。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し、動的にUserSigを取得します。詳細については、[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/1047/34385)をご参照ください。

[](id:step4)
## ステップ4：TUICallKitコンポーネントの呼び出し

表示したいページでTUICallKitのコンポーネントを呼び出すと、通話ページを表示することができます。

1. 次のようにTUICallKit UIをインポートします。
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

2. ユーザーログインし、電話をかけます
    2.1 [TUIKit](https://www.tencentcloud.com/document/product/1047/50061)のキットをすでに使用している場合は下記のコードをインポートし、TUICallKitがプラグインであることを宣言する必要があります。使用していない場合は下記のコードのインポートは必要ありません。
  ```
    import { TUICallKit } from './src/components/TUICallKit/Web/src/index';
    TUIKit.use(TUICallKit);
  ```

  2.2 ログインしたい場所で、次を実行します。
  ```
    import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
    TUICallKitServer.init({ SDKAppID, userID, userSig }); 
  ```
>? userSigは[ステップ3](#step3)で取得できます

  2.3 電話をかけたい場所で、次を実行します。
	```
		import { TUICallKitServer } from './src/components/TUICallKit/Web/src/index';
		TUICallKitServer.call({ userID, type }); // 2人通話
		TUICallKitServer.groupCall({ userIDList, groupID, type }); // 多人数通話
	```
	完了するとすぐに最初の電話をかけることができます。より詳細なインターフェースパラメータについては、[インターフェースドキュメント](https://www.tencentcloud.com/document/product/647/51015)をご参照ください。

3. 発展インターフェース
	このコンポーネントでは`beforeCalling`および`afterCalling`という2つのコールバックを提供しており、業務側に現在の通話状態を通知するために用いられます。
	- `beforeCalling`：通話前に実行します
	- `afterCalling`：通話後に実行します

例えば[サンプルdemo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/src/App.vue)のように、<`TUICallKit />;`コンポーネントの表示と折りたたみに用いることができます。
```javascript
function beforeCalling() {
  console.log("通話前にこの関数を実行");
}
function afterCalling() {
  console.log("通話後にこの関数を実行");
}
```
```javascript
<TUICallKit :beforeCalling="beforeCalling" :afterCalling="afterCalling"/>
```

## その他のドキュメント

- [TUICallKit API](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/API.md)
- [TUICallKit demoクイックスタート](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [TUICallKitインターフェースカスタマイズガイド](https://github.com/tencentyun/TUICallKit/blob/main/Web/docs/UI%20Customization.md)
- [TUICallKit (Web) に関するよくあるご質問](https://www.tencentcloud.com/document/product/647/51024)


## よくあるご質問

### 1. UserSigはどのように生成しますか。

>- UserSigの発行方法は、UserSigの計算コードをサーバーに統合し、プロジェクトのインターフェース向けに提供する方法となります。UserSigが必要なときは、プロジェクトから業務サーバーにリクエストを送信し動的にUserSigを取得します。その他の詳細については[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/1047/34385?lang=en&pg=)をご参照ください。

### 2. viteのインポートの問題

プロジェクトをviteで作成した場合は、ファイルパッケージの違いにより、`index.html`に`lib-generate-test-usersig.min.js`をインポートする必要があります
```javascript
// index.html
<script src="/public/debug/lib-generate-test-usersig.min.js"> </script>
```

また、元の`GenerateTestUserSig.js`にimportしたメソッドのアノテーションを行います

```javascript
// import * as LibGenerateTestUserSig from './lib-generate-test-usersig.min.js'
```

### 3. 環境要件

#### ブラウザのバージョン要件

| OS | ブラウザタイプ                   | ブラウザの最小バージョン要件 |
| -------- | ---------------------------- | ------------------ |
| Mac OS   | デスクトップ版Safariブラウザ         | 11+                |
| Mac OS   | デスクトップ版Chromeブラウザ         | 56+                |
| Mac OS   | デスクトップ版Firefoxブラウザ        | 56+                |
| Mac OS   | デスクトップ版Edgeブラウザ           | 80+                |
| Windows  | デスクトップ版Chromeブラウザ         | 56+                |
| Windows  | デスクトップ版QQブラウザ（クイックコア） |       10.4+        |
| Windows  | デスクトップ版Firefoxブラウザ        | 56+                |
| Windows  | デスクトップ版Edgeブラウザ           | 80+                |

>?詳細な互換性の照会については、[ブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)をご参照ください。また、[TRTC検査ページ](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)でオンライン検査することも可能です。

#### ネットワーク環境の要件

TUICallKitを使用する際、ユーザーはファイアウォールの制限によって正常にオーディオビデオ通話が行えない可能性があります。[ファイアウォール制限の対応関連](https://www.tencentcloud.com/document/product/647/35164)をご参照の上、対応するポートおよびドメイン名をファイアウォールのホワイトリストに追加してください。

#### ウェブサイトドメイン名プロトコルの要件

ユーザーのセキュリティ、プライバシーなどの問題を考慮し、ブラウザは本ドキュメントの連結コンポーネントの全機能をHTTPSプロトコルでしか正常に使用できないようにウェブページを制限しています。本番環境のユーザーが製品機能をスムーズに体験できるようにするため、ウェブサイトは**https://**プロトコルのドメイン名にデプロイしてください。

>! ローカル開発には、`http：// localhost`または`file://`プロトコルを使用してアクセスできます。

URLドメイン名およびプロトコルのサポート状況については、以下の表をご参照ください。

| ユースケース     | プロトコル             | 受信（再生） | 送信（プッシュ） | 画面共有 | 備考 |
| ------------ | ---------------- | ------------ | ------------ | -------- | ---- |
| 本番環境     | HTTPSプロトコル       | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| 本番環境     | HTTPプロトコル        | サポートあり         | サポートなし       | サポートなし   | -    |
| ローカルデバッグ環境 | http://localhost | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| ローカルデバッグ環境 | http://127.0.0.1 | サポートあり         | サポートあり         | サポートあり     | -    |
| ローカルデバッグ環境 | http://[ローカルマシンIP]  | サポートあり         | サポートなし       | サポートなし   | -    |
| ローカルデバッグ環境 | file:///         | サポートあり         | サポートあり         | サポートあり     | -    |
