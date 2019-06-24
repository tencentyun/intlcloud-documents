## 適用シナリオ

当該操作は単独リクエストで5GB以下のオブジェクトのアップロードに適用します。5GB以上のオブジェクトにつき、マルチパートアップロードを使用しなければなりません。

オブジェクトのサイズが大きい（例えば：100MB）場合、広い帯域幅または弱いネットワーク環境では、優先的にマルチパートアップロードを使用することをおすすめします。

## 使用方法
### REST APIの使用

REST APIを使って直接オブジェクトの簡単なアップロードのリクエストを送信することができます。[PUT Objectドキュメント説明](https://cloud.tencent.com/document/product/436/7749)を参照してください。

### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントのPut Objectの部分](https://cloud.tencent.com/document/product/436/12302#put-object)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. PutObject()を実行してオブジェクトをアップロードします。バケット名とオブジェクト鍵名およびアップロードの内容を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトをアップロードする方法を示しています。

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "object_name";
//requestの構造関数にローカルファイルのパスを入力する必要があります
qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
//Set方法を呼び出してメタデータ或いはACL等を設定します
req.SetXCosStorageClass("STANDARD_IA");

qcloud_cos::PutObjectByFileResp resp;
qcloud_cos::CosResult result = cos.PutObject(req, &resp);
```

ファイルストリームのオブジェクトを指定することで、ファイルストリームをCOSにアップロードすることができます。

``` cpp
std::istringstream iss("put object");

//requestの構造関数にistreamを入力する必要があります
qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
qcloud_cos::PutObjectByStreamResp resp;

qcloud_cos::CosResult result = cos.PutObject(req, &resp);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントのPUT Objectの部分](https://cloud.tencent.com/document/product/436/12263#put-object.EF.BC.88.E4.B8.8A.E4.BC.A0-object.EF.BC.89)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. PutObjectを実行してオブジェクトをアップロードします。ローカルファイル或いは入力ストリームをCOSにアップロードすることに対応します。

#### コード例

（1）`PutObjectRequest`は簡単なアップロードのリクエストをカプセル化しており、ローカルファイルのパスおよびCOSパスを入力することで、ストレージタイプや権限情報等の設定に対応します。アップロード完了後、`PutObjectResult`が返されます。完成に失敗した場合、エラーが表示されます。サンプルコードは下記のとおり

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

String key = "aaa/bbb.txt";
File localFile = new File("src/test/resources/len10M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// ストレージタイプを設定し、デフォルトでは、標準（standard）、低頻度（standard_ia）です。
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // PutObjectResultはファイルのetagを返します
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// クライアントの閉鎖
cosclient.shutdown();
```

（2）`PutObjectRequest`は入力ストリームの入力にも対応しています。ストリームからCOSにアップロードできるが、長さを指定する必要があります。サンプルコードは下記のとおりです：

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

String key = "aaa/bbb.txt";
File localFile = new File("src/test/resources/len10M.txt");

InputStream input = new ByteArrayInputStream(new byte[10]);
ObjectMetadata objectMetadata = new ObjectMetadata();
//入力ストリームからアップロードする場合、content lengthを設定する必要があります。さもなければhttpクライアントはすべてのデータをキャッシュメモリとして保存し、メモリOOMを起こすかもしれません
objectMetadata.setContentLength(10);
//デフォルトではcontenttypeをダウンロードする場合、cosパスkeyのサフィックスにより対応するcontenttypeを返すように設定します。アップロードする場合、contenttypeがデフォルト値を上書きするように設定します
objectMetadata.setContentType("image/jpeg");

PutObjectRequest putObjectRequest =
        new PutObjectRequest(bucketName, key, input, objectMetadata);
// ストレージタイプを設定し、デフォルトでは、標準（standard）、低頻度（standard_ia）です。
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // PutObjectResultはファイルのetagを返します
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// クライアントの閉鎖        
cosclient.shutdown();
```
### JavaScript SDKの使用

COSのJavaScript SDKはこの方法を提供しています。[JavaScript SDK APIドキュメントのPut Objectの部分](https://cloud.tencent.com/document/product/436/12260#put-object)を参照してください。

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例は簡単にオブジェクトをアップロードする方法を示しています。

```html
<script src="dist/cos-js-sdk-v5.min.js"></script>
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

// ユーザーがファイルを選択したかどうかをリスニングする
document.getElementById('file-selector').onchange = function () {

    var file = this.files[0];
    if (!file) return;

    cos.putObject({
        Bucket: Bucket,
        Region: Region,
        Key: file.name,
        Body: file,
    }, function (err, data) {
        console.log(err, data);
    });

};
</script>
```
### Node.js SDKの使用

COSのNode.js SDKはこの方法を提供しています。[Node.js SDK APIドキュメントのPut Objectの部分](https://cloud.tencent.com/document/product/436/12264#put-object)を参照してください。

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. アップロードされるファイル1.jpgを現在のディレクトリに入れます。
3. テストファイルtest.jsを作成し、コマンドラインで`node test.js`を実行します。

#### コード例

下記のコード例は簡単にオブジェクトをアップロードする方法を示しています。

```javascript
var fs = require('fs');
var path = require('path');
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    Body: fs.readFileSync(path.resolve(__dirname, '1.jpg'))
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントの簡単なアップロードの部分](https://cloud.tencent.com/document/product/436/12267#.E7.AE.80.E5.8D.95.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. PutObjectを実行してデータストリームをアップロードします。バケット名とオブジェクト鍵名を提供する必要があります。
3. fopenを通じてファイルストリームをアップロードします。

#### コード例

下記のコード例はオブジェクトを簡単にアップロードするステップを示しています。

* メモリのアップロード：
```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => '11',
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
* ファイルストリームのアップロード：
```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => '11',
        'Body'   => fopen($pathToFile, 'r+')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
'Body'   => fopen($pathToFile, 'r+')
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。[Python SDK APIドキュメントの簡単なアップロードの部分](https://cloud.tencent.com/document/product/436/12270#.E7.AE.80.E5.8D.95.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. put_object()を実行してオブジェクトをアップロードします。バケット名とオブジェクト鍵名およびアップロードの内容を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトをアップロードする方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのSecretIdに置き換えます
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)
bucket = 'testbucket-123456789'
file_name = 'test.txt'

response = client.put_object(
    Bucket=bucket,
    Key=file_name,
    Body='1234'         
)
```

ファイルストリームのオブジェクトを指定することで、ファイルストリームをCOSにアップロードすることができます。
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換え
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)
bucket = 'testbucket-123456789'
file_name = 'test.txt'

# ファイルを生成します
with open(file_name, 'wb') as fp:
    fp.write('helloworld!')
with open(file_name, 'rb') as fp:
    response = client.put_object(
        Bucket=bucket,
        Key=file_name,
        Body=fp
    )
```

特定のパラメータを設定することで、オブジェクトのメタ情報を設定できます。
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換え
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)
bucket = 'testbucket-123456789'
file_name = 'test.txt'

response = client.put_object(
    Bucket=bucket,
    Key=file_name,
    Body='123',
    StorageClass='STANDARD',
    ACL='public-read',
    CacheControl='no-cache',
    ContentDisposition='attachment; filename=test.txt',
    ContentEncoding='gzip',
    ContentLanguage='zh-cn',
    ContentType='text/html',
    Expires='Tue, 05 Dec 2017 10:01:19 GMT',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
