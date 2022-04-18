ここでは、主にTencent Cloud IM Demo（Web）を素早く実行する方法について説明します。
                    

## デモンストレーション
![](https://qcloudimg.tencent-cloud.cn/raw/fe5b7406d6b6061918c393019aee2980.png)


## 操作手順
[](id:step1)
### 手順1：アプリケーションの作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. 作成が完了すると、[コンソールの概要画面](https://console.cloud.tencent.com/im)で、新規作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、タグおよび有効期限を確認できます。SDKAppID情報を記録してください。
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)


[](id:step2)
### ステップ2：キー情報の取得
1. 対象のアプリケーションカードをクリックし、アプリケーションの基本設定画面に移動します。
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
2. **基本情報**セクションで、**表示キー**をクリックし、キー情報をコピーして保存します。
>!キー情報を適切に保管して、漏えいしないようにしてください。

[](id:step3)
### ステップ3： Demo ソースコードのダウンロードおよび設定

1. 実際のサービス要求に基づいて、SDKと付属の[Demoソースコード](https://intl.cloud.tencent.com/document/product/1047/33996)をダウンロードします。
<dx-codeblock>
:::  js

# コマンドラインの実行
git clone https://github.com/tencentyun/TIMSDK.git

# Webプロジェクトに参加

cd TIMSDK/Web/Demo

# 依存のインストール
npm install
:::
</dx-codeblock>
2. 端末のディレクトリのプロジェクトを開いて、対応する`GenerateTestUserSig`ファイルを見つけてください。パス：/public/debug/GenerateTestUserSig.js
3. `GenerateTestUserSig`ファイルの関連パラメータを設定します。
 - SDKAPPID：[手順1](#step1)で取得した実際のアプリケーションSDKAppIDを設定してください。
 - SECRETKEY： [ステップ2](#step2)で取得した実際のキー情報を設定してください。
 ![](https://main.qcloudimg.com/raw/e7f6270bcbc68c51595371bd48c40af7.png)


>!ここで言及するUserSigの取得方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適しています**。
>UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

[](id:step4)
###  手順4：コンパイル実行
プロジェクトの端末で以下のコマンドラインを実行してください。ブラウザで実行することができます。
<dx-codeblock>
:::  js
# コマンドラインの実行
npm run start
:::
</dx-codeblock>

## 参照ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demoソースコード](https://github.com/tencentyun/TIMSDK/tree/master/Web/Demo)
