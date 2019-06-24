## Use Cases

Multipart upload is well suited for large objects upload in weak networks or via high-bandwidth. The COS Console and SDKs can break a single object into parts and then upload. You can also do it by yourself and upload each part by API calls. Multipart upload has the following benefits:

-  In a weak network, smaller part size minimizes the impact of restarting a failed upload due to a network error.
-  In a high-bandwidth environment, use multipart upload to maximize the use of your available bandwidth by uploading object parts in parallel. Uploading parts out of order does not affect the final combined object.
-  With multipart upload, you can pause and resume the upload of a single large object at any time. All incomplete multipart uploads can be resumed at any time unless you abort the multipart upload.
-  Multipart upload can also be used to begin an upload before you know the final object size. You can initiate an upload and then combine the parts to get the full object size.

When uploaded, this set of parts is numbered consecutively. You can upload each part separately or upload them in any order. COS will combine the parts into an object based on their numbers. If the upload of any part fails, the failed part can be uploaded again without affecting other parts and the content as a whole. In a weak network environment, multipart upload is recommended for objects larger than 20 MB. In a high-bandwidth environment, multipart upload is recommended for objects larger than 100 MB.

## Directions

### Via REST API

You can initiate a multipart upload request directly using the REST API, which can be found in the following API documentation:

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Multipart Upload Operations section in C++ SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12302#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C). 

#### Directions

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Call InitMultiUpload() to initialize the multipart upload and get the upload Id.
3. Call the UploadPartData() method repeatedly to upload a part. The bucket name, key name, upload Id, part number, and file content to be uploaded must be included in UploadPartDataReq.
4. Execute the CompleteMultiUpload() method to complete a multipart upload. The bucket name, key name, UploadId, and all part information are required.

#### Sample codes

The following sample codes show how to upload an object in multiple parts:

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";
std::string upload_id = ""; 
std::vector<std::string> etags;
std::vector<int64_t> part_nums;

// 1. Call InitMultiUpload to get uploadId.
qcloud_cos::InitMultiUploadReq init_req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp init_resp;
qcloud_cos::CosResult init_result = cos.InitMultiUpload(init_req, init_resp);

if (init_result.IsSucc()) {
    upload_id = init_resp.GetUploadId();
} else {
    // do sth
}

// 2.1 Upload the first part.
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(1);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // After the upload is completed, record the part number and etag returned.
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(1);
    }
    is.close();
}

// 2.2 Upload the second part.
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // After the upload is completed, record the part number and etag returned.
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(2);
    }
    is.close();
}

// 2.x Upload subsequent parts.
...

// 3. Complete the multipart upload.
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_nums);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);

```

You can execute the AbortMultiUpload() method to abort a multipart upload operation. The bucket name, key name, and UploadId are required:
```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

You can execute the list_parts() method to list a multipart upload operation. The bucket name, key name, and UploadId are required:
``` cpp
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);
```

### Via Java SDK

