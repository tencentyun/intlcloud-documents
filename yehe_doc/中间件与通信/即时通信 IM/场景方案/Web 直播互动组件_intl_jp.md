- ここでは、UIを有するWeb端末ライブブロードキャストインタラクションコンポーネント、TUIPusher & TUIPlayerをご紹介します。[IM](https://intl.cloud.tencent.com/product/im)、TUIPusher & TUIPlayerは[TRTC](https://intl.cloud.tencent.com/product/trtc)などの基本SDKを統合し、企業によるライブブロードキャスト、eコマースマーケティング、業界研修、リモート教育などの様々なライブブロードキャストシーン向けに、すぐにリリースできるWeb端末ライブブロードキャストプッシュプルストリーミングツールによるソリューションをご提供します。

  TUIPusher & TUIPlayerのメリット：
  + ライブブロードキャストシーンのニーズに合わせ、UI付きのライブブロードキャストシーン向け汎用ソリューションをご提供します。ライブブロードキャストシーンの一般的な機能（デバイス選択、美顔、CSSプッシュ、視聴者によるプル、チャットなど）をすべて網羅し、ビジネスの速やかなリリースを支援します。
  + Tencent Cloud Real-Time Communication（TRTC）、Tencent Cloud Instant Messaging（IM）、およびTencent Cloud Super Player（TCPlayer） などの基本SDKに直接接続し、お客様のビジネス機能のフレキシブルな拡張に役立ちます。
  + Web端末はユーザーにとって使いやすく、機能のイテレーションも行いやすいというメリットがあります。

  ## クイック体験

  TUIPusherとTUIPlayerの機能デモンストレーションについては下図をご参照ください。また、TUIPusher & TUIPlayerの機能をすぐに体験していただけるよう、ユーザー管理システムとルーム管理システムを組み合わせた[TUIPusher体験リンク](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/login.html)および[TUIPlayer体験リンク](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/login.html)をご提供しています。
  >! TUIPusherとTUIPlayerを同時に体験するには、異なるアカウントを使用してログインする必要があります。  

  ![TUIPusherデモンストレーション](https://qcloudimg.tencent-cloud.cn/raw/8d33df705c07c80d75ad19096e681903.png)
  ![TUIPlayerデモンストレーション](https://qcloudimg.tencent-cloud.cn/raw/6490fdf7db4980db3a98b4b103fb52f1.png)

  ## コードのダウンロード

  Web端末ライブブロードキャストインタラクションコンポーネント（TUIPusher & TUIPlayer）のダウンロード方法は次のとおりです。
  + [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) 
  + [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer)
  
  
  ## 機能の説明
  ### TUIPusherプッシュコンポーネント
  - カメラとマイクからのストリームの収集とプッシュをサポート
    - 必要に応じてビデオパラメータ（フレームレート、解像度、ビットレート）を設定
    - 美顔の起動とビデオ美顔パラメータの設定をサポート
  - 画面共有ストリームの収集とプッシュをサポート
  - Tencent Real-Time Communicationバックエンドへのプッシュ、Tencent Cloud CDNへのプッシュをサポート
  - オンラインチャットルームをサポートし、オンライン視聴者とのインタラクティブなチャットを実現
  - 視聴者リストの取得、オンライン視聴者のミュート操作の実行をサポート
  
  ### TUIPlayerプルコンポーネント
  - オーディオビデオストリーミングと画面共有ストリーミングの同時再生をサポート
  - オンラインチャットルームをサポートし、キャスターおよびその他視聴者のインタラクティブなチャットを実現
  - 超低遅延ライブブロードキャスト（300msの遅延）、ライブイベントストリーミング（1000ms以下の遅延）、標準ライブブロードキャスト（超高速同時視聴をサポート）の3種類のプル回線をサポート
  - デスクトップブラウザおよびモバイルブラウザの互換性があり、モバイルブラウザの横画面表示が可能
  > !
  > 一部のブラウザはWebRTCをサポートせず、標準のライブブロードキャスト回線でしか視聴できません。他の回線を体験する場合はブラウザを変更してみてください。
  
  ## アクセス方法
  ### 注意事項
  - TUIPusher&TUIPlayerは、Tencent Cloud TRTCとInstant Messagingサービスをベースに開発されています。アカウントと認証を再利用するためには、TRTCアプリケーションとIMアプリケーションのSDKAppIDが一致している必要があります。
  - UserSigをローカルで計算する方式は、ローカルでの開発とデバッグのみに使用されます。SECRETKEYが漏洩すると、攻撃者がTencent Cloudトラフィックを盗用する可能性があるので、オンラインで直接発行しないでください。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appからサービスサーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。
  
  ### ステップ1：Tencent Cloudサービスのアクティブ化
  <dx-tabs>
  ::: 方法1：インスタントメッセージ\sIMの場合
  #### 手順1：IMアプリケーションの作成
  1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、**新しいアプリケーションの作成**をクリックするとダイアログボックスがポップアップします。
  ![](https://qcloudimg.tencent-cloud.cn/raw/7382cbcd81df7afbad1e9af641697c87.png)
  2. 自分のアプリケーション名を入力して、**確定**をクリックすると作成が完了します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/b3a630da00564cf7ef4a91b8492b646e.png)
  3. [IMコンソール](https://console.cloud.tencent.com/im)の概要画面で、新規作成したアプリケーションの状態、サービスバージョン、SDKAppID、作成時間、有効期限を確認することができます。SDKAppID情報を記録してください。
  
  #### 手順2：IMキーを取得してTRTC Video Serviceをアクティブにする
  1. [IMコンソール](https://console.cloud.tencent.com/im)の概要ページで、自分で作成を完了したIMアプリケーションをクリックして、直ちにそのアプリケーションの基本設定ページにリダイレクトします。**基本情報**領域で、**キーの表示**をクリックして、キー情報をコピーし保存します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/6f284cf687e9648d209567ed32983c84.png)
  >!キー情報を適切に保管して、漏えいしないようにしてください。
  2. そのアプリケーションの基本構成ページで、TRTCサービスをアクティブ化します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/8a9d1ca2c395fc6ebd26298a0f5226c4.png)
  :::
  ::: 方法2：TRTCの場合
  [](id:step1)
  #### 手順1：TRTCアプリケーションの作成
  1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)を行い、[Tencent Real-Time Communication（TRTC）](https://console.cloud.tencent.com/trtc)と[Instant Messaging](https://console.cloud.tencent.com/im)サービスをアクティブ化します。
  2. [TRTCコンソール](https://console.cloud.tencent.com/trtc) で、**アプリケーション管理>アプリケーションの作成** をクリックし、新たなアプリケーションを作成します。
  ![アプリケーションの作成](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)
  
  #### ステップ2： TRTCキー情報の取得
  1. **アプリケーション管理>アプリケーション情報**でSDKAppID情報を取得します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)
  2. **アプリケーション管理>クイックマスター**でアプリケーションのsecretKey情報を取得します。
  ![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)
  
  <dx-alert infotype="explain">
  - TRTCアプリケーションを初めて作成するTencent Cloudアカウントは、10000分間のオーディオビデオリソース無料トライアルパッケージを受け取ることができます。
  - TRTCプリケーションを作成すると、同じSDKAppIDのIMアプリケーションが自動的に作成され、[IMコンソール](https://console.cloud.tencent.com/im)でこのアプリケーションのパッケージ情報を設定することができます。</dx-alert>
  :::
  </dx-tabs>
  
  [](id:step2)
  ### ステップ2：プロジェクトの準備
  
  1. [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web)でTUIPusher & TUIPlayerコードをダウンロードします。
  2. TUIPusher & TUIPlayerのためにインストールして依存します。
  ```bash
  cd Web/TUIPusher
  npm install
  
  cd Web/TUIPlayer
  npm install
  ```
  3. sdkAppIdとsecretKeyを`TUIPusher/src/config/basic-info-config.js`、`TUIPlayer/src/config/basic-info-config.js`設定ファイルに入力します。
  ![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
  4. ローカル開発環境でTUIPusher＆TUIPlayerを実行します。
  ```bash
  cd Web/TUIPusher
  npm run serve
  
  cd Web/TUIPlayer
  npm run serve
  ```
  5. `http://localhost:8080`と`http://localhost:8081`を開き、TUIPusherとTUIPlayer機能を体験することができます。
  6. `TUIPusher/src/config/basic-info-config.js`、`TUIPlayer/src/config/basic-info-config.js`設定ファイル中のルーム，キャスターおよび視聴者などの情報を変更することができます。**TUIPusherとTUIPlayerのルーム情報、キャスター情報を一致させてください**。
  
  >!
  >- 上記設定が完了すると、TUIPusher & TUIPlayerを使用して超低遅延ライブブロードキャストを実行することができます。ライブイベントストリーミングと標準ライブブロードキャストをサポートする必要がある場合は、引き続き[ステップ3：Relayed Live Streaming](#step3)をご参照ください。
  >- UserSigをローカルで計算する方法は、ローカルの開発とデバッグにのみ使用されます。`SECRETKEY`が漏えいすると、攻撃者がTencent Cloudのトラフィックを盗用する可能性があるので、ネット上にそのままリリースしないでください。
  >- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appからサービスサーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。
  
  [](id:step3)
  ### ステップ3：Relayed live streaming
  
  TUIPusher&TUIPlayerによって実装されるライブイベントストリーミングと標準ライブブロードキャストはTencent Cloud[CSSサービス]（https://intl.cloud.tencent.com/document/product/267）に依存しているため、ライブイベントストリーミングと標準ライブブロードキャスト回線をサポートするには、Relayed Push機能を有効にする必要があります。
  
  1. [**TRTCコンソール**](https://console.cloud.tencent.com/trtc) で現在使用中のアプリケーションのRelayed Push設定を有効にします。必要に応じてRelayed Push用指定ストリームまたはGlobal Auto-relayを起動することができます。 
  ![](https://qcloudimg.tencent-cloud.cn/raw/b65584a5b096481ade6e302dabedcd5f.png)
  2. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)ページで独自の再生ドメイン名を追加します。具体的な内容は[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。
  3. `TUIPlayer/src/config/basic-info-config.js`設定ファイルで再生ドメイン名を設定します。
  
  上記設定が完了すると、TUIPusher & TUIPlayerがサポートする超低遅延ライブブロードキャスト、ライブイベントストリーミング、標準ライブブロードキャストの全機能を体験できます。
  
  [](id:step4)
  ### ステップ4：本番環境アプリケーション
  
  TUIPusher & TUIPlayerを本番環境アプリケーションに使用する場合は、TUIPusher & TUIPlayerにアクセスすることに加え、次の手順を実行する必要があります。
  
  - ユーザーID、ユーザー名、ユーザープロフィール画像などを含む製品ユーザー情報を管理するためのユーザー管理システムを作成します。
  - ライブブロードキャストルームID、ライブブロードキャストルーム名、ライブブロードキャストルームのホスト情報などを含む製品のライブブロードキャストルーム情報を管理するためのルーム管理システムを作成します。
  - サーバーがUserSigを発行します。
  > !
  > - ここでのUserSigの発行方法は、クライアントが入力したsdkAppIdとsecretKeyに基づきuserSigを発行する方法です。この方法で発行されるsecretKeyは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この方法はローカルのTUIPusher & TUIPlayerクイックスタート機能デバッグの実行のみに適しています**。
  > - UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、アプリケーションからサービスサーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
  - `TUIPusher/src/pusher.vue`、`TUIPlayer/src/player.vue`ファイルを参照し、ユーザー情報、ライブブロードキャストルーム情報、SDKAppId、UserSigなどのアカウント情報をvuexのstoreに送信し、グローバルストレージを実行すると、プッシュプルストリーミングする2つのクライアントの全機能をクイックスタートすることができます。詳細なサービスフローについては下図をご参照ください。
  ![](https://qcloudimg.tencent-cloud.cn/raw/30e959d1b4605532f6d4cac190cdd1df.png)
  
  ## 関連する質問
  ### Web端末での美顔機能の実現方法。
  [美顔を有効にする](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)をご参照ください。
  
  ### Web端末での画面共有の実現方法。
  [画面共有](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)をご参照ください。
  
  ### Web端末でのクラウドレコーディングの実現方法。
  1. **クラウドレコーディング**機能を有効にするための具体的な操作については、[クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426)をご参照ください 。
  2. **クラウドレコーディング**> **指定ユーザーレコーディング**を有効にすると、Web端末が[TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)インターフェース呼び出し時にuserDefineRecordIdパラメータを渡すことによってレコーディングを開始できます。
  
  ### Web端末でのCDNへのプッシュの実現方法。
  Web端末でのCDNへのプッシュについては、[CDNへのプッシュの実現](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html) をご参照ください。
  
  ## #Web端末でのライブイベントストリーミングプルの実現方法。
  ライブイベントストリーミングプルの実現方法は、Web SDKを介してCDNにプッシュした後、WebRTCプロトコルを使用してプルします。
  
  ## 注意事項
  ###  プラットフォームのサポート
  
  | オペレーションシステム（OS） | ブラウザタイプ                           | ブラウザ最低バージョン要件 | TUIPlayer                                          | TUIPusher    | TUIPusher画面共有                               |
  | :--------------------------- | :--------------------------------------- | :------------------------- | :------------------------------------------------- | :----------- | :---------------------------------------------- |
  | Mac OS                       | デスクトップ版Safariブラウザ             | 11+                        | サポートあり                                       | サポートあり | サポートあり（Safari13以降のバージョンが必要）  |
  | Mac OS                       | デスクトップ版Chromeブラウザ             | 56+                        | サポートあり                                       | サポートあり | サポートあり（Chrome72以降のバージョンが必要）  |
  | Mac OS                       | デスクトップ版Firefoxブラウザ            | 56+                        | サポートあり                                       | サポートあり | サポートあり（Firefox66以降のバージョンが必要） |
  | Mac OS                       | デスクトップ版Edgeブラウザ               | 80+                        | サポートあり                                       | サポートあり | サポートあり                                    |
  | Mac OS                       | デスクトップ版WeChat Embedded Web        | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Mac OS                       | デスクトップ版WeCom Embedded Web         | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Windows                      | デスクトップ版Chromeブラウザ             | 56+                        | サポートあり                                       | サポートあり | サポートあり（Chrome72以降のバージョンが必要）  |
  | Windows                      | デスクトップ版QQブラウザ（クイックコア） | 10.4+                      | サポートあり                                       | サポートあり | サポートなし                                    |
  | Windows                      | デスクトップ版Firefoxブラウザ            | 56+                        | サポートあり                                       | サポートあり | サポートあり（Firefox66以降のバージョンが必要） |
  | Windows                      | デスクトップ版Edgeブラウザ               | 80+                        | サポートあり                                       | サポートあり | サポートあり                                    |
  | Windows                      | デスクトップ版WeChat Embedded Web        | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Windows                      | デスクトップ版WeCom Embedded Web         | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | iOS                          | WeChat内蔵ブラウザ                       | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | iOS                          | WeChat Work内蔵ブラウザ                  | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | iOS                          | モバイル版Safariブラウザ                 | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | iOS                          | モバイル版Chromeブラウザ                 | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Android                      | WeChat内蔵ブラウザ                       | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Android                      | WeComブラウザ                            | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Android                      | モバイル版Chromeブラウザ                 | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Android                      | モバイル版QQブラウザ                     | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Android                      | モバイル版Firefoxブラウザ                | -                          | サポートあり                                       | サポートなし | サポートなし                                    |
  | Android                      | モバイル端末UCブラウザ                   | -                          | サポートあり（標準ライブブロードキャスト視聴のみ） | サポートなし | サポートなし                                    |
  
  ### ドメイン名要件
  ユーザーのセキュリティ、プライバシーなどの問題を考慮し、ブラウザはHTTPSプロトコルでしかTUIPusher & TUIPlayerの全機能を正常に使用できないようにウェブページを制限しています。本番環境のユーザーがTUIPusher & TUIPlayerの全機能にスムーズにアクセスし体験できるようにするには、HTTPSプロトコルを使用してオーディオビデオアプリケーションページにアクセスしてください。
  >! ローカル開発には、`http：// localhost`プロトコルを使用してアクセスできます。
  
  URLドメイン名およびプロトコルのサポート状況については、以下の表をご参照ください。
  
  | ユースケース     | プロトコル                  | TUIPlayer    | TUIPusher    | TUIPusher画面共有 | 備考 |
  | ---------------- | --------------------------- | ------------ | ------------ | ----------------- | ---- |
  | 本番環境         | HTTPSプロトコル             | サポートあり | サポートあり | サポートあり      | 推奨 |
  | 本番環境         | HTTPプロトコル              | サポートあり | サポートなし | サポートなし      | -    |
  | ローカル開発環境 | `http://localhost`          | サポートあり | サポートあり | サポートあり      | 推奨 |
  | ローカル開発環境 | `http://127.0.0.1`          | サポート     | サポート     | サポート          | -    |
  | ローカル開発環境 | `http://[ローカルマシンIP]` | サポートあり | サポートなし | サポートなし      | -    |
  
  ### ファイアウォールの制限
  TUIPusher & TUIPlayerは次のポートに依存してデータ送信を実行しています。これらのポートをファイアウォールのホワイトリストに追加してください。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com
  
  ## 結び
  今後のイテレーションにおいて、TRTC Web端末のプッシュプルコンポーネントは徐々にiOS、Andriodなどの各端末との接続が可能になるほか、Web端末上での視聴者のマイク接続、高度な美顔、カスタムレイアウト、複数のプラットフォームへのリツイート、画像・テキスト・音楽などのアップロード機能が実装されます。ぜひご利用いただき、貴重なご意見をお寄せください。
  
  ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
