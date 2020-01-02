## 概要

Tencent Cloud Gaming Multimedia Engine SDKをご利用いただき、ありがとうございます。iOS開発者のデバッグ作業、及びTencent Cloud Gaming Multimedia EngineのAPI製品へのアクセスを容易にするために、ここで、iOS開発に適用されるプロジェクトコンフィギュレーションを説明させていただきます。

## SDK 準備

下記方法によりSDKを取得することができます。

### 1.  [ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521) から関連するDemo及び SDKをダウンロードしてください。

### 2. インターフェースでiOSバージョンの SDKリソースを見つけます。

### 3.【ダウンロード】をクリックします。

ダウンロードされた SDK リソースが解凍されると、下記部分があります。

|名称     | 意味   |
| ------------- |:-------------:|
|GMESDK.framework|ネイティブ iOS関連リソースを開発します|
|libGMESDK.a|Unity iOS 関連リソースを開発します|

## システム要件

SDKはiOS7.0 及びそれ以降のシステムでの作動に対応しています。

## 準備作業

### 1.  SDK ファイルのインポート

必要に応じXcodeのLink Binary With Librariesに下記の依存ライブラリを追加し、SDKの所在するディレクトリを指向するためのFramework Search Paths設定を行います、下図の通りです。  

![](https://main.qcloudimg.com/raw/9dd8d458734bc6e475581049e6cf26b1.png)

### 2. 依存ライブラリの追加

下図の通りです。  

![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

### 3.  bitcodeを非アクティブにする

Bitcodeはプロジェクト依存のすべてのライブラリに対応する必要があります、SDK は現時点 Bitcodeに対応していないため、現時点において非アクティブにしてよいです。
このコンフィギュレーションを非アクティブにするには、 Targets - Build Settings で Bitcode をサーチし、対応するオプションを見つけてからNOに設定すればよいです。
下図の通りです。  
![](https://main.qcloudimg.com/raw/82c628e8a7d9a4bebc842c8545d9563a.png)

### 4.権限の申請

Tencentビデオ・オーディオエンジンのiOS プラットホームの必要となるプライバシー権限は下記の通りです。

|key     | 意味   |
| ------------- |:-------------:|
|Required background modes     |バックグラウンドでの実行を許可します（オプション）|
|Microphone Usage Description   |マイクホンの権限を許可します|

### 5.オフライン音声に対し HTTP アクセス権限を追加します
 Allow Arbitrary Loads 権限を追加する必要があります。

![](https://main.qcloudimg.com/raw/1aebf9111fd95e3e6b6fb4eb08193a26.png)
