このドキュメントは2つのパートから成り、ブラウザで実行できる一連のビデオ通話ソリューションを実装する方法について説明します。
- パート1：サービスをアクティブ化する方法および提供するDemoのクイックスタートについて説明します。
- パート2：TRTCCallingコンポーネントを使用して、独自のビデオ通話機能をすばやく構築する方法について説明します。

## 環境要件
最新バージョンのChromeブラウザをご使用ください。現在、デスクトップのChromeブラウザはTRTC Web SDKをサポートしており、関連機能は比較的整っていますので、Chromeブラウザを使用して体験することをお勧めします。

- TRTCCallingは以下のポートに依存してデータ送信を行っていますので、これらをファイアウォール・ホワイトリストに追加してください。設定が完了したら、[公式サイトDemo](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html)にアクセスして体験していただけば、設定が有効かどうかをチェックすることができます。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com
具体的には、[ファイアウォール制限の対処関連](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。

## サポートプラットフォーム
現在、このソリューションは、次のプラットフォームをサポートしています。

| OS |          ブラウザタイプ          | ブラウザの最小バージョン要件 |
| :------: | :--------------------------: | :----------------: |
|  Mac OS  |     デスクトップ版Safariブラウザ     |        11+         |
|  Mac OS  |     デスクトップ版Chromeブラウザ     |        56+         |
|  Mac OS  |     デスクトップ版Firefoxブラウザ     |        56+         |
|  Mac OS  |      デスクトップ版Edgeブラウザ      |        80+         |
|  Windows  |     デスクトップ版Chromeブラウザ     |        56+         |
| Windows  | デスクトップ版QQブラウザ（超高速コア） |       10.4+        |
|  Windows  |     デスクトップ版Firefoxブラウザ     |        56+         |
|  Windows  |      デスクトップ版Edgeブラウザ      |        80+         |

>? 互換性照会の詳細については、[ブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)をご参照ください。また、[TRTC検査ページ](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)でオンライン検査することも可能です。


## URLドメイン名プロトコルの制限
| ユースケース     | プロトコル             | 受信（再生） | 送信（マイク・オン） | 画面共有 | 備考 |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| 本番環境     | HTTPSプロトコル        | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| 本番環境     | HTTPプロトコル         | サポートあり         | サポートなし       | サポートなし   |  -    |
| ローカル開発環境 | http://localhost | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| ローカル開発環境 | http://127.0.0.1 | サポートあり         | サポートあり         | サポートあり     |  -    |
| ローカル開発環境 | http://[ローカルマシンIP]  | サポートあり         | サポートなし       | サポートなし   |   -   |
| ローカル開発環境 | file:///         | サポートあり         | サポートあり         | サポートあり     |   -   |


## Demoのクイックスタートテスト
[](id:step1)
### 手順1：アプリケーションの新規作成
1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、実名認証を完了させます。
2. TRTCコンソールにログインし、**開発支援** > [**Demoクイックスタート**](https://console.cloud.tencent.com/trtc/quickstart)を選択します。
3. アプリケーション名（例：TestTRTC）を入力し、**作成**をクリックします。

[](id:step2)
### 手順2：Demoのダウンロード
1. 実際のサービスニーズに応じてDemoソースコードをダウンロードするか、または、クリックして[TUICalling](https://github.com/tencentyun/TUICalling)に進み、Demoソースコードをダウンロードします。
2. ダウンロード完了後、**ダウンロード完了、次のステップへ**をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### ステップ3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Web/public/debug/GenerateTestUserSig.js`ファイルを見つけて開きます。
3. `GenerateTestUserSig.js` のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトでは0です。実際のSDKAppIDに設定してください。</li>
  <li>SECRETKEY：デフォルトでは空文字列です。実際のキー情報に設定してください。</li></ul> 
  <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. 貼り付け完了後、**貼り付け完了、次のステップへ**をクリックすると、作成が完了します。
5. コンパイル完了後、**コンソール概要に戻る**をクリックすると、終了します。

>!
>- ここで言及したUserSigの作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appからサービスサーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step4)
### 手順4：Demoの実行
1. Demoディレクトリに次のコマンドを順番に入力します。
```javascript
npm install
npm run serve
```
2. Chromeブラウザを起動し、リンク`http://localhost:8080/`を開きます。すべてが正常であれば、Demo実行インターフェースは次の図のようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/4bac4a925d537c29f1540fa90d570552.png)
3. useridを入力し、**ログイン**をクリックして、**ビデオ通話**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/eb1bcfd34409315b3bda70e72d5420f4.png)
4. 呼び出し先のuseridを入力し、**呼出**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/83e4ec55c1feb43c2ef68863a6b4beae.png)
5. ビデオ通話を開始できます。
![](https://qcloudimg.tencent-cloud.cn/raw/17bb3c8f1f49a4c1f100536bee37caef.png)


## 独自のビデオ通話の作成
### 手順1：TRTCCallingコンポーネントの統合

>?
>- 0.6.0以降は、[trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk)、[tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk)および[tsignaling](https://www.npmjs.com/package/tsignaling)の依存関係を手動でインストールする必要があります。
>- trtc-calling-js.jsのボリュームを縮小し、アクセス側で使用されているtrtc-js-sdk、tim-js-sdkおよびtsignalingのバージョン競合を回避するために、trtc-calling-js.jsは、外部依存関係としてtrtc-js-sdk、tim-js-sdk、tsignalingをパッケージ化しているので、使用する前に依存関係を手動でインストールする必要があります。

<dx-codeblock>
::: javascript javascript
// npm方式によるインストール
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

### 手順2：TRTCCallingオブジェクトの作成
TRTCCallingオブジェクトを作成し、SDKAppIDパラメータをお客様のSDKAppIDに設定します。
<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';

let options = {
  SDKAppID: 0, // アクセスするときは、0をお客様のSDKAppIDに置き換える必要があります。
  // v0.10.2から、timパラメータを追加します
  // timパラメータはサービス内にすでに存在するTIMインスタンスに使用され、TIMインスタンスの一意性を保証します。
  tim: tim
};
const trtcCalling = new TRTCCalling(options);
:::
</dx-codeblock>

### 手順3：ログインの完了
login関数を呼び出してログイン操作を完了します。パラメータのuserIDはユーザー名、userSigはユーザー署名です。userSigの計算方法については、[userSigの計算使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

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
trtcCalling.accept();
//拒否します
trtcCalling.reject()
```
- **ローカルカメラのオン**
```javascript
trtcCalling.openCamera()
```
- **リモートビデオ画面の表示**
```javascript
trtcCalling.startRemoteView({
  userID, //リモートユーザーID
  videoViewDomID //このユーザーデータはDOM IDノードにレンダリングされます
})
```
- **ローカルプレビュー画面の表示**
```javascript
trtcCalling.startLocalView({
  userID, //ローカルユーザーID
  videoViewDomID //このユーザーデータはDOM IDノードにレンダリングされます
})
```
- **通話終了**
```javascript
trtcCalling.hangup()
```
## よくあるご質問

#### 通話がつながらなかったり、強制オフラインになったりするのはなぜですか。
コンポーネントは現在、マルチインスタンスのログインや**オフラインプッシュのシグナリング**機能をサポートしていません。現在のログインアカウントの一意性をご確認ください。
> ?
> - **マルチインスタンス**：1つのUserIDで繰り返しログインしたり、異なるターミナルからログインしたりすると、シグナリングの混乱が生じます。
> - **オフラインプッシュ**：インスタンスはオンラインの場合にのみメッセージを受信できます。インスタンスがオフラインのときに受信したシグナリングは、オンラインになった後は再度プッシュされません。
その他よくあるご質問については、[TRTCCalling Webに関するご質問](https://intl.cloud.tencent.com/document/product/647/43096)をご参照ください。

## 技術的なお問い合わせ
詳細については、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)にご連絡をいただくか、colleenyu@tencent.comにメールでご連絡ください。



## 参考ドキュメント
- [TRTCCalling web公式サイトで体験](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html#/login)
- [TRTCCalling npm](https://www.npmjs.com/package/trtc-calling-js)
- [TRTCCalling web demoソースコード](https://github.com/tencentyun/TUICalling)
- [TRTCCalling web API](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/TRTCCalling.html)
- [TRTCCalling webに関するご質問](https://intl.cloud.tencent.com/document/product/647/43096)
