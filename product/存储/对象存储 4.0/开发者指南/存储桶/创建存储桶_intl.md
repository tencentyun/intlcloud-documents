## Use Cases

To use COS, you need to create a bucket that helps you use and manage objects. You can create buckets via the console, APIs, or SDKs.

You can use the following sample codes to create a bucket in the specified region. The supported parameters are:

-  Bucket: Specifies your complete bucket name, such as `testbuc-125235912`.
-  Region: Specifies the region where you want to deploy your Tencent Cloud COS buckets. The specified region of a bucket is unchangeable after the bucket is successfully created. For available regions, see [Region and Access Domain Name](https://cloud.tencent.com/document/product/436/6224).

## Directions
### Via the COS Console
For more information on how to create a bucket using the COS Console, see [Creating Bucket](https://cloud.tencent.com/document/product/436/13309) in Console Guide.

### Via REST API
You can use the REST API directly to initiate a bucket creation request. For more information, see [Put Bucket Documentation](https://cloud.tencent.com/document/product/436/7738).
### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Put Bucket section in C++ SDK API Documentation](https://cloud.tencent.com/document/product/436/12302#put-bucket).

#### Description

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Create PutBucketReq and PutBucketResp, where PutBucketReq is constructed according to the Bucket Name.
3. Execute the PutBucket method to create a bucket.

#### Sample codes

The following sample codes show how to create a bucket:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Put Bucket section in Java SDK API Documentation](https://cloud.tencent.com/document/product/436/12263#put-bucket).

#### Description

1. Initialize client cosclient.
2. Execute createBucket to create a bucket. When creating a bucket, you can specify the permissions (Public Read/Write or Private Read) of the bucket.

#### Sample codes

Call createBucket to create an bucket. The sample codes are as follows:

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

String bucketName = "publicreadbucket-1251668577";
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucketName);
// Set the permission of the bucket to PublicRead (Public Read/Private Write). Private (Private Read/Write) and PublicReadWrite (Public Read/Write) are also options available.
createBucketRequest.setCannedAcl(CannedAccessControlList.PublicRead);
Bucket bucket = cosclient.createBucket(createBucketRequest);
```
### Via JavaScript SDK

#### Description

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to create a bucket:

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

cos.putBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Via Node.js SDK

This method is provided in the Node.js SDK for COS. See the [Put Bucket section in Node.js SDK API Documentation](https://cloud.tencent.com/document/product/436/12264#put-bucket).

#### Description

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute `node test.js` in the command line.

#### Sample codes

The following sample codes show how to create a bucket:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Create Bucket section in PHP SDK API Documentation](https://cloud.tencent.com/document/product/436/12267#.E5.88.9B.E5.BB.BAbucket).

#### Description

1. Initialize client cosClient.
2. Execute createBucket to create a bucket. The bucket name is required.

#### Sample codes

The following sample codes show how to create a bucket:

```php
try {
    $result = $cosClient->createBucket(array('Bucket' => 'testbucket-125000000'));
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Create Bucket section in Python SDK API Documentation](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA-bucket).

#### Description

1. Use the CosConfig library for configuration, and initialize client CosS3Client.
2. Execute the create_bucket() method to create a bucket. The bucket name is required.

#### Sample codes

The following sample codes show how to create a bucket:

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
response = client.create_bucket(
    Bucket=bucket    
)
```

