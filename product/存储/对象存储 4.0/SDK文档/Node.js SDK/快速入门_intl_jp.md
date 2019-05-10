## 開発準備
### SDKの取得

COSのXML JS SDKリソースgithubアドレス：[tencentyun/cos-nodejs-sdk-v5](https://github.com/tencentyun/cos-nodejs-sdk-v5)。

Demoのダウンロードアドレス：[XML Node.js SDK Demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo)。

### npm導入
開発の前に環境依存関係をインストールする必要があります： [npm アドレス](https://www.npmjs.com/package/cos-nodejs-sdk-v5)。
 
```
npm i cos-nodejs-sdk-v5 --save
```

### 開発環境

1. SDKを使用するには、実行環境にnodejsおよびnpmが含まれている必要があり、nodejsバージョンは7.0以上であることが推奨されています。
2. npmをインストールした後、npm依存パッケージをインストールし、SDKの解凍されたディレクトリで`npm install`を実行する必要があります。
3.  [コンソール暗号鍵管理](https://console.cloud.tencent.com/capi)にアクセスして、プロジェクトのSecretIdおよびSecretKeyを取得します。

>?文章に記載されているSecretId、SecretKey、Bucketなどの名称の意味と取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

## クイックスタート	

1. [COSオブジェクトストレージコンソール](https://console.cloud.tencent.com/cos4)でバケットを作成し、Bucket（バケット名）と[Region](https://cloud.tencent.com/document/product/436/6224)（地域名称）を取得します。
2. [コンソール暗号鍵管理](https://console.cloud.tencent.com/capi)でプロジェクトSecretIdとSecretKeyを取得します。
3. 初期化方法は永続暗号鍵による初期化と一時暗号鍵による初期化と2つのがあります。
 - 永続暗号鍵による初期化
SecretId、SecretKey、BucketおよびRegionを実際の開発環境における値に変更し、アップロードされたファイルをテストし、以下のサンプルコードを参照してください。
```javascript
// モジュールを導入します
var COS = require('cos-nodejs-sdk-v5');
// 永続暗号鍵でインスタンスを作成します
var cos = new COS({
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
});
// シャードアップロード
cos.sliceUploadFile({
    Bucket: 'test-1250000000',
    Region: 'ap-guangzhou',
    Key: '1.zip',
    FilePath: './1.zip'
}, function (err, data) {
    console.log(err, data);
});
```

 - 一時暗号鍵による初期化。
	一時暗号鍵の生成および使用については、[一時暗号鍵の生成および使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。Node.js SDKは一時暗号鍵を渡すことにより初期化することをサポートし、以下のサンプルコードを参照してください。
```
// 一時暗号鍵でインスタンスを作成します
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 署名を非同時的に取得します
        $.get('../server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            callback({
                 TmpSecretId: data.credentials.tmpSecretId, 
                 TmpSecretKey: data.credentials.tmpSecretKey, 
                 XCosSecurityToken: data.credentials.sessionToken, 
                 ExpiredTime: data.expiredTime
            });
        });
    }
});
```

## 関連ドキュメント 

1. より多くの例については、[XML Node.js SDK Demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/)を参照してください 。
2. 完全なAPIドキュメントについては、[XML Node.js SDK API ドキュメント](https://cloud.tencent.com/document/product/436/12264)を参照してください。


