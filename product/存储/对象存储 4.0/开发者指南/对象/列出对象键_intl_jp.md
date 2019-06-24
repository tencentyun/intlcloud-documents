## 適用シナリオ

Tencent Cloud COSはプレフィックス順でオブジェクト鍵をリストすることに対応しています。また、オブジェクト鍵において`/`という記号を使って従来型のファイルシステムのようなレイヤ構造を実現することもできます。COSは区切り記号によるレイヤ構造の選択と閲覧にも対応しています。

単独バケットにおけるすべてのオブジェクト鍵を、プレフィックスのUTF-8二進法順によりリストでき、あるいは指定したプレフィックスのフィルターオブジェクト鍵のリストを選択することもできます。例えば、パラメータ`t`を加えると、`tapd`のオブジェクトがリストされ、一方`a`またはその他文字をプレフィックスとするオブジェクトがスキップされることになります。

`/`区切り記号を加えると、この区切り記号により改めてオブジェクト鍵を構成できます。プレフィックスと区切り記号を結びつけてフォルダ検索のような機能を実現することができます。例えば、プレフィックスパラメータ`t`と区切り記号`/`を加えると、`tapd/file`のようなオブジェクト鍵が直接リストされます。

Tencent Cloud COSは単独バケットにおいて無限の数のオブジェクトに対応しているため、オブジェクト鍵リストのサイズが非常に大きくなっている可能性があります。管理しやすいように、単一オブジェクトAPIは最大1000のキー値の結果を返し、同時にインジケータを返して遮断の有無を知らせます。インジケータと区切り記号により一連のオブジェクト鍵をリストするリクエストを送信することで、すべてのキー値をリストし、または必要なコンテンツを検索することができます。

## 使用方法

### REST APIの使用

