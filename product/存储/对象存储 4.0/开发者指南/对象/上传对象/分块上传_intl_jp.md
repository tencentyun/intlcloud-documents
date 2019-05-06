## 適用シナリオ

マルチパートアップロードは弱いネットワークまたは広い帯域幅環境でのより大きなサイズのオブジェクトのアップロードに適用します。COSのコンソールとSDKにより単一オブジェクトを複数のパートに分けてアップロードできます。また自らオブジェクトを分けてAPIを呼び出して各パートをアップロードすることもできます。マルチパートアップロードのいくつかのメリットがあります。

- 弱いネットワークでは、より小さなサイズのパートを使用すると、ネットワークのエラーによる中断の影響を低減させ、オブジェクトのブレイクポイントから再開を実現できます。
- 広い帯域幅環境では、同時にアップロードするオブジェクトパートは十分にネットワーク帯域幅を利用できるため、ランダムアップロードは最後のオブジェクトの組み合わせに影響及ぼすことがありません。
- マルチパートアップロードを利用する場合、単独のビッグサイズのオブジェクトのアップロードをいつでも中止・再開できます。終止しない限り、すべて未完成のオブジェクトのアップロードを随時再開できます。
- マルチパートアップロードは、オブジェクト全体のサイズが不明である場合のアップロードにも適用します。完全なサイズを取得するためにアップロードしてから、オブジェクトに組み合わせることができます。

アップロードの際に、これらのパートは連番となります。各パートを単独でアップロードし、あるいはランダムでアップロードして良いです。最後、COSはパートを番号順により改めて完全なオブジェクトに組み合わせます。いかなるパートの送信が失敗しても、改めてそのパートを送信できます。その他のパートと内容の完全性に影響を及ぼすことがありません。通常は、弱いネットワークでは、単一オブジェクトが20MB以上である場合、優先的にマルチパートアップロードを利用してください。広い帯域幅環境では、100MB以上のオブジェクトをマルチパートアップロードして良いです。

## 使用方法

### REST APIの使用

REST APIを使って直接マルチパートアップロードのリクエストを送信することができます。下記のAPIドキュメントを参照してください。

- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746)
- [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742)
- [Upload Part](https://cloud.tencent.com/document/product/436/7750)
- [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740)

### C++ SDKの使用

COSのC++ SDKはこの方法を提供しています。[C++ SDK APIドキュメントのマルチパートアップロード操作の部分](https://cloud.tencent.com/document/product/436/12302#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C)を参照してください。

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. InitMultiUpload()を呼び出してマルチパートアップロードを初期化し、アップロードIDを取得します。
3. 繰り返してUploadPartData()を呼び出してパートをアップロードします。そのうち、UploadPartDataReqにバケット名、オブジェクト鍵名、アップロードID、パート番号およびアップロードするファイルの内容を提供する必要があります。
4. CompleteMultiUpload()を実行してマルチパートアップロードを完成します。バケット名、オブジェクト鍵名、UploadId、およびすべてのパート情報を提供する必要があります。

#### コード例

下記のコード例はオブジェクトをマルチパートアップロードする方法を示しています。

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";
std::string upload_id = "";
std::vector<std::string> etags;
std::vector<int64_t> part_nums;

// 1.InitMultiUploadを呼び出してuploadIdを取得します
qcloud_cos::InitMultiUploadReq init_req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp init_resp;
qcloud_cos::CosResult init_result = cos.InitMultiUpload(init_req, init_resp);

if (init_result.IsSucc()) {
    upload_id = init_resp.GetUploadId();
} else {
    // do sth
}

// 2.1 最初のパートをアップロードします
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(1);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // アップロードができたら、パート番号および返されたetagを記録する必要があります
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(1);
    }
    is.close();
}

// 2.2 2番目のパートをアップロードします
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // アップロードができたら、パート番号および返されたetagを記録する必要があります
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(2);
    }
    is.close();
}

// 2.x後続のパートをアップロードします
...

// 3. マルチパートアップロードを終了します
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_nums);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);

