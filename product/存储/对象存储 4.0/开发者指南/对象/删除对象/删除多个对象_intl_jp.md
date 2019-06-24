## 適用シナリオ

Tencent Cloud COSは複数オブジェクトの一括削除に対応します。コンソール、APIやSDK等の様々な方式でオブジェクトを一括削除できます。

デフォルトでは、削除タスクが全部完成された場合、通常、ブランクは返されます。エラーが発生した場合、エラー情報は返されます。

>注意：毎回リクエストで最大1000までのオブジェクトを削除できます。それ以上のオブジェクトを削除するには、リスト分割後、別々にリクエストを送信してください。

## 使用方法

### COSコンソールの使用
COSコンソールを使って複数オブジェクトを一括削除することができます。[オブジェクトの削除](https://cloud.tencent.com/document/product/436/13323)コンソールガイドドキュメントを参照してください。

### REST APIの使用

直接REST APIを使ってオブジェクト一括削除のリクエストを送信することができます。[Delete Multiple Object ](https://cloud.tencent.com/document/product/436/8289)ドキュメントを参照してください。

### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントのDelete Objectの部分](https://cloud.tencent.com/document/product/436/12263#delete-object)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. DeleteObjectsを実行してオブジェクトを削除します。削除するオブジェクト鍵名を提供する必要があります。
3. 実行が完成したら、DeleteObjectsResultオブジェクトは返されます。それはすべての削除されたオブジェクト鍵を含みます。一部が完成し、一部が失敗した場合（例えば、当該オブジェクトに削除権限がない場合）、MultiObjectDeleteException類の情報は返されます。その他の失敗による異常につき、異常類の情報（CosClientException/CosServiceException）は返されます。SDK異常類説明を参照してください。

#### コード例

（1）下記のコードは複数オブジェクト（マルチバージョンなし）を削除するサンプルコードを示しています。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// 削除するkeyリストを設定します。毎回最大で1000個までを削除できます
ArrayList<KeyVersion> keyList = new ArrayList<>();
// 削除するファイル名を入力します
keyList.add(new KeyVersion("aaa.txt"));
keyList.add(new KeyVersion("bbb.mp4"));
keyList.add(new KeyVersion("ccc/ddd.jpg"));
deleteObjectsRequest.setKeys(keyList);

// ファイルを一括削除します
try {
    DeleteObjectsResult deleteObjectsResult = cosclient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // 一部が完成し、一部が失敗した場合、MultiObjectDeleteExceptionは返されます
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // その他のエラーの場合（例えば、パラメータエラーや身分検証不合格等）、CosServiceExceptionは返されます
    e.printStackTrace();
} catch (CosClientException e) { // クライアントのエラーの場合、例えば、COSに接続できない場合
    e.printStackTrace();
}
```

（2）下記のコードは複数オブジェクト（マルチバージョンを含む）を削除するサンプルコードを示しています。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// 削除するkeyリストを設定します。毎回最大で1000個までを削除できます
ArrayList<KeyVersion> keyList = new ArrayList<>();
// 削除するファイル名を入力します
keyList.add(new KeyVersion("aaa.txt", "axbefagagaxxfafa"));
keyList.add(new KeyVersion("bbb.mp4", "awcafa1faxg0lx"));
keyList.add(new KeyVersion("ccc/ddd.jpg", "kafa1kxxaa2ymh"));
deleteObjectsRequest.setKeys(keyList);

// ファイルを一括削除します
try {
    DeleteObjectsResult deleteObjectsResult = cosclient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // 一部が完成し、一部が失敗した場合、MultiObjectDeleteExceptionは返されます
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // その他のエラーの場合（例えば、パラメータエラーや身分検証不合格等）、CosServiceExceptionは返されます
    e.printStackTrace();
} catch (CosClientException e) { // クライアントのエラーの場合、例えば、COSに接続できない場合
    e.printStackTrace();
}
```



### JavaScript SDKの使用

COSのJavaScript SDKはこの方法を提供しています。[JavaScript SDK APIドキュメントにおけるDelete Objectの部分](https://cloud.tencent.com/document/product/436/12260#delete-object)を参照してください。

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例は複数オブジェクトを削除する方法を示しています。

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

cos.deleteMultipleObject({
    Bucket: Bucket,
    Region: Region,
    Objects: [
        {Key: '1mb.zip'},
        {Key: '3mb.zip'},
    ]
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDKの使用

COSのNode.js SDKはこの方法を提供しています。[Node.js SDK APIドキュメントにおけるDelete Objectの部分](https://cloud.tencent.com/document/product/436/12264#delete-object)を参照してください。

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで```node test.js```を実行します。

#### コード例

下記のコード例は複数オブジェクトを削除する方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteMultipleObject({
    Bucket: Bucket,
    Region: Region,
    Objects: [
        {Key: '1mb.zip'},
        {Key: '3mb.zip'},
    ]
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。PHP SDK APIドキュメント[PHP SDK APIドキュメントにおけるファイル削除の部分](https://cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4.E6.96.87.E4.BB.B6)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. DeleteObjectを実行して複数オブジェクトを削除します。バケット名とオブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例は複数オブジェクトを削除する方法を示しています。

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'bucket-125000000',
        'Objects' => array(
            array(
                'Key' => 'string',
            ),
            // ... repeated
        ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。[Python SDK APIドキュメントにおけるファイル削除の部分](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. delete_objects()を実行して複数オブジェクトを削除します。バケット名と複数オブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例は複数オブジェクトを削除する方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.delete_objects(
    Bucket=bucket,
    Delete={
        "Quiet": "true",
        "Object": [
            {
                "Key": "test1.txt"
            },
            {
                "Key": "test2.txt"
            }
        ]
    }    
)
```

マルチバージョンを有効にした場合、指定のパラメータVersionIdを通じて指定のバージョンのオブジェクトを削除することができます。
```python
bucket = 'testbucket-123456789'
response = client.delete_objects(
    Bucket=bucket,
    Delete={
        "Quiet": "true",
        "Object": [
            {
                "Key": "test1.txt",
                "VersionId": "MTg0NDY3NDI1NjExNjQwNDUxMzU"
            },
            {
                "Key": "test2.txt",
                "VersionId": "MTg0NDY3NDI1NjExNjQwNDUxMzA"
            }
        ]
    }    
)
```
