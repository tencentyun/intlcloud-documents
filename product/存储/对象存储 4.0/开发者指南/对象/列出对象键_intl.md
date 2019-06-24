## Use Cases

Tencent Cloud COS supports listing keys by prefix. You can use the separator (`/`) in the key to implement a hierarchical structure similar to the traditional file system. In COS, you can use the separator to select and browse keys hierarchically.

You can list all the keys in a single bucket in UTF-8 binary order of prefixes, or filter the key list by specifying the prefix. For example, by adding the parameter `t`, the `tapd` object can be listed, and objects prefixed with `a` or other characters will be skipped.

Keys can be reorganized based on the added separator (`/`). You can use the prefix and separator together to implement a folder retrieval feature. For example, if you add the prefix parameter `t` and the separator (`/`), related keys such as `tapd/file` are listed.

Tencent Cloud COS supports storing an unlimited number of objects in a single bucket, so the key list can be very large. To management purposes, a maximum of 1000 key values are returned for a List Objects request, and an indicator will be returned to inform if the result is truncated. You can send a range of List Objects requests based on indicators and separators, to list all key values or to search the required content.

## Directions

### Via REST API

You can use the REST API to initiate a GET Object request. See [Get Bucket Documentation](https://intl.cloud.tencent.com/document/product/436/7734).

### Via C++ SDK

This method is provided in the C++ SDK for COS. See the [Get Bucket section in C++ SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12302#get-bucket).

#### Directions

1. Pass the configuration file path to initialize CosConfig and the CosAPI object.
2. Execute the GetBucket() method to list objects. The bucket name is required.

#### Sample codes

The following sample codes show how to list keys:

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// The bucket_name is required in the constructor of GetBucketReq.
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);
```

You can specify parameters to control the listed keys. MaxKeys means the maximum number of objects returned; Prefix means that only keys with the specified prefix are returned; Delimiter means only keys containing the separator are returned:
``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// The bucket_name is required in the constructor of GetBucketReq.
qcloud_cos::GetBucketReq req(bucket_name);
req.SetPrefix("prefix");
req.SetDelimiter(";");
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);
```
### Via Java SDK

This method is provided in the Java SDK for COS. See the [Get Bucket (List Objects) section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#get-bucket-(list-objects)).

#### Directions

1. Initialize client cosclient.
2. Use listObjects to list objects (up to 1000 objects at a time). To list more objects, call listObjects repeatedly.

#### Sample codes
(1) `ListObjectsRequest` is used to list objects. You can set the prefix and separator of objects to be listed. The sample codes are as follows:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates the key of the listed objects started with the prefix.
listObjectsRequest.setPrefix("aaa/bbb");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
listObjectsRequest.setDelimiter("");
// If the object path contains special characters, URL encoding is recommended. After the object key is obtained, perform URL decoding.
listObjectsRequest.setEncodingType("url");
// Set the maximum number of traversed objects (up to 1000 for one listobject).
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
try {
    objectListing = cosclient.listObjects(listObjectsRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// The common prefix indicates the path truncated by delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
List<String> commonPrefixs = objectListing.getCommonPrefixes();

// The object summary indicates a list of all listed objects.
List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
    // File path key
    String key = cosObjectSummary.getKey();
    // If the encodingtype is url, perform URL decoding.
    try {                                                               
        key = URLDecoder.decode(key, "utf-8"); 
    } catch (UnsupportedEncodingException e) {                          
        continue;                                                       
    }
    // File etag
    String etag = cosObjectSummary.getETag();
    // File length
    long fileSize = cosObjectSummary.getSize();
    // File storage type
    String storageClasses = cosObjectSummary.getStorageClass();
}

cosclient.shutdown();
```
(2) To get objects that exceed the number specified in MaxKeys or get all objects, you must call listobject repeatedly by using the last "next marker" returned as the "marker" for next call until the returned truncated is false.

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates the key of the listed objects started with the prefix.
listObjectsRequest.setPrefix("aaa/bbb");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
listObjectsRequest.setDelimiter("");
// If the object path contains special characters, URL encoding is recommended. After the object key is obtained, perform URL decoding.
listObjectsRequest.setEncodingType("url");
// Set the maximum number of traversed objects (up to 1000 for one listobject).
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {

    try {
        objectListing = cosclient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // The common prefix indicates the path truncated by delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary indicates a list of all listed objects.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // File path key
        String key = cosObjectSummary.getKey();
        // If the encodingtype is url, perform URL decoding.
        try {
            key = URLDecoder.decode(key, "utf-8");
        } catch (UnsupportedEncodingException e) {
            continue;
        }
        // File etag
        String etag = cosObjectSummary.getETag();
        // File length
        long fileSize = cosObjectSummary.getSize();
        // File storage type
        String storageClasses = cosObjectSummary.getStorageClass();
    }
    
    // Get the next marker for the next request.
    String nextMarker = "";
    try {
        nextMarker = URLDecoder.decode(objectListing.getNextMarker(), "utf-8");
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
        return;
    }
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());

cosclient.shutdown();
```

### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Get Bucket section in JavaScript SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12260#get-bucket).

#### Directions

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to list keys:

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

cos.getBucket({
    Bucket: Bucket,
    Region: Region,
}, function (err, data) {
    console.log(err, data);
});
</script>
```
### Via Node.js SDK

This method is provided in the Node.js SDK for COS. See the [Get Bucket section in Node.js SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12264#get-bucket).

#### Directions

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute ```node test.js``` in the command line.

#### Sample codes

The following sample codes show how to list keys:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.getBucket({
    Bucket: Bucket,
    Region: Region,
    Prefix: '',    // Prefix,
    MaxKeys: '100' // List the number.
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Get Bucket List section in PHP SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12267#.E8.8E.B7.E5.8F.96bucket.E5.88.97.E8.A1.A8).

#### Directions

1. Initialize client cosClient.
2. Execute listObjects to list objects. The bucket name is required.

#### Sample codes

The following sample codes show how to list keys:

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'testbucket-125000000'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Get File List section in Python SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12270#.E8.8E.B7.E5.8F.96.E6.96.87.E4.BB.B6.E5.88.97.E8.A1.A8).

#### Directions

1. Use the CosConfig library for configuration, and initialize client CosS3Client.
2. Execute the list_objects() method to list objects. The bucket name is required.

#### Sample codes

The following sample codes show how to list keys:

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
response = client.list_objects(
    Bucket=bucket       
)
```

You can specify parameters to control the listed keys. MaxKeys means the maximum number of objects returned; Prefix means that only keys with the specified prefix are returned; Delimiter means only keys containing the separator are returned:
```python
bucket = 'testbucket-123456789'
response = client.list_objects(
    Bucket=bucket,
    Delimiter='/',
    MaxKeys=100,
    Prefix='test'
)
```

