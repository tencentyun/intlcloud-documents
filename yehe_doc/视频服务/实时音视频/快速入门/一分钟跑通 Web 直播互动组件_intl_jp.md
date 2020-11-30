ここでは、Tencent CloudのWebライブストリーミングインタラクティブコンポーネントの体験Demoをどのように素早く実行するかについてご説明いたします。

## 環境要件

- 最新バージョンのChromeブラウザを使用してください。
- TWebLiveは以下のポートに依存してデータ送信を行っていますので、これらをファイアウォール・ホワイトリストに追加してください。設定が完了したら、[公式サイト Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)にアクセスして体験していただけば、設定が有効かどうかチェックすることができます。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  -ドメイン名：qcloud.rtc.qq.com

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了済みです。

## 操作手順

<span id="step1"></span>
### 手順1：アプリケーションの新規作成

1.[Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2.[【アプリケーション管理】](https://console.cloud.tencent.com/trtc/app)に進み、【アプリケーションの作成】をクリックして、 `testtrtc`など、アプリケーション名を入力し、【確定】をクリックします。

<span id="step2"></span>
### ステップ2：SDKAppIDとキーの取得

1.アプリケーションリストから作成したアプリケーションを見つけ、右側の【アプリケーション情報】をクリックして詳細ページに進みます。ここで`SDKAppID`情報をコピーして保存することができます。
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
2.【すぐに作業を開始】タブをクリックし、【ステップ2 UserSigを発行するためのキーを取得】タブを表示し、【キーのコピー】をクリックします。
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>! キー情報を適切に保管して、漏えいしないようにしてください。

<span id="step3"></span>
### ステップ3：Demoのソースコードのダウンロードとコンフィグレーション

1.Tencent Cloud WebライブストリーミングインタラクティブコンポーネントのDemoプロジェクトをダウンロードします[ダウンロードアドレス](https://github.com/tencentyun/TWebLive)。
2.`TWebLive/dist/debug/GenerateTestUserSig.js`ファイルを開き、関連パラメータを設定します。
 -SDKAPPID：[ステップ2](#step2)で取得した実際のアプリケーション `SDKAppID`に設定してください。
 -SECRETKEY：[ステップ2](#step2)で取得した実際のキー情報に設定してください。




>!
>- UserSigのローカル計算方法は、ローカル開発とデバッグにのみ使用されます。ネット上にそのまま公開しないでください。 `SECRETKEY`が漏えいすると、攻撃者がTencent Cloudのトラフィックを盗用する可能性があります。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

<span id="step4"></span>
### 手順4：Demoの動作

Chromeブラウザを使用して `dist`ディレクトリのindex.htmlファイルを開くと、Demoが実行されます。

>!
>- 通常、Demoを体験する場合、サーバーにデプロイして `https://ドメイン名/xxx` 経由でアクセスするか、またはサーバーをローカルに直接構築して、`localhost:ポート`経由でアクセスする必要があります。
- 現在、デスクトップのChromeブラウザはTRTCデスクトップブラウザSDKをサポートしており、関連特性は比較的万全です。従って、Chromeブラウザを使用して体験することをお勧めします。

TWebLiveは、カメラとマイクを使用して、オーディオとビデオを収集する必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合、【許可】をクリックします。


## サポートプラットフォーム

WebRTCのテクノロジーはGoogleが初めて提唱し、現在、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザ及びモバイル版Safariブラウザでは比較的万全なサポートが提供されています。その他のプラットフォーム（Androidプラットフォームブラウザなど）のサポート状況は未だ不十分です。

- お客様のユースケースが主に教育シーンである場合、教師用端末はより安定性の高い[Electron](https://intl.cloud.tencent.com/document/product/647/35097) ソリューションを使用することをお勧めします。このソリューションは、大小のデュアルチャネル画面、より柔軟性の高い画面共有ソリューション及び脆弱なネットワークに対する高い回復力をサポートしています。

| OS | ブラウザタイプ | 最小バージョン要件 | 受信（再生）| 送信（マイク・オン）|
|:-------:|:-------:|:-------:|:-------:|:-------:|
| Mac OS  | デスクトップ版Safariブラウザ |  11+ | サポート | サポート | 
| Mac OS  | デスクトップ版Chromeブラウザ |  47+ | サポート | サポート | 
| Windows  | デスクトップ版Chromeブラウザ|  52+ | サポート | サポート | 
| Windows  | デスクトップ版QQブラウザ||  10.2 | サポート | サポート | 
| iOS | モバイル版Safariブラウザ | 11.1.2 | サポート | サポート | 
| iOS | WeChat Embedded Webページ| 12.1.4 | サポート | サポートなし | 
| Android | モバイル版QQブラウザ| - | サポートなし | サポートなし | 
| Android | モバイル版UCブラウザ| - | サポートなし | サポートなし | 
| Android | WeChatビルトイン型ウェブページ| 12.1.4 | サポート | サポートなし | 

>! H.264 版の権限の制限によって、Huaweiシステムの Chrome ブラウザおよび Chrome WebView をコアとするブラウザでは、 TRTC デスクトップ型ブラウザ SDK の正常動作をサポートしていません。

## よくあるご質問

### 1. キーをクエリするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？

TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。

### 2. クライアントエラーの発生：“RtcError: no valid ice candidate found”の対処方法は？

このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、環境要件に従ってファイアウォールのコンフィグレーションを確認してください。

### 3.クライアントエラーの発生：「RtcError: ICE/DTLS Transport connection failed」または「RtcError: DTLS Transport connection timeout」の対処方法は？

このエラーが発生した場合、TRTCデスクトップブラウザSDKがメディア伝送チャネルの確立に失敗したことを意味しますので、環境要件に従ってファイアウォールのコンフィグレーションを確認してください。

### 4.10006 errorが発生したときの対処方法は？

`"「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」"`が発生した場合、Tencent Real-Time Communicationアプリケーションのサーバー状態が使用可能かどうかご確認ください。
 [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/rav)にログインし、新規作成したアプリケーションをクリックし、【アカウント情報】をクリックすると、アカウント情報画面でサービス状態を確認することができます。
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)


## 関連資料

- [TWebLive インターフェースマニュアル](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [オンラインDemo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
