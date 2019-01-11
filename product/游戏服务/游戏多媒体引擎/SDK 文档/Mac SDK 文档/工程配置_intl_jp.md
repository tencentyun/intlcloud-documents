## 概要

Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。Mac開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでMac開発のためのプロジェクト構成を紹介します。

## SDKの準備

SDKは以下の方法で入手できます。

### 1. [ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連のDemoとSDKをダウンロードしてください。

### 2. 画面でMacバージョンのSDKリソースを見つけます。

### 3. 【ダウンロード】バタンを押します。

ダウンロードしたSDKリソースを解凍後に次の内容が含まれます。

|名称     | 意味   
| ------------- |:-------------:|
|GMESDK.framework			|GME関連リソース

## 準備作業

### 1. SDKファイルのインポート

下図に示すように、必要に応じて次の依存ライブラリをXcodeのLink Binary With Librariesに追加し、SDKのディレクトリに指向するようにFramework Search Pathsを設定します。  

### 2. 依存ライブラリを追加します

下図を参照します。  

![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)



