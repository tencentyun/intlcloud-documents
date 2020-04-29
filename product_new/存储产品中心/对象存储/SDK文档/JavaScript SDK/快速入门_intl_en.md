## Download and Installation

#### Relevant resources

- Download the COS XML SDK source code for JavaScript [here](https://github.com/tencentyun/cos-js-sdk-v5).
- SDK quick download address: [XML JavaScript SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-js-sdk-v5/latest/cos-js-sdk-v5.zip?_ga=1.75025362.1783616852.1583375173).
- Download the demo [here](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).

#### Preparing the environment

1. The SDK for JavaScript requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file uploading and file MD5 checksum calculation.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.
4. Configure CORS rule. Put in `*` for `AllowHeader`. For `ExposeHeaders`, put in `ETag`, `Content-Length`, and the other header fields that JS needs to read as shown below. For more information, please see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
   ![CORS example](https://main.qcloudimg.com/raw/bdb4f616f2afe4ca18ba663446873fd4.png)

> ?For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see COS’s [Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing the SDK

You can install the SDK in the following ways:

#### Importing through script

```html
<script src="./cos-js-sdk-v5.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name COS, and its constructor can create an SDK instance.

#### Importing through webpack

Install the SDK dependencies by running `npm i cos-js-sdk-v5 --save`, which supports webpack packaging scenarios. You can use the import npm as a module with the following code:

```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

### Getting a temporary key

If the key is placed on the frontend, the `SecretId` and `SecretKey` will be exposed; therefore, we put the permanent key on the backend, and the frontend gets a temporary key from the backend through AJAX. In actual deployment, please add an additional authentication step to your website on the backend. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

### Initialization

1. Create a `web.html` file, enter the following code, and modify the bucket name and region in `web.html`.
2. Deploy the temporary key service on the backend and modify the key service address in `getAuthorization`.
3. Place the `web.html` file on the web server, please visit the page in a browser, and test file uploading. The sample code for `web.html` is as follows:

```html
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'examplebucket-1250000000';
var Region = 'COS_REGION';     /* Bucket region, which is required */

// Initializing an instance
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        $.get('http://example.com/server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            var credentials = data && data.credentials;
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
            });
        });
    }
});

// The COS instance can then be used to call a COS request
// TODO

</script>
```

### Configuration Items

#### Use cases

Create a COS SDK instance in the following methods:

- Method 1 (recommended). The backend gets a temporary key and sends it to the frontend for signature calculation.

[//]: # ".cssg-snippet-global-init-sts"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server examples for other programming languages, please see the [COS SDK for STS](https://github.com/tencentyun/qcloud-cos-sts-sdk)
        // For the STS documentation, please visit https://intl.cloud.tencent.com/document/product/436/14048
        $.get('http://example.com/server/sts.php', {
            // You can obtain the required parameters from options
        }, function (data) {
            var credentials = data && data.credentials;
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
            });
        });
    }
});
```

- Method 2 (recommended). Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through Scope.

[//]: # ".cssg-snippet-global-init-sts-scope"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server example: https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/scope.md
        $.ajax({
            method: 'POST',
            url: ' http://example.com/server/sts-scope.php',
            data: JSON.stringify(options.Scope),
            beforeSend: function () {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken
                    // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting the key to be reused only for the same request
                });
            }
        });
    }
});
```

- Method 3 (not recommended). The frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a fixed or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control permissions for multipart upload and thus is not recommended.

