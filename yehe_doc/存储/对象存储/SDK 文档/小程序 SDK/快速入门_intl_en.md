## Download and Installation

#### Relevant resources

- Download COS XML SDK source code for WeChat Mini Programs source code here [XML SDK for WeChat Mini Program](https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the XML mini program SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-wx-sdk-v5/latest/cos-wx-sdk-v5.zip).
- Download the demo here [XML SDK for WeChat Mini Program Demo](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- For the complete sample code, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/MiniProgram).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, please see [Mini Program SDK FAQs](https://intl.cloud.tencent.com/document/product/436/38958).

>? If you encounter errors such as non-existent functions or methods when using the SDK, please update the SDK to the latest version and try again.
>

#### Environmental dependencies

1. This SDK is only applicable to WeChat Mini Programs.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region information](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

>? 
> - For the definition of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see COS’s [Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
> - Use instructions for cross-device frameworks (such as uni-app): for mobile apps that cannot be packaged for normal use after being developed using the Mini Program SDK, such as Android and iOS apps, you need to use the corresponding Android SDK and iOS SDK.
> 


#### Installing SDK

There are two ways to install the SDK for WeChat Mini Programs: manual installation and installation through npm as detailed below.

#### Installing manually

Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) file in the source code directory to any path in the root directory of your WeChat Mini Program code and reference it using a relative path:

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

#### Installing through npm

If the code of your WeChat Mini Program is packaged using webpack, install the dependencies via npm:

```plaintext
npm install cos-wx-sdk-v5
```

The WeChat Mini Program code is referenced with `var COS = require('cos-wx-sdk-v5');`.

## Getting Started

### Configuring domain name whitelist for WeChat Mini Programs

To request COS in your WeChat Mini Program, you need to log in to the [WeChat Official Accounts Platform](https://mp.weixin.qq.com) and configure the domain allowlist by navigating to **Development** > **Development Settings** > **Server Domain Name**. The SDK uses the following two APIs:

1. For cos.postObject, use the wx.uploadFile API.
2. For other methods, use the wx.request API.

For both methods, you need to configure the COS domain name. There are two forms of domain name whitelists.

1. For standard requests, you can configure the bucket domain name as the whitelist domain name, for example:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`
2. If multiple buckets are used in your WeChat Mini Program, you can choose to use suffixed COS requests by passing in `ForcePathStyle: true` when instantiating the SDK. In this case, you need to configure the region domain name as the whitelist, such as `cos.ap-guangzhou.myqcloud.com`.

### Initialization

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

```js
var cos = new COS({
    // ForcePathStyle: true, // If multiple buckets are used, you can use suffixed requests to reduce the number of whitelisted domain names to be configured; the region domain name will be used for requests.
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously.
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                bucket: options.Bucket,
                region: options.Region,
            },
            dataType: 'json',
            success: function (result) {
                var data = result.data;
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
            }
        });
    }
});

