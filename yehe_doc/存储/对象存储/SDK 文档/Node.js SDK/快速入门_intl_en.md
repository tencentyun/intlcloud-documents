## Download and Installation

#### Relevant Resources

- Download the COS XML SDK for JS resources [here](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- Download the demo [here](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).

#### Environmental Requirements

1. To use the SDK, your operating environment need to have Node.js and npm.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's SecretId and SecretKey.

>- For the definitions of SecretId, SecretKey, Bucket and other terms, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).

#### Installing the SDK

Install the SDK via npm; download [npm](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## Getting Started

### Initialization

#### Initializing with a permanent key

Please refer to the following sample code. Replace the SecretId, SecretKey, Bucket, and Region with actual values in your development environment to test file upload.

[//]: # (.cssg-snippet-global-init)
```js
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY'
});
```

#### Initializing with a temporary Key

The SDK for Node.js supports initialization with a temporary key. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). The sample code is as shown below:

[//]: # (.cssg-snippet-global-init-sts)
```js
var request = require('request');
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        request({
            url: '../server/sts.php',
            data: {
                // The required parameters can be obtained from options
            }
        }, function (err, response, body) {
            try {
                var data = JSON.parse(body);
                var credentials = data.credentials;
            } catch(e) {}
            callback({
                    TmpSecretId: credentials.tmpSecretId, // tmpSecretId of the temporary key
                    TmpSecretKey: credentials.tmpSecretKey, // tmpSecretKey of the temporary key
                    XCosSecurityToken: credentials.sessionToken, // sessionToken needs to be passed to XCosSecurityToken
                    ExpiredTime: data.expiredTime, // Temporary key expiration timestamp, which is the timestamp when applying for a temporary key plus durationSeconds
            });
        });
    }
});
```

Below are some examples of common APIs. For more detailed initialization methods, please see the [Demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/demo.js).

### Configuration Items

#### Parameters of the constructor

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User SecretKey. We recommend you only use the SecretKey for frontend debugging to avoid key disclosure | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure. Default value: 3 (a request will be made 4 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When using uploadFiles for batch upload, if the file size is greater than this value, multipart upload will be used, otherwise simple upload will be called, unit is byte, the default value is 1048576 (1MB) | Number | No |
| CopyChunkParallelLimit | When performing the multipart copy operation, number of concurrent multipart copy uploads. The default value is 20 | Number | No |
| CopyChunkSize | When using sliceCopyFile to copy files in multipart, the byte size of each part, the default value is 10485760 (10MB) | Number | No |
| CopySliceSize | When copying a file using sliceCopyFile, if the file size is greater than this value, multipart copy will be used; otherwise simple copy will be called. The default value is 10485760(10MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress`; unit: millisecond. Default value: 1,000 | Number | No |
| Protocol | The protocol used when the request is made; value range: `https:`, `http:`. By default, `http:` will be used when the current page is determined to be in `http:`; otherwise, `https:` will be used | String | No |
| ServiceDomain | The request domain name when the getService method is called, such as `cos.ap-beijing.myqcloud.com` | String | No |
| Domain | Custom request domain names when calling buckets and objects APIs. You can use templates, <br>such as`" {Bucket} .cos. {Region}.myqcloud.com"`, that is, when calling the API, the bucket and region passed in the parameters will be used | String | No |
| UploadQueueSize | The maximum size of a queue. If the maximum is exceeded, failed, completed, and canceled tasks will be cleared. Default value: 1,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix to send requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces to verify Content-MD5 for file uploads, which will calculate the MD5 checksum of the file request body and place it in the Content-MD5 field of the header. Default value: false | Boolean | No |
| GetAuthorization | The callback method used to get the signature. If there is no SecretId or SecretKey, this parameter is required | Function | No |
| Timeout | Timeout, unit in milliseconds, default value is 0, that is, no timeout is set | Number | No |
| Proxy | Uses an HTTP proxy when requesting, such as: `http://127.0.0.1:8080` | String | No |

#### getAuthorization Callback Function Descriptions (Using Method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object | No |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| callback | Callback method after the temporary key is obtained | Function |

Callback posts back an object after the temporary key is acquired. Here is a list of the attributes of this object:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | tmpSecretId of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |
| ExpiredTime | expiredTime of the obtained temporary key, i.e., the timeout period | String | No |

#### getAuthorization Callback Function (Using Method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object | No |
| - Method | Current request method | String |
| - Pathname | Request path used for signature calculation | String | No |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | No |
| - Query | Query parameter object of the current request in the format of {key: 'val'} | Object | No |
| - Headers | Header parameter object of the current request in the format of {key: 'val'} | Object | No |
| callback | Callback after the temporary key is obtained | Function | No |

After the calculation of getAuthorization is completed, callback parameter supports two formats:
Format 1: Returns the authentication string Authorization.
Format 2: Returns an object. The object attribute list is as follows:


| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |

#### Acquiring authentication credentials

You can obtain the authentication credentials for your instance in three ways by passing in different parameters during instantiation:

1. During instantiation, pass in the SecretId and SecretKey, and each time a signature is required, it will be internally calculated by the instance.
2. Pass in the getAuthorization callback. This allows the signature, every time it is required, to be calculated and returned to the instance by this callback.
3. During instantiation, pass in the getSTS callback, and each time a temporary key is required, it will be returned to the instance through this callback for signature calculation within the instance during each request.

### Creating a bucket

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

### Querying bucket list

[//]: # (.cssg-snippet-get-service)
```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an object

This API is suitable for uploading small files. For large files, please use the multipart upload API. For more information, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/30596).

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fs.createReadStream('./exampleobject'), // Uploading file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### Querying the object list

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Prefix: 'a/', /*Optional*/
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an object

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Key: 'exampleobject', /*Required*/
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

### Deleting an object

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```
