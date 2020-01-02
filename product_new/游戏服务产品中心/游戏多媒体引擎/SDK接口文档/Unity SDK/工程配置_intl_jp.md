Tencent Cloud Gaming Multimedia Engine SDKをご購入いただき、ありがとうございます。Unity開発者のデバッグ作業、及びTencent Cloud Gaming Multimedia Engine製品のAPI製品へのアクセスを容易にするために、ここで、Unity開発に適用されるプロジェクトコンフィギュレーションを説明させていただきます。

## SDK 準備

下記手順によりSDKを取得することができます。

###  SDKをダウンロードする

[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)から関連するDemo及びSDKをダウンロードしてください。

インターフェースで Unity バージョンの SDK リソースを見つけます。

【ダウンロード】ボタンをクリックします。ダウンロードされた SDK リソースを解凍すると、下記の幾つかの部分があります。

![](https://main.qcloudimg.com/raw/55494d9bb9145938f0594416f73b29f7.png)

ファイルの説明：

|ファイル名       | 説明           |
| ------------- |:-------------:|
| Plugins   |SDK データベースファイル|
| Scripts     |SDK コードファイル|

## 準備作業

### 1.  Plugins ファイルをインポートする
SDKにあるPluginsフォルダーのファイルを、 UnityプロジェクトにあるAssets の Plugins フォルダーにコピーします。下図の通りです。  
![](https://main.qcloudimg.com/raw/1221a25f62cedd3831cf2bb27bb1ea45.png)

### 2. コードファイルをインポートする
SDKにあるScripts フォルダーのファイルを、 Unityプロジェクトのコード保存フォルダーにコピーします、下図の通りです。  
![](https://main.qcloudimg.com/raw/8904a83c6173fa7c5b04ddb0e48138ca.png)

### 3. オーディオコンフィギュレーション
 Unity エディッターでは、Edit-Project Setting-Audioはシステムデフォルトを使ってよいです。修正すると、Unity 再生サウンドエフェクトはiOSにおけるハードキャッシュエリアの設定に影響されます、表現としてはサウンドエフェクトが中断されてしまいます。
![](https://main.qcloudimg.com/raw/df14517cac7fc29383c90720627572c7.png)

下図のようなモードにすると、Unity 再生サウンドエフェクトはiOS におけるハードキャッシュエリアの設定に影響されます、表現としてはサウンドエフェクトが中断されてしまいます。
![](https://main.qcloudimg.com/raw/69857f53bdc2ee7c7ad5e48777620df1.png)


## 異なるプラットホームをエクスポートする

 Unity エンジンから異なるプラットホームをエクスポートするには、対応するプロジェクトコンフィギュレーションを行う必要があります。

|プラットホーム       | プロジェクトコンフィギュレーショ    |
| ------------- |:-------------:|
| Android |[Android プロジェクトコンフィギュレーショドキュメンテーション](https://intl.cloud.tencent.com/document/product/607/10783)|
| iOS     |[iOS プロジェクトコンフィギュレーショドキュメンテーション](https://intl.cloud.tencent.com/document/product/607/10783)|
| Mac     |[Mac プロジェクトコンフィギュレーショドキュメンテーション](https://intl.cloud.tencent.com/document/product/607/10783)|