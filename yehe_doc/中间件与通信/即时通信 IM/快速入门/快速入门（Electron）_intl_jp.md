````javascript
このドキュメントでは、Tencent CloudのIM Demo（Electron）を速やかに実行する方法と、Electron SDKを統合する方法について説明します。

## 環境要件

| プラットフォーム     | バージョン                |
| -------- | ------------------- |
| Electron | 13.1.5以上のバージョン。 |
|Node.js|v14.2.0|

## サポートするプラットフォーム

現在、MacosとWindows両方のプラットフォームをサポートしています。

## 体験DEMO

導入を開始する前に、[DEMO](https://intl.cloud.tencent.com/document/product/1047/34279)をご利用いただくと、Tencent Cloud IM Electron SDKを簡単にご覧いただけます。

##  前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順

[](id:step1)

### 手順1：アプリケーションの作成

1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
  >?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
  >　同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)した後、新しいアプリケーションを作成することができます。**アプリケーションが削除された後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
    ![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID情報を保存してください。コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、タグ、作成時間、有効期限を確認できます。
   ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 作成後のアプリケーションをクリックし、左側のナビゲーションバーで**支援ツール**>**UserSig発行&チェック**をクリックすると、UserIDおよびそれに対応するUserSigが作成されます。署名情報をコピーし、後でログインして使用します。
    ![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)

###　ステップ2：Electron SDKの統合に適した方法の選択

IMは2種類の統合方法を提供しており、最適な方法を選択して統合を行うことができます。

| 継承方式  | 適用シナリオ                                                                                                                                                                |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEMOの使用 | IM Demoは完全なチャット機能を含み、コードはオープンソース化されています。チャットライクなユースケースを実装したい場合は、Demoを使用して二次開発を行うことができます。今すぐ[Demo体験](https://intl.cloud.tencent.com/document/product/1047/34279)が可能です。 |
| 自己実装    | この方法は、Demoがアプリケーションの機能インターフェース要件を満たしていない場合に使用できます。                                                                                                                |

IM SDKのAPIの理解を深めるために、[APIドキュメント](https://comm.qq.com/im/doc/electron/zh/)も用意されています。

[](id:step3)

### ステップ3：Demoの使用

1. Instant Messaging IM Electron Demoソースコードをローカルにクローンします。
  ```javascript
  git clone https://github.com/TencentCloud/tc-chat-demo-electron.git
  ```
2. プロジェクトの依存関係をインストールします。
  ```javascript
  // プロジェクトのルートディレクトリ
  npm install

  // レンダリングプロセスディレクトリ
  cd src/client
  npm install
  ```
3. プロジェクトを実行します。
```javascript
// プロジェクトのルートディレクトリ
npm start
```
4. プロジェクトをパッケージ化します。
  ```javascript
  // macパッケージ化
  npm run build:mac
  // windowsパッケージ化
  npm run build:windows
  ```

>? demo内のメインプロセスのディレクトリは`src/app/main.js`であり、レンダリングプロセスのディレクトリは`src/client`です。実行中に問題が発生した場合は、FAQを使用して解決することができます。

[](id:step4)

###　ステップ4：自己実装

**Electron SDKのインストール**
次のコマンドを使用して、最新バージョンのElectron SDKをインストールします。
コマンドラインでの実行：

```
npm install im_electron_sdk
```

**SDKの初期化完了**

1.　`sdkAppID`を`TimMain`に渡します。
```javascript
//　メインプロセス
const TimMain = require('im_electron_sdk/dist/main')

const sdkappid=0;// Tencent Cloud　IMコンソールで申し込みます。
const tim = new TimMain({
  sdkappid:sdkappid
})
```
2.　`TIMInit`を呼び出してSDKの初期化を完了します。
```javascript
// レンダリングプロセス
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
// 初期化
timRender.TIMInit()
```
3.　テストユーザーにログインします。
この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。
`timRender.TIMLogin`メソッドを呼び出し、テストユーザとしてログインします。
戻り値`code`が0の場合、ログインは成功です。
```javascript
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
let {code} = await timRender.TIMLogin({
  userID: "userID",
  userSig:"userSig" // userSigの生成を参照
})
```

>? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、`UserSig`の計算コードをサーバーに統合し、Appのインターフェースを提供することです。`UserSig`が必要なときは、Appから業務サーバーに対し、動的に`UserSig`を取得するリクエストを送信します。詳細については[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

**メッセージ送信**
ここでは、テキストメッセージの送信を例として、`code`が0を返すとメッセージ送信が成功したことを意味します。
サンプルコード：

```javascript
const TimRender = require('im_electron_sdk/dist/render')
const timRender = new TimRender();
let param:MsgSendMessageParamsV2 = {    // param of TIMMsgSendMessage
    conv_id: "conv_id",
    conv_type: 1,
    params: {
        message_elem_array: [{
            elem_type: 1,
            text_elem_content:'Hello Tencent!',

        }],
        message_sender: "senderID",
    },
    callback: (data) => {}
  }
let {code} = await timRender.TIMMsgSendMessageV2(param);
```

> ?送信に失敗した場合は、sdkAppIDが知らない人宛てのメッセージ送信をサポートしていないことが原因の可能性があります。コンソールで有効にしてからテストに使用してください。 [このリンクをクリック](https://console.cloud.tencent.com/im/login-message)して、フレンドリレーションシップチェーンのチェックを無効にしてください。

**セッションリストの取得**
前の手順でテストメッセージの送信が完了しましたので、別のテストアカウントでログインし、セッションリストをプルできるようになりました。
一般的なユースケースは次のようなものです：
アプリケーションの起動後すぐにセッションリストを取得し、その後は長時間リンクを監視して、セッションリストの変更をリアルタイムに更新します。

```javascript
let param:getConvList = {
            userData:userData,
        }
let data:commonResult<convInfo[]> = await timRenderInstance.TIMConvGetConvList(param)
```

この時点で、前の手順で別のテストアカウントを使用して送信したメッセージのセッションを見ることができるようになりました。

**メッセージの受信**
一般的なユースケースは次のようなものです：

1. インターフェースが新しいセッションに入ると、まず一定量のメッセージ履歴を一括でリクエストし、メッセージ履歴リストの表示に用います。
2. 長時間接続を監視し、新しいメッセージをリアルタイムに受信してメッセージ履歴リストに追加します。

メッセージ履歴リストの一括リクエスト

```javascript
let param:MsgGetMsgListParams = {
        conv_id: conv_id,
        conv_type: conv_type,
        params: {
            msg_getmsglist_param_last_msg: msg,
            msg_getmsglist_param_count: 20,
            msg_getmsglist_param_is_remble: true,
        },
        user_data: user_data
    }
    let msgList:commonResult<Json_value_msg[]> = await timRenderInstance.TIMMsgGetMsgList(param);
```

監視による新メッセージのリアルタイム取得
callbackをバインドするサンプルコードは次のとおりです：

```javascript
let param : TIMRecvNewMsgCallbackParams = {
            callback: (...args)=>{},
            user_data: user_data
        }
timRenderInstance.TIMAddRecvNewMsgCallback(param);
```

この時点で、IMモジュールの開発は基本的に完了し、メッセージの送受信や様々なセッションに入ることが可能になりました。
続いて、グループ、ユーザープロファイル、リレーションシップチェーン、オフラインプッシュ、ローカル検索などの関連機能の開発を完了することができます。
詳細については、[APIドキュメント](https://comm.qq.com/im/doc/electron/zh/Callback/readme.html)をご参照ください。

## よくあるご質問

#### サポートされているプラットフォームはどれですか？

現在、MacosとWindows両方のプラットフォームをサポートしています。

#### エラーコードのクエリー方法

IM SDKのAPIレベルのエラーコードについては、[エラーコード](https://intl.cloud.tencent.com/document/product/1047/34348)をご確認ください。

####　開発環境インストール問題で、`npm ERR！gyp ERR！stack TypeError：Cannot assign to read only property'cflags'of object'#<Object>'`エラーが発生した場合の解決方法は。

nodeのバージョンを下げてください。16.18.1をお勧めします。

#### 開発環境インストールの問題で、`gypgyp ERR!ERR`エラーが発生した場合の解決方法は。

[gypgyp ERR!ERR! ](https://stackoverflow.com/questions/57879150/how-can-i-solve-error-gypgyp-errerr-find-vsfind-vs-msvs-version-not-set-from-c)をご参照ください。

####　`npm install`を実行すると`npm ERR!　Fix the upstream dependency conflict,or retry`のエラーが発生した場合の解決方法

npmV7より前のバージョンで依存性の競合が発生すると、依存性の競合は無視され、インストールが続行されます。
npmV7リリースからは自動的に無視されず、ユーザーが手動でコマンドを入力する必要があります。
以下のコマンドを実行してください：
<dx-codeblock>
:::  sh
npm install --force
:::
</dx-codeblock>


####　`npm run start`を実行すると`Error：error:0308010C:digital envelope routines::unsupported`のエラーが発生します。どうすればいいですか。

nodeのバージョンを下げてください。16.18.1をお勧めします。

#### Mac側のDemoで`npm run start`を実行すると白い画面が表示される場合の解決方法は。

Macで`npm run start`を実行すると白い画面が表示される原因は、レンダリングプロセスコードのbuildが完了しておらず、メインプロセスによって開かれた3000ポートがブランクページであるためです。レンダリングプロセスコードのbuildが完了した後にウインドウを更新することで、この問題を解決できます。または`cd src/client && npm run dev:react`, `npm run dev:electron`を実行し、レンダリングプロセスとメインプロセスを別々に開始します。

####　`vue-cli-plugin-electron-builder`で構築されたプロジェクトは`native modules`をどのように使用しますか？

`vue-cli-plugin-electron-builder`を使用して構築されたプロジェクトで`native modules`を使用するには、[No native build was found for platform=xxx](https://github.com/nklayman/vue-cli-plugin-electron-builder/issues/1492)をご参照ください。

####　`webpack`で構築されたプロジェクトはどのように`native modules`を使用しますか？

webpackを使用して独自に構築されたプロジェクトでnative modulesを使用するには、[WindowsのFAQ](https://blog.csdn.net/Yoryky/article/details/106780254)をご参照ください。

####　`Dynamic Linking Error`が表示されますか？

Dynamic Linking Error. electron-builderの設定

``` javascript
   extraFiles:[
    {
      "from": "./node_modules/im_electron_sdk/lib/",
      "to": "./Resources",
      "filter": [
        "**/*"
      ]
    }
  ]
```xxxxxxxxxx    extraFiles:[    {      "from": "./node_modules/im_electron_sdk/lib/",      "to": "./Resources",      "filter": [        "**/*"      ]    }  ]javascript
````
