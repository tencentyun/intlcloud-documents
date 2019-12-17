## Download and Installation

#### Relevant Resources

- Download the COS XML SDK for JS resources [here](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- Download the demo [here](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).

#### Environmental Requirements

1. To use the SDK, your operating environment need to have Node.js and npm.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's SecretId and SecretKey.

> For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).

#### Installing the SDK

Install the SDK via npm; download [npm](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## Getting Started

### Initialization

#### Initializing with a Permanent Key

Please refer to the following sample code. Replace the SecretId, SecretKey, Bucket, and Region with actual values in your development environment to test file upload.

```javascript
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY'
});
```

#### Initializing with a Temporary Key

The SDK for Node.js supports initialization with a temporary key. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). The sample code is as shown below:

```
var request = require('request');
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
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime,
            });
        });
    }
});
```

Below are some examples of common APIs. For more detailed initialization methods, please see the [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/demo.js).

### Configuration Items

#### Constructor Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User SecretKey. It is recommended to only use the SecretKey for frontend debugging to avoid key disclosure | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for a single file; default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure. Default value: 3 (a request will be made 4 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When multiple files are uploaded using `uploadFiles`, if the file size is over the value of this parameter, multipart upload (`sliceUploadFile`) will be used; otherwise, simple upload (`putObject`) will be used | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for a single file; default value: 3 | Number | No |
| CopyChunkSize | Number of retries upon multipart upload failure. Default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No |
| CopySliceSize | Part size in the multipart upload; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress`; unit: millisecond. Default value: 1,000 | Number | No |
| Protocol | The protocol used to make a request; valid values: `https:`, `http:`. By default, `http:` will be used when the current page is using `http:`; otherwise, `https:` will be used | String | No |
| ServiceDomain | The domain name requested by the getService method. <br>Example: `cos.ap-beijing.myqcloud.com`| String | No |
| Domain | The domain name used to call a bucket, which can be a template. <br>Example: `{Bucket}.cos.{Region}.myqcloud.com` | String | No |
| UploadQueueSize | The maximum size of a queue. If the maximum is exceeded, failed, completed, and canceled tasks will be cleared. Default value: 1,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: `false` | Boolean | No |
| UploadCheckContentMd5  | Forces to verify Content-MD5 for file uploads, which will calculate the MD5 checksum of the file request body and pass it in the Content-MD5 field of the header. Default value: `false` | Boolean | No |
| GetAuthorization | The callback method used to get the signature. If there is no SecretId or SecretKey, this parameter is required | Function | No |

#### getAuthorization Callback Function Descriptions (Using Method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the temporary key | Function |
| - Bucket  | Bucket name in the format of `BucketName-APPID` | String |
| - Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | tmpSecretId of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |
| ExpiredTime | expiredTime of the obtained temporary key, i.e., the timeout period | String | No |

#### getAuthorization Callback Function Descriptions (Using Method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions:

| Parameter Name | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | -------- | ---- |
| options | Parameter object necessary for getting the signature | Object | No |
| - Method | Method of the current request | Object | No |
| - Pathname | Request path used for signature calculation | String | No |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | No |
| - Query | Query parameter object of the current request in the format of {key: 'val'} | Object | No |
| - Headers | Header parameter object of the current request in the format of {key: 'val'} | Object | No |
| callback | Callback after the temporary key is obtained | Function | No |

After the getAuthorization calculation is completed, the callback returns a signature string or an object:
If a signature string is returned, the string is the credential field "Authorization" in the authentication header to be used by the request.
If an object is returned, the attributes of the object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | Calculated signature string                                         | String | Yes   |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting an Authentication Credential

You can obtain the authentication credentials for your instance in three ways by passing in different parameters during instantiation:

1. During instantiation, pass in the SecretId and SecretKey, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getSTS callback, and each time a temporary key is required, it will be returned to the instance through this callback for signature calculation within the instance during each request.

### Creating a Bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

### Querying Bucket List

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an Object

This API is suitable for uploading small files. For large files, please use the multipart upload API. For more information, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31710).

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'destination path/picture.jpg',
    Body: fs.createReadStream('./picture.jpg'), // Pass in the prefix here
}, function (err, data) {
    console.log(err || data);
});
```

### Querying Object List

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/', // Pass in the prefix of the files to be listed
}, function (err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an Object

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'exampleobject.txt',
    Output: fs.createWriteFile(__dirname + '/exampleobject.txt'),
}, function (err, data) {
    console.log(err || data.Body);
});
```

### Deleting an Object

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
}, function (err, data) {
    console.log(err || data);
});
```
