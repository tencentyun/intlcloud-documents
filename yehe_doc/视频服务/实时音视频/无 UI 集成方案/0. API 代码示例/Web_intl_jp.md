ここでは、主にTencent Cloud TRTC Web SDK Demoを素早く実行する方法をご紹介します。
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
| ローカル開発環境 | http://localhost | サポートあり       | サポートあり       | サポートあり     | **推奨 ** |
| ローカル開発環境 | http://127.0.0.1 | サポートあり         | サポートあり         | サポートあり     |      -    |
| ローカル開発環境 | http://[ローカルマシンIP]  | サポートあり         | サポートなし       | サポートなし   |   -   |
| ローカル開発環境 | file:///         | サポートあり         | サポートあり         | サポートあり     |  -    |

### ファイアウォールの制限
TRTC Web SDKを使用する際、ユーザーはファイアウォールの制限によって正常にオーディオビデオ通話が行えない可能性があります。[ファイアウォール制限の対応関連](https://www.tencentcloud.com/document/product/647/35164)をご参照の上、対応するポートおよびドメイン名をファイアウォールのホワイトリストに追加してください。


##  前提条件
[Tencent Cloudの登録](https://intl.cloud.tencent.com/document/product/378/17985)によりアカウントを登録している。

## 操作手順

### 手順1：新規アプリケーションの作成

1. TRTCコンソールにログインし、【[アプリケーション管理](https://console.tencentcloud.com/trtc/app)】を選択します。

2. 【アプリケーションの作成】をクリックし、`APIExample`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合は、【既存のアプリケーションを選択】にチェックを入れ、【次のステップ】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### ステップ2：サンプルコードのダウンロード

1. UIなしの統合を選択後、ご自身の業務プラットフォームに合わせて、Githubで対応するプラットフォームのサンプルコードをダウンロードします。
2. ダウンロード完了後、【次のステップ】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### ステップ3：プロジェクトの設定
1. サンプルプロジェクトのクイックスタート段階で【デバッグ段階】を選択します。その後、ご自身のSDKAppID、Secret keyを記録しておきます。
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. ダウンロードしたサンプルコードを開き、図の指示に従って対応するファイルの場所を探し、ご自身のSDKAppID、Secret keyに変更します。プロジェクトの設定はこれで完了です。【次のステップ】をクリックしてください。

>?
>- ここで言及したUserSigの作成法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのTRTC-API-Exampleクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。


## よくあるご質問

### 1. クライアントエラーの発生：“RtcError: no valid ice candidate found”にはどう対処すればよいでしょうか。
このエラーの発生は、TRTC Web SDKがSTUNホールパンチングに失敗したことを意味します。[ファイアウォール制限の対応関連](https://www.tencentcloud.com/document/product/647/35164)に基づいてファイアウォール設定をチェックしてください。

### 2. クライアントエラーの発生：「RtcError: ICE/DTLS Transport connection failed"」または 「RtcError: DTLS Transport connection timeout」にはどう対処すればよいでしょうか。
このエラーの発生は、TRTC Web SDKがメディア伝送チャネルの確立の際に失敗したことを意味します。[ファイアウォール制限の対応関連](https://www.tencentcloud.com/document/product/647/35164)に基づいてファイアウォール設定をチェックしてください。

### 3. 10006 error が出現したときの対処方法は？
「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」が発生した場合は、Tencent Real-Time Communicationアプリケーションのサーバー状態が正常かどうかご確認ください。
[TRTCコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックし、**アプリケーション情報**をクリックすると、アプリケーション情報パネルでサービスステータスを確認できます。
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? その他のよくあるご質問については、[Web端末に関するご質問](https://intl.cloud.tencent.com/document/product/647/37340)をご参照ください。
