このドキュメントでは、主にTencent Cloud TRTC Demo (Windows C++）を素早く実行する方法を紹介します。

## 環境要件
- Microsoft Visual Studio 2017バージョン以上、Microsoft Visual Studio 2019の使用を推奨します。
- [QT](https://download.qt.io/archive/qt/5.14/5.14.2/)（QT 5.14.xバージョン）開発環境をダウンロードしてインストールします。
- [.vsix](https://download.qt.io/official_releases/vsaddin/2.7.2/)プラグインファイルをダウンロードしてインストールします。公式サイトで対応するプラグインのバージョンを探してインストールすると完了できます。
- VSを開いてツールバーから`QT VS Tools -> Qt Options -> Qt Versions`をさがし、自分のQtコンパイラ msvcをadd（追加）します。
- `SDK/CPlusPlus/Win64/lib` 下のすべての `.dll` ファイルをプロジェクトディレクトリ下の `debug` / `release` フォルダ下にコピーする必要があります。
>! `Debug/release`フォルダはいずれもVSの環境構成後に自動的に生成されます。32bitプログラムならば、`SDK/CPlusPlus/Win64/lib`下のすべての`.dll`を`debug` / `release` フォルダ下にコピーする必要があります。


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

### 手順4：コンパイルと実行
設定完了後、Microsoft Visual Studio（Microsoft Visual Studio 2019の使用を推奨）を使用して、TRTC-API-Example-Qtディレクトリ下のソースコードプロジェクト`QTDemo.sln`を開いてQT環境を設定します（QT5.14バージョンの使用を推奨）。【実行】をクリックすれば体験できます。


## よくあるご質問

### 1. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか。
2台のデバイスでDemoを実行するときは、異なるUserIDを使用していることを確認してください。TRTCでは、2台のデバイスでの同一UserID（SDKAppIDが異なる場合を除く）の同時使用をサポートしていません。


### 2. ファイアウォールにはどのような制限がありますか。
SDKがUDPプロトコルを使用してオーディオ・ビデオ伝送を行っているため、UDPをブロックするオフィスネットワークでは使用できません。類似した問題がおありの際は、[企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題及び原因解決にお役立てください。
