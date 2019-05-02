## Use Cases

The copy operation creates a copy of an object that is already stored in COS. You can create a copy of your object up to 5 GB in a single operation. For copying an object that is greater than 5 GB, you must use the multipart upload API. Using the copy operation, you can:

-  Create a copy of an object.
-  Rename the object by copying it and deleting the original one.
-  Modify the storage type of the object. In the copy operation, you select the same object as the source and target, and modify the storage type.
-  Copy objects across different Tencent Cloud COS regions.
-  Modify object metadata. In the copy operation, you select the same object as the source and target, and modify object metadata.

In the copy operation, the metadata of the original object is inherited by default, but the creation date is subject to the new object.

## Directions

### Via REST API

You can use the REST API to initiate an object copy request. See [Put Object Copy Documentation](https://cloud.tencent.com/document/product/436/10881).

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Put Object Copy section in C++ SDK API Documentation](https://cloud.tencent.com/document/product/436/12302#put-object-copy).

#### Description

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Execute PutObjectCopy() to copy an object. The bucket name, key name, source bucket for upload, source object key, and source region must be included in PutObjectReq.

#### Sample codes

The following sample codes show how to copy an object:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Put Object Copy section in Java SDK API Documentation](https://cloud.tencent.com/document/product/436/12263#put-object-copy).

#### Description

1. Initialize client cosclient.
2. Use the copyObject API to complete the copy.

#### Sample codes

`CopyObjectRequest` is used to copy object by setting the regions, bucket names, and paths of the source file and the destination file. The following sample codes show how to copy an object:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
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
    CopyObjectResult copyObjectResult = cosclient.copyObject(copyObjectRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
cosclient.shutdown();
```

### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Put Object Copy section in JavaScript SDK API Documentation](https://cloud.tencent.com/document/product/436/12260#put-object-copy).

#### Description

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to copy an object:

```html
<script src="cos-js-sdk-v5.min.js"></script>
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

cos.putObjectCopy({
    Bucket: Bucket,
    Region: Region,
    Key: '1.new.jpg',
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg'
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Via Node.js SDK

#### Description

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute `node test.js` in the command line.

#### Sample codes

The following sample codes show how to copy an object:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putObjectCopy({
    Bucket: Bucket,
    Region: Region,
    Key: '1.new.jpg',
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Copy Objects section in PHP SDK API Documentation](https://cloud.tencent.com/document/product/436/12267#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).

#### Description

1. Initialize client cosClient.
2. Execute "Copy" to copy an object in multiple parts. The bucket name and key names are required.

#### Sample codes

The following sample codes show how to copy an object:
```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'bucket-125000000',
        'CopySource' => 'bucket-appid.region.myqcloud.com/cos_path',
        'Key' => 'string',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Copy a File section in Python SDK API Documentation](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E6.8B.B7.E8.B4.9D).

#### Description

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute copy_object() to copy an object. The bucket name, key name, source bucket for copy, source object key, and source region are required.

#### Sample codes

The following sample codes show how to copy an object:

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # Replaced with user's secretId
secret_key = 'xxxxxxx'      # Replaced with user's secretKey
region = 'ap-beijing-1'     # Replaced with user's Region
token = ''                  # Token is required to use a temporary key. It is optional. Default is empty.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'
response = client.copy_object(
    Bucket=bucket,
    Key=file_name,
    CopySource={
        'Bucket': 'test-121212121',
        'Key': '1MB.txt',
        'Region': 'ap-guangzhou'
    }      
)
```

