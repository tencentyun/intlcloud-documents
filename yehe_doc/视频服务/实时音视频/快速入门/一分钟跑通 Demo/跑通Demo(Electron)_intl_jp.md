ここでは、主にTRTC Demo (Electron)を素早く実行する方法をご紹介します。

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順

[](id:step1)

### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援**>**[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. **アプリケーションの作成**をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、**既存のアプリケーションを選択**をクリックします。
3. 実際の業務ニーズに応じてタグを追加または編集し、**作成**をクリックします。
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)

>?
>-アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード
1.実際のビジネスニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2.ダウンロード完了後、**ダウンロードしました。次のステップ**をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### ステップ3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2.  `Electron/js/GenerateTestUserSig.js` ファイルを見つけて開きます。
3. `GenerateTestUserSig.js` のファイルの関連するパラメータを設定します。
<ul>
 <li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
 <li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
 <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

**ファイルディレクトリの説明**
```bash
.
|---README.md                             READMEファイルです。よくお読みください
|---main.electron.js                      Electronメインファイル
|---public                             静的ファイルに保存
|---babel.config.js
|---package.json
|---vue.config.js                         vue-cliプロジェクトファイル
|---src                                   ソースコードディレクトリ
| |---app.vue
| |---common.css
| |---main.js
| |---components                          UIコンポーネントディレクトリ
| | |---main-menu.vue
| | |---nav-bar.vue
| | |---show-screen-capture.vue
| |---common                  ツール関数、パブリックコーパスなど
| | |---live-room-service.js
| | |---log.js                            ログツール
| | |---mtah5.js                          
| | |---routes.js
| | |---rand.js
| |---pages                          ページディレクトリ
| | |---index.vue                         メインページ
| | |---trtc                       ビデオミーティング関連ページ
| | | |---trtc-room.vue        ビデオミーティングルームページ
| | | |---trtc-index.vue   ビデオミーティングエントリーページ
| | |---404.vue
| | |---live               ライブストリーミングページ
| | | |---live-index.vue   ライブストリーミングエントリーページ
| | | |---live-room-audience.vue     ライブルーム視聴者ページ
| | | |---live-room-anchor.vue     ライブルームキャスターのページ
| |---debug    注意！デプロイするとき、このフォルダ内の署名ロジックをサーバーに移動して実装してください
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

[](id:step4)

### ステップ4：コンパイル実行
<dx-tabs>
::: Windowsプラットフォーム
1.  Nodeの最新バージョンをインストールします。64bitの`.msi`ファイルの使用を推奨します。[Nodeダウンロードアドレス](https://nodejs.org/en/download/)。
2.  `win + r`を押してcmdを入力し、管理者権限でコマンドラインウィンドウを起動し、[プロジェクトディレクトリ](#projectFolder)のディレクトリを見つけて、以下のコマンドを実行します。
```shell
$ npm install
​```![インストール](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)

4．npmの依存パッケージのインストール完了を待って、コマンドラインウィンドウで以下のコマンドを引き続き実行してDemoを実行します。
​```shell
$ npm run start  # 初回の実行の場合、しばらくしてからウィンドウにUIが現れます
​```![demo実行](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

:::
::: MacOSプラットフォーム
1.  ターミナル（Terminal）またはcmdウィンドウを開き、以下のコマンドを実行しHomebrewをインストールします。すでにインストールされている場合は、この手順をスキップしてください。
​```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2．以下のコマンドを実行し、Node.jsをインストールします。
```shell
$ brew install node
```

3. Homebrewのデフォルトアドレスを使用したNode.jsのインストールが遅い場合は、国内のイメージアドレスに置き替えることをご検討ください。
 ```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
 ```

4.  cdコマンドによってプロジェクトディレクトリの位置を特定し、以下のコマンドを実行します。
```shell
$ npm install 
​```![](https://main.qcloudimg.com/raw/8bcc95adad07ff37e7f0a27893b8b7cf.png)

5. npm依存パッケージのインストールが完了してから、引き続きコマンドラインウィンドウで以下のコマンドを実行し、Demoを実行します。
​```shell
$ npm run start # 初回の実行の場合、しばらくしてからウィンドウにUIが現れます
​```![macでの項目実行](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
:::
</dx-tabs>
    
### プロジェクトのメインコマンド

| コマンド | 説明 |
|--|--|
| npm run start | 開発環境でDemoを実行 |
| npm run pack:mac | Macの.dmgインストールファイルのパッケージング|
| npm run pack:win64 | Windows 64ビットの.exe インストールファイルのパッケージング |

## よくあるご質問

### 1. キーをクエリーするとき、パブリックキーとプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか。

TRTC SDK 6.6バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化鍵を取得するために、署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合でも、[旧バージョンアルゴリズムECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)を引き続き使用できます。

**アップグレード操作：**
1.  [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2.  左側ナビゲーションバーで**アプリケーション管理**を選択し、ターゲットアプリケーションのある行の**アプリケーション情報**をクリックします。
3．**クイックマスター**タブを選択して**ステップ2 UserSigを発行するためのキーを取得**エリアの**ここをクリックしてアップグレード**をクリックします。

### 2. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか。

2台のデバイスでDemoを実行するときは、異なるUserIDを使用していることを確認してください。TRTCでは、2台のデバイスでの同一UserID（SDKAppIDが異なる場合を除く）の同時使用をサポートしていません。

![](https://main.qcloudimg.com/raw/9a03335e435de0f12e2a26882f53db02.png)

### 3. ファイアウォールにはどのような制限がありますか。

SDKがUDPプロトコルを使用してオーディオ・ビデオ伝送を行っているため、UDPをブロックするオフィスネットワークでは使用できません。類似した問題がおありの際は、[企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題及び原因解決にお役立てください。

>? その他の関連するご質問については、[Electronについてのよくあるご質問](https://intl.cloud.tencent.com/document/product/647/43093)をご参照ください。

## 技術的なお問い合わせ
詳細な情報については[お問い合わせ](https://intl.cloud.tencent.com/contact-us)までご連絡ください。


## 参考ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demoソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCSimpleDemo)
- [API Exampleソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example)
- [Electronについてのよくあるご質問](https://intl.cloud.tencent.com/document/product/647/43093)

```