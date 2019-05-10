## 적용 시나리오

5GB보다 큰 객체를 복사하려면 멀티파트 복사를 사용해야 합니다. 멀티파트 업로드한 API를 사용하여 새로운 객체를 생성하고 Part Copy의 기능을 사용하여 `x-cos-copy-source` 헤더를 전달하며 소스 객체를 지정합니다. 프로세스는 다음과 같습니다.

1. 멀티파트 업로드한 객체를 초기화합니다.
2. 소스 객체의 데이터를 복사합니다. `x-cos-copy-range` 헤더를 지정하고 한 번에 최대 5GB의 데이터를 복사할 수 있습니다.
3. 멀티파트 업로드 완료.

Tencent Cloud COS에서 제공하는 SDK를 사용하여 멀티파트 복사를 손쉽게 완성할 수 있습니다.

## 사용 방법

### C++ SDK 사용

COS의 C++ SDK에서 이 방법을 제공하며 C++ SDK API 문서의 다음 부분을 참조할 수 있습니다.

- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/12302#initiate-multipart-upload)
- [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/12302#complete-multipart-upload)

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. InitMultiUpload()를 호출하여 멀티파트 업로드를 초기화하고 업로드 ID를 가져옵니다.
3. 부품을 복사하려면 UploadPartCopyData() 방법을 반복적으로 호출합니다. 버킷 이름,객체 키 이름, 업로드 ID 및 부품 번호는 UploadPartCopyDataReq에 포함되어야 합니다. UploadPartCopyDataReq::SetXCosCopySource를 사용하여 복사할 소스 파일을 설정할 수 있습니다.
4. CompleteMultiUpload() 방법을 실행하여 멀티파트 업로드를 완료합니다. 버킷 이름, 객체 키 이름, UploadID 및 모든 파트 정보가 필요합니다.

#### 예제 코드

다음 예제 코드는 멀티파트 업로드하는 방법을 보여줍니다.

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";
std::string upload_id = "";
std::vector<std::string> etags;
std::vector<int64_t> part_nums;

// 1. InitMultiUpload를 호출하여 uploadID를 가져옵니다.
qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult init_result = cos.InitMultiUpload(init_req, init_resp);

if (init_result.IsSucc()) {
    upload_id = init_resp.GetUploadId();
} else {
    // do sth
}

// 2.1. 첫 샤딩을 복사합니다.
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

// 2.2. 두 번째 샤딩을 복사합니다.
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

// 2.x 후속 샤딩을 복사합니다.
...

//.3. CompleteMultiUpload를 호출하여 멀티파트 복사를 완료합니다.
qcloud_cos::CompleteMultiUploadReq comp_req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp comp_resp;
comp_req.SetEtags(etags);
comp_req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult comp_result = cos.CompleteMultiUpload(comp_req, &comp_resp);
```

copy() 방법을 통해 객체를 복사할 수 있습니다. 복사할 소스 객체의 크기와 소재 지역을 기반으로 자동으로 API를 호출합니다. 버킷 이름, 객체 키 이름, 복사할 소스 버킷, 소스 객체 키 및 소스 지역만 제공하면 됩니다.

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
### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 복사 부분](https://cloud.tencent.com/document/product/436/12263#.E6.8B.B7.E8.B4.9D.E6.96.87.E4.BB.B6)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. TransferManager에서 제공하는 고급 copy API를 사용하여 복사를 완성합니다.

#### 예제 코드

5GB보다 큰 파일을 복사하려면 멀티파트 업로드 중의 copypart를 통해서 구현해야 합니다. 단계가 복잡합니다. 따라서 copy API가 TransferManager에 캡슐화되어 파일 크기에 따라 자동적으로 API 선택을 지원하여 5GB가 넘는 파일의 복사도 지원합니다. 이 API는 파일 복사에 권장됩니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);


ExecutorService threadPool = Executors.newFixedThreadPool(32);
// threadpool을 입력합니다. 스레드 풀이 없으면 기본적으로 단일 스레드 풀이 TransferManager에 생성됩니다.
TransferManager transferManager = new TransferManager(cosclient, threadPool);

// 복사할 bucket region입니다. 교차 지역 복사가 지원됩니다.
Region srcBucketRegion = new Region("ap-shanghai");
// 소스 버킷. 버킷 이름에는 appid가 포함되어야 합니다.
String srcBucketName = "srcBucket-1251668577";
// 복사할 소스 파일입니다.
String srcKey = "aaa/bbb.txt";
// 대상 버킷입니다. 버킷 이름에는 appid가 포함되어야 합니다.
String destBucketName = "destBucket-1251668577";
// 복사할 대상 파일입니다.
String destKey = "ccc/ddd.txt";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest);
    返回一个异步结果copy, 可同步的调用waitForCopyResult等待copy结束, 成功返回CopyResult, 失败抛出异常.
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



### PHP SDK 사용

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. Copy를 실행하여 멀티파트로 객체를 복사합니다. 버킷 이름과 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 멀티파트 업로드하는 방법을 보여줍니다.

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
### Python SDK 사용

COS의 Python SDK에서 이 방법을 제공하며 Python SDK API 문서의 다음 부분을 참조할 수 있습니다.

- [멀티파트 업로드 생성](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [멀티파트 업로드 완료](https://cloud.tencent.com/document/product/436/12270#.E5.AE.8C.E6.88.90.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.

2. create_multipart_upload() 방법을 실행하여 멀티파트 업로드를 초기화합니다. 버킷 이름과 객체 키 이름이 필요합니다.

3. 파트를 복사하려면 upload_part_copy() 방법을 반복적으로 호출합니다. 버킷 이름, 객체 키 이름, UploadID 및 각 파트의 내용이 필요합니다.

4. complete_multipart_upload() 방법을 실행하여 멀티파트 업로드를 완료합니다. 버킷 이름, 객체 키 이름, UploadID 및 모든 파트 정보가 필요합니다.

#### 예제 코드

다음 예제 코드는 멀티파트 업로드하는 방법을 보여줍니다.

```python
secret_id = 'xxxxxxxx'      # 사용자의 secretId로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'

# 1. 멀티파트 업로드 초기화
response = client.create_multipart_upload(
    Bucket=bucket,
    Key=file_name       
)
uploadid = response['UploadId']

# 2.각 파트를 복사합니다.
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

# 3.멀티파트 업로드 완료.
response = client.complete_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid,
    MultipartUpload={'Part': lst}
)
```

copy() 방법을 통해 객체를 복사할 수 있습니다. 복사할 소스 객체의 크기와 소재 지역을 기반으로 자동으로 API를 호출합니다. 버킷 이름, 객체 키 이름, 복사할 소스 버킷, 소스 객체 키 및 소스 지역만 제공하면 됩니다.
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