```

AbortMultiUpload()でマルチパートアップロードを終了することができます。バケット名、オブジェクト鍵名およびUploadIdを提供する必要があります。
```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

list_parts()でマルチパートアップロードをリストすることができます。バケット名、オブジェクト鍵名およびUploadIdを提供する必要があります。
``` cpp
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);
```

### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントPUT Objectにおけるマルチパートアップロードの部分](https://cloud.tencent.com/document/product/436/12263#put-object.EF.BC.88.E4.B8.8A.E4.BC.A0-object.EF.BC.89)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. initiateMultipartUploadでマルチパートアップロードを初期化して新しいuploadidを取得し、あるいはlistMultipartUploadsを呼び出して前の未完成のマルチパートアップロードからuploadidを取得します。
3. アップロードされたパートをlistPartsを使って取得できます。アップロードしていないパートにつき、uploadPartを使ってパートのデータをアップロードし、あるいはcopyPartを使ってほかのファイルからパートを既存ファイルにコピーできます。これでブレイクポイントから再開機能を実現します。アップロードされたパートに対して再びuploadPartあるいはcopyPartを呼び出したら、アップロードされたパートのデータを上書きします。
4. completeMultipartUploadを使ってマルチパートアップロードを完成し、あるいはabortMultipartUploadを呼び出してマルチパートアップロードを終止します。

#### コード例

