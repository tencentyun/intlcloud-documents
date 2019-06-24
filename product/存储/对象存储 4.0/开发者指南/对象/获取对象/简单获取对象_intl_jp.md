## 適用シナリオ

COSにおけるオブジェクトを取得するリクエストを直接送信することができます。オブジェクトの取得は下記の機能に対応します。

- 完全なる単一オブジェクトの取得：直接GETリクエストを送信すると完全なるオブジェクトデータを取得できます。
- 単一オブジェクトの一部の内容の取得：GETリクエストに`Range`リクエストヘッダーを入力すれば、特定のバイト範囲の検索ができます。ただし、複数範囲の検索に対応しません。

オブジェクトのメタデータはHTTP応答ヘッダーとしてオブジェクト内容につれて返されます。GETリクエストは、URLパラメータにより応答された一部のメタデータ値をカバーすることに対応します。例えば、`Content-Dispositon`の応答値。変更可能な応答ヘッダーは以下を含みます。

- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## 使用方法

### REST APIの使用

直接REST APIを使ってオブジェクトを取得するリクエストを送信することができます。[GET Objectドキュメント説明](https://cloud.tencent.com/document/product/436/7753)を参照してください。

### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントにおけるGet Objectの部分](https://cloud.tencent.com/document/product/436/12302#get-object)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. GetObject()を実行してファイルをローカルまたはデータストリームにダウンロードします。バケット名とオブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトを取得する方法を示しています。

``` cpp
//ローカルファイルにダウンロードします
{
    //requestはappid、bucketname、objectおよびローカルのパスを提供する必要があります（ファイル名を含みます）
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // ダウンロードに成功した場合、GetObjectByFileRespのメンバー関数を呼び出すことができます
    } else {
        //ダウンロードに失敗した場合、CosResultのメンバー関数を呼び出し、エラー情報（例えばrequestID等）を出力することができます
    }
}

//ストリームにダウンロードします
{
    //requestに関して、appid、bucketname、objectおよび出力ストリームを提供する必要があります
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        //ダウンロードに成功した場合、GetObjectByStreamRespのメンバー関数を呼び出すことができます
    } else {
        //ダウンロードに失敗した場合、CosResultのメンバー関数を呼び出し、エラー情報（例えばrequestID等）を出力することができます
    }
}

//マルチスレッドでファイルをローカルにダウンロードします
{
    //requestはappid、bucketname、objectおよびローカルのパスを提供する必要があります（ファイル名を含みます）
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        //ダウンロードに成功した場合、MultiGetObjectRespのメンバー関数を呼び出すことができます
    } else {
        //ダウンロードに失敗した場合、CosResultのメンバー関数を呼び出し、エラー情報（例えばrequestID等）を出力することができます
    }
}
```

Requestのメンバー関数を設定することで、特定の応答ヘッダーを設定することができます。

``` cpp
//応答ヘッダーにおけるContent-Typeパラメータの設定
void SetResponseContentType(const std::string& str);

//応答ヘッダーにおけるContent-Languageパラメータの設定
void SetResponseContentLang(const std::string& str);

//応答ヘッダーにおけるContent-Expiresパラメータの設定
void SetResponseExpires(const std::string& str);

//応答ヘッダーにおけるCache-Controlパラメータの設定
void SetResponseCacheControl(const std::string& str);

//応答ヘッダーにおけるContent-Dispositionパラメータの設定
void SetResponseContentDisposition(const std::string& str);

//応答ヘッダーにおけるContent-Encodingパラメータの設定
void SetResponseContentEncoding(const std::string& str);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントにおけるGet Objectの部分](https://cloud.tencent.com/document/product/436/12263#get-object)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. getObject方法を実行して入力ストリームを取得し、あるいは内容をローカルに保存します。

#### コード例
（1）下記のコード例はオブジェクトをダウンロードする方法を示しています（バージョン制御なし）。

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名を設定します
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    // ファイルのダウンロード
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // 入力ストリームを取得します
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // 入力ストリームを終了します
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
（2）`GetObjectRequest`はオブジェクトから検索するデータバイトの範囲を指定することに対応します。下記のコードはバイトの指定方法を示しています。

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
//2 バケットの地域を設定します。COS地域の略称については、https://cloud.tencent.com/document/product/436/6224を参照してください
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名を設定します
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    // 前の11バイトをダウンロードすることを設定します
    getObjectRequest.setRange(0, 10);
    // ファイルのダウンロード
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // 入力ストリームを取得します
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // 入力ストリームを終了します
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
（3）オブジェクトの検索時、`ResponseHeaderOverrides`を実行し、また関連リクエストの属性を設定することで、応答ヘッダー値を置き換えることもできます。下記にこの方法の例を示します。

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名を設定します
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
    String responseContentType="image/x-icon";
    String responseContentEncoding = "gzip,deflate,compress";
    String responseContentLanguage = "zh-CN";
    String responseContentDispositon = "filename=\"abc.txt\"";
    String responseCacheControl = "no-cache";
    String expireStr = DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24 * 3600 * 1000));
    responseHeaders.setContentType(responseContentType);
    responseHeaders.setContentEncoding(responseContentEncoding);
    responseHeaders.setContentLanguage(responseContentLanguage);
    responseHeaders.setContentDisposition(responseContentDispositon);
    responseHeaders.setCacheControl(responseCacheControl);
    responseHeaders.setExpires(expireStr);
    getObjectRequest.setResponseHeaders(responseHeaders);
    // ファイルのダウンロード
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // 入力ストリームを取得します
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // 入力ストリームを終了します
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
### JavaScript SDKの使用

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例は簡単にオブジェクトを取得する方法を示しています。

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

cos.getObject({
    Bucket: config.Bucket,
    Region: config.Region,
    Key: '1.txt',
}, function (err, data) {
    console.log(err || 'ファイル内容のサイズ：' + data.Body.length);
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
下記のコード例は簡単にオブジェクトを取得する方法を示しています。

```javascript
var fs = require('fs');
var path = require('path');
var COS = require('..');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.getObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    Output: fs.createWriteStream(path.resolve(__dirname, '1.download.jpg'))
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントにおけるファイルのダウンロードの部分](https://cloud.tencent.com/document/product/436/12267#.E4.B8.8B.E8.BD.BD.E6.96.87.E4.BB.B6)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. getObjectを実行してオブジェクトを取得します。バケット名を提供する必要があります。
3. SaveAsフィールドを追加し、取得したデータストリームをローカルファイルとして保存します。

#### コード例

下記のコード例は簡単にオブジェクトを取得する方法を示しています。

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => 'hello.txt',
        'SaveAs' => 'hello.txt'));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。[Python SDK APIドキュメントにおけるファイルのダウンロードの部分](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD)を参照してください。

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. get_object()を実行してデータストリームを取得します。バケット名とオブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例は簡単にオブジェクトを取得する方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換え
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
)
# オブジェクトを取得してローカルファイルとして保存します
response['Body'].get_stream_to_file('output.txt')
```

オブジェクトのファイルストリームを取得したい場合は、get_raw_stream()により実現できます。
```python
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
)
fp = response['Body'].get_raw_stream()
# read()を呼び出してファイルストリームを読み取ります
print fp.read(2)
```

Rangeパラメータの設定を通じて指定範囲のオブジェクトを取得できます。そのフォーマットはbytes=first-lastです。
```python
# オブジェクトの前の10バイトを取得します
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
    Range='bytes=0-9'
)
```

Response Headerのパラメータを設定することで、特定の応答ヘッダーを設定することができます。
```python
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
    ResponseCacheControl='no-cache',
    ResponseContentDisposition='attachment; filename=test.txt',
    ResponseContentEncoding='gzip',
    ResponseContentLanguage='zh-cn',
    ResponseContentType='text/html',
    ResponseExpires='Tue, 05 Dec 2017 10:01:19 GMT'
)
```
