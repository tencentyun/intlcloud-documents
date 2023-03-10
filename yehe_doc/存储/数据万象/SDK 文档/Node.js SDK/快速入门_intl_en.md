## Download and Installation

#### Related resources

- The COS XML JS SDK source code can be downloaded [here](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- Download the XML Java SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-nodejs-sdk-v5/latest/cos-nodejs-sdk-v5.zip).
- The demo can be downloaded [here](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).
- For all the code samples, see [here](https://github.com/tencentyun/cos-snippets/tree/master/NodeJS).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/CHANGELOG.md).

>? If you encounter errors such as non-existent functions or methods when using the SDK, update the SDK to the latest version and try again.
>

#### Environmental dependencies

1. To use the SDK, your operating environment should have Node.js 6 or later and npm.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product//436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

>? For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, see [Introduction](https://intl.cloud.tencent.com/document/product//436/7751).
>

#### Installing SDK

Install the SDK through npm, which can be downloaded [here](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## Getting Started

### Initialization

#### Initializing with permanent key

Get the `SecretId` and `SecretKey` on the [API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console.
Replace the `SecretId`, `SecretKey`, bucket, and region with actual values in your development environment. To test file upload, see the following sample code:

[//]: # ".cssg-snippet-global-init"
```js
// Log in to https://console.cloud.tencent.com/cam/capi to check and manage the `SecretId` and `SecretKey` of your project.
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
```

#### Initializing with temporary key

For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product//436/14048). The Node.js SDK supports initialization by passing in a temporary key as shown in the sample code below:

[//]: # ".cssg-snippet-global-init-sts"
```js
var request = require('request');
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        request({
            url: 'https://example.com/sts',
            data: {
                // The required parameters can be obtained from `options`
            }
        }, function (err, response, body) {
            try {
                var data = JSON.parse(body);
                var credentials = data.credentials;
            } catch(e) {}
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,        // `tmpSecretId` of the temporary key
                TmpSecretKey: credentials.tmpSecretKey,      // `tmpSecretKey` of the temporary key
                SecurityToken: credentials.sessionToken, // `sessionToken` of the temporary key
                ExpiredTime: data.expiredTime,               // Expiration timestamp of the temporary key, which is calculated by adding `durationSeconds` to the timestamp during application for the temporary key
            });
        });
    }
});
```

Below are some examples of common APIs. For more detailed initialization methods, see the [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/demo.js).

### Configuration Items

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User `SecretId` | String | Yes |
| SecretKey | User `SecretKey` | String | Yes |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3. | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3. | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload/copy failure. Default value: 2 (a request will be made three time in total, including the initial one). | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB). | Number | No |
| SliceSize | When files are uploaded in batches by using `uploadFiles`, if the file size is over the value of this parameter in bytes, multipart upload will be used; otherwise, simple upload will be used. Default value: 1048576 (1 MB). | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20. | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10485760 (10 MB). | Number | No |
| CopySliceSize | When a file is copied by using `sliceCopyFile`, if the file size is over the value of this parameter, multipart copy will be used; otherwise, simple copy will be used. Default value: 10485760 (10 MB). | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` will be used when the current page is determined to be in `http:`; otherwise, `https:` will be used. | String | No |
| ServiceDomain | The request domain name when the `getService` method is called, such as `service.cos.myqcloud.com`. | String | No |
| Domain | Custom request domain name used to call an API to manipulate a bucket or object. A template can be used, such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the parameters for replacement when an API is called. | String | No |
| UploadQueueSize | Maximum size of the upload queue. Excessive tasks that have failed or been completed or canceled will be cleared. Default value: 1,000. | Number | No |
| ForcePathStyle | Whether to forcibly use a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false. | Boolean | No |
| UploadCheckContentMd5  | Whether to forcibly verify `Content-MD5` for file uploads, which will calculate the MD5 checksum of the file request body and place it in the `Content-MD5` field of the header. Default value: false. | Boolean | No |
| Timeout                | Timeout period in milliseconds. Default value: 0, indicating not to set a timeout period.               | Number   | No   |
| KeepAlive              | Whether to send multiple requests over the same TCP connection. Default value: true. We recommend you enable this if there are high numbers of requests.   | Boolean   | No   |
| StrictSsl              | Whether to strictly verify the HTTPS certificate. Default value: true. | Boolean | No |
| Proxy | Uses an HTTP proxy when making requests, such as `http://127.0.0.1:8080`. | String | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required. | Function | No |
| UseAccelerate          | Whether to enable a global acceleration endpoint. Default value: false. If you set the value to `true`, you need to enable global acceleration for the bucket. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product//436/33406). | Boolean | No   |


#### getAuthorization callback function description (format 1)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` parameter descriptions:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object for getting the temporary key | Object   |
| - Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format. | String |
| - Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product//436/6224). | String |
| callback | Callback method after the temporary key is obtained. | Function |

After the temporary key is obtained, the callback returns an object. The parameters of the returned object are as listed below:

| Parameter | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | Yes |
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. | String | Yes |
| StartTime | The timestamp in seconds when the key is obtained, such as `1580000000`. Passing in this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No   |
| ExpiredTime | `expiredTime` of the obtained temporary key in seconds, i.e., the timeout timestamp, such as 1580000900. | String | Yes |

#### getAuthorization callback function description (format 2)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` parameter descriptions:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object for getting the signature | Object |
| - Method | Method of the current request |  String   |
| - Pathname | Request path used for signature calculation | String |
| - Key      | Object key (object name), which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| - Query | Query parameter in the current request. Format: {key: 'val'}. | Object |
| - Headers | Headers in the current request. Format: {key: 'val'}. | Object |
| callback | Callback after the temporary key is obtained | Function |

Once the `getAuthorization` callback function is finished, it returns one of the following:
An `Authorization` string.
An object whose parameters are as listed follows:


| Parameter | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | Calculated signature string                                         | String | Yes   |
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. | String | No |

#### Getting authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function. Each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback. Each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

### Tips

In most cases, you only need to create a COS SDK instance and use it directly where SDK methods need to be called.

```js
var cos = new COS({
  ....
});

/* Self-encapsulated upload method */
function myUpload() {
  // COS SDK instances don't need to be created in each method
  // var cos = new COS({
  //   ...
  // });
  cos.putObject({
    ....
  });
}

/* Self-encapsulated deletion method */
function myDelete() {
  // COS SDK instances don't need to be created in each method
  // var cos = new COS({
  //   ...
  // });
  cos.deleteObject({
    ....
  });
}
```

Below are some common APIs. For more detailed initialization methods, see the [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo/demo.js).

### Creating bucket

[//]: # ".cssg-snippet-put-bucket"
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

### Querying bucket list

[//]: # ".cssg-snippet-get-service"
```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading object

This API is used to upload small files. For large files, use the multipart upload API. For more information, see [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/43551).

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject',              /* Required */
    StorageClass: 'STANDARD',
    Body: fs.createReadStream('./exampleobject'), // Upload the file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### Querying object list

[//]: # ".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Required */
    Prefix: 'a/',           /* Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading object

[//]: # ".cssg-snippet-get-object-stream"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject',              /* Required */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

### Deleting object

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'exampleobject'       /* Required */
}, function(err, data) {
    console.log(err || data);
});
```
