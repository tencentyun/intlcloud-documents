## Download and Installation

#### Related resources

- Download the source code for the COS XML JS SDK [here](https://github.com/tencentyun/cos-js-sdk-v5).
- Download the XML JavaScript SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-js-sdk-v5/latest/cos-js-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).
- Find the complete code [here](https://github.com/tencentyun/cos-snippets/tree/master/JavaScript).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/CHANGELOG.md).

#### Preparing environment

1. The SDK for JavaScript requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file uploading and MD5 checksum calculation.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get the `SecretId` and `SecretKey` of your project.
4. Configure CORS rule. Set `AllowHeader` to `*` and set `ExposeHeaders` to `ETag`, `Content-Length`, and the other header fields that JS needs to read, as shown below. For detailed directions, please see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
   ![](https://main.qcloudimg.com/raw/925cef63c1a4a5e849f464984e0446e7.png)

> ?For the definitions of `SecretId`, `SecretKey`, `Bucket`, and other terms, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing SDK

You can install the SDK in the following ways:

#### Importing via script
>? You can download the latest cos-js-sdk-v5.min.js [here](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/dist/cos-js-sdk-v5.min.js).
```html
<script src="https://unpkg.com/cos-js-sdk-v5/dist/cos-js-sdk-v5.min.js"></script>
```

If the SDK is specified in the script tag, the SDK occupies the global variable name COS. SDK instances can be created through its constructor.

#### Importing via webpack

Install the SDK dependencies by running `npm i cos-js-sdk-v5 --save`, which supports webpack packaging scenarios. You can use npm import as a module with the following code:

```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

### Getting a temporary key

As placing a permanent key on the frontend may cause security risks, we recommend you use temporary keys during formal deployment. The implementation process is as follows: the frontend first requests the server, and then the server uses the permanent key to call the STS service to apply for a temporary key (for more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048)) and returns it to the frontend.

>!If the site has a login state, login state verification should be added to the temporary key getting API.

### Initialization

1. Create a web.html file, enter the following code, and modify the bucket name and region in web.html.
2. Deploy the temporary key service on the backend and modify the key service address in getAuthorization.
3. Place the `web.html` file on the web server, visit the page in a browser, and test file uploading. The sample code for `web.html` is as follows:

```html
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'examplebucket-1250000000';
var Region = 'COS_REGION';      /* Bucket region. Required */

// Initialize an instance.
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously.
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
                // We recommend using the time the server receives the credentials as the StartTime to avoid signature error due to time deviations.
                StartTime: data.startTime, // Timestamp (in seconds), such as 1580000000
                ExpiredTime: data.expiredTime, // Timestamp (in seconds), such as 1580000900
            });
        });
    }
});

// The COS instance can then be used to call a COS request.
// TODO

</script>
```

### Configuration items

#### Use cases

Create a COS SDK instance in the following methods:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

[//]: # ".cssg-snippet-global-init-sts"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For examples of other server-side programming languages, please visit COS STS SDK: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, please visit https://intl.cloud.tencent.com/document/product/436/14048
        $.get('http://example.com/server/sts.php', {
            // The required parameters can be obtained from options.
        }, function (data) {
            var credentials = data && data.credentials;
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                // We recommend using the time the server receives the credentials as the StartTime to avoid signature error due to time deviations.
                StartTime: data.startTime, // Timestamp (in seconds), such as 1580000000
                ExpiredTime: data.expiredTime, // Timestamp (in seconds), such as 1580000900
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
            beforeSend: function (xhr) {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    // We recommend using the time the server receives the credentials as the StartTime to avoid signature error due to time deviations.
                    StartTime: data.startTime, // Timestamp (in seconds), such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp (in seconds), such as 1580000900
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting the key to be reused only for the same request.
                });
            }
        });
    }
});
```

- Method 3 (not recommended): the frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control permissions for multipart upload and thus is not recommended.

[//]: # ".cssg-snippet-global-init-signature"
```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, please see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: there may be a security risk associated with this method. The backend needs to strictly control the permission through method and pathname, such as prohibiting put /
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
    ProgressInterval: 1000,  // Controls the interval of upload `onProgress` callbacks
});
```

- Method 4 (not recommended): the frontend uses a permanent key to calculate the signature. This method can be used for frontend debugging. If you use this method, be sure to avoid key disclosure.

[//]: # ".cssg-snippet-global-init"
```js
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
});
```

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User's `SecretKey`, which we recommend to be used only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload/copy failure. Default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using `uploadFiles`, if the file size is greater than the value of this parameter (in bytes), multipart upload is used; otherwise, simple upload is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent multipart copy uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10485760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template, such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies Content-MD5 when uploading files, which is false by default. If it is enabled, the MD5 checksum of the uploading files will be calculated, which may be time-consuming for large files | Boolean | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required | Function | No |
| Timeout | Timeout period in milliseconds. Default value: 0, indicating no timeout period. | Number | No |

#### getAuthorization Callback function description (method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Bucket | Bucket name in the format: `BucketName-APPID` | String |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are listed as follows:

| Attribute | Description | Type  |Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
| StartTime | The timestamp (in seconds) of the time when you obtained the key, such as `1580000000`. Passing this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No |
| ExpiredTime | `expiredTime` of the obtained temporary key (in seconds), i.e., the timeout timestamp, such as 1580000900 | String | Yes |

#### getAuthorization Callback function description (method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Method | Method of the current request | String |
| - Pathname | Request path used for signature calculation | String |
| - Key | An object key (object name) is the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - Query | Query parameter object of the current request in the format {key: 'val'} | Object |
| - Headers | Headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function | 

Once the `getAuthorization` callback function is finished, it returns one of the following:
An Authorization string.
An object whose attributes are listed as follows:

| Attribute | Description | Type  |Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting an authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function. Each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getAuthorization` callback. When the callback is called, a temporary key will be returned. After the key expires, the callback will be called again.

Below are some examples of common APIs. For more detailed initialization methods, please see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading an object

This API is suitable for uploading small files. To upload large files, please use the multipart upload API. For more information, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31538).

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',              /* Required */
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the file object.
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
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/', /*Optional*/
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an object

> !This API is used to read object content. If you need to launch a browser to download the file, you can get the URL through `cos.getObjectUrl` and then start the download in the browser. For more information, please see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31540).

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',              /* Required */
}, function(err, data) {
    console.log(err || data.Body);
});
```

### Deleting an object

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject'        /* Required */
}, function(err, data) {
    console.log(err || data);
});
```
