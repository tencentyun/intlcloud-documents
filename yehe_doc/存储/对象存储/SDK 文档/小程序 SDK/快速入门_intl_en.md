## Download and Installation

#### Relevant resources

- Download the COS XML SDK for WeChat Mini Program source code [here](https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the XML SDK for WeChat Mini Program [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-wx-sdk-v5/latest/cos-wx-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- Find the complete sample code [here](https://github.com/tencentyun/cos-snippets/tree/master/MiniProgram).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/CHANGELOG.md).

#### Environmental dependency

1. This SDK is only applicable to WeChat Mini Program.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region information](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

> ?For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751#cos-glossary).

#### Installing SDK

There are two ways to install the SDK for WeChat Mini Programs: manual installation and installation through npm as detailed below.

#### Installing manually

Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) file in the source code directory to any path in the root directory of your WeChat Mini Program code and reference it using a relative path:

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

#### Installing through npm

If the code of your WeChat Mini Program is packaged with webpack, install the dependencies through npm:

```plaintext
npm install cos-wx-sdk-v5
```

The WeChat Mini Program code is referenced with `var COS = require('cos-wx-sdk-v5');`.

## Getting Started

### Configuring domain name allowlist for WeChat Mini Program

To request COS in your WeChat Mini Program, you need to log in to the [WeChat Official Accounts Platform](https://mp.weixin.qq.com) and configure the domain name allowlist in **Development** > **Basic Configuration** > **Server Domain**. The SDK uses the following two APIs:

1. For cos.postObject, use the wx.uploadFile API.
2. For other methods, use the wx.request API.

For both methods, you need to configure the COS domain name. There are two forms of domain name allowlists.

1. For standard requests, you can configure the bucket domain name as the allowlist domain name, for example:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
2. If multiple buckets are used in your WeChat Mini Program, you can choose to use suffixed COS requests by passing in `ForcePathStyle: true` when instantiating the SDK. In this case, you need to configure the region domain name as the allowlist, such as `cos.ap-guangzhou.myqcloud.com`.

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
                    // We recommend you use the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations.
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

### Configuration items

#### Samples

Create a COS SDK instance in the following methods:

- Method 1 (recommended): the backend gets a temporary key and sends it to the frontend for signature calculation.

```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, please see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://cloud.tencent.com/document/product/436/14048
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                // The required parameters can be obtained from options
            },
            success: function (result) {
                var data = result.data;
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    // We recommend you use the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
                });
            }
        });
    }
});
```
>?For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

- Method 2 (recommended): the permission is controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can finely manage the permission through Scope.

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
                    // We recommend you use the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting that the key can be reused only for the same request
                });
            }
        });
    }
});
```

>?For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

- Method 3 (not recommended): the frontend needs to get a signature through getAuthorization before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control the permission to multipart uploads and thus is not recommended.

```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, please see the COS SDK for the corresponding programming language: https://intl.cloud.tencent.com/document/product/436/6474
        // Note: there may be a security risk associated with this method. The backend needs to strictly control the permission through method and pathname, such as prohibiting put /
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
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
});
```

#### Constructor parameter description

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User's `SecretId` | String | No |
| SecretKey | User's `SecretKey`, which we recommend you use only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload/copy failure. Default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is greater than the value of this parameter, multipart upload (sliceUploadFile) is used; otherwise, simple upload (putObject) is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation with sliceCopyFile. Default value: 10485760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied using sliceCopyFile, if the file size is greater than the value of this parameter, multipart copy (sliceCopyFile) is used; otherwise, simple copy (putObjectCopy) is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | Protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| ServiceDomain | The request domain name when the `getService` method is called, such as `service.cos.myqcloud.com` | String | No |
| Domain | Custom request domain name used to call a bucket or object API. You can use a template such as `"{Bucket}.cos.{Region}.myqcloud.com" ` which will use the bucket and region information passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces the verification of Content-MD5 for file uploads, which calculates the MD5 checksum of the file request body and places it in the Content-MD5 field of the header. Default value: false | Boolean | No |
| GetAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required | Function | No |

#### getAuthorization callback function descriptions (using method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting a temporary key | Object |
| - Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |
| StartTime | Key acquisition start time measured in seconds, i.e., the timestamp of the key acquisition time, such as 1580000000. This parameter is used as the signature start time. Passing in this parameter can avoid signature expiration issues due to time deviation on the frontend |String|No|
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | No |

#### getAuthorization callback function description (using method 2)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` callback parameters:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object |
| - Method | Method of the current request | Object |
| - Pathname | Request path used for signature calculation | String |
| - Key | Object key (object name), which is the unique identifier of the object in the bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - Query | Query parameter object of the current request in the format of `{key: 'val'}` | Object |
| - Headers | Headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function |

Once the getAuthorization callback function is finished, it returns one of the following:
Format 1. An Authorization string.
Format 2. An object whose attributes are listed as follows:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback, and each time a temporary key is required, it will be returned to the instance by this callback for signature calculation within the instance during each request.

Below are some examples of common APIs. For more detailed initialization methods, please see the examples in the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/).

### Creating bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

> ! If you need to create a bucket in the WeChat Mini Program, but the bucket name is unknown, you cannot configure the bucket name as a domain name allowlist. Instead, you can use the suffix to call it. For applicable measures, please see [FAQs](https://intl.cloud.tencent.com/document/product/436/10687).

### Querying bucket list

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading object

The WeChat Mini Program upload API "wx.uploadFile" only supports POST requests. To upload files with the SDK, you need to use the postObject API. If only the file uploading API is needed in your WeChat Mini Program, we do not recommend you reference the SDK. For more information, please see [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js).

```js
// First, select the file to get the temporary path
wx.chooseImage({
    count: 1, // Default value: 9
    sizeType: ['original'], // You can specify whether to use the original or compressed image. The original is used by default value.
    You can specify whether the source is an album or camera. Both are included by default.
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

### Downloading object

> !This API is used to read the object content. If you need to launch a browser to download the file, you can get the URL through `cos.getObjectUrl` and then start a download in the browser. For more information, please see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31711).

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'exampleobject.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### Deleting object

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
}, function (err, data) {
    console.log(err || data);
});
```
