## 適用シナリオ

COSにおいて保存されたオブジェクトを簡単なコピー操作で、新しいオブジェクトのコピーを作成することができます。毎回の操作において、最大5GBまでのオブジェクトをコピーできます。オブジェクトが5GBを超える場合、マルチパートアップロードのAPIによりコピーしなければなりません。オブジェクトのコピーには下記の機能があります。

- 新しいオブジェクトのコピーを作成します。
- オブジェクトをコピーして再命名します。オリジナルオブジェクトを削除し、再命名を完成します。
- オブジェクトのストレージタイプを変更します。コピーにあたって、同じソースと目標オブジェクト鍵を選択し、ストレージタイプを変更します。
- 異なるTencent Cloud COS地域においてオブジェクトをコピーします。
- オブジェクトのメタデータを変更します。コピーにあたって、同じソースと目標オブジェクト鍵を選択し、またそのうちのメタソースを変更します。

オブジェクトのコピーにあたって、デフォルトではオリジナルオブジェクトのメタデータを継承するが、作成日は新しいオブジェクトの作成時間に準じます。

## 使用方法

### REST APIの使用

REST APIを使って直接オブジェクトコピーのリクエストを送信することができます。[Put Object Copyドキュメント説明](https://cloud.tencent.com/document/product/436/10881)を参照してください。

### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントにおけるPut Object Copyの部分](https://cloud.tencent.com/document/product/436/12302#put-object-copy)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. PutObjectCopy()を実行してオブジェクトをコピーします。PutObjectReqにバケット名、オブジェクト鍵名およびコピーソースバケット、ソースオブジェクト鍵、ソース地域を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトをコピーする方法を示しています。

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントにおけるPut Object Copyの部分](https://cloud.tencent.com/document/product/436/12263#put-object-copy)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. copyObject APIを使ってcopyを完成します。

#### コード例

`CopyObjectRequest`はcopyオブジェクトのリクエストを含みます。ソースファイルの所在地域、バケット名、パス、および目標ファイルの地域、バケット名、パスの設定により、リクエストを送信します。下記のコード例は簡単にオブジェクトをコピーする方法を示しています。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// コピーされるバケット地域。キャンパス間コピーをサポートします
Region srcBucketRegion = new Region("ap-shanghai");
// ソースバケット。バケット名はappidを含む必要があります
String srcBucketName = "srcBucket-1251668577";
// コピーされるソースファイル
String srcKey = "aaa/bbb.txt";
// 目標バケット。バケット名はappidを含む必要があります
String destBucketName = "destBucket-1251668577";
// コピーされる目的ファイル
String destKey = "ccc/ddd.txt";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    CopyObjectResult copyObjectResult = cosclient.copyObject(copyObjectRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
cosclient.shutdown();
```

### JavaScript SDKの使用

COSのJavaScript SDKはこの方法を提供しています。[JavaScript SDK APIドキュメント](https://cloud.tencent.com/document/product/436/12260#put-object-copy)のPut Object Copyの部分を参照してください。

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例は簡単にオブジェクトをコピーする方法を示しています。

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

cos.putObjectCopy({
    Bucket: Bucket,
    Region: Region,
    Key: '1.new.jpg',
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg'
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDKの使用

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで`node test.js`を実行します。

#### コード例

下記のコード例はオブジェクトをコピーする方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putObjectCopy({
    Bucket: Bucket,
    Region: Region,
    Key: '1.new.jpg',
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントにおけるオブジェクトコピーの部分](https://cloud.tencent.com/document/product/436/12267#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. Copyパートコピーオブジェクトを実行します。バケット名とオブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトをコピーする方法を示しています。
```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'bucket-125000000',
        'CopySource' => 'bucket-appid.region.myqcloud.com/cos_path',
        'Key' => 'string',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。 [Python SDK APIドキュメントにおけるファイルコピーの部分](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E6.8B.B7.E8.B4.9D)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. copy_object()を実行してオブジェクトをコピーします。バケット名、オブジェクト鍵名およびコピーソースバケット、ソースオブジェクト鍵、ソース地域を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトをコピーする方法を示しています。

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
file_name = 'test.txt'
response = client.copy_object(
    Bucket=bucket,
    Key=file_name,
    CopySource={
        'Bucket': 'test-121212121',
        'Key': '1MB.txt',
        'Region': 'ap-guangzhou'
    }      
)
```
