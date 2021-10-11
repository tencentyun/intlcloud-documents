このドキュメントは2つの部分から成り、ブラウザで実行できる一連の音声通話ソリューションを実装する方法についてご紹介しています。
- 第1部：サービスをアクティブ化する方法を紹介し、提供するDemoを行います。
- 第2部：TRTCCallingコンポーネントを使用して、独自の音声通話機能をすばやく構築する方法についてご紹介します。

## 環境要件
最新バージョンのChromeブラウザをご使用ください。現在、デスクトップのChromeブラウザはTRTC Web SDKをサポートしており、関連機能は比較的整っていますので、Chromeブラウザを使用して体験することをお勧めします。

TRTCCallingは以下のポートに依存してデータ送信を行っていますので、これらをファイアウォール・ホワイトリストに追加してください。設定が完了したら、[公式サイト Demo](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html)にアクセスして体験していただけば、設定が有効かどうかチェックすることができます。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com

現在、このソリューションは、次のプラットフォームをサポートしています。

| OS |          ブラウザタイプ          | ブラウザの最小バージョン要件 |
| :------: | :--------------------------: | :----------------: |
|  Mac OS  |     デスクトップ版Safariブラウザ     |        11+         |
|  Mac OS  |     デスクトップ版Chromeブラウザ     |        56+         |
|  Mac OS  |     デスクトップ版Firefoxブラウザ     |        56+         |
|  Mac OS  |      デスクトップ版Edgeブラウザ      |        80+         |
|  Windows  |     デスクトップ版Chromeブラウザ     |        56+         |
| Windows  | デスクトップ版QQブラウザ（クイックコア） |       10.4+        |
|  Windows  |     デスクトップ版Firefoxブラウザ     |        56+         |
|  Windows  |      デスクトップ版Edgeブラウザ      |        80+         |

## テストDemo実行

[](id:step1)
### 手順1：アプリケーションの新規作成
1.[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、実名認証を完了します。
2．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
3. アプリケーション名（例：`TestTRTC`）を入力し、【作成】をクリックします。

[](id:step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Web/js/debug/GenerateTestUserSig.js`ファイルを見つけて開きます。
3. `GenerateTestUserSig.js`のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 


4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step4)
### 手順4：Demoの実行
1. Demoディレクトリに次のコマンドを順番に入力します。
```
npm install
npm run serve
```
2. Chromeブラウザを起動し、リンク`http://localhost:8080/`を開きます。すべてが正常であれば、Demo実行インターフェースは次の図のようになります。
3. ユーザーIDを入力し、【ログイン】をクリックして、【音声通話】を選択します。
4. 呼び出し先のユーザーIDを入力し、【呼出】をクリックします。
5. 音声通話を開始できます。


## 独自の音声通話の作成
### 手順1：TRTCCallingコンポーネントの統合
>?
>- 0.6.0以降は、[trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk)、[tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk)および[tsignaling](https://www.npmjs.com/package/tsignaling)の依存関係を手動でインストールする必要があります。
>- trtc-calling-js.jsのボリュームを縮小し、アクセス側で使用されているtrtc-js-sdk、tim-js-sdkおよびtsignalingのバージョン競合を回避するために、trtc-calling-js.jsは、外部依存関係としてtrtc-js-sdk、tim-js-sdk、tsignalingをパッケージ化しているので、使用する前に依存関係を手動でインストールする必要があります。

<dx-codeblock>
::: javascript javascript
// npm方式でのインストール
  npm install trtc-js-sdk --save

  npm install tim-js-sdk --save

  npm install tsignaling --save

  npm install trtc-calling-js --save
:::
</dx-codeblock>
<dx-codeblock>
::: html html
//スクリプト方式によってtrtc-calling-jsを使用する必要がある場合は、順序どおりに次のリソースをインポートする必要があります。

  <script src="./trtc.js"></script>
  <script src="./tim-js.js"></script>
  <script src="./tsignaling.js"></script>
  <script src="./trtc-calling-js.js"></script>
:::
</dx-codeblock>

### 手順2：TRTCCallingオブジェクトの新規作成
TRTCCallingオブジェクトを新規作成し、SDKAppIDパラメータをお客様のSDKAppIDに設定します。
```javascript
import TRTCCalling from 'trtc-calling-js';


let options = {
  SDKAppID: 0, // アクセスするときは、0をお客様のSDKAppIDに置き換える必要があります。
  // v0.10.2から、timパラメータを追加します
  // timパラメータはサービス内にすでに存在するTIMインスタンスに使用され、TIMインスタンスの一意性を保証します。
  tim: tim
};
const trtcCalling = new TRTCCalling(options);
```

### 手順3：ログインの完了
```javascript
trtcCalling.login({
  userID,
  userSig,
});
```

### 手順4：1v1通話の実現
- **発呼者：特定ユーザーを呼び出す**
```javascript
trtcCalling.call({
  userID,  //ユーザーID
  type: 2, //通話タイプ。0-不明、1-音声通話、2-ビデオ通話
  timeout  //招待タイムアウト時間、単位s（秒）
});
```
- **着呼者：新しい呼び出しに応答**
```javascript
// 応答
trtcCalling.accept({
  inviteID, //招待ID。1回の招待を表示
  roomID,   //通話ルーム番号ID
  callType  //0-不明、1-音声通話、2-ビデオ通話
});
//拒否します
trtcCalling.reject({ 
  inviteID, //招待ID。1回の招待を表示
  isBusy //通話中の有無。0-不明、1-音声通話、2-ビデオ通話
})
```
- **通話の終了**
```javascript
trtcCalling.hangup()
```
