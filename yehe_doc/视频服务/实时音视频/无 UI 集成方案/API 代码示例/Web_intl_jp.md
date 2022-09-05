このドキュメントでは、主にTencent Cloud TRTC Web SDK Demoを素早く実行する方法をご紹介します。
## 準備作業
TRTC Web SDK Demoを実行する前に理解すべきの事項。

### サポートするプラットフォーム
TRTC Web SDKはWebRTCに基づき実現され、現在、デスクトップとモバイル端末の主流ブラウザをサポートしています。詳細なサポートレベルの表については、[サポートしているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。
お客様のユースケースは対応表に記載されていない場合は、[TRTC Web SDK機能テスト画面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開けて、WebViewなど、現在の環境がWebRTCのすべての機能をサポートしているかどうかをチェックすることができます。

- お客様のユースケースが主に教育シーンである場合は、教師用端末では[Electron](https://intl.cloud.tencent.com/document/product/647/35097)ソリューションの使用をお勧めし、大小2チャネル画面、よりフレキシブルな画面共有方法およびより強力な弱ネットワークリカバリー機能をサポートしています。 

### URLドメイン名プロトコルの制限
ブラウザセキュリティポリシーの制限により、WebRTC機能を使用したページへのアクセスプロトコルには厳しい要件があります。以下の表を参照してアプリケーションの開発とデプロイを行ってください。

| ユースケース     | プロトコル             | 受信（再生） | 送信（マイク・オン） | 画面共有 | 備考 |
|----------|:-----------------|:---------|----------|--------|----------|
| 本番環境     | HTTPSプロトコル       | サポートあり       | サポートあり       | サポートあり     | **推奨** |
| 本番環境     | HTTPプロトコル        | サポートあり         | サポートなし       | サポートなし   | -     |
| ローカル開発環境 | http://localhost | サポートあり       | サポートあり       | サポートあり     | **推奨** |
| ローカル開発環境 | http://127.0.0.1 | サポートあり         | サポートあり         | サポートあり     |      -    |
| ローカル開発環境 | http://[ローカルマシンIP]  | サポートあり         | サポートなし       | サポートなし   |   -   |
| ローカル開発環境 | file:///         | サポートあり         | サポートあり         | サポートあり     |  -    |

### ファイアウォールの制限
TRTC Web SDKを使用する時、ユーザはファイアーフォールの制限でオーディオビデオ通話を利用できない可能性がありますので、[ファイアウォール制限への対応](https://www.tencentcloud.com/document/product/647/35164) を参照し、関連するポートとドメイン名をファイアウォールのホワイトリストに追加してください。

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順

[](id:step1)

### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援** > **[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. **アプリケーションの作成**をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、**既存のアプリケーションを選択**をクリックします。
3. 実際の業務ニーズに応じてタグを追加または編集し、**作成**をクリックします。

![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)

>?
>- アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
>- タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびDemoソースコードのダウンロード
1. Web端末のSDKとそれに付随するDemoソースコードをダウンロードします。
2. ダウンロード完了後、**ダウンロードしました。次のステップ**をクリックします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### ステップ3：SDKAppIDとキー（SecretKey）を取得 
1.設定変更ページに進み、`SDKAppID`と`キー`を取得します。
2. SDKAppIDとキー（SecretKey）の貼り付け完了後、**貼り付けました。次のステップへ**をクリックして作成は完了します。

![](https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png)

[](id:step4)
### 手順4：Demoの動作 

さまざまなお客様のニーズに応えるため、TRTC Webでは現在次のような基本Demoが提供されています：
- **Demo 1:base-js**
開発フレーム：jQuery + ネイティブJavaScript
TRTC Webの基本Demo（jQueryバージョン）は、TRTC Web SDKの基本的なオーディオビデオ通話、デバイス選択などの機能を統合し、ブラウザで直接実行できます。クイックエクスペリエンスの場合は、[base-jsオンライン体験アドレス](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html)にアクセスしてください。
- **Demo 2:quick-demo-js**
開発フレーム：フレームなし、ネイティブJavaScript
TRTC Webクイック実行Demo（ネイティブJavaScriptバージョン）では、TRTC Web SDKの基本的なオーディオビデオ通話、デバイス選択などの機能を統合し、ブラウザから直接実行できます。クイックエクスペリエンスの場合は、[quick-demo-jsオンライン体験アドレス](https://web.sdk.qcloud.com//trtc/webrtc/demo/quick-demo-js/index.html)にアクセスしてください。
- **Demo 3:quick-demo-vue2-js**
開発フレーム：Vue2 + JavaScript
TRTC Webクイック実行Demo（Vue2バージョン）では、TRTC Web SDKの基本的なオーディオビデオ通話、デバイス選択などの機能を統合しています。利用するにはNode環境をインストールする必要があります。クイックエクスペリエンスの場合は、[quick-demo-vue2-jsオンライン体験アドレス](https://web.sdk.qcloud.com/trtc/webrtc/demo/quick-demo-vue2-js/index.html)にアクセスしてください。
- **Demo 4:quick-demo-vue3-ts**
開発フレーム：Vue3 + TypeScript
TRTC Webクイック実行Demo（Vue3バージョン）では、TRTC Web SDKの基本的なオーディオビデオ通話、デバイス選択などの機能を統合しています。利用するにはNode環境をインストールする必要があります。クイックエクスペリエンスの場合は、[quick-demo-vue3-tsオンライン体験アドレス](https://web.sdk.qcloud.com/trtc/webrtc/demo/quick-demo-vue3-ts/index.html)にアクセスしてください。

<dx-tabs>
::: Demo 1
ディレクトリは`TRTC_Web/base-js`です。

1. ダウンロードしたソースコードで`TRTC_Web/base-js/js/debug/GenerateTestUserSig.js`ファイルを探して開きます。
2. `GenerateTestUserSig.js`ファイルの関連するパラメータを設定します。
  - SDKAPPID：デフォルトでは0です。実際の`SDKAppID`を設定してください。
  - SECRETKEY：デフォルトでは空文字列です。実際の`キー`情報を設定してください。 

3. Demoの実行
Chromeブラウザを使用してDemoルートディレクトリの`index.html`ファイルを開けば、Demoを実行できます。

<dx-alert infotype="notice">
<li>通常の場合は、体験Demoは、サーバーにデプロイし、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、`localhost:ポート経由で`アクセスする必要があります。</li>
<li>現在デスクトップ版Chromeブラウザは、TRTC Web SDK関連機能のサポート状況がかなり整っていますので、Chromeブラウザを使用して体験することをお勧めします。</li></dx-alert>


- **ルーム追加**をクリックして、オーディオビデオ通話ルームを追加し、ローカルのオーディオビデオストリームをデプロイします。
 複数ページを開き、各画面で**ルーム追加**をクリックすることができます。正常状態では、複数画面を見てリアルタイムなオーディオビデオ通話をシミュレーションできます。
- カメラアイコンをクリックすると、カメラデバイスを選択できます。
- マイクのアイコンをクリックすると、マイクデバイスを選択できます。

<dx-alert infotype="explain">WebRTCは、カメラとマイクを使用して、オーディオとビデオをキャプチャする必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合、**許可**をクリックします。</dx-alert>

:::
::: Demo 2
ディレクトリは`TRTC_Web/quick-demo-js`です。
1. ダウンロードしたソースコードで`TRTC_Web/quick-demo-js/index.html`ファイルを探してブラウザで開きます。

<dx-alert infotype="explain">
<li>TRTC Web SDKのサポートするブラウザについては、[TRTC Web SDKがサポートするプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。</li>
<li>TRTC Web SDKドメイン名とポートのホワイトリストの構成については、[TRTC Web SDKドメイン名とポートのホワイトリストの構成](https://intl.cloud.tencent.com/document/product/647/35164#webrtc-.E9.9C.80.E8.A6.81.E9.85.8D.E7.BD.AE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.E6.88.96.E5.9F.9F.E5.90.8D.E4.B8.BA.E7.99.BD.E5.90.8D.E5.8D.95.EF.BC.9F)をご参照ください。</li></dx-alert>

2. ブラウザで開いたページに、<a href="#step3">ステップ3</a>で取得したSDKAppIdとSecretKeyを入力します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f22cfb136e41ebb28100ea5fc1d6fa6f.png" width="800px">

3. 機能体験：
  - **ルーム参加**ボタンをクリックしてルームに参加します
  - **ストリームのリリース**ボタンをクリックしてローカルストリームをリリースします
  - **ストリームのリリース解除**ボタンをクリックして、ローカルストリームのリリースを解除します
  - **ルーム退出**ボタンをクリックしてルームを退出します
  - **画面共有の開始**ボタンをクリックして画面共有ストリームをリリースします
  - **画面共有の停止**ボタンをクリックして、画面共有ストリームのリリースをキャンセルします
4. ルームに参加した後、招待リンクを共有することで、招待された人とTRTC Webオーディオビデオ通信機能を体験することができます。
:::
::: Demo 3
ディレクトリは`TRTC_Web/quick-demo-vue2-js`です。
1. ダウンロードしたソースコードで`TRTC_Web/quick-demo-vue2-js/`ディレクトリを探して移動します。
2. ローカルでDemoを実行します。
```shell
npm start
```
デフォルトブラウザは自動的に`http://localhost:8080/`を開きます。

<dx-alert infotype="notice">
<li>ポート番号はDemoをローカルで実行した後の実際のポート番号とし、デフォルトでは8080です。</li>
<li>TRTC Web SDKのサポートするブラウザについては、[TRTC Web SDKがサポートするプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。</li>
<li>TRTC Web SDKドメイン名プロトコルの制限については、[TRTC Web SDKドメイン名プロトコルの制限](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。</li>
<li>TRTC Web SDKドメイン名とポートのホワイトリストの構成については、[TRTC Web SDKドメイン名とポートのホワイトリストの構成](https://intl.cloud.tencent.com/document/product/647/35164#webrtc-.E9.9C.80.E8.A6.81.E9.85.8D.E7.BD.AE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.E6.88.96.E5.9F.9F.E5.90.8D.E4.B8.BA.E7.99.BD.E5.90.8D.E5.8D.95.EF.BC.9F)をご参照ください。</li></dx-alert>

3. ブラウザで開いたページに、<a href="#step3">ステップ3</a>で取得したSDKAppIdとSecretKeyを入力します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/621de0ce3313a39bca88905185d40658.png" width="800px">

4. 機能体験：
  - **ルーム参加**ボタンをクリックしてルームに参加します
  - **ストリームのリリース**ボタンをクリックしてローカルストリームをリリースします
  - **ストリームのリリース解除**ボタンをクリックして、ローカルストリームのリリースを解除します
  - **ルーム退出**ボタンをクリックしてルームを退出します
  - **画面共有の開始**ボタンをクリックして画面共有ストリームをリリースします
  - **画面共有の停止**ボタンをクリックして、画面共有ストリームのリリースをキャンセルします
5. ルームに参加した後、招待リンクを共有することで、招待された人とTRTC Webオーディオビデオ通信機能を体験することができます。
:::
::: Demo 4
ディレクトリは`TRTC_Web/quick-demo-vue3-ts`です。
1. ダウンロードしたソースコードで`TRTC_Web/quick-demo-vue2-js/`ディレクトリを探して移動します。
2. ローカルでDemoを実行します。
```shell
npm start
```
デフォルトブラウザは自動的に`http://localhost:8080/`を開きます。

<dx-alert infotype="notice">
<li>ポート番号はDemoをローカルで実行した後の実際のポート番号とし、デフォルトでは8080です。</li>
<li>TRTC Web SDKのサポートするブラウザについては、[TRTC Web SDKがサポートするプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。</li>
<li>TRTC Web SDKドメイン名プロトコルの制限については、[TRTC Web SDKドメイン名プロトコルの制限](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。</li>
<li>TRTC Web SDKドメイン名とポートのホワイトリストの構成については、[TRTC Web SDKドメイン名とポートのホワイトリストの構成](https://intl.cloud.tencent.com/document/product/647/35164#webrtc-.E9.9C.80.E8.A6.81.E9.85.8D.E7.BD.AE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.E6.88.96.E5.9F.9F.E5.90.8D.E4.B8.BA.E7.99.BD.E5.90.8D.E5.8D.95.EF.BC.9F)をご参照ください。</li></dx-alert>

3. ブラウザで開いたページに、<a href="#step3">ステップ3</a>で取得したSDKAppIdとSecretKeyを入力します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/621de0ce3313a39bca88905185d40658.png" width="800px">
4. 機能体験：
- **ルーム参加**ボタンをクリックしてルームに参加します
- **ストリームのリリース**ボタンをクリックしてローカルストリームをリリースします
- **ストリームのリリース解除**ボタンをクリックして、ローカルストリームのリリースを解除します
- **ルーム退出**ボタンをクリックしてルームを退出します
- **画面共有の開始**ボタンをクリックして画面共有ストリームをリリースします
- **画面共有の停止**ボタンをクリックして、画面共有ストリームのリリースをキャンセルします
5. ルームに参加した後、招待リンクを共有することで、招待された人とTRTC Webオーディオビデオ通信機能を体験することができます。
:::
</dx-tabs>
<dx-alert infotype="notice" title="注意：">
<ul style="margin:0"><li>このドキュメントで使用したUserSigのソリューションは、クライアントでSECRETKEYを構成することです。この方法では、SECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのためこの方法は、<strong>ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します</strong>。</li><li>UserSigを正しく発行するには、UserSigコンピューティングコードをサーバー側に渡し、App指向のインターフェースを提供してもらいます。Appは、UserSigが必要なときに、サービスサーバーに対してダイナミックUserSigを取得するためのリクエストを開始します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/647/35166#Server">サーバー側でのUserSig生成</a>をご参照ください。</li></ul>
</dx-alert>

## よくあるご質問
### 1. キーをクエリーするとき、パブリックキーとプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか。
TRTC SDK 6.6（Web SDK 4.0）バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化鍵を取得するために、署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合でも、[旧バージョンアルゴリズム ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレードされた場合は、必要に応じて新旧アルゴリズムを切り替えます。

アップグレード/切替の操作：
1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2. 左側ナビゲーションバーで**アプリケーション管理**を選択し、ターゲットアプリケーションのある行の**アプリケーション情報**をクリックします。
3．**クイックマスター**タブを選択して**ステップ2 UserSigを発行するためのキーを取得**エリアの**HMAC-SHA256**をクリックします。
  - 旧バージョンアルゴリズムの ECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. クライアントエラーの発生：「RtcError: no valid ice candidate found」にはどう対処すればよいでしょうか。
このエラーが発生した場合、TRTC Web SDKがSTUNトンネリングに失敗したことを意味しますので、[ファイアウォールの制限の対応関連](https://www.tencentcloud.com/document/product/647/35164)ファイアウォールの設定を確認してください。

### 3. クライアントエラーの発生：「RtcError: ICE/DTLS Transport connection failed"」または 「RtcError: DTLS Transport connection timeout」にはどう対処すればよいでしょうか。
このエラーが発生した場合、TRTC Web SDKがメディア伝送チャネルの確立に失敗したことを意味しますので、[ファイアウォールの制限の対応関連](https://www.tencentcloud.com/document/product/647/35164)ファイアウォールの設定を確認してください。

### 4.10006 エラーが発生したときはどう対処すればよいでしょうか。
「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」が発生した場合は、Tencent Real-Time Communicationアプリケーションのサーバー状態が正常かどうかご確認ください。
[TRTCコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックし、**アプリケーション情報**をクリックすると、アプリケーション情報パネルでサービスステータスを確認できます。
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? その他のよくあるご質問については、[Web端末に関するご質問](https://intl.cloud.tencent.com/document/product/647/37340)をご参照ください。
