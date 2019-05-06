## 適用シナリオ

デフォルトでは、バケットとオブジェクトはいずれもプライベートです。サードパーティにオブジェクトをダウンロードさせたい場合、しかもサードパーティにCAMアカウントまたは一時暗号鍵等を告知しかねる場合、事前署名付きURLの形で署名をサードパーティに、一時的なダウンロード操作用に提供することができます。有効の事前署名付きURLを取得したいかなる者でも、オブジェクトをダウンロードできます。

事前署名付きURLにつき、署名においてオブジェクト鍵が署名に含まれるように設定し、指定のオブジェクトのダウンロードのみを許可することができます。また、アプリにおいて事前署名付きURLの有効期間を指定することで、タイムアウトになると、当該URLが認証対象者以外の者に使用されないように確保することもできます。

## 使用方法

### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントの事前署名リンク生成の部分](https://cloud.tencent.com/document/product/436/12263#.E7.94.9F.E6.88.90.E9.A2.84.E7.AD.BE.E5.90.8D.E9.93.BE.E6.8E.A5)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. generatePresignedUrlを実行してダウンロード署名を取得します。httpのダウンロード入力はGETです。

#### コード例

（1）下記のコードは事前署名を生成するダウンロードリンクを示しています。

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名を設定します。バケット名はappidを含む必要があります
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 署名の期限切れ時間（選択可能）を設定します。期限切れ時間につき、制限がないが、現時点より遅ければよいです。未設定の場合、デフォルトでClientConfigにおける署名の期限切れ時間（5分間）を使用します
// ここでの署名が30分後に期限切れになるように設定します
Date expirationDate = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
req.setExpiration(expirationDate);

URL url = cosclient.generatePresignedUrl(req);
System.out.println(url.toString());
```

（2）`GeneratePresignedUrlRequest`はダウンロード時に返されるhttpヘッダーの設定に対応します。例えば、content-typeやcontent-disposition等。サンプルコードは下記のとおりです：

```java
// 1 ユーザー身分情報（appid, secretId, secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名を設定します。バケット名はappidを含む必要があります
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// ダウンロード時に返されるhttpヘッダーを設定します
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
String responseContentDispositon = "filename=\"abc.txt\"";
String responseCacheControl = "no-cache";
String expireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24 * 3600 * 1000));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(expireStr);
req.setResponseHeaders(responseHeaders);
URL url = cosclient.generatePresignedUrl(req);

System.out.println(url.toString());
```

（3）また、`GeneratePresignedUrlRequest`は匿名バケットのダウンロードリンクの生成にも対応します。匿名バケットのダウンロードリンクにおいて署名がいらないため、暗号鍵情報を入力する必要がありません。サンプルコードは下記のとおりです：

```java
// 1 匿名バケットに対して、身分情報を入力する必要がありません
COSCredentials cred = new AnonymousCOSCredentials();
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名を設定します。バケット名はappidを含む必要があります
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosclient.generatePresignedUrl(req);

System.out.println(url.toString());
```

### JavaScript SDKの使用

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例は事前署名認証によるダウンロードの方法を示しています。

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

cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg', // ダウンロードするファイルのパスを置き換えます
    Expires: 60
}, function (err, data) {
    console.log(err || data.Url);
});
</script>
```

### Node.js SDKの使用

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで```node test.js```を実行します。

#### コード例

下記のコード例は事前署名認証によるダウンロードの方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
var url = cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg', // ダウンロードするファイルのパスを置き換えます
    Expires: 60
});
console.log(url);
```
### Python SDKの使用

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. get_presigned_download_url()を実行して事前署名のダウンロードオブジェクトを取得します。バケット名とオブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例は事前署名認証によるダウンロードの方法を示しています。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換え
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換え
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                 # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'
download_url = client.get_presigned_download_url(
    Bucket=bucket,
    Key=file_name,
)
print download_url
```
