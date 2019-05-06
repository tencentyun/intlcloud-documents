## 適用シナリオ

5GB以上のオブジェクトをコピーする場合、パートコピーを選択する必要があります。パートアップロードのAPIで新しいオブジェクトを作成し、またPart Copyの機能で、`x-cos-copy-source`ヘッダーを付けてソースオブジェクトを指定します。そのプロセスは以下を含みます。

1. マルチパートアップロードのオブジェクトを初期化します。
2. ソースオブジェクトのデータをコピーします。`x-cos-copy-range`ヘッダーを指定できます。毎回5GBまでのデータをコピーできます。
3. マルチパートアップロードを完成します。

Tencent COSが提供するSDKを使って、パートコピーの機能を簡単に実現できます。

## 使用方法

### C++ SDKの使用

COSのC++ SDKは方法を提供しています。C++ SDK APIドキュメントにおける下記の部分を参照してください。

- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/12302#initiate-multipart-upload)
- [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/12302#complete-multipart-upload)

#### 手順説明

1. 構成ファイルのパス初期化CosConfigを入力し、CosAPIオブジェクトを初期化します。
2. InitMultiUpload()を呼び出してマルチパートアップロードを初期化し、アップロードIDを取得します。
3. 繰り返してUploadPartCopyData()を呼び出してパートをコピーします。そのうち、UploadPartCopyDataReqにバケット名、オブジェクト鍵名、アップロードID、パート番号を提供し、またUploadPartCopyDataReq::SetXCosCopySourceを使ってコピー待ちのソースファイルを設定する必要があります。
4. CompleteMultiUpload()を実行してマルチパートアップロードを完成します。バケット名、オブジェクト鍵名、UploadId、およびすべてのパート情報を提供する必要があります。

#### コード例

下記のコード例はオブジェクトをパートコピーする方法を示しています。

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";
std::string upload_id = "";
std::vector<std::string> etags;
std::vector<int64_t> part_nums;

// 1.InitMultiUploadを呼び出してuploadIdを取得します
qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult init_result = cos.InitMultiUpload(init_req, init_resp);

if (init_result.IsSucc()) {
    upload_id = init_resp.GetUploadId();
} else {
    // do sth
}

// 2.1 最初のシャードをコピーします
{
    std::string part_number = 1;
    qcloud_cos::UploadPartCopyDataReq req(bucket_name, object_name, upload_id, part_number);
    req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
    qcloud_cos::UploadPartCopyDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartCopyData(req, &resp);
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(part_number);
    }
}

// 2.2 2番目のシャードをコピーします
{
    std::string part_number = 2;
    qcloud_cos::UploadPartCopyDataReq req(bucket_name, object_name, upload_id, part_number);
    req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
    qcloud_cos::UploadPartCopyDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartCopyData(req, &resp);
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(part_number);
    }
}

// 2.x 次のシャードをコピーします
...

// 3. CompleteMultiUploadを呼び出してシャードコピーを終了します
qcloud_cos::CompleteMultiUploadReq comp_req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp comp_resp;
comp_req.SetEtags(etags);
comp_req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult comp_result = cos.CompleteMultiUpload(comp_req, &comp_resp);
```

copy()を使ってオブジェクトをコピーすることができます。自動でコピーソースオブジェクトのサイズと地域によりそれぞれのAPIを呼び出します。バケット名、オブジェクト鍵名およびコピーソースバケット、ソースオブジェクト鍵、ソース地域を提供するだけでよいです。

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";

qcloud_cos::CopyReq req(bucket_name, object_name);
qcloud_cos::CopyResp resp;

req.SetXCosCopySource("sevenyou-54321.cos.ap-beijing.myqcloud.com/sevenyou_copy_test");
qcloud_cos::CosResult result = cos.Copy(req, &resp);
```
### Java SDKの使用

