## Use Cases

Tencent Cloud COS supports deleting one or multiple objects. To delete one object, you only need to provide the object name (key) to call an API request to delete it.

## Directions

### Via the COS Console
You can delete multiple objects in batches on the COS Console. See [Deleting Object](https://intl.cloud.tencent.com/document/product/436/13323) in Console Guide.

### Via REST API

You can use the REST API to initiate a DELETE Object request. See [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743).

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Delete Object section in C++ SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12302#delete-object).

#### Directions

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Execute the DeleteObject() method to delete an object. The bucket name and key name are required.

#### Sample codes

The following sample codes show how to delete an object:

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);
```

If there are multiple versions, you can specify the parameter VersionId to delete the specific version of the object:
``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
req.SetXCosVersionId("12345");
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Delete Object section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#delete-object).

#### Directions

1. Initialize client cosclient.
2. Execute the deleteObject method to delete the object. Provide the bucketName and the key to be deleted.

#### Sample codes

  Call deleteObject to create an object. The sample codes are as follows:

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
try {
    cosclient.deleteObject(bucketName, key);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// Shut down the client
cosclient.shutdown();
```
### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Delete Object section in JavaScript SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12260#delete-object).

#### Directions

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to delete an object:

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

cos.deleteObject({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Via Node.js SDK

This method is provided in the Node.js SDK for COS. See the [Delete Object section in Node.js SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12264#delete-object).

#### Directions

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute ```node test.js``` in the command line.

#### Sample codes

The following sample codes show how to delete an object:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Delete a File section in PHP SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4.E6.96.87.E4.BB.B6).

#### Directions

1. Initialize client cosClient.
2. Execute deleteObject to delete an object. The bucket name and key name are required.

#### Sample codes

The following sample codes show how to delete an object:

```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'bucket-125000000',
        'Key' => 'hello.txt'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Deleting Files section in Python SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD).

#### Directions

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute delete_object() to delete an object. The bucket name and key name are required.

#### Sample codes

The following sample codes show how to delete an object:

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
response = client.delete_object(
    Bucket=bucket,
    Key=file_name      
)
```

If there are multiple versions, you can specify the parameter VersionId to delete the specific version of the object:
```python
bucket = 'testbucket-123456789'
file_name = 'test.txt'
response = client.delete_object(
    Bucket=bucket,
    Key=file_name,
    VersionId='MTg0NDY3NDI1NjExNjQwNDUxMzU'    
)
```

