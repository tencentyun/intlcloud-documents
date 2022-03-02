このドキュメントでは、主にTencent Cloud IM Demo（Electron）を素早く実行する方法をご紹介します。

## 環境要件

| プラットフォーム | バージョン |
|---------|---------|
| Electron | 13.1.5以上のバージョン。 |
|Node.js|v14.2.0|

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順
[](id:step1)
## 手順1：アプリケーションの作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
>
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID情報を保存してください。コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認できます。
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 作成後のアプリケーションをクリックし、左側のナビゲーションバーで**支援ツール**>**UserSig発行&チェック**をクリックすると、UserIDおよびそれに対応するUserSigが作成されます。署名情報をコピーし、後でログインして使用します。
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
## 手順2：ソースコードをダウンロードし、依存関係をインストールして実行
1. Instant Messaging IM Electron Demoソースコードをローカルにクローンします。
```javascript
git clone https://github.com/tencentyun/im_electron_demo.git
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



## よくあるご質問

### サポートされているプラットフォームはどれですか。
現在、MacosとWindows両方のプラットフォームをサポートしています。

### 開発環境インストールの問題で、`gypgyp ERR!ERR`エラーが出現した場合の解決方法。
[gypgyp ERR!ERR! ](https://stackoverflow.com/questions/57879150/how-can-i-solve-error-gypgyp-errerr-find-vsfind-vs-msvs-version-not-set-from-c)をご参照ください。

### Macで`npm run start`を実行すると白い画面が表示される場合の解決方法。
Macで`npm run start`を実行すると白い画面が表示される原因は、レンダリングプロセスコードのbuildが完了しておらず、メインプロセスによって開かれた3000ポートがブランクページであるためです。レンダリングプロセスコードのbuildが完了した後にウインドウを更新することで、この問題を解決できます。または`cd src/client && npm run dev:react`, `npm run dev:electron`を実行し、レンダリングプロセスとメインプロセスを別々に開始します。
