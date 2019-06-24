## Use Cases

You can initiate a request to get objects directly in COS. You have the following options when getting an object:

- Get a complete object: Get the complete object data directly by initiating a GET request.
- Get a part of an object: Use the `Range` request header in a GET request to retrieve a specific range of bytes in an object. Retrieving multiple ranges is not supported.

When you retrieve an object, its metadata is returned in the HTTP response header along with the object's content. You can use URL parameters in a GET response to override certain response metadata values, such as the `Content-Dispositon` response value. The modifiable response headers include:

- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## Directions

### Via REST API

You can use the REST API to initiate a GET Object request. See [GET Object Documentation](https://intl.cloud.tencent.com/document/product/436/7753).

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Get Object section in C++ SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12302#get-object).

#### Directions

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Execute the GetObject() method to download a file to a local path or data stream. The bucket name and key name are required.

#### Sample codes

The following sample codes show how to get an object:

``` cpp
// Downloads to a local file
{
    // Parameters appid, bucketname and object, as well as the local path (including file name) are required for the request
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // Download succeeded. Call GetObjectByFileResp's member functions.
    } else {
        // Download failed. Call CosResult's member functions to output error information, such as requestID.
    }
}

// Download to a stream
{
    // Parameters appid, bucketname and object, as well as output stream are required for the request.
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // Download succeeded. Call GetObjectByStreamResp's member functions.
    } else {
        // Download failed. Call CosResult's member functions to output error information, such as requestID.
    }
}

// Downloads file to a local path in multiple threads.
{
    // Parameters appid, bucketname and object, as well as the local path (including file name) are required for the request
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // Download succeeded. Call MultiGetObjectResp's member functions.
    } else {
        // Download failed. Call CosResult's member functions to output error information, such as requestID.
    }
}
```

You can set a specific response header by setting the member function of the Request:

``` cpp
// Set the Content-Type parameter in the response header.
void SetResponseContentType(const std::string& str);

// Set the Content-Language parameter in the response header.
void SetResponseContentLang(const std::string& str);

// Set the Content-Expires parameter in the response header.
void SetResponseExpires(const std::string& str);

// Set the Cache-Control parameter in the response header.
void SetResponseCacheControl(const std::string& str);

// Set the Content-Disposition parameter in the response header.
void SetResponseContentDisposition(const std::string& str);

// Set the Content-Encoding parameter in the response header.
void SetResponseContentEncoding(const std::string& str);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Get Object section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#get-object).

#### Directions

1. Initialize client cosclient.
2. Execute the getObject method to get the input stream or save the content locally.

#### Sample codes
(1) The following sample codes show how to download an object (no version control):

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// Set the bucket name.
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    // Download a file.
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // Get the input stream.
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // Close the input stream.
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
(2) `GetObjectRequest` supports specifying the range of data bytes to be retrieved from the object. The following sample codes show how to specify byte range:

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// Set the bucket name.
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    // Set the first 11 bytes for download.
    getObjectRequest.setRange(0, 10);
    // Download a file.
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // Get the input stream.
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // Close the input stream.
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
(3) When retrieving an object, you can also use the `ResponseHeaderOverrides` object and set the corresponding request attributes to replace the response header value. The following is an example of this method:

```java
// 1. Initialize user authentication information (appid, secretId, and secretKey).
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// Set the bucket name.
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
    String responseContentType="image/x-icon";
    String responseContentEncoding = "gzip,deflate,compress";
    String responseContentLanguage = "zh-CN";
    String responseContentDispositon = "filename=\"abc.txt\"";
    String responseCacheControl = "no-cache";
    String expireStr = DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24 * 3600 * 1000));
    responseHeaders.setContentType(responseContentType);
    responseHeaders.setContentEncoding(responseContentEncoding);
    responseHeaders.setContentLanguage(responseContentLanguage);
    responseHeaders.setContentDisposition(responseContentDispositon);
    responseHeaders.setCacheControl(responseCacheControl);
    responseHeaders.setExpires(expireStr);
    getObjectRequest.setResponseHeaders(responseHeaders);
    // Download a file.
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // Get the input stream.
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // Close the input stream.
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
### Via JavaScript SDK

#### Directions

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to get an object:

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

cos.getObject({
    Bucket: config.Bucket,
    Region: config.Region,
    Key: '1.txt',
}, function (err, data) {
    console.log(err || 'File size：' + data.Body.length);
});
</script>
```

### Via Node.js SDK

#### Directions

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute `node test.js` in the command line.

#### Sample codes
The following sample codes show how to get an object:

```javascript
var fs = require('fs');
var path = require('path');
var COS = require('..');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.getObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    Output: fs.createWriteStream(path.resolve(__dirname, '1.download.jpg'))
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Download Files section in PHP SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12267#.E4.B8.8B.E8.BD.BD.E6.96.87.E4.BB.B6).

#### Directions

1. Initialize client cosClient.
2. Execute the getObject method to get objects. The bucket name is required.
3. Add the SaveAs field to save the obtained data stream as a local file.

#### Sample codes

The following sample codes show how to get an object:

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => 'hello.txt',
        'SaveAs' => 'hello.txt'));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Download Files section in Python SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD).

#### Directions

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute the get_object() method to get the data stream. The bucket name and key name are required.

#### Sample codes

The following sample codes show how to get an object:

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # Replaced with user's secretId
secret_key = 'xxxxxxx'      # Replaced with user's secretKey
region = 'ap-beijing-1'     # Replaced with user's Region
token = ''                 # Token is required to use a temporary key. It is optional. Default is empty.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
)
# Get an object to a local file.
response['Body'].get_stream_to_file('output.txt')
```

You can use the get_raw_stream() method to get the file stream of an object:
```python
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
)
fp = response['Body'].get_raw_stream()
# Call the read() method to read the file stream.
print fp.read(2)
```

You can get a specific range of bytes of the object by setting the Range parameter, in the format of bytes=first-last:
```python
# Get the first 10 bytes of the object.
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
    Range='bytes=0-9'
)
```

You can set a specific response header by setting the Response Header parameter:
```python
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
    ResponseCacheControl='no-cache',
    ResponseContentDisposition='attachment; filename=test.txt',
    ResponseContentEncoding='gzip',
    ResponseContentLanguage='zh-cn',
    ResponseContentType='text/html',
    ResponseExpires='Tue, 05 Dec 2017 10:01:19 GMT'
)
```

