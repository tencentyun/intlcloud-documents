## 適用シナリオ

COSの使用につき、オブジェクトを使用・管理するため、バケットを作成しておく必要があります。コンソール、APIまたはSDKによりバケットを作成できます。

バケットが存在しない場合、以下のコード例で指定の地域においてバケットを作成できます。バケットのサポートするパラメータは：

- Bucket：完全なるバケット名の指定に用いられます。フォーマットの例：`testbuc-125235912`。
- Region：Tencent Cloudサービスの地域を選択してください。作成が終わると、バケットの移動・変更ができなくなります。使用可能な地域名については、[Availability Zone](https://cloud.tencent.com/document/product/436/6224)ドキュメントを参照してください。

## 使用方法
### COSコンソールの使用
COSコンソールでバケットを作成する場合、[作成と削除](https://cloud.tencent.com/document/product/436/13309)コンソールガイドドキュメントを参照してください。

### REST APIの使用
REST APIでバケットの作成リクエストを送信することができます。[Put Bucketドキュメント説明](https://cloud.tencent.com/document/product/436/7738)を参照してください。
### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントにおけるPut Bucketの部分](https://cloud.tencent.com/document/product/436/12302#put-bucket)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. PutBucketReq、PutBucketRespを作成します。そのうち、PutBucketReqをBucket Nameにより構成します。
3. PutBucketを実行してバケットを作成します。

#### コード例

以下のコード例はバケットの作成方法を示しています。

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントにおけるPut Bucketの部分](https://cloud.tencent.com/document/product/436/12263#put-bucket)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. CreateBucketを実行してバケットを作成します。バケットの作成にあたって、バケットの権限を指定できます（パブリック読み書きまたはプライベート読み）。

#### コード例

CreateBucketを呼び出してバケットを作成します。コード例は下記のとおりです：

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);

String bucketName = "publicreadbucket-1251668577";
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucketName);
// バケットの権限をPublicRead（パブリック読み取り・プライベート書き込み）に設定します。ほかには、Private（プライベート読み書き）、PublicReadWrite（パブリック読み書き）が選択可能です
createBucketRequest.setCannedAcl(CannedAccessControlList.PublicRead);
Bucket bucket = cosclient.createBucket(createBucketRequest);
```
### JavaScript SDKの使用

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

以下のコード例はバケットの作成方法を示しています。

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

cos.putBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDKの使用

COSのNode.js SDKはこの方法を提供しています。[Node.js SDK APIドキュメントにおけるPut Bucketの部分](https://cloud.tencent.com/document/product/436/12264#put-bucket)を参照してください。

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで`node test.js`を実行します。

#### コード例

以下のコード例はバケットの作成方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントにおけるBucketの作成の部分](https://cloud.tencent.com/document/product/436/12267#.E5.88.9B.E5.BB.BAbucket)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. createBucketを実行してバケットを作成します。バケット名を提供する必要があります。

#### コード例

以下のコード例はバケットの作成方法を示しています。

```php
try {
    $result = $cosClient->createBucket(array('Bucket' => 'testbucket-125000000'));
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。[Python SDK APIドキュメントにおけるBucketの作成の部分](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA-bucket)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. create_bucket()を実行してバケットを作成します。バケット名を提供する必要があります。

#### コード例

以下のコード例はバケットの作成方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'     # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'     # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'    # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.create_bucket(
    Bucket=bucket    
)
```
