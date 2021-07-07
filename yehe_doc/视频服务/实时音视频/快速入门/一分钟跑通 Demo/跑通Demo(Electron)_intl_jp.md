ここでは、主にTencent CloudのTRTC Demo (Electron)を素早く実行する方法をご紹介します。

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。実名認証を行っていないユーザーは、中国国内のTRTCサービスを購入できません。

## 操作手順

[](id:step1)

### 手順1：アプリケーションの新規作成

1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：TestTRTC）を入力し、【作成】をクリックします。

[](id:step2)

### 手順2：SDKおよびDemoのソースコードをダウンロード
1.実際の業務のニーズにもとづき、SDKおよびセットのDemoソースコードをダウンロードします。
2.ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `TRTCSDK/Electron/TRTCSimpleDemo/` ディレクトリをさがします。これが*プロジェクトディレクトリ**となります。後述の<span id="projectFolder"></span>“プロジェクトディレクトリ”は、`TRTCSDK/Electron/TRTCSimpleDemo/`ディレクトリを指します。
2．プロジェクトディレクトリの `debug/gen-test-user-sig.js` ファイルを探して開きます。
3．`gen-test-user-sig.js` ファイルの関連パラメータを設定します。
<ul>
 <li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
 <li/>SECRETKEY：デフォルトは空文字列、実際のキー情報を設定してください。</ul>
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれは作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

**ファイルディレクトリの説明**
```bash
.
|---README.md                             READMEファイル，詳しくご覧ください
|---main.electron.js                      Electronメインファイル
|---public                             静的ファイルに保管
|---babel.config.js
|---package.json
|---vue.config.js                         vue-cli プロジェクトファイル
|---src                                   ソースコードディレクトリ
| |---app.vue
| |---common.css
| |---main.js
| |---components                          UIコンポーネントディレクトリ
| | |---main-menu.vue
| | |---nav-bar.vue
| | |---show-screen-capture.vue
| |---common                  ツール関数、パブリックコーパス等
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
| |---debug    注意！デプロイするとき、このフォルダ内の署名ロジックをサーバーに移動してください。
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

[](id:step4)

### 手順4：コンパイル動作
#### Windowsプラットフォーム
1.  Nodeの最新バージョンをインストールします（64bitの`.msi`ファイルの使用を推奨）。[Node ダウンロードアドレス](https://nodejs.org/en/download/)。
2.   `win + r` を押して cmdを入力し、管理者権限でコマンドラインウィンドウを起動し、[プロジェクトディレクトリ](#projectFolder)のディレクトリを見つけて、以下のコマンドを実行します。
```
$ npm install
```
![](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)
3．npmの依存パッケージのインストール完了を待って、コマンドラインウィンドウで以下のコマンドを引き続き実行してDemoを実行します。
```shell
$ npm run start  # 初めての実施では、しばらくすると、インターフェースにUIが現れます。
```
![](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

#### MacOSプラットフォーム
1.  ターミナル（Terminal）またはcmdインターフェースを開き、以下のコマンドを実行しHomebrewをインストールし、インストール済ならこの手順はスキップしてください。
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2．以下のコマンドを実行し、Node.jsをインストールします。
```shell
$ brew install node
```
3. Homebrewのデフォルトのアドレスを使用してNode.jsをインストールすると遅い場合は、国内のミラーリングアドレスに置き替えることをご検討ください。
 ```shell
$ cd `brew --repo`
$ git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
$ brew update
 ```
4.  cdコマンドによってプロジェクトディレクトリの位置を特定し、以下のコマンドを実行します。
```shell
$ npm install 
```
![](https://main.qcloudimg.com/raw/8bcc95adad07ff37e7f0a27893b8b7cf.png)
5. npm依存パッケージのインストールが完了してから、引き続きコマンドラインウィンドウで以下のコマンドを実行し、Demoを実行します。
```shell
$ npm run start # 初めての動作では、しばらく待つと、インターフェースにUIが現れます。
```
![](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
    
### 項目主要コマンド

| コマンド | 説明 |
|--|--|
| npm run start | 開発環境でDemoを動作 |
| npm run pack:mac | Macの.dmgインストールファイルのパッケージング|
| npm run pack:win64 | Windows 64ビットパッケージ .exe インストールファイル |

## よくあるご質問

### 1. キーをクエリーするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか。

TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

**アップグレード操作：**
1.  [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログイン。
2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
3．【クイックマスター】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【ここをクリックしてアップグレード】をクリックします。

### 2. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか。

2台のデバイスがDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2台のデバイスで同時に使用することをサポートしていません。

### 3. ファイアウォールにはどのような制限がありますか。

SDKがUDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるパブリックネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。



```

```