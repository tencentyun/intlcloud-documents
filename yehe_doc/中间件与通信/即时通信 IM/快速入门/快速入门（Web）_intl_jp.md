- # [Chat UIKit React](https://www.tencentcloud.com/document/product/1047/34279/)
  >Chat UIKitはTencent Cloud IM SDKをベースにしたUIコンポーネントライブラリであり、汎用UIコンポーネント及び会話、チャット、リレーションシップチェーン、グループ、オーディオビデオ通話などの機能を提供します。
  >UIコンポーネントを使用すれば、自分の業務ロジックを積み木を組み合わせるように素早く構築できます。
  >Chat UIKitが提供したコンポーネントは、UI機能を実装すると同時に、IM SDKに応じてインスタンスを呼出して、IMに関するロジックとデータ処理も実装します。そのため、開発者がChat UIKitを使用する時、自分の業務とカスタム拡張だけに集中するだけです。


  ## Example App
  チャット機能をデモするプログラムをご用意しておりますので、公式サイトでこれらの[demo](https://web.sdk.qcloud.com/im/demo/intl/index.html)を参照できます。また、GitHubで関連の[オープンソースコード](https://github.com/TencentCloud/chat-uikit-react)も公開しています。

  ![img.png](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/home.png)

  ### Demoのクイックスタート

  ### ステップ1：ソースコードのダウンロード
  ```
  # Run the code in CLI
  $ git clone https://github.com/TencentCloud/chat-uikit-react
  # Go to the project  
  $ cd chat-uikit-react
  # Install dependencies of the demo
  $ npm install && cd examples/sample-chat && npm install
  ```
  ### ステップ2：demoの設定
  1. `examples/sample-chat`プロジェクトを開き、`./examples/sample-chat/src/debug/GenerateTestUserSig.js`パスで`GenerateTestUserSig.js`ファイルに進みます。
  2. `GenerateTestUserSig.js`ファイルで`SDKAPPID`と`SECRETKEY`を設定します。具体的な値は[IMコンソール](https://console.tencentcloud.com/im)から取得してください。対象アプリケーションカードをクリックし、設定ページに進みます。
     ![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
  3. **Basic Information**エリアで**Display key**をクリックし、キーの情報をコピーしてGenerateTestUserSigファイルに保存します。
  >!
  >- ここで説明するUserSigの作成は、クライアントのソースコードでSECRETKEYを設定する方法を使用します。この方法では、逆コンパイルによってSECRETKEYがハックされる可能性が大きいです。キーが漏洩すると、攻撃者はご利用中のTencent Cloudのトラフィックを盗用できます。そのため**この方法は、ローカルでのDemoクイックスタートおよび機能デバッグにのみ適します**。
  >- UserSigの正しい発行方法として、UserSigの演算コードをご利用中のサーバーに集約し、Appのインターフェースを提供し、UserSigを必要とする場合、ご利用中のAppから業務サーバーにリクエストを送信し動的UserSigの取得を要求します。詳しくは、[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/1047/34385)をご参照ください。

  ### ステップ3：プロジェクトの起動
  ```
  # Launch the project
  $ cd examples/sample-chat
  $ npm run start
  ```

  ### ステップ4:初メッセージの送信
  1. プロジェクトを正常に起動した後、「+」アイコンをクリックし、会話を作成します。
  2. 入力ボックスで他のユーザーのuserIDを検索します。
  3. ユーザープロファイルフォトをクリックして会話を開始します。
  4. 入力ボックスにメッセージを入力し、「enter」キーを押して送信します。
     ![](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/chat-English.gif)


  ### Quick Links
  - [Demo App](https://web.sdk.qcloud.com/im/demo/intl/index.html)
  - [Client API](https://www.tencentcloud.com/document/product/1047/33999)
  - [Free Demos](https://www.tencentcloud.com/document/product/1047/34279)
  - [FAQ](https://www.tencentcloud.com/document/product/1047/34455)
  - [GitHub Source](https://github.com/TencentCloud/chat-uikit-react)
  - [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385)
