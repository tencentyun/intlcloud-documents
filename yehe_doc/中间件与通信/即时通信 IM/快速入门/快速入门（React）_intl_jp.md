
## TUIKit紹介

TUIKitはTencent Cloud IM SDKに基づいたUIコンポーネントライブラリで、会話、チャット、リレーショナルチェーン、グループ、オディオ・ビデオ通話などの機能を含む汎用的なUIコンポーネントを提供しています。
UIコンポーネントに基づいて、独自のビジネスロジックを積み木のようにすばやく構築できます。
TUIKitが提供したコンポーネントは、UI機能を実装すると同時に、IM SDKのインターフェースを呼出して、IMに関するロジックとデータ処理も実装します。そのため、開発者がTUIKitを使用する時、自分の業務とカスタム拡張だけに集中するだけです。
Reactに基づいて開発されたTUIKitのインターフェーススタイルは、海外のお客様の使用習慣と一致し、国際化をサポートしています。業務が海外へ進出する際には、ぜひご利用ください。

## Example App
体験可能なオンライン[demo](https://web.sdk.qcloud.com/im/demo/intl/index.html)を構築し、コードをgithub,[chat-uikit-react](https://github.com/TencentCloud/chat-uikit-react)に掲載しました。

## 開発環境要件
- React ≥ v18.0
- TypeScript
- node（12.13.0 ≤ nodeバージョン ≤ 17.0.0、Node.jsのLTS公式バージョン 16.17.0をお勧めします）
-　npm（バージョンはnodeバージョンと一致してください）

## demoのクイックスタート

### 手順1：ソースコードのダウンロード
```
# Run the code in CLI
$ git clone https://github.com/TencentCloud/chat-uikit-react
# Go to the project  
$ cd chat-uikit-react
# Install dependencies of the demo and build chat-uikit-react
$ npm install && npm run build
$ cd examples/sample-chat && npm install
```

>! プロジェクト`examples/sample-chat`の下で依存している`@tencentcloud/chat-uikit-react`はローカルパッケージなので、`npm run build`または`npm run start`を`chat-uikit-react`のルートディレクトリで実行する必要があります。後者は`npm run rollup-c-w`を起動します。プロジェクト`examples/sample-chat`は変更されたコンポーネントライブラリをリアルタイムでロードします。コンポーネントライブラリの独自開発・変更を行う際に使用することをお勧めします。


### 手順2：demoの設定
1. `examples/sample-chat`プロジェクトを開き、パス`./examples/sample-chat/src/debug/GenerateTestUserSig.js`で`GenerateTestUserSig.js`ファイルを探します。
2. `GenerateTestUserSig.js`ファイルに`SDKAPPID`と`SECRETKEY`を設定します。これらの値は[IMコンソール](https://console.cloud.tencent.com/im)で取得できます。対象のアプリカードをクリックすると、アプリケーションの基本設定ページに移動します。例えば、
3.　**図に示されている**領域で、**コピー**をクリックし、`GenerateTestUserSig.js`ファイルの元の`SDKAPPID`と`SECRETKEY`を置換します。
>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します。**
>- 正しい UserSigの発行方法は、 UserSig の計算コードをお客様のサーバーに統合して、App向けのインタフェースを用意し、UserSig を必要とするときは、App から業務サーバーにリクエストを出して、ダイナミックUserSigを取得することです。より詳細な内容については、 [サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。
   [](id:2-4)
4.　アプリのアカウント管理ページにアクセスし、今後メッセージ送信先であるテストユーザーとしてアカウントを作成し、userIDを取得します。

### ステップ3：プロジェクトの起動
```
# Launch the project
$ cd examples/sample-chat
$ npm run start
```

###　手順4：送信した最初のメッセージ
1.　プロジェクトの起動に成功したら、「+」アイコンをクリックして、セッションを作成します。
2.　入力ボックス内で他のユーザのuserIDを検索します（参照：[ステップ2.4]（#2−4））。
3.　ユーザーのプロファイル画像をクリックしてセッションを開始します。
4.　入力ボックスにメッセージを入力し、「enter」キーを押して送信します。

## よくあるご質問

#### UserSigとは何ですか？

UserSigは、ユーザーがIMにログインするためのパスワードです。その本質は、UserIDおよびその他の情報を暗号化して得られる暗号文です。

#### どうやってUserSigを生成しますか？

UserSigの発行方法は、UserSig の計算コードをお客様のサーバーに統合して、プロジェクト向けのインターフェースを提供することです。UserSig を必要とするときは、プロジェクトから業務サーバーにリクエストを出して、ダイナミック UserSigを取得できます。詳細については、 [サーバーでのUserSig生成](https://intl.cloud.tencent.com/document/product/1047/34385#GeneratingdynamicUserSig)をご参照ください。

>　!このコード例で使用されるUserSigの取得方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのクイックスタートおよび機能デバッグにのみ適しています**。正しいUserSigの発行方法は上文をご参照ください。

##  関連ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/1047/34281)
