## Download and Installation

#### Relevant resources

- Download the COS XML SDK for JS resources [here](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- Fast SDK download: [XML Node.js SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-nodejs-sdk-v5/latest/cos-nodejs-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).

#### Environmental dependencies

1. The use of SDKs requires a Node.js runtime environment and npm.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's SecretId and SecretKey.

>For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing SDKs

Install the SDK via npm; download [npm](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## Getting Started

### Initialization

#### Initializing with a permanent key

First, log in to the CAM Console, and get your SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
Replace `SecretId`, `SecretKey`, bucket, and region with the actual values in your development environment. To test file upload, please see the following sample code.

[//]: # (.cssg-snippet-global-init)
```js
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY'
});
```

#### Initializing with a temporary key

For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). The SDK for Node.js supports initialization by passing in a temporary key as shown in the sample code below:

[//]: # (.cssg-snippet-global-init-sts)
```js
var request = require('request');
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        request({
            url: 'https://example.com/sts',
            data: {
                // You can obtain the required parameters from options
            }
        }, function (err, response, body) {
            try {
                var data = JSON.parse(body);
                var credentials = data.credentials;
            } catch(e) {}
            if (!data || !credentials) return console.error('credentials invalid');
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

### Configuration

#### Parameters of the constructor

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | Yes |
| SecretKey | User SecretKey. We recommend you only use the SecretKey for frontend debugging to avoid exposing your key | String | Yes |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure. Default value: 3 (a request will be made 4 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in byte for the multipart upload. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When using uploadFiles for batch upload, if the file size is greater than this value, multipart upload will be used, otherwise simple upload will be called, unit is byte, the default value is 1048576 (1MB) | Number | No |
| CopyChunkParallelLimit | When performing the multipart copy operation, number of concurrent multipart copy uploads. The default value is 20 | Number | No |
| CopyChunkSize | When using sliceCopyFile to copy files in multipart, the byte size of each part, the default value is 10485760 (10MB) | Number | No |
| CopySliceSize | When copying a file using sliceCopyFile, if the file size is greater than this value, multipart copy will be used; otherwise simple copy will be called. The default value is 10485760(10MB) | Number | No |
| ProgressInterval | Callback frequency in milliseconds for the upload progress callback method onProgress; default value: 1,000 | Number | No |
| Protocol | The protocol used when the request is made; value range: `https:`, `http:`. By default, `http:` will be used when the current page is determined to be in `http:`; otherwise, `https:` will be used | String | No |
| ServiceDomain | The requested domain name when the getService method is called, such as `cos.ap-beijing.myqcloud.com` | String | No |
| Domain | Custom request domain names when calling buckets and objects APIs. You can use templates, <br>such as`" {Bucket} .cos. {Region}.myqcloud.com"`, that is, when calling the API, the bucket and region passed in the parameters will be used | String | No |
| UploadQueueSize | The maximum size of a queue. If the maximum is exceeded, failed, completed, and canceled tasks will be cleared. Default value: 1,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix to send requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces to verify Content-MD5 for file uploads, which will calculate the MD5 checksum of the file request body and place it in the Content-MD5 field of the header. Default value: false | Boolean | No |
| Timeout | Timeout period in milliseconds. Default value is 0, that is, no timeout period is set. | Number | No |
| KeepAlive              | Indicates that more than one request is sent over one TCP connection. Default value: true. This parameter is recommended for a large number of concurrent requests.   | Boolean   | No   |
| StrictSsl              | Verifies the HTTPS certificate strictly. Default value: `true` | Boolean | No   |
| Proxy | Uses an HTTP proxy when requesting, such as: `http://127.0.0.1:8080` | String | No |
| GetAuthorization | The callback method for getting the signature. If there is no SecretId or SecretKey, this parameter is mandatory. | Function | No |


#### getAuthorization callback function (Format 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function parameters:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Bucket  | Bucket name in the format of `BucketName-APPID` | String|
| - Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| callback | Callback method after the temporary key is obtained | Function |

Callback passes back an object after the temporary key is acquired. Here is a list of the attributes of this object:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |
| StartTime | The timestamp in seconds when you obtain the key, such as `1580000000`. Passing in this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No   |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | No |

#### getAuthorization callback function (Format 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function parameters:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Method | Current request method | String |
| - Pathname | Request path used for signature calculation | String |
| - Key | An object key (object name) which uniquely identifies an object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - Query | The Query parameter in the current request. Format: {key: 'val'} | Object |
| - Headers | The headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function | 

Once the getAuthorization callback function finishes, it returns one of the following:
An Authorization string.
An object whose attributes are listed as follows:


| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Acquiring authentication credentials

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in the SecretId and SecretKey. Every time a signature is required, it will be internally calculated by the instance.
2. Pass in the getAuthorization callback function. This allows the signature, every time it is required, to be calculated and returned to the instance by this callback.
3. During instantiation, pass in the `getSTS` callback, and each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

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

This API (PUT Object) is used to upload small files. For large files, please use the multipart upload API. For more information, see [Actions on Objects](https://intl.cloud.tencent.com/document/product/436/31710).

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
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

### Querying object list

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
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
    Region: 'COS_REGION',/*Required*/
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
    Region: 'COS_REGION',/*Required*/
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```
