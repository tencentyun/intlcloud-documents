## Use Cases

For copying an object that is greater than 5 GB, you must use the multipart copy. Use the multipart upload API to create an object, and use the Part Copy to carry the `x-cos-copy-source` header to specify the source object. The process is as follows:

1. Initialize an object for multipart upload.
2. Copy the data of the source object. You can specify the `x-cos-copy-range` header and copy up to 5 GB of data at a time.
3. Complete multipart upload.

SDKs provided by Tencent Cloud COS can be used to implement multipart copy.

## Directions

### Via C++ SDK

This method is provided in the C++ SDK for COS. See following sections in the C++ SDK API documentation:

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/12302#initiate-multipart-upload)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/12302#complete-multipart-upload)

#### Description

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Call InitMultiUpload() to initialize the multipart upload and get the upload Id.
3. Call the UploadPartCopyData() method repeatedly to copy a part. The bucket name, key name, upload Id, and part number must be included in UploadPartCopyDataReq. You can use UploadPartCopyDataReq::SetXCosCopySource to set the source file to be copied.
4. Execute the CompleteMultiUpload() method to complete a multipart upload. The bucket name, key name, UploadId, and all part information are required.

#### Sample codes

The following sample codes show how to copy an object in multiple parts:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";
std::string upload_id = ""; 
std::vector<std::string> etags;
std::vector<int64_t> part_nums;

// 1. Call InitMultiUpload to get uploadId.
qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult init_result = cos.InitMultiUpload(init_req, init_resp);

if (init_result.IsSucc()) {
    upload_id = init_resp.GetUploadId();
} else {
    // do sth
}

// 2.1 Copy the first part.
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

// 2.2 Copy the second part.
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

// 2.x Copy subsequent parts.
...

// 3. Call CompleteMultiUpload to complete multipart copy.
qcloud_cos::CompleteMultiUploadReq comp_req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp comp_resp;
comp_req.SetEtags(etags);
comp_req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult comp_result = cos.CompleteMultiUpload(comp_req, &comp_resp);
```

You can copy an object via the copy() method. APIs can be called automatically based on the size and region of the source object for upload. You only need to provide the bucket name, key name, source bucket for upload, source object key, and source region:

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
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Copying File section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#.E6.8B.B7.E8.B4.9D.E6.96.87.E4.BB.B6).

#### Description

1. Initialize client cosclient.
2. Use the "copy" high-level API provided in TransferManager to complete the copy.

#### Sample codes

For copying an object that is greater than 5 GB, you must call the "copypart" multipart upload API. The steps may be complex. Therefore, a "copy" API is encapsulated in TransferManager to support the selection of APIs based on the file size and copy of files greater than 5 GB. This API is recommended for copying files. The sample codes are as follows:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);


ExecutorService threadPool = Executors.newFixedThreadPool(32);
// Input a threadpool. If there is no thread pool, a single-thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(cosclient, threadPool);

// The region of bucket to copy. Cross-region copy is supported.
Region srcBucketRegion = new Region("ap-shanghai");
// The source bucket. The bucket name must contain appid.
String srcBucketName = "srcBucket-1251668577";
// The source file to copy
String srcKey = "aaa/bbb.txt";
// The destination bucket. The bucket name must contain appid.
String destBucketName = "destBucket-1251668577";
// The destination file to copy
String destKey = "ccc/ddd.txt";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // 返回一个异步结果copy, 可同步的调用waitForCopyResult等待copy结束, 成功返回CopyResult, 失败抛出异常.
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



### Via PHP SDK

#### Description

1. Initialize client cosClient.
2. Execute "Copy" to copy an object in multiple parts. The bucket name and key names are required.

#### Sample codes

The following sample codes show how to copy an object in multiple parts:

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
### Via Python SDK

This method is provided in the Python SDK for COS. See following sections in the Python SDK API documentation:

- [Create multipart upload](https://intl.cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [Complete multipart upload](https://intl.cloud.tencent.com/document/product/436/12270#.E5.AE.8C.E6.88.90.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)

#### Description

1. Use the CosConfig class for configuration, and initialize CosS3Client.

2. Execute the create_multipart_upload() method to initialize a multipart upload. The bucket name and key name are required.

3. Call the upload_part_copy() method repeatedly to copy a part. The bucket name, key name, UploadId, and content of each part are required.

4. Execute the complete_multipart_upload() method to complete a multipart upload. The bucket name, key name, UploadId, and all part information are required.

#### Sample codes

The following sample codes show how to copy an object in multiple parts:

```python
secret_id = 'xxxxxxxx'      # Replaced with user's secretId
secret_key = 'xxxxxxx'      # Replaced with user's secretKey
region = 'ap-beijing-1'     # Replaced with user's Region
token = ''                  # Token is required to use a temporary key. It is optional. Default is empty.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'

# 1. Initialize Multipart Upload
response = client.create_multipart_upload(
    Bucket=bucket,
    Key=file_name       
)
uploadid = response['UploadId']
    
# 2. Copy each part.
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

# 3. Complete Multipart Upload
response = client.complete_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid,
    MultipartUpload={'Part': lst}
)
```

You can copy an object via the copy() method. APIs can be called automatically based on the size and region of the source object for upload. You only need to provide the bucket name, key name, source bucket for upload, source object key, and source region:
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

