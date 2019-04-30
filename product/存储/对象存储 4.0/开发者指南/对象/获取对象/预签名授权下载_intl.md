## Use Cases

All buckets and objects are private by default. If you want any third party to be able to download an object, but you don't want them to use CAM account or temporary keys, signatures can be provided by pre-signed URLs for download operations. Anyone who receives a valid pre-signed URL can download an object.

When creating a pre-signed URL, you can include keys in your signature to specify the allowed object to download. Besides, the validity period of pre-signed URLs can be provided in SDKs to ensure that expired URLs will not be used by any unauthorized party.

## Directions

### Via Java SDK

This method is provided in the Java SDK for COS. See the [Generating a Pre-Signed URL section in Java SDK API Documentation](https://cloud.tencent.com/document/product/436/12263#.E7.94.9F.E6.88.90.E9.A2.84.E7.AD.BE.E5.90.8D.E9.93.BE.E6.8E.A5).

#### Description

1. Initialize client cosclient.
2. Execute the generatePresignedUrl method to get the download signature and pass GET in the http method.

#### Sample codes

(1) The following sample codes show how to generate a pre-signed download URL:

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// Set the bucket name. The bucket name must contain appid.
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the signature expiration time (optional). The expiration time is not limited, but must be later than the current time. If it is not set, the signature expiration time (5 minutes) in ClientConfig is used by default.
// Set signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
req.setExpiration(expirationDate);

URL url = cosclient.generatePresignedUrl(req);
System.out.println(url.toString());
```

(2) `GeneratePresignedUrlRequest` supports setting the http header returned for download, such as content-type and content-disposition. The sample codes are as follows:

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// Set the bucket name. The bucket name must contain appid.
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the http header returned for download.
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
String responseContentDispositon = "filename=\"abc.txt\"";
String responseCacheControl = "no-cache";
String expireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24 * 3600 * 1000));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(expireStr);
req.setResponseHeaders(responseHeaders);
URL url = cosclient.generatePresignedUrl(req);

System.out.println(url.toString());
```

(3) `GeneratePresignedUrlRequest` also supports generating a download URL for an anonymous bucket. A signature is not required for the anonymous bucket download URL, so you don't need to specify the key information. The sample codes are as follows:

```java
// 1. For anonymous buckets, no user authentication information is required.
COSCredentials cred = new AnonymousCOSCredentials();
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// Set the bucket name. The bucket name must contain appid.
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosclient.generatePresignedUrl(req);

System.out.println(url.toString());
```

### Via JavaScript SDK

#### Description

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to download via a pre-signed URL:

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

cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg', // Replace the URL of a file to be downloaded.
    Expires: 60
}, function (err, data) {
    console.log(err || data.Url);
});
</script>
```

### Via Node.js SDK

#### Description

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute ```node test.js``` in the command line.

#### Sample codes

The following sample codes show how to download via a pre-signed URL:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
var url = cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg', // Replace the URL of a file to be downloaded.
    Expires: 60
});
console.log(url);
```
### Via Python SDK

#### Description

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute the get_presigned_download_url() method to get pre-signed URL to download an object. The bucket name and key name are required.

#### Sample codes

The following sample codes show how to download via a pre-signed URL:

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
download_url = client.get_presigned_download_url(
    Bucket=bucket,
    Key=file_name,
)
print download_url
```

