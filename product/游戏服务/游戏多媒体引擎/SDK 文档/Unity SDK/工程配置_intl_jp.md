Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。Unity開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでUnity開発のためのプロジェクト構成を紹介します。

## SDKの準備

SDKは以下の手順で入手できます。

### SDKのダウンロード

[ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連のDemoとSDKをダウンロードしてください。

画面でUnityバージョンのSDKリソースを見つけます。

【ダウンロード】ボタンをクリックします。ダウンロードしたSDKリソースを解凍後に次の内容が含まれます。
![](https://main.qcloudimg.com/raw/55494d9bb9145938f0594416f73b29f7.png)
ファイル説明：

|ファイル名       | 説明           
| ------------- |:-------------:|
| Plugins   	|SDKライブラリファイル|
| Scripts     	|SDKコードファイル|

## 準備作業

### 1. Pluginsファイルのインポート
図に示すように、開発キットのPluginsフォルダ配下のファイルをUnityプロジェクトのAssetsのPluginsフォルダにコピーします。  
![](https://main.qcloudimg.com/raw/1221a25f62cedd3831cf2bb27bb1ea45.png)

### 2. コードファイルのインポート
図に示すように、開発キットのScriptsフォルダ配下のファイルをUnityプロジェクトのコード保存用フォルダにコピーします。  
![](https://main.qcloudimg.com/raw/8904a83c6173fa7c5b04ddb0e48138ca.png)

### 3. オーディオ設定
Unityエディタで、Edit-Project Setting-Audioはシステムデフォルトを使用すればよい。変更すれば、Unityの効果音再生は、iOSでハードウェアバッファの設定によって影響（効果音が中断される）されます。
![](https://main.qcloudimg.com/raw/df14517cac7fc29383c90720627572c7.png)

下図に示すようなモードに設定された場合、Unityの効果音再生は、iOSでハードウェアバッファの設定によって影響（効果音が中断される）されます。
![](https://main.qcloudimg.com/raw/69857f53bdc2ee7c7ad5e48777620df1.png)

