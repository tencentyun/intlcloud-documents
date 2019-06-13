## Use Cases

This operation is useful for uploading an object less than 5 GB in a single request. For objects larger than 5 GB, multipart upload is recommended.

When your object is large (for example, 100 MB), we recommend that you use multipart upload in a high-bandwidth or weak network environment.

## Directions
### Via REST API

You can use the REST API to initiate a simple upload request. See [PUT Object Documentation](https://intl.cloud.tencent.com/document/product/436/7749).

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Put Object section in C++ SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12302#put-object).

#### Description

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Execute the PutObject() method to upload an object. The bucket name, key name and content to be uploaded are required.

#### Sample codes

The following sample codes show how to upload an object using simple upload:

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "object_name";
// The local file path is required in the constructor of the request.
qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
// Call Set method to set metadata or ACL
req.SetXCosStorageClass("STANDARD_IA");

qcloud_cos::PutObjectByFileResp resp;
qcloud_cos::CosResult result = cos.PutObject(req, &resp);
```

A file stream can be uploaded to COS by specifying a file stream object:

``` cpp
std::istringstream iss("put object");

// The istream is required in the constructor of the request.
qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
qcloud_cos::PutObjectByStreamResp resp;

qcloud_cos::CosResult result = cos.PutObject(req, &resp);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [PUT Object section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#put-object.EF.BC.88.E4.B8.8A.E4.BC.A0-object.EF.BC.89).

#### Description

1. Initialize client cosclient.
2. Execute the putObject method to upload the object. You can upload local files or input streams to COS.

#### Sample codes

(1) The simple upload request is encapsulated in `PutObjectRequest` and is implemented by specifying the local file path and COS path. You can set the storage type and permission information. After the upload is completed, `PutObjectResult` is returned. If the upload fails, an exception will be thrown. The sample codes are as follows:

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
File localFile = new File("src/test/resources/len10M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Set the storage type: Standard (default) and standard_ia.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // The file etag is returned by putobjectResult.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// Shut down the client
cosclient.shutdown();
```

(2) Input stream upload is supported in `PutObjectRequest`. Files can be uploaded to COS via streams, but the content length must be specified. The sample codes are as follows:

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
File localFile = new File("src/test/resources/len10M.txt");

InputStream input = new ByteArrayInputStream(new byte[10]);
ObjectMetadata objectMetadata = new ObjectMetadata();
// The content length must be specified for uploading by input streams, otherwise the http client may cache all data, causing OOM.
objectMetadata.setContentLength(10);
// For download, return the contenttype by default according to the suffix of the COS path key. For upload, the contenttype is set to override the default value.
objectMetadata.setContentType("image/jpeg");

PutObjectRequest putObjectRequest =
        new PutObjectRequest(bucketName, key, input, objectMetadata);
// Set the storage type: Standard (default) and standard_ia.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // The file etag is returned by putobjectResult.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// Shut down the client        
cosclient.shutdown();
```
### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Put Object section in JavaScript SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12260#put-object).

#### Description

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to upload an object using simple upload:

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

    cos.putObject({
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

This method is provided in the Node.js SDK for COS. See the [Put Object section in Node.js SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12264#put-object).

#### Description

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Place the 1.jpg file to be uploaded in the current directory.
3. Create the test file test.js, and execute `node test.js` in the command line.

#### Sample codes

The following sample codes show how to upload an object using simple upload:

```javascript
var fs = require('fs');
var path = require('path');
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    Body: fs.readFileSync(path.resolve(__dirname, '1.jpg'))
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Simple Upload of File section in PHP SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12267#.E7.AE.80.E5.8D.95.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0).

#### Description

1. Initialize client cosClient.
2. Execute the putObject method to upload the data stream. The bucket name and key name are required.
3. Upload the file stream via fopen.

#### Sample codes

The following sample codes show how to upload an object using simple upload:

* Memory upload:
```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => '11',
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
* File stream upload:
```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => '11',
        'Body'   => fopen($pathToFile, 'r+')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
'Body'   => fopen($pathToFile, 'r+')
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Simple Upload of File section in Python SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12270#.E7.AE.80.E5.8D.95.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0).

#### Description

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute the put_object() method to upload an object. The bucket name, key name and content to be uploaded are required.

#### Sample codes

The following sample codes show how to upload an object using simple upload:

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

response = client.put_object(
    Bucket=bucket,
    Key=file_name,
    Body='1234'         
)
```

A file stream can be uploaded to COS by specifying a file stream object:
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

# Generate a file
with open(file_name, 'wb') as fp:
    fp.write('helloworld!')
with open(file_name, 'rb') as fp:
    response = client.put_object(
        Bucket=bucket,
        Key=file_name,
        Body=fp
    )
```

You can set the meta information of an object by setting specific parameters:
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

response = client.put_object(
    Bucket=bucket,
    Key=file_name,
    Body='123',
    StorageClass='STANDARD',
    ACL='public-read',
    CacheControl='no-cache',
    ContentDisposition='attachment; filename=test.txt',
    ContentEncoding='gzip',
    ContentLanguage='zh-cn',
    ContentType='text/html',
    Expires='Tue, 05 Dec 2017 10:01:19 GMT',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```

