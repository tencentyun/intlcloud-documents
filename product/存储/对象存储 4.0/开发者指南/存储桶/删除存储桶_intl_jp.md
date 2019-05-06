## 適用シナリオ
バケットを削除する必要がある場合、コンソール、APIまたはSDKを通じてバケットを削除できます。

> **注意：**
> 現在、クリア済みのバケットの削除にのみ対応しています。バケットにオブジェクトが残っている場合、削除失敗となります。バケットを削除する前に、バケットにオブジェクトがないことを確認してください。

バケットの削除にあたって、操作者の身分には当該操作の権限が授与されていること、また正しいバケット名（Bucket）と地域（Region）パラメータを入力したことを確認する必要があります。

## 使用方法
### COSコンソールの使用
COSコンソールを使ってバケットを削除する必要がある場合、[バケットの削除](https://cloud.tencent.com/document/product/436/13309)コンソールガイドドキュメントを参照してください。

### REST APIの使用
REST APIでバケットの削除リクエストを送信することができます。[Delete Bucketドキュメント説明](https://cloud.tencent.com/document/product/436/7732)を参照してください。

### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントにおけるDelete Bucketの部分](https://cloud.tencent.com/document/product/436/12302#delete-bucket)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. DeleteBucket()を実行してバケットを削除します。バケット名を提供し、バケットがブランクであることを確保する必要があります。

#### コード例

以下のコード例はバケットの削除方法を示しています。

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// DeleteBucketReqの構造関数にbucket_nameを入力する必要があります
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントにおけるDelete Bucketの部分](https://cloud.tencent.com/document/product/436/12263#delete-bucket)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. deleteBucketを実行してバケットを削除します。バケットには一切のデータも含まれていないことを確認してください。さもなければデータを消去しておく必要があります。

#### コード例

deleteBucketを呼び出してバケットを削除します。コード例は下記のとおり：

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);

// バケット名はappidを含む必要があります
String bucketName = "publicreadbucket-1251668577";
// バケットを削除します。一切のデータも含まれていないバケットのみを削除できます
cosclient.deleteBucket(bucketName);
```

### JavaScript SDKの使用

COSのJavaScript SDKはこの方法を提供しています。[JavaScript SDK APIドキュメントにおけるDelete Bucketの部分](https://cloud.tencent.com/document/product/436/12260#delete-bucket)を参照してください。

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

以下のコード例はバケットの削除方法を示しています。

```html
<script src="cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000'; //ユーザーのバケットに置き換えます
var Region = 'ap-guangzhou';    //ユーザーのRegionに置き換えます

// インスタンスの初期化
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 署名を非同時的に取得します
        var url = 'auth.php?method=' + options.Method.toLowerCase() + '&pathname=' + encodeURIComponent('/' + (options.Key || ''));
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            callback(e.target.responseText);
        };
        xhr.send();
    }
});

cos.deleteBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDKの使用

COSのNode.js SDKはこの方法を提供しています。[Node.js SDK APIドキュメントにおけるDelete Bucketの部分](https://cloud.tencent.com/document/product/436/12264#delete-bucket)を参照してください。

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで```node test.js```を実行します。

#### コード例

以下のコード例はバケットの削除方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントにおけるBucketの削除の部分](https://cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4bucket)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. deleteBucketを実行してバケットを削除します。バケット名を提供する必要があります。

#### コード例

下記のコードはバケットを削除するステップを示しています。

```php
try {
    $result = $cosClient->deleteBucket(array(
        'Bucket' => 'testbucket-125000000'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。[Python SDK APIドキュメントにおけるBucketの削除の部分](https://cloud.tencent.com/document/product/436/12270#.E5.88.A0.E9.99.A4-bucket)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. delete_bucket()を実行してバケットを削除します。バケット名を提供し、バケットがブランクであることを確保する必要があります。

#### コード例

以下のコード例はバケットの削除方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換え
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換え
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.delete_bucket(
    Bucket=bucket    
)
```