（1）`InitiateMultipartUploadRequest`はマルチパートアップロード初期化のリクエストであり、マルチパートアップロードのパスやストレージタイプ等の情報を含みます。initiateMultipartUploadを呼び出すことで新しいマルチパートアップロードIDを取得できます。

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
InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);
// ストレージタイプを設定し、デフォルトでは、標準（standard）、低頻度（standard_ia）です。
request.setStorageClass(StorageClass.Standard_IA);
try {
    InitiateMultipartUploadResult initResult = cosclient.initiateMultipartUpload(request);
    //uploadidの取得
    String uploadId =  initResult.getUploadId();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

（2） `UploadPartRequest`はマルチパートアップロードのリクエストであり、アップロードするデータやパート番号を含みます。uploadPartを呼び出してブロックをアップロードし、パートのpartEtagを取得できます。

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
// uploadid（initiateMultipartUploadあるいはListMultipartUploadsを通じて取得します）
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

// アップロードするデータを生成します。ここでは1Mのデータを1つ初期化します
byte data[] = new byte[1024 * 1024];
UploadPartRequest uploadPartRequest = new UploadPartRequest();
uploadPartRequest.setBucketName(bucketName);
uploadPartRequest.setKey(key);
uploadPartRequest.setUploadId(uploadId);
// パートのデータソースの入力ストリームを設定します
uploadPartRequest.setInputStream(new ByteArrayInputStream(data));
// パートの長さを設定します
uploadPartRequest.setPartSize(data.length); // データの長さを設定します
uploadPartRequest.setPartNumber(10);     // アップロードするpart番号が10だと仮定します

try {
    UploadPartResult uploadPartResult = cosclient.uploadPart(uploadPartRequest);
    PartETag partETag = uploadPartResult.getPartETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

（3） `CompleteMultipartUploadRequest`はマルチパートアップロード完成のリクエストであり、前にアップロードしたすべてのパートのpartEtagを入力する必要があります。completeMultipartUploadを呼び出してマルチパートアップロードを完成します。サンプルコードを下記に示します。

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
// uploadid（initiateMultipartUploadあるいはListMultipartUploadsを通じて取得します）
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

// ここでブランクのキューを初期化することで、アップロードされたシャード情報を保存します。コードを直接実行してはいけません。前のuploadpartあるいはlist partsの結果から取得し、partEtagsキューに導入する必要があります
List<PartETag> partETags = new LinkedList<>();

//シャードアップロード終了後、completeを呼び出してシャードアップロードを完成します
CompleteMultipartUploadRequest completeMultipartUploadRequest =
        new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
try {
    CompleteMultipartUploadResult completeResult =
            cosclient.completeMultipartUpload(completeMultipartUploadRequest);
    String etag = completeResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

（4） `AbortMultipartUploadRequest`はマルチパートアップロード終了のリクエストであり、completeしていないマルチパートアップロードを終了します。中断・終了前にアップロードされたパートを示します。abortMultipartUploadを呼び出してマルチパートアップロードのリクエストを終了します。サンプルコードを下記に示します。

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
// uploadid（initiateMultipartUploadあるいはListMultipartUploadsを通じて取得します）
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosclient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

（5）`ListPartsRequest`はアップロードされたパートをリストするリクエストであり、ブレイクポイントから再開に用いられます。listPartsを呼び出してアップロードされたパートを取得します。サンプルコードを下記に示します。

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
// uploadid（initiateMultipartUploadあるいはListMultipartUploadsを通じて取得します）
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

List<PartETag> partETags = new LinkedList<>();      // アップロードされたシャード情報を保存します
PartListing partListing = null;
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
do {
    try {
        partListing = cosclient.listParts(listPartsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
    } catch (CosClientException e) {
        e.printStackTrace();
    }
    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }
    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());

cosclient.shutdown();
```

（6）`CopyPartResult`はパートcopyのリクエストです。当該パートのデータがほかのファイルの特定部分に由来することを意味します。コピーするソースファイルのパス、バケット情報、バイト範囲により、copyPartを呼び出してパートをコピーできます。サンプルコードを下記に示します。

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
// uploadid（initiateMultipartUploadあるいはListMultipartUploadsを通じて取得します）
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

CopyPartRequest copyPartRequest = new CopyPartRequest();
// コピーされるソースファイルの位置するregion
copyPartRequest.setSourceBucketRegion(new Region("ap-beijing-1"));
// コピーされるソースファイルのbucket名
copyPartRequest.setSourceBucketName(bucketName);
// コピーされるソースファイルのパス
copyPartRequest.setSourceKey("aaa/ccc.txt");
// コピーされるソースファイルのデータ範囲（content-rangeに似ています）を指定します
copyPartRequest.setFirstByte(0L);
copyPartRequest.setLastByte(1048575L);
// 目標bucket名
copyPartRequest.setDestinationBucketName(bucketName);
// 目標パス名
copyPartRequest.setDestinationKey(key);

// uploadid
copyPartRequest.setUploadId(uploadId);
try {
    CopyPartResult copyPartResult = cosclient.copyPart(copyPartRequest);
    PartETag partETag = copyPartResult.getPartETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```
### JavaScript SDKの使用

COSのJavaScript SDKはこの方法を提供しています。[JavaScript SDK APIドキュメントのマルチパートアップロード操作の部分](https://cloud.tencent.com/document/product/436/12260#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C)を参照してください。

#### 手順説明

1. 署名サーバーを用意し、auth.php APIをフロントエンドに与えて署名を取得します。[バックエンド署名例](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)を参照してください。

2. テストファイルtest.htmlを作成し、下記に示すコードを書込み、静的サーバーに導入し、` http://127.0.0.1/test.html `でアクセスします。

#### コード例

下記のコード例はオブジェクトをマルチパートアップロードする方法を示しています。

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

    cos.sliceUploadFile({
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

COSのNode.js SDKはこの方法を提供しています。[Node.js SDK APIドキュメントのマルチパートアップロード操作の部分](https://cloud.tencent.com/document/product/436/12264#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C)を参照してください。

#### 手順説明

1. npm依存パッケージのインストール：
```shell
npm i cos-nodejs-sdk-v5
```

2. アップロードされるファイル1.jpgを現在のディレクトリに入れます。

3. テストファイルtest.jsを作成し、コマンドラインで`node test.js`を実行します。

#### コード例

下記のコード例はオブジェクトをマルチパートアップロードする方法を示しています。

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; //ユーザーのSecretIdに置き換えます
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    //ユーザーのSecretKeyに置き換えます
var Bucket = 'test-1250000000';                        //ユーザー操作のBucketに置き換えます
var Region = 'ap-guangzhou';                           //ユーザー操作のRegionに置き換えます

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.sliceUploadFile({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    FilePath: '1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDKの使用

COSのPHP SDKはこの方法を提供しています。[PHP SDK APIドキュメントのマルチパートアップロード操作の部分](https://cloud.tencent.com/document/product/436/12267#.E5.88.86.E5.9D.97.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0)を参照してください。

#### 手順説明

1. クライアントcosClientを初期化します。
2. upload方法を実行してデータストリームをアップロードします。バケット名とオブジェクト鍵名を提供する必要があります。
3. fopenを通じてファイルストリームをアップロードします。

#### コード例

下記のコード例はオブジェクトをマルチパートアップロードするステップを示しています。

* メモリのアップロード：
```php
try {
    $result = $cosClient->upload(
                 $bucket='testbucket-125000000',
                 $key = '111.txt',
                 $body = 'HELLO';
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
* ファイルストリームのアップロード：
```php
try {
    $result = $cosClient->upload(
                 $bucket='testbucket-125000000',
                 $key = '111.txt',
                 $body = fopen($pathToFile, 'r+'));
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。Python SDK APIドキュメントにおける以下の部分を参照してください。

- [マルチパートアップロードの作成](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [パートのアップロード](https://cloud.tencent.com/document/product/436/12270#.E4.B8.8A.E4.BC.A0.E5.88.86.E5.9D.97)
- [マルチパートアップロードの完成](https://cloud.tencent.com/document/product/436/12270#.E5.AE.8C.E6.88.90.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [マルチパートアップロードの放棄](https://cloud.tencent.com/document/product/436/12270#.E6.94.BE.E5.BC.83.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [マルチパートアップロードのリスト](https://cloud.tencent.com/document/product/436/12270#.E5.88.97.E5.87.BA.E4.B8.8A.E4.BC.A0.E5.88.86.E5.9D.97)

#### 手順説明

1. CosConfig類で構成し、クライアントCosS3Clientを初期化します。
2. create_multipart_upload()を実行してマルチパートアップロードを初期化します。バケット名とオブジェクト鍵名を提供する必要があります。
3. 繰返してupload_part()を実行してパートをアップロードします。バケット名、オブジェクト鍵名、UploadIdおよび単独のパートの内容を提供する必要があります。
4. complete_multipart_upload()を実行してマルチパートアップロードを完成します。バケット名、オブジェクト鍵名、UploadIdおよびすべてのパート情報を提供する必要があります。

#### コード例

下記のコード例はオブジェクトをマルチパートアップロードする方法を示しています。

```python
secret_id = 'xxxxxxxx'     # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'     # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'     # ユーザーのRegionに置き換える
token = ''                  # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'

# 1.マルチパートアップロードを初期化します
response = client.create_multipart_upload(
    Bucket=bucket,
    Key=file_name       
)
uploadid = response['UploadId']

# 2.単独のパートをアップロードします
lst = list()
part_number = 1
with open('test.txt', 'rb') as fp:
    while True:
        data = fp.read(1024*1024)
        if data == "":
            break
        response = client.upload_part(
            Bucket=bucket,
            Key=file_name,
            UploadId=uploadid,
            PartNumber=part_number,
            Body=data
        )
        lst.append({'PartNumber': part_number, 'ETag': response['ETag']})
        part_number += 1

# 3.マルチパートアップロードを完成します
response = client.complete_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid,
    MultipartUpload={'Part': lst}
)
```

abort_multipart_upload()を使ってマルチパートアップロードを終了できます。バケット名、オブジェクト鍵名およびUploadIdを提供する必要があります。
```python
response = client.abort_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid
)
```

list_parts()を使ってマルチパートアップロードをリストすることができます。バケット名、オブジェクト鍵名およびUploadIdを提供する必要があります。
```python
response = client.list_parts(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid
)
```

list_multipart_uploads()を使ってバケットにおけるすべての未完成のマルチパートアップロードをリストできます。バケット名を提供する必要があります。
```python
response = client.list_multipart_uploads(
    Bucket=bucket
)
```
####
