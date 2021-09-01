このドキュメントでは、Tencent Cloud Web TWebLive コンポーネントの体験 Demoのクイックスタートの方法を紹介します。

## 効果の表示


## 環境要件

- 最新バージョンのChrome ブラウザを使用してください。
- TWebLiveは、以下のポートに依存してデータ転送を行いますので、これらをファイアウォールのホワイトリストに追加してください。設定完了後、 [公式ウェブサイトの Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)にアクセスして体験し、設定が有効かどうかをチェックすることができます。
  - TCP ポート：8687
  - UDP ポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com

## 前提条件

 [Tencent Cloudの登録](https://intl.cloud.tencent.com/document/product/378/17985)アカウントがあり、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了している必要があります。実名認証を行っていない場合、中国国内のTRTCインスタンスを購入することができません。

##　操作手順
<span id="step1"></span>
### ステップ1：新規アプリケーションの作成

1.  [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2. [【アプリケーション管理】](https://console.cloud.tencent.com/trtc/app)に入り、【アプリケーションの作成】をクリックして、アプリケーション名（例：`testtrtc`）を入力し、【確定】をクリックします。
<span id="step2"></span>
### ステップ2：SDKAppID とキーの取得

1. アプリケーションリストの中から、作成したアプリケーションをさがし、右側の【アプリケーション情報】をクリックして、詳細画面に入れば、`SDKAppID`情報をコピーして保存できます。
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
2. 【クイックマスター】タブをクリックし、【第2ステップ 発行したUserSig キーの取得】のタブを見つけ、【キーのコピー】をクリックします。
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>! キー情報は適切に保管し、決して漏洩することがないようにしてください。
<span id="step3"></span>
### ステップ3： Demo ソースコードのダウンロードおよび設定

1. Tencent Cloud Web TWebLiveコンポーネントのDemoプログラムをダウンロードします。[ダウンロードアドレス](https://github.com/tencentyun/TWebLive)。
2. `TWebLive/dist/debug/GenerateTestUserSig.js` のファイルを開き、関連パラメータを設定します。
 - SDKAPPID： [ステップ2](#step2) で取得した実際のアプリケーションの`SDKAppID`を設定してください。
 - SECRETKEY： [ステップ2](#step2)で取得した実際のキー情報を設定してください。




>!
>- ローカルで UserSigを計算する方式は、ローカルでの開発デバッグにのみ使用し、オンライン上に直接リリースしないでください。一度 `SECRETKEY`が漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。
>- 正しい UserSigの発行方法は、 UserSig の計算コードをお客様のサーバーに統合して、App向けのポートを用意し、UserSig を必要とするときは、App から業務サーバーにリクエストを出して、ダイナミック UserSigを取得することです。より詳細な内容については、 [サーバーでの UserSig生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。
<span id="step4"></span>
### ステップ4：Demoの動作

Chrome ブラウザを使用して `dist` ディレクトリの下の `index.html`のファイルを開けば、Demoが動作します。

>!
>- 通常の場合、体験 Demo はサーバーにデプロイする必要があり、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、 `localhost:ポート`経由でアクセスします。
- 現在デスクトップ版Chrome ブラウザでは、TRTC デスクトップブラウザ SDKの関連機能がかなり完全にサポートされています。よってChrome ブラウザを使用して体験することをお勧めします。

**Demoの実行画面は次の図のとおりです。**

TWebLiveではカメラとマイクを使用してビデオキャプチャと集音を行う必要があります。体験のプロセスで Chrome ブラウザから関連する通知を受け取った場合は、【許可する】をクリックしてください。

## サポートするプラットフォーム

WebRTCの技術は Googleが一番早く提案し、現在は主に、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザおよびモバイル版のSafariブラウザでかなり完全にサポートされています。その他のプラットフォーム（例：Androidプラットフォームブラウザ）のサポート状況はこれに比べると劣ります。

- ユースケースが主に教育系シナリオである場合は、教師側にはより安定性の高い [Electron](https://intl.cloud.tencent.com/document/product/647/35097) のソリューションを使用することをお勧めします。大小2系統の画面、よりフレキシブルな画面共有プラン、脆弱なネットワークからのより強力なリカバー能力をサポートしています。

|  OS   |          ブラウザタイプ          | ブラウザの最低バージョン要件 | 受信（再生） | 送信（マイク・オン） |
| :---------: | :--------------------------: | :----------------: | :----------: | :----------: |
|   Mac OS    |     デスクトップ版 Safari ブラウザ     |        11+         |     サポート     |     サポート     |
|   Mac OS    |     デスクトップ版 Chrome ブラウザ     |        56+         |     サポート     |     サポート     |
|   Mac OS    |    デスクトップ版 Firefox ブラウザ     |        56+         |     サポート     |     サポート     |
|   Mac OS    |      デスクトップ版 Edge ブラウザ      |        80+         |     サポート     |     サポート     |
|   Windows   |     デスクトップ版 Chrome ブラウザ     |        56+         |     サポート     |     サポート     |
|   Windows   | デスクトップ版 QQ ブラウザ（超高速カーネル） |       10.4+        |     サポート     |     サポート     |
|   Windows   |    デスクトップ版 Firefox ブラウザ     |        56+         |     サポート     |     サポート     |
|   Windows   |      デスクトップ版 Edge ブラウザ      |        80+         |     サポート     |     サポート     |
| iOS 11.1.2+ |     モバイル版 Safari ブラウザ     |        11+         |     サポート     |     サポート     |
| iOS 12.1.4+ |         WeChat埋込みウェブページ         |         -          |     サポート     |    未サポート    |
|   Android   |       モバイル版 QQ ブラウザ       |         -          |    未サポート    |    未サポート    |
|   Android   |       モバイル版 UC ブラウザ       |         -          |    未サポート    |    未サポート    |
|   Android   |   WeChat埋込みウェブページ（TBS カーネル）   |         -          |     サポート     |     サポート     |
|   Android   |  WeChat埋込みウェブページ（XWEB カーネル）   |         -          |     サポート     |    未サポート    |

>! H.264の版権の制限により、ファーウェイのシステムの Chrome ブラウザおよび Chrome WebViewをカーネルとするブラウザでは、TRTC デスクトップブラウザ版SDKの正常な動作をサポートしていません。

## よくあるご質問

### 1. キーの確認時にパブリックキーとプライベートキーの情報しか取得できません。キーを取得するにはどうすればいいですか？

TRTC SDK 6.6 バージョン（2019年8月）以降、新しい署名アルゴリズム HMAC-SHA256を採用しています。これ以前に作成したアプリケーションで、新しい暗号化キーを取得するには、先に署名アルゴリズムをレベルアップする必要があります。

### 2. クライアントエラー：“RtcError: no valid ice candidate found”が出現したときの対処方法は？

このエラーの出現は、 TRTC デスクトップブラウザ SDK が STUNでの穴あけに失敗したことを意味します。環境要件にしたがってファイアウォールの設定をチェックしてください。

### 3. クライアントエラー：“RtcError: ICE/DTLS Transport connection failed”または “RtcError: DTLS Transport connection timeout”が出現したときの対処方法は？

このエラーの出現は、TRTC デスクトップブラウザ SDKがメディア転送ルートの作成時に失敗したことを表します。環境要件にしたがってファイアウォールの設定をチェックしてください。

### 4. 10006 error が出現したときの対処方法は？

`"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"`が出現した場合は、お客様のTRTCアプリケーションのサービス状態が使用可能かどうかを確認してください。
 [TRTCコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックして、【アカウント情報】をクリックすれば、アカウント情報パネルでサービス状態を確認できます。
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)



## 関連資料

- [TWebLive インターフェースマニュアル](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [オンライン Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
