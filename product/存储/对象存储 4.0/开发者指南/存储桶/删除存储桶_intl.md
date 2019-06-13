## Use Cases
Buckets can be deleted via the console, APIs, or SDKs.

> **Notes:**
> Only empty buckets can be deleted. If there are still objects in the bucket, the deletion will fail. Make sure there are no objects in the bucket before deleting it.

Before deleting a bucket, make sure that the current identity has been authorized to delete it and that you specify the correct Bucket and Region parameters.

## Directions
### Via the COS Console
For more information on how to delete a bucket using the COS Console, see [Deleting Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

### Via REST API
You can use the REST API directly to initiate a bucket deletion request. For more information, see [Delete Bucket Documentation](https://intl.cloud.tencent.com/document/product/436/7732).

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Delete Bucket section in C++ SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12302#delete-bucket).

#### Directions

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Execute the DeleteBucket() method to delete a bucket. The bucket name is required. Make sure the bucket is empty.

#### Sample codes

The following sample codes show how to delete a bucket:

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// The bucket_name is required in the constructor of DeleteBucketReq.
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Delete Bucket section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#delete-bucket).

#### Directions

1. Initialize client cosclient.
2. Execute deleteBucket to delete the bucket. The bucket must not contain any data, otherwise you need to clear the data first.

#### Sample codes

Call deleteBucket to delete a bucket. The sample codes are as follows:

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

// The bucket name must contain appid.
String bucketName = "publicreadbucket-1251668577";
// Delete the bucket. Only empty buckets can be deleted.
cosclient.deleteBucket(bucketName);
```

### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Delete Bucket section in JavaScript SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12260#delete-bucket).

#### Directions

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to delete a bucket:

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

cos.deleteBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Via Node.js SDK

This method is provided in the Node.js SDK for COS. See the [Delete Bucket section in Node.js SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12264#delete-bucket).

#### Directions

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute ```node test.js``` in the command line.

#### Sample codes

The following sample codes show how to delete a bucket:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Delete Bucket section in PHP SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4bucket).

#### Directions

1. Initialize client cosClient.
2. Execute deleteBucket to delete a bucket. The bucket name is required.

#### Sample codes

The following codes show how to delete a bucket:

```php
try {
    $result = $cosClient->deleteBucket(array(
        'Bucket' => 'testbucket-125000000'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Delete Bucket section in Python SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12270#.E5.88.A0.E9.99.A4-bucket).

#### Directions

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute the delete_bucket() method to delete a bucket. The bucket name is required. Make sure the bucket is empty.

#### Sample codes

The following sample codes show how to delete a bucket:

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
response = client.delete_bucket(
    Bucket=bucket    
)
```

