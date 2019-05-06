## 概要

ここのすべてのツールとDemoは、[Github倉庫](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML)に格納されます。

本書では、ユーザーサーバーとユーザークライアントの2つの部分を紹介します。

## ユーザーサーバーの構築
本例では、ユーザーサーバーは、一時暗号鍵の機能のみを提供します。cos\_signer\_liteは、flaskサービスフレームワークに基づく一時暗号鍵サービスです。このプロジェクトはpython3で作成され、ユーザーは自分のマシンまたは仮想マシンでこのPythonプロジェクトを実行し、COS端末（Android/iOS）SDKに一時暗号鍵サービスを提供できます。
>!このプロジェクトは参考例のみです。生産環境に使用してはいけません。生産環境でCOSサーバーSDKの一時暗号鍵APIを使用できます。

### 構成環境

cossignは、現時点でPython3のみをサポートし、一時暗号鍵サービスを提供します。あなたがpipコマンドを使ってインストールできます。
```
pip3 install cossign
```

### サービスを起動する
インストールした後、次のコマンドを使って一時暗号鍵サービスを起動できます。
```
cossign --secret_id your_secret_id --secret_key your_secret_key --port 5000
```
>?ポートのデフォルト値は5000で、コマンドを実行するときにポート番号を指定しなくてもいいです。
>暗号鍵情報について、[クラウドAPI暗号鍵コンソール](https://console.cloud.tencent.com/cam/capi)で確認できます。


### テストサービス
ブラウザを通じて`http://your_server_ip:5000/sign`リンクにアクセスするか、次のコマンドを実行しテストを行います。
```
curl http://your_server_ip:5000/sign
```    
下記情報が返された場合、サービス実行が成功することを示します。
```
{
 "code":0,
 "message":"",
 "codeDesc":"Success",
 "data":{
  "credentials":{
   "sessionToken":"634aa09dccc3274045ba413ec081c1df64007f0a30001",
   "tmpSecretId":"AKIDwxHZGTUvXAfcbLaOedJUQuwBXWUXG4m3",
   "tmpSecretKey":"kriDdZsOuuF9zrZPlSAVVG0Sg4RXZu6M"},
  "expiredTime":1530515889}
 }
```

### トラブルシューティング
一時暗号鍵を構築するときにエラーが発生した場合、次の手順で調べてください。
1.  **トラブル：**インストールコマンド`pip3 install flask`を実行すると`comment not found pip3`が表示されます。    
**分析：**Python 3がインストールされていないか、Python 3がインストールされたがpathが正しく設定されていない。
**対策：**システムに応じてPython3のインストール方法を選択しインストールするか、path設定を確認してください。

2. **トラブル：**サービスが実行された後、一時暗号鍵を取得するときに`URLError: urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed`エラーが表示されます。
**対策：**このトラブルは、MAC OS Xシステムによく見られます。certifiモジュールをインストールすると解決できます。具体的な操作方法について、[Stack Overflow FAQ](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error/42334357#42334357)を参照してください。

## ユーザークライアントの構築
### クライアントの構成
QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.hファイルを変更し、APPIDおよび一時暗号鍵を取得するための上記配置済アドレスを入力し、次のコマンドを実行します。
```
pod install
```
コマンドを実行した後、QCloudCOSXMLDemo.xcworkspaceを開くとDemo体験に入ります。
### Demoを実行
#### Bucketリストを照合しBucketを作成
1、App例を起動した後、下図のように、現時点ですべての使用可能なRegionを表示します。    
![choose region](https://main.qcloudimg.com/raw/c7cdd4171e7ab4314299df399954942c.png)

2、下図のように、あるRegionを選択し入るとカレントアカウントのこのRegionでのすべてのBucketが表示されます。  
![bucket](https://main.qcloudimg.com/raw/9dae084c02f2e19cc6682588cada1e28.png)

下図のように、この画面で右上のBucket作成ボタンをクリックし、カレントのRegionで1つのBucketを作成します。 
![](https://main.qcloudimg.com/raw/fefd8a545c2a0924d3d60722b8d2affb.png)


#### ファイルのアップロード
下図のように、一番下のボタン【アルバム】>【アップロード】>【一時停止】>【再開】> 【キャンセル】を順にクリックしアップロードテストを行います。 
![](https://main.qcloudimg.com/raw/7050892158c428a9c5470eb472680844.png)

#### ファイルのダウンロード
下図のように、ダウンロード画面に入ると、カレントのBucket内のすべてのファイルが表示されます。【ダウンロード】をクリックしダウンロードテストを行います。
![](https://main.qcloudimg.com/raw/25fc6b09c7b6f3da7f1a427ecabb4ecb.png)