// The COS instance can then be used to call a COS request.
// TODO
```

### Configuration Item

#### Sample code

Create a COS SDK instance in the following methods:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

```js
var cos = new COS({
    // Required parameter
    getAuthorization: function (options, callback) {
        // Server examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                // The required parameters can be obtained from options.
            },
            success: function (result) {
                var data = result.data;
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
            }
        });
    }
});
```
>? For more information about how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

- Method 2 (recommended): Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through Scope.

```js
var cos = new COS({
    // Required parameter
    getAuthorization: function (options, callback) {
        // Server example: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
        wx.request({
            url: 'https://example.com/server/sts-scope.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
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

>? For more information about how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

- Method 3 (not recommended): the frontend needs to get a signature through getAuthorization before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control the permission to multipart uploads and thus is not recommended.

```js
var cos = new COS({
    // Required parameter
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, please see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: there may be a security risk associated with this method. The backend needs to strictly control permissions through method and pathname, such as prohibiting put /
        wx.request({
            url: 'https://example.com/server/auth.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                if (!data || !data.authorization) return console.error('authorization invalid');
                callback({
                    Authorization: data.authorization,
                    // XCosSecurityToken: data.sessionToken, // If a temporary key is used, sessionToken needs to be passed to XCosSecurityToken
                });
            }
        });
    },
});
```

- Method 4 (not recommended): the frontend uses a permanent key to calculate the signature. This method can be used for frontend debugging. If you use this method, be sure to avoid key disclosure.

```js
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to check and manage the `SecretId` and `SecretKey` of your project.
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
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
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is greater than the value of this parameter, multipart upload (sliceUploadFile) is used; otherwise, simple upload (putObject) is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: `10485760` (10 MB) | Number | No |
| CopySliceSize | When a file is copied using sliceCopyFile, if the file size is greater than the value of this parameter, multipart copy (sliceCopyFile) is used; otherwise, simple copy (putObjectCopy) is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | Protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| ServiceDomain | The request domain name when `getService` is called, such as `service.cos.myqcloud.com` | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template such as `"{Bucket}.cos.{Region}.myqcloud.com" ` which will use the bucket and region information passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces the verification of Content-MD5 for file uploads, which calculates the MD5 checksum of the file request body and places it in the Content-MD5 field of the header. Default value: false | Boolean | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required. <br>**Note: This callback method is passed in during instance initialization, and is only executed to obtain the signature when the instance calls APIs. ** | Function | No |

#### getAuthorization Callback function description (Format 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as listed below:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
| StartTime | The timestamp in seconds of when you obtained the key, such as `1580000000`. Passing in this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No   |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | Yes |

#### getAuthorization Callback function description (Format 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object |
| - Method | Method of the current request | Object | 
| - Pathname | Request path used for signature calculation | String |
| - Key | An object key (object name), the unique identifier of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). <br> **Note: This parameter is empty if the API that uses the instance is not an object-operation API.** | String |
| - Query | Query parameter in the current request. Format: {key: 'val'} | Object |
| - Headers | Headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function | 

Once the getAuthorization callback function is finished, it returns one of the following:
An Authorization string.
An object whose attributes are listed as follows:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting an authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback, and each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

Below are some examples of common APIs. For more detailed initialization methods, see the examples in the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/).

### Creating a bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

>! If you need to create a bucket via the WeChat Mini Program, but the bucket name is unknown, you cannot configure the bucket name as a allowlisted domain name. Instead, you can use suffixed calls. For more information, please see [FAQs](https://intl.cloud.tencent.com/document/product/436/10687).
>

### Querying the bucket list

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an object

The WeChat Mini Program upload API "wx.uploadFile" only supports POST requests. To upload files with the SDK, you need to use the postObject API. If only the file uploading API is needed in your WeChat Mini Program, we do not recommend referencing the SDK. For more information, please see the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js).

```js
// First, select the file to get the temporary path
wx.chooseImage({
    count: 1, // Default value: 9
    sizeType: ['original'], // You can specify whether to use the original or compressed image. The original is used by default value.
    sourceType: ['album', 'camera'], // You can specify whether the source is an album or camera. Both are included by default. 
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var filename = filePath.substr(filePath.lastIndexOf('/') + 1);
        cos.postObject({
            Bucket: 'examplebucket-1250000000',
            Region: 'ap-beijing',
            Key: 'destination path/' + filename,
            FilePath: filePath,
            onProgress: function (info) {
                console.log(JSON.stringify(info));
            }
        }, function (err, data) {
            console.log(err || data);
        });
    }
});
```

### Query objects

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/', // Pass in the file prefixes to be listed here
}, function (err, data) {
    console.log(err || data.Contents);
});
```

### Download an object

>! This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, please see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31711).
>

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'exampleobject.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### Delete an object

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
}, function (err, data) {
    console.log(err || data);
});
```