This method is provided in the Java SDK for COS. See the [Multipart Upload section of PUT Object in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#put-object.EF.BC.88.E4.B8.8A.E4.BC.A0-object.EF.BC.89).

#### Directions

1. Initialize client cosclient.
2. Use initiateMultipartUpload to initialize the multipart upload to get a new uploadid, or call listMultipartUploads to get the incomplete multipart upload operations and get the uploadid.
3. Uploaded parts can be obtained using listParts. Parts that have not been uploaded can be uploaded using uploadPart, or copied from a file to the current file using copyPart. In this way, the feature of resuming upload from breakpoint is implemented. If uploadPart or copyPart is called again for the uploaded parts, the uploaded part data will be overwritten.
4. Complete the multipart upload using completeMultipartUpload or call abortMultipartUpload to abort the upload.

#### Sample codes

(1) `InitiateMultipartUploadRequest` is used to initialize the multipart upload, including the path of the multipart upload and storage type. A new multipart upload ID can be obtained by calling initiateMultipartUpload.

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";

String key = "aaa/bbb.txt";
InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);
// Set the storage type: Standard (default) and standard_ia. 
request.setStorageClass(StorageClass.Standard_IA);
try {
    InitiateMultipartUploadResult initResult = cosclient.initiateMultipartUpload(request);
    // Get uploadid.
    String uploadId =  initResult.getUploadId();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

(2) `UploadPartRequest` is a multipart upload request, which contains the data to be uploaded, and the part number. Upload parts by calling uploadPart and get the partEtag.

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (obtained via initiateMultipartUpload or ListMultipartUploads)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

// Generate data to be uploaded. In this case, initialize 1 MB data.
byte data[] = new byte[1024 * 1024];
UploadPartRequest uploadPartRequest = new UploadPartRequest();
uploadPartRequest.setBucketName(bucketName);
uploadPartRequest.setKey(key);
uploadPartRequest.setUploadId(uploadId);
// Set the input stream of part data source.
uploadPartRequest.setInputStream(new ByteArrayInputStream(data));
// Set the part length.
uploadPartRequest.setPartSize(data.length); // Set the data length.
uploadPartRequest.setPartNumber(10);     // Suppose that the number of the part to be uploaded is 10.

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

(3) `CompleteMultipartUploadRequest` is used to complete the multipart upload. The partEtag data of all parts are required before the upload. The multipart upload is completed by calling completeMultipartUpload. The sample code is as follows:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (obtained via initiateMultipartUpload or ListMultipartUploads)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

// In this case, initialize an empty queue to save the uploaded part information. The code cannot be executed directly, but can be obtained from the previous results of uploadPart or listParts and added to the partEtags queue. 
List<PartETag> partETags = new LinkedList<>();

// After the upload is completed, call the "complete" method to complete the multipart upload.
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

(4) `AbortMultipartUploadRequest` is used to abort a multipart upload. To abort an incomplete multipart upload, all uploaded parts from the aborted multipart upload are destroyed. The multipart upload request can be aborted by calling abortMultipartUpload. The sample code is as follows:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (obtained via initiateMultipartUpload or ListMultipartUploads)
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

(5) `ListPartsRequest` is used to list the uploaded parts. It can be used for resuming upload from breakpoint. The uploaded parts can be obtained by calling listParts. The sample code is as follows:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (obtained via initiateMultipartUpload or ListMultipartUploads)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

List<PartETag> partETags = new LinkedList<>();      // It is used to save information of all uploaded parts.
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

(6) `CopyPartResult` is used to copy parts. The part data is copied from a part of a file. The path to the source file to be copied, the bucket information, and the range of bytes are required. The parts can be copied by calling copyPart. The sample code is as follows:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (obtained via initiateMultipartUpload or ListMultipartUploads)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

CopyPartRequest copyPartRequest = new CopyPartRequest();
// The region where the source file to be copied resides
copyPartRequest.setSourceBucketRegion(new Region("ap-beijing-1"));
// The bucket name of the source file to be copied
copyPartRequest.setSourceBucketName(bucketName);
// The path to the source file to be copied
copyPartRequest.setSourceKey("aaa/ccc.txt");
// Specify the range of data of the source file to be copied (similar to content-range)
copyPartRequest.setFirstByte(0L);
copyPartRequest.setLastByte(1048575L);
// Name of the destination bucket
copyPartRequest.setDestinationBucketName(bucketName);
// Name of the destination path
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
### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Multipart Upload Operations section in JavaScript SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12260#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C).

#### Directions

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to upload an object in multiple parts:

```html
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000'; // Replaced with user's Bucket
var Region = 'ap-guangzhou';    // Replaced with user's Region

// Initialize the instance.
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Obtain the signature asynchronously
        var url = 'auth.php?method=' + options.Method.toLowerCase() + '&pathname=' + encodeURIComponent('/' + (options.Key || ''));
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            callback(e.target.responseText);
        };
        xhr.send();
    }
});

// Listen on the selection of files
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
### Via Node.js SDK

This method is provided in the Node.js SDK for COS. See the [Multipart Upload Operations section in Node.js SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12264#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C).

#### Directions

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Place the 1.jpg file to be uploaded in the current directory.

3. Create the test file test.js, and execute `node test.js` in the command line.

#### Sample codes

The following sample codes show how to upload an object in multiple parts:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

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
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Multipart Upload section in PHP SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12267#.E5.88.86.E5.9D.97.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0).

#### Directions

1. Initialize client cosClient.
2. Execute the "upload" method to upload the data stream. The bucket name and key name are required.
3. Upload the file stream via fopen.

#### Sample codes

The following sample codes show how to upload an object in multiple parts:

* Memory upload:
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
* File stream upload:
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
### Via Python SDK

This method is provided in the Python SDK for COS. See following sections in the Python SDK API documentation:

- [Create multipart upload](https://intl.cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [Upload a part](https://intl.cloud.tencent.com/document/product/436/12270#.E4.B8.8A.E4.BC.A0.E5.88.86.E5.9D.97)
- [Complete multipart upload](https://intl.cloud.tencent.com/document/product/436/12270#.E5.AE.8C.E6.88.90.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [Abort multipart upload](https://intl.cloud.tencent.com/document/product/436/12270#.E6.94.BE.E5.BC.83.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [List uploaded parts](https://intl.cloud.tencent.com/document/product/436/12270#.E5.88.97.E5.87.BA.E4.B8.8A.E4.BC.A0.E5.88.86.E5.9D.97)

#### Directions

1. Use the CosConfig library for configuration, and initialize client CosS3Client.
2. Execute the create_multipart_upload() method to initialize a multipart upload. The bucket name and key name are required.
3. Call the upload_part() method repeatedly to upload a part. The bucket name, key name, UploadId, and content of each part are required.
4. Execute the complete_multipart_upload() method to complete a multipart upload. The bucket name, key name, UploadId, and all part information are required.

#### Sample codes

The following sample codes show how to upload an object in multiple parts:

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
    
# 2. Upload a Part
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

# 3. Complete Multipart Upload
response = client.complete_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid,
    MultipartUpload={'Part': lst}
)
```

You can execute the abort_multipart_upload() method to abort a multipart upload operation. The bucket name, key name, and UploadId are required:
```python
response = client.abort_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid
)
```

You can execute the list_parts() method to list a multipart upload operation. The bucket name, key name, and UploadId are required:
```python
response = client.list_parts(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid
)
```

You can execute the list_multipart_uploads() method to list all incomplete multipart upload operations. The bucket name is required:
```python
response = client.list_multipart_uploads(
    Bucket=bucket
)
```


