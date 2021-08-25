このドキュメントでは、Tencent CloudのインタラクティブなWebライブ配信コンポーネントの体験Demoを迅速に実行する方法をご紹介します。

## 前提条件
[Tencent Cloudのアカウント登録](https://intl.cloud.tencent.com/document/product/378/17985)と、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。

## 操作手順

### ステップ1.アプリケーションの作成

1.[インスタントメッセージングIMコンソール](https://console.cloud.tencent.com/im)にログインします。
2.**新しいアプリケーションを追加**をクリックします。
3.**アプリケーションを作成**のダイアログボックスが表示されたら、アプリケーション名を入力し、**OK**をクリックします。
 作成後、コンソールの[概要]ページで、新規作成のアプリケーションの状態、サービスバージョン、`SDKAppID`、作成時間、有効期限を確認できます。`SDKAppID`情報を記録してください。


### ステップ2：キー情報の取得とリアルタイム音声・ビデオサービスの有効化

1. 対象のアプリケーションカードをクリックし、[アプリケーションの基本設定]ページに進みます。
2. **基本情報**セクションで**キーを表示**をクリックし、キー情報をコピーして保存します。
 >!キー情報は第三者に知られないように適切に保管してください。
3. Tencent Cloudリアルタイム音声・ビデオサービスを実行します。

### ステップ3：Demoソースコードのダウンロードと設定

1. Tencent CloudのインタラクティブなWebライブ配信コンポーネントDemoプロジェクトをダウンロードし、[アドレスをダウンロード](https://github.com/tencentyun/TWebLive)します。
2. `TWebLive/dist/debug/GenerateTestUserSig.js`ファイルを開いて、関連パラメータを設定します。
 - SDKAPPID：ステップ1で取得した実際のアプリケーションSDKAppIDに設定してください。
 - SECRETKEY：ステップ2で取得した実際のキー情報に設定してください。


>!
>- UserSigをローカルで計算する方法は、ローカルでの開発とデバッグにのみ適用されます。オンラインで直接公開しないでください。`SECRETKEY`が漏洩してしまうと、攻撃者がTencentCloudトラフィックを盗用する可能性があります。
>- UserSigを正しく発行するには、UserSig計算コードをサーバー側に渡し、App指向のインターフェースを提供してもらいます。Appは、UserSigが必要なときに、サービスサーバーに対して動的なUserSigを取得するためのリクエストを開始します。詳細については、[サーバー側でのUserSig生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご覧ください。

### ステップ4：Demoの実行
Chromeブラウザを使用して`dist`ディレクトリで`index.html`ファイルを開き、Demoを実行します。
>!
>- 通常の状況では、Demoを体験するには、サーバーにデプロイし、`https://域名/xxx`を介してアクセスするか、サーバーをローカルに直接構築して`localhost：ポート`を介してアクセスする必要があります。
>- 現在、デスクトップ用ChromeブラウザはTRTCデスクトップ用ブラウザSDKの全機能をサポートしているので、Demoの体験ではChromeブラウザを使用することをお勧めします。




WebRTCでは、カメラとマイクを使用して音声・ビデオを収集します。これに関するメッセージが、体験中にChromeブラウザから表示された場合は、**許可**をクリックします。

## 環境要件
- 最新版のChromeブラウザをご使用ください。
- TWebLiveは、データ送信を以下のポートから行っています。これらのポートをファイアウォール許可リストに追加してください。設定が完了したら、[公式ウェブサイトDemo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)にアクセスしてDemoを体験し、設定が有効かどうかを確認できます。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com

## よくあるご質問

### 1. キーが表示される場合は、公開鍵と秘密鍵に関する情報しか取得できません。キーの取得方法を教えてください。
TRTC SDKバージョン6.6（2019年8月）から、新しい署名アルゴリズムHMAC-SHA256が導入されました。これ以前に作成されたアプリケーションの場合、新しい暗号化キーを取得するには、署名アルゴリズムをアップグレードする必要があります。

### 2. クライアントエラー「RtcError: no valid ice candidate found」が発生しました。対処方法について教えてください。
このエラーは、TRTCデスクトップ用ブラウザSDKがSTUNを超えられなかったことを意味します。環境要件に従ってファイアウォール設定を確認してください。

### 3. クライアントエラー「RtcError: ICE/DTLS Transport connection failed」または「RtcError: DTLS Transport connection timeout」が発生しました。対処方法について教えてください。
このエラーは、TRTCデスクトップ用ブラウザSDKがメディア伝送チャネルの確立に失敗したことを意味します。環境要件に従ってファイアウォール設定を確認してください。

### 4. 10006　errorが発生しました。対処方法について教えてください。
「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」エラーが発生した場合、リアルタイム音声・ビデオアプリケーションのサービスステータスが利用可能であるかを確認してください。
[リアルタイム音声・ビデオコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックし、**アカウント情報**をクリックすると、[アカウント情報]パネルでサービスステータスを確認できます。


## 関連資料

- [TWebLiveインターフェースマニュアル](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [オンラインDemo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
