## Download and Installation

#### Relevant Resources

- Download the COS XML SDK for WeChat Mini Program source code [here](https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the demo [here](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).

#### Environmental Requirements

1. This SDK is only applicable to WeChat Mini Programs.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region information](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's SecretId and SecretKey.

> For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).

#### Installing the SDK

There are two ways to install the SDK for WeChat Mini Program: manual installation and installation via npm as detailed below.

#### Manual Installation

Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) file in the source code directory to the code directory of your WeChat Mini Program. The code can be referenced with a relative path:
```shell
var COS = require('./cos-wx-sdk-v5.js')
```

#### Installing via npm

If the code of your WeChat Mini Program is packaged using webpack, install the dependencies via npm:
```shell
npm install cos-wx-sdk-v5
```

The WeChat Mini Program code is referenced with `var COS = require('cos-wx-sdk-v5');`.

## Getting Started

### Configuring the WeChat Mini Program Whitelist

To request COS in the WeChat Mini Program, you need to log in to the [WeChat Official Accounts Platform](https://mp.weixin.qq.com) and configure the domain name whitelist in **Development** > **Development Settings**. The SDK uses the following two APIs:

1. For cos.postObject, use the wx.uploadFile API.
2. For other methods, use the wx.request API.

You need to configure COS domain names in corresponding whitelists. There are two forms of whitelisted domain names.

1. For standard requests, you can configure the bucket domain name as the whitelisted domain name, for example:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`。
2. If multiple buckets are used in the WeChat Mini Program, you can choose to use suffixed COS requests by passing in `ForcePathStyle: true` when instantiating the SDK. In this case, you need to configure the region domain name as the whitelisted domain name, such as `cos.ap-guangzhou.myqcloud.com`.

### Initialization

```js
var cos = new COS({
    // ForcePathStyle: true, // If multiple buckets are used, you can use suffixed requests to reduce the number of whitelisted domain names to be configured; and the region domain name will be used for requests
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                bucket: options.Bucket,
                region: options.Region,
            },
            dataType: 'text',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime,
                });
            }
        });
    }
});

// Next you can use a COS instance to call a COS request
// TODO
```

### Configuration Items

#### Use Cases

Create a COS SDK instance in the following methods:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

```js
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://cloud.tencent.com/document/product/436/14048
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                // The required parameters can be obtained from options
            },
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime,
                });
            }
        });
    }
});
```

- Method 2 (recommended): The permissions are controlled in a fine-grained manner. The backend gets a temporary key and sends it to the frontend. The frontend only reuses the key for the same request, and the backend can manage the permissions in a fine-grained manner through Scope.

```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side example: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
        wx.request({
            url: 'https://example.com/server/sts-scope.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime,
                    ScopeLimit: true, // You need to set the fine-grained permission control to true to make sure that the key will only be reused for the same request
                });
            }
        });
    }
});
```

- Method 3 (not recommended): The frontend needs to get a signature through getAuthorization before each request, and the backend uses a fixed or temporary key to calculate the signature and returns it to the frontend. This method will make it hard for you to control the permissions for multipart uploads and thus is not recommended.

```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: This method involves security risks. The backend needs to strictly control the permissions through method and pathname, such as prohibiting `PUT` /
        wx.request({
            url: 'https://example.com/server/auth.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                callback({
                    Authorization: data.authorization,
                    // XCosSecurityToken: data.sessionToken, // If a temporary key is used, sessionToken needs to be passed to XCosSecurityToken
                });
            }
        });
    },
});
```

- Method 4 (not recommended): The frontend uses a fixed key to calculate the signature. This method can be used for frontend debugging. If you use this method, be sure to avoid key disclosure.

```js
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
});
```

#### Constructor Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User SecretKey. It is recommended to only use the SecretKey for frontend debugging to avoid key disclosure | String | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for a single file; default value: 3 | Number | No |
| CopyChunkSize | Number of retries upon multipart upload failure. Default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No |
| CopySliceSize | Part size in a multipart upload; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| Protocol | The protocol used to make a request; valid values: `https:`, `http:`. By default, `http:` will be used when the current page is using `http:`; otherwise, `https:` will be used | String | No |
| ServiceDomain | The domain name requested by the getService method. <br>Example: `cos.ap-beijing.myqcloud.com`| String | No |
| Domain | The domain name used to call a bucket, which can be a template. <br>Example: `"{Bucket}.cos.{Region}.myqcloud.com`| String | No |
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
| Authorization | The authorization calculated with a permanent or temporary key | String | Yes |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting an Authentication Credential

You can obtain the authentication credentials for your instance in three ways by passing in different parameters during instantiation:

1. During instantiation, pass in the SecretId and SecretKey, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getSTS callback, and each time a temporary key is required, it will be returned to the instance through this callback for signature calculation within the instance during each request.

Below are some examples of common APIs. For more detailed initialization methods, see the examples in the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/).

### Creating a Bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
}, function (err, data) {
    console.log(err || data);
});
```

> ! If you need to create a bucket in the WeChat Mini Program, but the bucket name is unknown, you cannot configure the bucket name as a whitelisted domain name. Instead, you can use suffixed calls. For details, see [FAQs](https://intl.cloud.tencent.com/document/product/436/10687).

### Querying Bucket List

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an Object

The WeChat Mini Program upload API `wx.uploadFile` only supports `POST` requests. To upload files with the SDK, you need to use the `postObject` API. If you only need to use the file upload API in your WeChat Mini Program, it is recommended not to reference the SDK. For more information, see the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js).

```js
// First, select the file to get the temporary path
wx.chooseImage({
    count: 1, // Default value: 9
    sizeType: ['original'], // You can specify whether to use the original or compressed image. The original is used by default
    sourceType: ['album', 'camera'], // You can specify whether the source is album or camera. Both can be the source by default
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

> ! This API is used to read the object content. If you need to launch a browser to download the file, you can get the URL through cos.getObjectUrl and then start a download in the browser. For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31711).

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'exampleobject.txt',
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
