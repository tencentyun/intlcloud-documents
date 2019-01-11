## 概要

Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。iOS開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでiOS開発のためのプロジェクト構成を紹介します。

## SDKの準備

SDKは以下の方法で入手できます。

### 1. [ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連のDemoとSDKをダウンロードしてください。

### 2. 画面でiOSバージョンのSDKリソースを見つけます。

### 3. 【ダウンロード】バタンを押します。

ダウンロードしたSDKリソースを解凍後に次の内容が含まれます。

|名称     | 意味   
| ------------- |:-------------:|
|GMESDK.framework			|GME関連リソース

## システム要件

SDKはiOS7.0以降のシステムでの実行をサポートします。

## 準備作業

### 1. SDKファイルのインポート

下図に示すように、必要に応じて次の依存ライブラリをXcodeのLink Binary With Librariesに追加し、SDKのディレクトリに指向するようにFramework Search Pathsを設定します。  

![](https://main.qcloudimg.com/raw/9dd8d458734bc6e475581049e6cf26b1.png)

### 2. 依存ライブラリを追加します

下図を参照します。  

![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

### 3. bitcodeの無効化

Bitcodeはプロジェクトが依存するすべてのクラスライブラリによって同時にサポートされる必要があり、SDKは現時点でBitcodeをサポートしませんので、一応無効にします。
この設定を無効にするには、Targets - Build SettingsからBitcodeを検索して該当オプションを特定し、NOに設定します。
下図のように示します。  
![](https://main.qcloudimg.com/raw/82c628e8a7d9a4bebc842c8545d9563a.png)

### 4. 権限申請

Tencent音声ビデオエンジンのiOSプラットフォームで必要なプライバシー権限が以下の通りです。

|key     | 意味   
| ------------- |:-------------:|
|Required background modes    		 |バックグラウンド実行可能|
|Microphone Usaeg Description   	|マイク権限付与可能|

### 5. オフラインボイスへHTTPアクセス権限の追加
Allow Arbitrary Loads権限を追加する必要があります。

![](https://main.qcloudimg.com/raw/1aebf9111fd95e3e6b6fb4eb08193a26.png)

