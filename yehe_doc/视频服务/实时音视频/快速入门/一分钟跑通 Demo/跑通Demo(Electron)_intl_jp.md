ここでは、主にTencent CloudのTRTC Demo (Electron)を速く操作する方法を紹介します。

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了済みです。

## 操作手順

<span id="step1" name="step1"> </span>

### 手順1：アプリケーションの新規作成

1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestTRTC`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

<span id="step2" name="step2"> </span>

### 手順2：SDKおよびDemoのソースコードをダウンロード

1.  マウスを該当するカードまで移動し，【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)】をクリックしてGithub（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Electron_latest.zip)】をクリック）にジャンプし、関連するSDKおよび付属のDemoソースコードをダウンロードします。
    ![img](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="step3" name="step3"> </span>

### 手順3：Demoプロジェクトファイルの設定
1. [手順2](#step2)でダウンロードしたソースコードパッケージを解凍し、`TRTCSDK/Electron/TRTCSimpleDemo/`ディレクトリを探し，これが**項目ディレクトリ**になります。以下に記載した<span id="projectFolder" name="projectFolder"> “項目ディレクトリ”</span>は`TRTCSDK/Electron/TRTCSimpleDemo/`ディレクトリを指します。

2．項目ディレクトリの `debug/gen-test-user-sig.js` ファイルを探して開きます。

3．`gen-test-user-sig.js` ファイルの関連パラメータを設定します。

    - SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。
    - SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。
    
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。

5.【ガイドを閉じてコンソールへ進む】をクリックします。

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
| | |---log.jsログツール
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
| | | |---live-room-anchor.vue     ホストページ
| |---debug    注意！デプロイするとき、このフォルダ内の署名ロジックをサーバーに移動してください。
| | |---lib-generate-test-usersig.min.js  
| | |---gen-test-user-sig.js              
```

<span id="step4"></span>

### 手順4：コンパイル動作

#### Windowsプラットフォーム

1．Nodeの最新バージョンのインストールには、64bitの`.msi` ファイルを選択することを推奨します。[Node ダウンロードアドレス](https://nodejs.org/en/download/)

2.   `win + r` を押して cmdを入力し，管理者権限でコマンドラインウィンドウを起動し，[プロジェクトディレクトリ](#projectFolder)のディレクトリを見つけて、以下のコマンドを実行します。
	
```shell
$ npm install
```
	
![インストール](https://main.qcloudimg.com/raw/5aba25ba2d5eddb5d956406ca5b6b9ac.png)


3．npmのリクエストパッケージのインストール完了を待って、コマンドラインウィンドウで以下のコマンドを引き続き実行してDemoを実行します。

```shell
$ npm run start  # 初めての実施では、しばらくすると、インターフェースにUIが現れます。
```
    
![demo動作](https://main.qcloudimg.com/raw/47f6e01acb2d927f6d9e24a7c9f78af1.png)

#### Mac OS プラットフォーム

1.  ターミナル（Terminal）またはcmdインターフェースを開き、以下のコマンドを実行しHomebrewをインストールし、インストール済ならこの手順はスキップしてください。

```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2．以下のコマンドを実行し、Node.jsをインストールします。

```shell
$ brew install node
```

3．cdコマンドによって項目ディレクトリを位置決めし、以下のコマンドを実行します。

 ```shell
$ npm install 
 ```
    
    ![macでのインストール](https://main.qcloudimg.com/raw/3f8e92e9c59ff1bdb9fd0b2a0f34852a.png)
    
4．npmのリクエストパッケージがすべてインストール完了するのを待って、コマンドラインウィンドウで引き続き以下のコマンドを実行し、Demoを動作します。

```shell
$ npm run start # 初めての動作では、しばらく待つと、インターフェースにUIが現れます。
```
    
![macでの項目実行](https://main.qcloudimg.com/raw/423dae368118e5250e7fa878022bb26f.png)
    
### 項目主要コマンド

| コマンド | 説明 |
|--|--|
| npm run start | 環境開発でDemoを動作 |
| npm run pack:mac | Mac をパッケージ .dmg インストールファイル|
| npm run pack:win64 | Windows 64ビットパッケージ .exe インストールファイル |

## よくあるご質問

### 1. キーをクエリするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？

TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

**アップグレード操作：**

1.  [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログイン。
2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
3．【すぐに作業を開始】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【このアップグレードをクリック】、【非対称暗号化】または【HMAC-SHA256】をクリックします。

### 2. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？

2台のデバイスがDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2台のデバイスで同時に使用することをサポートしていません。

### 3. ファイアウォールにどのような制限がありますか？

SDK が UDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるパブリックネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。


