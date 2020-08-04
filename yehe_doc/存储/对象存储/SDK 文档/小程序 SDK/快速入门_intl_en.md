## Download and Installation

#### Relevant resources

- Download the COS XML SDK source code for WeChat Mini Programs [here](https://github.com/tencentyun/cos-wx-sdk-v5).
- SDK quick download address: [XML Mini Program SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-wx-sdk-v5/latest/cos-wx-sdk-v5.zip?_ga=1.29585407.1783616852.1583375173).
- Download the demo [here](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).

#### Environmental dependency

1. This SDK is only applicable to WeChat Mini Programs.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region information](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

> ?For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see COS’s [Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing the SDK

There are two ways to install the SDK for WeChat Mini Programs: manual installation and installation through npm as detailed below.

#### Installing manually

Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) file in the source code directory to any path in the root directory of your WeChat Mini Program code and reference it using a relative path:

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

#### Installing through npm

If the code of your WeChat Mini Program is packaged using webpack, install the dependencies via npm:

```shell
npm install cos-wx-sdk-v5
```

The WeChat Mini Program code is referenced with `var COS = require('cos-wx-sdk-v5');`.

## Getting Started

### Configuring domain name allowlist for WeChat Mini Programs

To send a COS request using WeChat Mini Program, log in to [Wechat Official Accounts Platform](https://mp.weixin.qq.com), select **Development** > **Settings** > **Server Domains**, and then configure a domain allowlist.The SDK uses the following two APIs:

1. For cos.postObject, use the wx.uploadFile API.
2. For other methods, use the wx.request API.

For both methods, you need to configure the COS domain name. There are two forms of domain name allowlists.

1. For standard requests, you can configure the bucket domain name as the allowlist domain name, for example:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
2. If multiple buckets are used in your WeChat Mini Program, you can choose to use suffixed COS requests by passing in `ForcePathStyle: true` when instantiating the SDK. In this case, you need to configure the region domain name as the allowed domain name, such as `cos.ap-guangzhou.myqcloud.com`.

### Initialization

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

```js
var cos = new COS({
    // ForcePathStyle: true, // If multiple buckets are used, you can use suffixed requests to reduce the number of allowed domain names to be configured; the region domain name will be used for requests
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
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

// The COS instance can then be used to call a COS request
// TODO
```

### Configuration Items

#### Use cases

Create a COS SDK instance in the following methods:

- Method 1 (recommended). The backend gets a temporary key and sends it to the frontend for signature calculation.

```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server examples for other programming languages, please see the [COS SDK for STS](https://github.com/tencentyun/qcloud-cos-sts-sdk)
        // For the STS documentation, please visit https://intl.cloud.tencent.com/document/product/436/14048
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                // You can obtain the required parameters from options
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
>?For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

- Method 2 (recommended). Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through Scope.

```js
var cos = new COS({
    // Required parameters
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

>?For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

- Method 3 (not recommended). The frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a fixed or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control permissions for multipart upload and thus is not recommended.

```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, please see the COS SDK for the corresponding programming language: https://intl.cloud.tencent.com/document/product/436/6474
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

- Method 4 (not recommended). The frontend uses a fixed key to calculate a signature. This method is suitable for frontend debugging. If you use this method, be sure to avoid key disclosure.

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
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is greater than the value of this parameter (measured in bytes), multipart upload (sliceUploadFile) is used; otherwise, simple upload (putObject) is used. Default value: 1,048,576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10,485,760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10,485,760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` measured in milliseconds. Default value: 1,000 | Number | No |
| Protocol | Protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| ServiceDomain | The request domain name when `getService` is called, such as `service.cos.myqcloud.com` | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template such as `""{Bucket}.cos.{Region}.myqcloud.com""` which will use the bucket and region information passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces the verification of `Content-MD5` for file uploads, which calculates the MD5 checksum of the file request body and places it in the `Content-MD5` field of the header. Default value: false | Boolean | No |
| GetAuthorization | Callback method for getting a signature. If there is no `SecretId` or `SecretKey`, this parameter is mandatory | Function | No |

#### `getAuthorization` callback function description (using method 1)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` Callback Parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting a temporary key | Function |
| - Bucket  | Bucket name in the format `BucketName-APPID`. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, callback returns an object. The attributes of the returned object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |
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
| - Method | Method of the current request | Object |
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
3. During instantiation, pass in the `getSTS` callback, and each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

Below are some examples of commonly used APIs. For more detailed initialization methods, please see the examples in the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/).

### Creating a bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

> !If you need to create a bucket in your WeChat Mini Program, but the bucket name is unknown, you cannot configure the bucket name as a domain name allowlist. Instead, you can use the suffix to call it. For applicable measures, please see [FAQs](https://intl.cloud.tencent.com/document/product/436/10687#.E5.B0.8F.E7.A8.8B.E5.BA.8F.E9.87.8C.E8.AF.B7.E6.B1.82.E5.A4.9A.E4.B8.AA.E5.9F.9F.E5.90.8D.EF.BC.8C.E6.88.96.E8.80.85.E5.AD.98.E5.82.A8.E6.A1.B6.E5.90.8D.E7.A7.B0.E4.B8.8D.E7.A1.AE.E5.AE.9A.EF.BC.8C.E6.80.8E.E4.B9.88.E8.A7.A3.E5.86.B3.E7.99.BD.E5.90.8D.E5.8D.95.E9.85.8D.E7.BD.AE.E5.92.8C.E9.99.90.E5.88.B6.E9.97.AE.E9.A2.98.EF.BC.9F).

### Querying a bucket list

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an object

The WeChat Mini Program upload API ""wx.uploadFile"" only supports POST requests. To upload files with the SDK, you need to use the postObject API. If only the file uploading API is needed in your WeChat Mini Program, we do not recommended referencing the SDK. For more information, please see the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js).

```js
// First, select the file to get the temporary path
wx.chooseImage({
    count: 1, // Default value: 9
    sizeType: ['original'], // You can specify whether to use the original or compressed image. The original is used by default
    sourceType: ['album', 'camera'], // You can specify whether the source is an album or camera. Both can be used as the default source 
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

### Querying object list

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/', // Pass in the file prefixes to be listed here
}, function (err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an object

> !This API is used to read object content. If you need to launch a browser to download the file, you can get the URL through `cos.getObjectUrl` and then start the download in the browser. For more information, please see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/30598).

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'exampleobject.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### Deleting an object

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
}, function (err, data) {
    console.log(err || data);
});
```
