## 適用シナリオ

デフォルトでは、バケットとオブジェクトはいずれもプライベートです。サードパーティにオブジェクトをバケットにアップロードさせたい場合、しかもサードパーティにCAMアカウントまたは一時暗号鍵等を告知しかねる場合、事前署名付きURLの形で署名をサードパーティに、一時的なアップロード操作用に提供することができます。有効の事前署名付きURLを取得しているいかなる者でも、オブジェクトをアップロードできます。

事前署名付きURLにつき、署名においてオブジェクト鍵が署名に含まれるように設定し、指定のパスへのアップロードのみを許可することができます。またHTTPのリクエスト方法を設定し、詳しいオブジェクトの操作を制限することもできます。例えば：アップロード、ダウンロードや削除など。更に、アプリにおいて事前署名付きURLの有効期間を指定することで、タイムアウトになると、当該URLが認証対象者以外の者に使用されないように確保することもできます。

## 使用方法

### REST APIの使用

直接REST APIを使ってオブジェクトを取得するリクエストを送信することができます。[GET Objectドキュメント説明](https://cloud.tencent.com/document/product/436/7753)を参照してください。

### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントの事前署名リンク生成の部分](https://cloud.tencent.com/document/product/436/12263#.E7.94.9F.E6.88.90.E9.A2.84.E7.AD.BE.E5.90.8D.E9.93.BE.E6.8E.A5)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. generatePresignedUrlを実行してアップロード署名を取得します。httpの入力パラメータはPUTです。

#### コード例

下記のコード例は事前署名を生成するアップロードリンクを示しており、それでアップロードを行います。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントの生成
COSClient cosclient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
Date expirationTime = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
// 事前署名アップロードURLを生成します
URL url = cosclient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);

// 事前署名付きURLを使ってファイルをアップロードします
try {
    HttpURLConnection connection = (HttpURLConnection) url.openConnection();
    connection.setDoOutput(true);
    connection.setRequestMethod("PUT");
    OutputStreamWriter out = new OutputStreamWriter(connection.getOutputStream());
    // アップロードするデータを書き込みます
    out.write("This text uploaded as object.");
    out.close();
    int responseCode = connection.getResponseCode();
    System.out.println("Service returned response code " + responseCode);
} catch (ProtocolException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

### Node.js SDKの使用

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. テストファイルtest.jsを作成し、コマンドラインで```node test.js```を実行します。

#### コード例

```javascript
var COS = require('cos-nodejs-sdk-v5');
var request = require('request');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
var url = cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Method: 'PUT',
    Key: '1.jpg', // ダウンロードするファイルのパスを置き換えます
    Expires: 60
});
console.log(url);

// 自動でファイルをアップロードします
request({
    method: 'PUT',
    url: url,
    body: fs.readFileSync('./1.jpg'),
}, function (err, response, body) {
    console.log(response.statusCode);
    console.log(response.headers.etag);
    console.log(body);
});
```
