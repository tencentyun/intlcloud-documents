このドキュメントは2つの部分から成り、ブラウザで実行できる一連の音声通話ソリューションを実装する方法についてご紹介しています。
- 第1部：サービスをアクティブ化する方法を紹介し、提供するDemoを行います。
- 第2部：TRTCCallingコンポーネントを使用して、独自のビデオ通話機能をすばやく構築する方法についてご紹介します。

## 環境要件
最新バージョンのChromeブラウザをご使用ください。現在、デスクトップのChromeブラウザはTRTCデスクトップブラウザSDKをサポートしており、関連特性は比較的万全です。従って、Chromeブラウザを使用して体験することをお勧めします。

- TRTCCallingは以下のポートに依存してデータ送信を行っていますので、これらをファイアウォール・ホワイトリストに追加してください。設定が完了したら、[公式サイト Demo]にアクセスして体験していただけば、設定が有効かどうかチェックすることができます。
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

<span id ="step1"></span>
### 手順1：アプリケーションの新規作成

- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了します。実名認証を行っていないユーザーは、中国大陸のリアルタイム音声通話のインスタンスを購入できません。
2．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
3．【今すぐ開始】をクリックし、例えば、`TestTRTC`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

<span id ="step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. マウスを対応するカードに動かして、【[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Web/TRTCScenesDemo/trtc-calling-web)】をクリックしてGitHubに移動し（または【[ZIP](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/H5_latest.zip?_ga=1.195966252.185644906.1567570704)】をクリック）、関連するSDKおよび付属のDemoのソースコードをダウンロードします。
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。


<span id ="step3"></span>
### 手順3：Demoプロジェクトファイルの設定

1. [手順2](#step2)でダウンロードしたソースコードパッケージを解凍します。
2. `Web/TRTCScenesDemo/trtc-calling-web/public/debug/GenerateTestUserSig.js` ファイルを見つけて開きます。
3. `GenerateTestUserSig.js`のファイルの関連するパラメータを設定します。
  - SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。
  - SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!
>- 本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

<span id ="step4"></span>
### 手順4：Demoの動作
1. npmコマンドラインウィンドウに次のコマンドを入力します。
```
npm install
npm run serve
```
2. Chromeブラウザを起動し、リンク`http://localhost:8080/` を開きます。すべてが正常であれば、Demo実行インターフェースは次の図のようになります。
3. ユーザーIDを入力し、【ログイン】をクリックして、【音声通話】を選択します。
4. 呼び出し先のユーザーIDを入力し、【呼出】をクリックします。
5. 音声通話を開始できます。


## 独自の音声通話の作成
### 手順1：TRTCCallingコンポーネントの統合
>?
>- 0.6.0以降は、 [trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk) 、 [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk) および[tsignaling](https://www.npmjs.com/package/tsignaling) の依存関係を手動でインストールする必要があります。
>- trtc-calling-js.jsのボリュームを縮小し、アクセス側で使用されているtrtc-js-sdk、tim-js-sdkおよびtsignalingのバージョン競合を回避するために、trtc-js-sdk、tim-js-sdkおよびtsignalingはtrtc-calling-js.jsにパッケージ化されなくなっているので、使用する前に依存関係を手動でインストールする必要があります。

```javascript
  npm i trtc-js-sdk --save
  npm i tim-js-sdk --save
  npm i tsignaling --save
  npm i trtc-calling-js --save



  //スクリプト方式によってtrtc-calling-jsを使用する場合は、順序どおりにまずtrtc.jsを手動でインポートする必要があります。
  <script src="./trtc.js"></script>
  
  // 続いて、tim-js.jsを手動でインポートします。
  <script src="./tim-js.js"></script>
  
  // 次に、tsignaling.jsを手動でインポートします。
  <script src="./tsignaling.js"></script>



  // 最後に、trtc-calling-js.jsを手動でインポートします。
  <script src="./trtc-calling-js.js"></script>
```
### 手順2：TRTCCallingオブジェクトの新規作成
TRTCCallingオブジェクトを新規作成し、SDKAppIDパラメータをお客様のSDKAppIDに設定します。
```javascript
import TRTCCalling from 'trtc-calling-js';


let options = {
  SDKAppID: 0 // アクセスするときは、0をお客様のSDKAppIDに置き換える必要があります。
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

### 手順4： 1v1 通話の実現
#### 発呼者：特定ユーザーを呼び出す
```javascript
trtcCalling.call({
  userID,  //ユーザーID
  type: 2, //通話タイプ、0-不明、1-音声通話、2-ビデオ通話
  timeout  //招待タイムアウト、単位s（秒）
});
```

#### 着呼者：新しい呼び出しに応答
```javascript
// 応答
trtcCalling.accept({
  inviteID, //招待ID、1回の招待を表示
  roomID,   //通話ルーム番号ID
  callType  //0-不明、1-音声通話、2-ビデオ通話
});
// 拒否します
trtcCalling.reject({ 
  inviteID, //招待ID、1回の招待を表示
  isBusy //通話中の有無、0-不明、1-音声通話、2-ビデオ通話
  })
```

#### 通話の終了
```javascript
trtcCalling.hangup()
```