COSのJava SDKはこの方法を提供しています。[Java SDK APIドキュメントにおけるファイルコピーの部分](https://cloud.tencent.com/document/product/436/12263#.E6.8B.B7.E8.B4.9D.E6.96.87.E4.BB.B6)を参照してください。

#### 手順説明

1. クライアントcosclientを初期化します。
2. TransferManagerが提供する高級API copyを使ってコピーを完成します。

#### コード例

5G以上のファイルにつき、マルチパートアップロードにおけるcopypartを通じて実現する必要があります。ステップが複雑なので、TransferManagerにはcopy APIがカプセル化されています。ファイルサイズに応じて自動でAPIを選択できる上、5G以上のファイルコピーにも対応しています。当該APIを使ってファイルのcopyを行うことをおすすめします。サンプルコードを下記に示します。

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントを生成します
COSClient cosclient = new COSClient(cred, clientConfig);


ExecutorService threadPool = Executors.newFixedThreadPool(32);
// threadpoolを入力し、スレッドプールを入力しなければ、デフォルトではTransferManagerにシングルスレッドのスレッドプールが生成されます。
TransferManager transferManager = new TransferManager(cosclient, threadPool);

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
    Copy copy = transferManager.copy(copyObjectRequest);
    // 非同期結果copyを返し、waitForCopyResultを同期的に呼び出してcopyの終了を待つことができ、成功した場合、CopyResultを返し、失敗した場合、異常をスローします。
    CopyResult copyResult = copy.waitForCopyResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

transferManager.shutdownNow();
cosclient.shutdown();
```



### PHP SDKの使用

#### 手順説明

1. クライアントcosClientを初期化します。
2. Copyパートコピーオブジェクトを実行します。バケット名とオブジェクト鍵名を提供する必要があります。

#### コード例

下記のコード例はオブジェクトをパートコピーする方法を示しています。

```php
try {
    $result = $cosClient->Copy($bucket = 'bucket-125000000',
        $key = 'hello.txt',
        $copysource = 'bucket-appid.region.myqcloud.com/cos_path',);
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDKの使用

COSのPython SDKはこの方法を提供しています。Python SDK APIドキュメントにおける以下の部分を参照してください。

- [マルチパートアップロードの作成](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [マルチパートアップロードの完成](https://cloud.tencent.com/document/product/436/12270#.E5.AE.8C.E6.88.90.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)

#### 手順説明

1. CosConfig類により構成します。クライアントCosS3Clientを初期化します。

2. create_multipart_upload()を実行してマルチパートアップロードを初期化します。バケット名とオブジェクト鍵名を提供する必要があります。

3. 繰返してupload_part_copy()を実行してパートをコピーします。バケット名、オブジェクト鍵名、UploadIdおよび単独のパートの内容を提供する必要があります。

4. complete_multipart_upload()を実行してマルチパートアップロードを完成します。バケット名、オブジェクト鍵名、UploadIdおよびすべてのパート情報を提供する必要があります。

#### コード例

下記のコード例はオブジェクトをパートコピーする方法を示しています。

```python
secret_id = 'xxxxxxxx'     # ユーザーのsecretIdに置き換える
secret_key = 'xxxxxxx'     # ユーザーのsecretKeyに置き換える
region = 'ap-beijing-1'    # ユーザーのRegionに置き換える
token = ''                 # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。

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

# 2.単独のパートをコピーします
copy_source = {
    'Bucket': 'test-121212121',
    'Key': '10GB.txt',
    'Region': 'ap-guangzhou'
}
lst = list()
part_number = 1

response = client.upload_part_copy(
        Bucket=bucket,
        Key=file_name,
        UploadId=uploadid,
        PartNumber=part_number,
        CopySource=copy_source,
        CopySourceRange='bytes=0-1048575'
)
lst.append({'PartNumber': part_number, 'ETag': response['ETag']})
part_number += 1

response = client.upload_part_copy(
        Bucket=bucket,
        Key=file_name,
        UploadId=uploadid,
        PartNumber=part_number,
        CopySource=copy_source,
        CopySourceRange='bytes=1048576-2097151'
)
lst.append({'PartNumber': part_number, 'ETag': response['ETag']})
part_number += 1
# more ...

# 3.マルチパートアップロードを完成します
response = client.complete_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid,
    MultipartUpload={'Part': lst}
)
```

copy()を使ってオブジェクトをコピーすることができます。自動でコピーソースオブジェクトのサイズと地域によりそれぞれのAPIを呼び出します。バケット名、オブジェクト鍵名およびコピーソースバケット、ソースオブジェクト鍵、ソース地域を提供するだけでよいです。
```python
bucket = 'testbucket-123456789'
file_name = 'test.txt'
copy_source = {
    'Bucket': 'test-121212121',
    'Key': '10GB.txt',
    'Region': 'ap-guangzhou'
}
response = client.copy(
    Bucket=bucket,
    Key=file_name,
    CopySource=copy_source
)
```