[//]: # ".cssg-snippet-global-init-signature"
```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, please see the COS SDK for the corresponding programming language: https://intl.cloud.tencent.com/document/product/436/6474
        // Note: there may be a security risk associated with this method. The backend needs to strictly control permissions through method and pathname, such as prohibiting put /
        $.get('http://example.com/server/auth.php', {
            method: options.Method,
            pathname: '/' + options.Key,
        }, function (data) {
            if (!data || !data.authorization) return console.error('authorization invalid');
            callback({
                Authorization: data.authorization,
                // XCosSecurityToken: data.sessionToken, // If a temporary key is used, sessionToken needs to be passed to XCosSecurityToken
            });
        });
    },
    // Optional parameters
    FileParallelLimit: 3,    // Controls the number of concurrent file uploads
    ChunkParallelLimit: 3,   // Controls the number of concurrent part uploads for a single file
    ProgressInterval: 1000,  // Controls the upload interval of `onProgress` callbacks
});
```

- Method 4 (not recommended). The frontend uses a fixed key to calculate a signature. This method is suitable for frontend debugging. If you use this method, be sure to avoid key disclosure.

[//]: # ".cssg-snippet-global-init"
```js
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
});
```

#### Constructor Parameters 

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User's `SecretId` | String | No |
| SecretKey | User's `SecretKey`, which we recommend to be used only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries for multipart upload/copy failure. Default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No|
| ChunkSize | Part size within the multipart upload measured in bytes. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is greater than the value of this parameter (measured in bytes), multipart upload is used; otherwise, simple upload is used. Default value: 1,048,576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10,485,760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10,485,760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` measured in milliseconds. Default value: 1,000 | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies Content-MD5 when uploading files, which is false by default. If it is enabled, the MD5 value of the uploading files will be calculated, which may be time-consuming for large files | Boolean | No |
| GetAuthorization | Callback method for getting a signature. If there is no `SecretId` or `SecretKey`, this parameter is mandatory | Function | No |
| Timeout                | Timeout period measured in milliseconds. Default value: 0, indicating no timeout period               | Number   | No   |

#### `getAuthorization` callback function description (using method 1)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` Callback Parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting a temporary key | Object   |
| - Bucket  | Bucket name in the format `BucketName-APPID`. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, please see [Bucket Region Information](https://intl.cloud.tencent.com/document/product/436/6224) | String   |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, callback returns an object. The attributes of the returned object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | Yes |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
| StartTime | Key acquisition start time measured in seconds, i.e., the timestamp of the key acquisition time, such as 1580000000. This parameter is used as the signature start time. Passing in this parameter can avoid signature expiration issues due to time deviation on the frontend | String | No |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | No |

#### `getAuthorization` callback function description (using method 2)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` callback parameters:

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object |
| - Method | Method of the current request |  String   |
| - Pathname | Request path used for signature calculation | String |
| - Key | An object key (Object name) is the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - Query | Query parameter object of the current request in the format `{key: 'val'}` | Object |
| - Headers | Header parameter object of the current request in the format `{key: 'val'}` | Object |
| callback | Callback after the temporary key is obtained | Function |

After `getAuthorization` is calculated, the `callback` parameter supports two formats:
Format 1. The authentication credential string `Authorization` is called back.
Format 2. An object is called back with the following attributes:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | Calculated signature string                                         | String | Yes   |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |

#### Getting an authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in the `SecretId` and `SecretKey`, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getAuthorization` callback. When this callback is called, a temporary key will be returned, and after the key expires, the callback will be called again.

Below are some examples of common APIs. For more detailed initialization methods, please see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading an object

The simple upload API can be used to upload small files. For large files, use the multipart upload API. For more information, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/30596).

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region, which is required */
    Key: 'exampleobject',              /* Required */
    StorageClass: 'STANDARD',
    Body: fileObject, // Uploads the file object
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
    Region: 'COS_REGION',     /* Bucket region, which is required */
    Prefix: 'a/',           /* Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an object

> !This API is used to read object content. If you need to launch a browser to download the file, you can get the URL through `cos.getObjectUrl` and then start the download in the browser. For more information, please see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/30598).

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region, which is required */
    Key: 'exampleobject',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

### Deleting an object

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region, which is required */
    Key: 'exampleobject'        /* Required */
}, function(err, data) {
    console.log(err || data);
});
```