直接REST APIを使ってオブジェクトを取得するリクエストを送信することができます。[Get Bucketドキュメント説明](https://cloud.tencent.com/document/product/436/7734)を参照してください。

### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントのGet Bucketの部分](https://cloud.tencent.com/document/product/436/12302#get-bucket)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. GetBucket()を実行してオブジェクトをリストします。バケット名を提供する必要があります。

#### コード例

下記のコード例はオブジェクト鍵をリストする方法を示しています。

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// GetBucketReqの構造関数にbucket_nameを入力する必要があります
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);
```

指定のパラメータによってリストされるオブジェクト鍵を管理することができます。MaxKeysは今回の返された最大のオブジェクト数を指定します。Prefixは指定のプレフィックスのオブジェクト鍵のみの返しを指定します。Delimiterは指定の区切り記号のオブジェクト鍵のみの返しを指定します。
``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// GetBucketReqの構造関数にbucket_nameを入力する必要があります
qcloud_cos::GetBucketReq req(bucket_name);
req.SetPrefix("prefix");
req.SetDelimiter(";");
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントのGet Bucket (List Objects)の部分](https://cloud.tencent.com/document/product/436/12263#get-bucket-(list-objects))を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. listObjectsを使ってObjectをリストする場合、毎回最大で1000のObjectをリストすることができます。すべてのObjectあるいは1000以上のObjectをリストするには、繰り返してlistObjectsを呼び出す必要があります。

#### コード例
（1） `listObjectsRequest`はObjectをリストするリクエストを含みます。リストされるObjectのプレフィックス、区切り記号を設定することができます。サンプルコードは下記のとおりです：

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// バケット名を設定します
listObjectsRequest.setBucketName(bucketName);
// prefixは、リストされるObjectのKeyがprefixから始まることを意味します
listObjectsRequest.setPrefix("aaa/bbb");
// deliterは区切り記号で、/に設定される場合、現在のディレクトリ下のObjectをリストすることを意味します。ブランクに設定される場合、すべてのObjectをリストすることを意味します
listObjectsRequest.setDelimiter("");
// Objectのパスには特殊な文字がある場合、urlエンコード方法を使用することをおすすめします。ObjectのKeyを取得した後、url decodeを行う必要があります
listObjectsRequest.setEncodingType("url");
// 最大でいくつのオブジェクトを走査するかを設定します。毎回のlistObjectは最大で1000に対応します
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
try {
    objectListing = cosclient.listObjects(listObjectsRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// common prefixとは、delimiterに遮断されるパスのことで、delimterが/に設定される場合、common prefixはすべてのサブディレクトリのパスを意味します
List<String> commonPrefixs = objectListing.getCommonPrefixes();

// object summaryは、リストされているすべてのObjectリストを意味します
List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
    // ファイルのパスKey
    String key = cosObjectSummary.getKey();
    // 使用するencodingtypeがurlである場合、url decodeを行います
    try {                                                               
        key = URLDecoder.decode(key, "utf-8");
    } catch (UnsupportedEncodingException e) {                          
        continue;                                                       
    }
    // ファイルのetag
    String etag = cosObjectSummary.getETag();
    // ファイルの長さ
    long fileSize = cosObjectSummary.getSize();
    // ファイルのストレージタイプ
    String storageClasses = cosObjectSummary.getStorageClass();
}

cosclient.shutdown();
```
（2） maxKey数以上のObjectあるいはすべてのObjectを取得するには、繰り返してlistObjectを呼び出し、前回返されるnext markerを次回呼び出すmarkerとし、返されるtruncatedがfalseになるまで続けます。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// バケット名を設定します
listObjectsRequest.setBucketName(bucketName);
// prefixは、リストされるObjectのKeyがprefixから始まることを意味します
listObjectsRequest.setPrefix("aaa/bbb");
// deliterは区切り記号で、/に設定される場合、現在のディレクトリ下のObjectをリストすることを意味します。ブランクに設定される場合、すべてのObjectをリストすることを意味します
listObjectsRequest.setDelimiter("");
// Objectのパスには特殊な文字がある場合、urlエンコード方法を使用することをおすすめします。ObjectのKeyを取得した後、url decodeを行う必要があります
listObjectsRequest.setEncodingType("url");
// 最大でいくつのオブジェクトを走査するかを設定します。毎回のlistObjectは最大で1000に対応します
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {

    try {
        objectListing = cosclient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // common prefixとは、delimiterに遮断されるパスのことで、delimterが/に設定される場合、common prefixはすべてのサブディレクトリのパスを意味します
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // object summaryは、リストされているすべてのObjectリストを意味します
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // ファイルのパスKey
        String key = cosObjectSummary.getKey();
        // 使用するencodingtypeがurlである場合、url decodeを行います
        try {
            key = URLDecoder.decode(key, "utf-8");
        } catch (UnsupportedEncodingException e) {
            continue;
        }
        // ファイルのetag
        String etag = cosObjectSummary.getETag();
        // ファイルの長さ
        long fileSize = cosObjectSummary.getSize();
        // ファイルのストレージタイプ
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    // 次回リクエストのnext markerを取得します
    String nextMarker = "";
    try {
        nextMarker = URLDecoder.decode(objectListing.getNextMarker(), "utf-8");
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
        return;
    }
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());

cosclient.shutdown();
```

### JavaScript SDKの使用

COSのJavaScript SDKはこの方法を提供しています。[JavaScript SDK APIドキュメントのGet Bucketの部分](https://cloud.tencent.com/document/product/436/12260#get-bucket)を参照してください。

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例はオブジェクト鍵をリストする方法を示しています。

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

cos.getBucket({
    Bucket: Bucket,
    Region: Region,
}, function (err, data) {
    console.log(err, data);
});
</script>
```
### Node.js SDKの使用

COSのNode.js SDKはこの方法を提供しています。[Node.js SDK APIドキュメントのGet Bucketの部分](https://cloud.tencent.com/document/product/436/12264#get-bucket)を参照してください。

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで```node test.js```を実行します。

#### コード例

下記のコード例はオブジェクト鍵をリストする方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.getBucket({
    Bucket: Bucket,
    Region: Region,
    Prefix: '',    // プレフィックス、
    MaxKeys: '100' // 数をリストします
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントのバケットリストの取得](https://cloud.tencent.com/document/product/436/12267#.E8.8E.B7.E5.8F.96bucket.E5.88.97.E8.A1.A8)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. listObjectsを実行してオブジェクトをリストします。バケット名を提供する必要があります。

#### コード例

下記のコード例はオブジェクト鍵をリストする方法を示しています。

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'testbucket-125000000'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。[Python SDK APIドキュメントのファイルリスト取得の部分](https://cloud.tencent.com/document/product/436/12270#.E8.8E.B7.E5.8F.96.E6.96.87.E4.BB.B6.E5.88.97.E8.A1.A8)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. list_Objects()を実行してオブジェクトをリストします。バケット名を提供する必要があります。

#### コード例

下記のコード例はオブジェクト鍵をリストする方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換え
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.list_objects(
    Bucket=bucket       
)
```

指定のパラメータによってリストされるオブジェクト鍵を管理することができます。MaxKeysは今回の返された最大のオブジェクト数を指定します。Prefixは指定のプレフィックスのオブジェクト鍵のみの返しを指定します。Delimiterは指定の区切り記号のオブジェクト鍵のみの返しを指定します。
```python
bucket = 'testbucket-123456789'
response = client.list_objects(
    Bucket=bucket,
    Delimiter='/',
    MaxKeys=100,
    Prefix='test'
)
```
