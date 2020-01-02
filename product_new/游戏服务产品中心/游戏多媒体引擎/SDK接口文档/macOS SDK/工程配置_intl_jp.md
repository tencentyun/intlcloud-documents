## 概要

Tencent Cloud Gaming Multimedia Engine SDKを利用頂き、有難うございました。Macを使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、Macでの開発に向けるプロジェクト構成について説明させていただきます。

## SDKの準備

以下の方法でSDKを入手できます。

### 1. [ダウンロードガイド]（https://intl.cloud.tencent.com/document/product/607/18521）から関連DemoとSDKをダウンロードしてください。

### 2. インターフェースでMac向けのSDKリソースを見付けてください。

### 3.【ダウンロード】ボタンをクリックしてください。

ダウンロードしたSDKリソースを解凍すると、以下の構成内容があります。

|名前     | 意味   
| ------------- |:-------------:|
|GMESDK.framework|Gaming Multimedia Engineの関連リソース

## 準備作業

### 1. SDKファイルのインポート

図に示している通り、必要に応じて次の依存ライブラリをXcodeのLink Binary With Librariesに追加し、Framework Search PathsにSDKの所在ディレクトリを設定する必要があります。  

### 2. 依存ライブラリの追加

下図を参照してください。  

![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)


