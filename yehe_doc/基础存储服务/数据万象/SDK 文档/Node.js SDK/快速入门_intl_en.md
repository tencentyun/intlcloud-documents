## Download and Installation

#### Relevant resources

- Download the COS XML SDK resources for Node.js [here](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- SDK download: [XML Node.js SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-nodejs-sdk-v5/latest/cos-nodejs-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).
- For the complete sample code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/NodeJS).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/CHANGELOG.md).

>? If you encounter errors such as non-existent functions or methods when using the SDK, you can update the SDK to the latest version and try again.
>

#### Environmental dependencies

1. The SDK requires your runtime environment to include Node.js (v6 or later) and npm.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

>? For the definition of terms such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>

#### Installing SDK

Install the SDK through npm which can be downloaded [here](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## Getting Started

### Initialization



>!
>- We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


#### Using a temporary key for initialization (recommended)

For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). The SDK for Node.js supports initialization by passing in a temporary key as shown in the sample code below:

[//]: # ".cssg-snippet-global-init-sts"
```js
var request = require('request');
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    getAuthorization: function (options, callback) {
        // It will not be called during initialization and will be entered only when a COS method such as `cos.putObject` is called.
        // Get a temporary key asynchronously.
        request({
            url: 'https://example.com/sts',
            data: {
                // The required parameters can be obtained from options.
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
                SecurityToken: credentials.sessionToken, // sessionToken of the temporary key
                ExpiredTime: data.expiredTime, // Expiration timestamp of the temporary key, which is calculated by adding durationSeconds to the timestamp when applying for the temporary key 
            });
        });
    }
});
```

#### Using a permanent key for initialization (not recommended)

When using a permanent key for initialization, store the key properly to prevent leakage.
First, log in to the CAM console, and get your `SecretId` and `SecretKey` from the [Access Key](https://console.cloud.tencent.com/cam/capi) page.
Replace `SecretId`, `SecretKey`, `bucket`, and `region` with the actual values in your development environment. To test file upload, see the following sample code.

[//]: # ".cssg-snippet-global-init"
```js
// Log in to https://console.cloud.tencent.com/cam/capi to check and manage the SecretId and SecretKey of your project.
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: process.env.SecretId, // User `SecretId`. We recommend you obtain it from the environment variable. In addition, we recommended you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    SecretKey: process.env.SecretKey, // User `SecretKey`. We recommend you obtain it from the environment variable. In addition, we recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
});
```

Below are some common APIs. For more detailed initialization methods, see the [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/demo.js).

### Configuration item

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | Yes |
| SecretKey | User SecretKey | String | Yes |             
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries for multipart upload failure. Default value: 2 (a request will be made 3 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using `uploadFiles`, if the file size is greater than the value of this parameter (measured in bytes), multipart upload is used; otherwise, simple upload is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10485760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| ServiceDomain | The request domain name when `getService` is called, such as `service.cos.myqcloud.com` | String | No |
| Domain | Custom request domain name used to call a bucket or object API. You can use a template <br>such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region information passed in the replacement parameters when an API is called.</br> | String | No |
| UploadQueueSize | The maximum size of the upload queue. If the maximum is exceeded, failed, completed, and canceled tasks will be cleared. Default value: 1000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces the verification of `Content-MD5` for file uploads, which calculates the MD5 checksum of the file request body and places it in the `Content-MD5` field of the header. Default value: false | Boolean | No |
| Timeout | Timeout period in milliseconds. Default value: 0, indicating no timeout period. | Number | No |
| KeepAlive              | Indicates that more than one request is sent over one TCP connection. Default value: `true`. This parameter is recommended for a large number of concurrent requests.   | Boolean   | No   |
| StrictSsl              | Strict verification of the HTTPS certificate. Default value: `true` | Boolean | No   |
| Proxy | Uses an HTTP proxy when making requests, such as: `http://127.0.0.1:8080` | String | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required | Function | No |
| UseAccelerate          | Whether to enable a global acceleration endpoint. Default value: `false`. If you set the value to `true`, you need to enable global acceleration for the bucket. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406). | Boolean | No   |


#### getAuthorization Callback function description (Format 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function parameters:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as listed below:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | Yes |
| SecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
| StartTime | The timestamp in seconds of when you obtained the key, such as `1580000000`. Passing in this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No   |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | Yes |

#### getAuthorization Callback function description (Format 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function parameters:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object for getting the signature | Object |
| - Method | Method of the current request | String |
| - Pathname | Request path used for signature calculation | String |
| - Key | ObjectKey (object name) is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| - Query | Query parameter in the current request. Format: {key: 'val'} | Object |
| - Headers | Headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function | 

Once the getAuthorization callback function is finished, it returns one of the following:
An Authorization string.
An object whose attributes are listed as follows:


| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting an authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function. Each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback. Each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

### How to use

#### Callback method
The callback method is used by default in the documentation. Below is the sample code:

```js
// The initialization process and upload parameters are omitted here.
var cos = new COS({ ... });
cos.uploadFile({ ... }, function(err, data) {
  if (err) {
    console.log('Upload failed', err);
  } else {
    console.log('Uploaded successfully', data);
  }
});
```

#### Promise
The SDK also supports calling through the promise method. For example, the code of the callback method above is equivalent to the following code:

```js
// The initialization process and upload parameters are omitted here.
var cos = new COS({ ... });
cos.uploadFile({ ... }).then(data => {
  console.log('Uploaded successfully', data);
}).catch(err => {
  console.log('Upload failed', err);
});
```

#### Sync method
The sync method is based on JavaScript's async and await. The code of the callback method above is equivalent to the following code:

```js
async function upload() {
  // The initialization process and upload parameters are omitted here.
  var cos = new COS({ ... });
  try {
    var data = await cos.uploadFile({ ... });
    return { err: null, data: data }
  } catch (err) {
    return { err: err, data: null };
  }
}
// The returned value of the request can be obtained synchronously. Here is only an example. The format of the actual returned data can be customized.
var uploadResult = await upload();
if (uploadResult.err) {
  console.log('Upload failed', uploadResult.err);
} else {
  console.log('Uploaded successfully', uploadResult.data);
}
```

>! `cos.getObjectUrl` currently only supports the callback method.
>

### Tips

In most cases, you only need to create a COS SDK instance, and use it directly where SDK methods need to be called.  

```js
var cos = new COS({
  ....
});

/* Self-encapsulated upload method */
function myUpload() {
  // COS SDK instances do not need to be created in each method
  // var cos = new COS({
  //   ...
  // });
  cos.putObject({
    ....
  });
}

/* Self-encapsulated deletion method */
function myDelete() {
  // COS SDK instances do not need to be created in each method
  // var cos = new COS({
  //   ...
  // });
  cos.deleteObject({
    ....
  });
}
```

Below are some common APIs. For more detailed initialization methods, see the [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo/demo.js).

### Creating a bucket

[//]: # ".cssg-snippet-put-bucket"
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

### Querying the bucket list

[//]: # ".cssg-snippet-get-service"
```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an object

This API is used to upload small files. For large files, use the multipart upload API. For more information, see [Object Operations](https://www.tencentcloud.com/document/product/436/43551).

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
    Key: 'exampleobject', /* Required */
    StorageClass: 'STANDARD',
    Body: fs.createReadStream('./exampleobject'), // Uploading file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### Querying objects

[//]: #	".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
    Prefix: 'a/', /*Optional*/
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an object

[//]: # ".cssg-snippet-get-object-stream"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
    Key: 'exampleobject', /* Required */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

### Deleting an object

[//]: #	".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
    Key: 'exampleobject'       /* Required */
}, function(err, data) {
    console.log(err || data);
});
```
**
