## Download and Installation

#### Related resources

- Download the COS XML Mini Program SDK source code from [GitHub](https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the XML Mini Program SDK from [GitHub](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-wx-sdk-v5/latest/cos-wx-sdk-v5.zip).
- Download the XML Mini Program SDK demo from [GitHub](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- For all the code samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/MiniProgram).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [FAQs](https://intl.cloud.tencent.com/document/product/436/38958).

>? If you encounter errors such as non-existent functions or methods when using the SDK, update the SDK to the latest version and try again.
>

#### Environmental dependencies

1. This SDK is only applicable to the WeChat Mini Program environment.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and region information as described in [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

>? 
> - For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, see [Introduction](https://intl.cloud.tencent.com/document/product/436/7751).
> - If you use cross-platform frameworks such as uni-app and encounter problems when packaging the iOS or Android app, use the iOS SDK or Android SDK instead.
> - SDKs on versions earlier than 1.2.0 support the `XCosSecurityToken` field only. For later SDKs, use `SecurityToken` instead.
> 


#### Installing SDK

There are two ways to install the Mini Program SDK: manual installation and installation through npm, as detailed below.

#### Manual installation

Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) file in the source code directory to any path in the root directory of your mini program code and reference it by using a relative path:

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

#### Installation through npm

If the code of your mini program is packaged with webpack, install the dependencies through npm:

```plaintext
npm install cos-wx-sdk-v5
```

Here, the program code is referenced by using `var COS = require('cos-wx-sdk-v5');`. For more information, see [Support for npm](https://developers.weixin.qq.com/miniprogram/dev/devtools/npm.html).

## Getting Started

### Configuring domain name allowlist for mini program

To request COS in your mini program, you need to log in to the [Weixin Official Accounts Platform](https://mp.weixin.qq.com) and configure the domain name allowlist by navigating to **Development** > **Development Settings** > **Server Domain Name**. The SDK uses the following two APIs:

1. For `cos.postObject`, use the `wx.uploadFile` API.
2. For other methods, use the `wx.request` API.

For both methods, you need to configure the COS domain name. There are two forms of domain name allowlists:

1. For standard requests, you can configure the bucket domain name as the allowed domain name, for example:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
2. If multiple buckets are used in your mini program, you can choose to use suffixed COS requests by passing in `ForcePathStyle: true` when instantiating the SDK. In this case, you need to configure the region domain name as the allowed domain name, for example, `cos.ap-guangzhou.myqcloud.com`.

### Initialization

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

```js
var cos = new COS({
    // ForcePathStyle: true, // If multiple buckets are used, you can use suffixed requests to reduce the number of allowed domain names to be configured. The region domain name will be used for requests.
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
    getAuthorization: function (options, callback) {
        // It will not be called during initialization and will be entered only when a COS method such as `cos.putObject` is called.
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
                    // For SDKs on versions earlier than 1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    SecurityToken: credentials.sessionToken,
                    // We recommend you use the server time as the signature start time, so as to avoid signature errors due to time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000.
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900.
                });
            }
        });
    }
});

// The COS instance can then be used to call a COS request.
// TODO
```

### Configuration items

#### Sample code

Create a COS SDK instance in the following ways:

- Option 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

```js
var cos = new COS({
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
    // Required parameter
    getAuthorization: function (options, callback) {
        // For server-side samples for JS and PHP, visit https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/.
        // For server-side samples for other programming languages, see the COS STS SDK at https://github.com/tencentyun/qcloud-cos-sts-sdk.
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048.
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                // The required parameters can be obtained from `options`
            },
            success: function (result) {
                var data = result.data;
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    // For SDKs on versions earlier than 1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    SecurityToken: credentials.sessionToken,
                    // We recommend you use the server time as the signature start time, so as to avoid signature errors due to time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000.
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900.
                });
            }
        });
    }
});
```
>? For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

- Option 2 (recommended): Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through `Scope`.

```js
var cos = new COS({
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
    // Required parameter
    getAuthorization: function (options, callback) {
        // Server-side sample: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
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
                    // For SDKs on versions earlier than 1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    SecurityToken: credentials.sessionToken,
                    // We recommend you use the server time as the signature start time, so as to avoid signature errors due to time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000.
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900.
                    ScopeLimit: true, // For refined permission control, you need to set this parameter to `true`, so that the key can be reused only for the same request.
                });
            }
        });
    }
});
```

>? For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

- Option 3 (not recommended): The frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This option makes it difficult to control permissions for multipart upload and thus is not recommended.

```js
var cos = new COS({
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
    // Required parameter
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, see the COS SDK for the corresponding programming language at https://cloud.tencent.com/document/product/436/6474.
        // Note: There may be a security risk associated with this option. The backend needs to strictly control permissions through `method` and `pathname`, such as prohibiting `put /`.
        wx.request({
            url: 'https://example.com/server/auth.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                if (!data || !data.authorization) return console.error('authorization invalid');
                callback({
                    Authorization: data.authorization,
                    // For SDKs on versions earlier than 1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    // SecurityToken: data.sessionToken, // If a temporary key is used, `sessionToken` needs to be passed to `SecurityToken`.
                });
            }
        });
    },
});
```

- Option 4 (not recommended): The frontend uses a permanent key to calculate the signature. This option can be used for frontend debugging. If you use this option, be sure to avoid key disclosure.

```js
// Log in at https://console.cloud.tencent.com/cam/capi to view and manage the `SECRETID` and `SECRETKEY`.
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
});
```

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | Your `SecretId`. | String | No |
| SecretKey | Your `SecretKey`. We recommend you only use it for frontend debugging and avoid disclosing it. | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: `3`. | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: `3`. | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload/copy failure. Default value: `2` (a request will be made three times in total, including the initial one). | Number | No |
| ChunkSize | Part size in the multipart upload in bytes. Default value: `1048576` (1 MB). | Number | No |
| SliceSize | When files are uploaded in batches through `uploadFiles`, if the file size is greater than the value of this parameter, multipart upload (sliceUploadFile) will be used; otherwise, simple upload (putObject) will be used. Default value: `1048576` (1 MB). | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: `20`. | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation through `sliceCopyFile`. Default value: `10485760` (10 MB). | Number | No |
| CopySliceSize | When a file is copied through `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy (sliceCopyFile) will be used; otherwise, simple copy (putObjectCopy) will be used. Default value: `10485760` (10 MB). | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: `1000`. | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` will be used when the current page is determined to be in `http:`; otherwise, `https:` will be used. | String | No |
| ServiceDomain | The request domain name when the `getService` method is called, such as `service.cos.myqcloud.com`. | String | No |
| Domain | The custom request domain name used to call an API to manipulate a bucket or object. A template can be used, such as `"{Bucket}.cos.{Region}.myqcloud.com"`, which will use the bucket and region passed in the parameters for replacement when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excessive tasks will be cleared if their status is not `waiting`, `checking`, or `uploading`. Default value: `10000`. | Number | No |
| ForcePathStyle | Whether to forcibly use a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: `false`. | Boolean | No |
| UploadCheckContentMd5  | Whether to forcibly verify `Content-MD5` for file uploads, which will calculate the MD5 checksum of the file request body and place it in the `Content-MD5` field of the header. Default value: `false`. | Boolean | No |
| getAuthorization | The callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter will be required. <br>**Note: This callback method is passed in during instance initialization and is only executed to obtain the signature when the instance calls APIs.** | Function | No |
| UseAccelerate          | Whether to enable a global acceleration endpoint. Default value: `false`. If you set the value to `true`, you need to enable global acceleration for the bucket. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406). | Boolean | No   |
| SimpleUploadMethod     | The name of the method for simply uploading small files during advanced upload and batch upload. Valid values: `postObject`, `putObject`. Default value: `postObject`. This parameter is supported starting from v1.3.0. | String | No |

#### getAuthorization callback function description (format 1)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` callback parameter descriptions:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | The parameter object for getting the temporary key. | Object   |
| - Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format. | String |
| - Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String   |
| callback | Callback method after the temporary key is obtained. | Function |

After the temporary key is obtained, the callback will return an object. The parameters of the returned object are as listed below:

| Parameter | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | Yes |
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. Use `XCosSecurityToken` instead of `SecurityToken` for SDKs on versions earlier than 1.2.0. | String | Yes |
| StartTime | The timestamp in seconds when the key is obtained, such as `1580000000`. Passing in this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No   |
| ExpiredTime | `expiredTime` of the obtained temporary key in seconds, i.e., the timeout timestamp, such as 1580000900. | String | Yes |

#### getAuthorization callback function description (format 2)

```
getAuthorization: function(options, callback) { ... }
```

`getAuthorization` callback parameter descriptions:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | The parameter object for getting the signature | Object |
| - Method | The method of the current request | Object |
| - Pathname | The request path used for signature calculation | String |
| - Key | Object key (object name), which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). <br>**Note: This parameter will be empty if the API that uses the instance is not an object-operation API.** | String |
| - Query | Query parameter in the current request. Format: {key: 'val'}. | Object |
| - Headers | Headers in the current request. Format: {key: 'val'}. | Object |
| callback | Callback after the temporary key is obtained. | Function |

Once the `getAuthorization` callback function is completed, it will return one of the following:
Format 1: An `Authorization` string.
Format 2: An object with the following parameters:

| Parameter | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | Calculated signature string                                         | String | Yes   |
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. Use `XCosSecurityToken` instead of `SecurityToken` for SDKs on versions earlier than 1.2.0. | String | No |

#### Getting authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function. Each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback. Each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

### Enabling DataInsight

We have introduced [DataInsight](https://beacon.tencent.com/) into the SDK to track and optimize the SDK quality for a better user experience.
>? DataInsight only monitors the COS request performance but doesn't report the business data.
>

To enable this feature, make sure that the SDK version is 1.4.0 or later and specify `EnableTracker` as `true` during initialization.
Then, add the following to the valid request domain name allowlist of the mini program: `https://h.trace.qq.com;https://oth.str.beacon.qq.com;https://otheve.beacon.qq.com;`.

```js
new COS({
  EnableTracker: true,
})
```

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

Below are some common API samples. For more detailed initialization methods, see the demo at [GitHub](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/).

### Creating bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

>! If you need to create a bucket via the mini program, but the bucket name is unknown, you cannot configure the bucket name as an allowed domain name. In this case, you can use suffixed calls. For more information, see [APIs](https://intl.cloud.tencent.com/document/product/436/10687).
>

### Querying bucket list

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading object

We strongly recommend you use the advanced upload API `uploadFile`, which automatically uses simple upload for small files and multipart upload for large files for a better performance. For more information, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/43881).
If you use the temporary key method, you need to grant the permissions of both simple upload and multipart upload as instructed in [Working with COS API Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580).
For more information on how to troubleshoot common upload errors, see [FAQs](https://intl.cloud.tencent.com/document/product/436/40775).

```js
/* Initialize COS */
var cos = new COS({
  // getAuthorization: funciton() {}, // See above for initialization.
  SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload.
});

function handleFileInUploading(fileName, filePath) {
  cos.uploadFile({
      Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
      Region: 'COS_REGION',     /* Bucket region (required) */
      Key: fileName,              /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
      FilePath: filePath, /* Path of the file to be uploaded (required) */
      SliceSize: 1024 * 1024 * 5,     /* The customizable threshold (5 MB in this example) to trigger multipart upload (optional). */
      onProgress: function(progressData) {
          console.log(JSON.stringify(progressData));
      }
  }, function(err, data) {
      if (err) {
        console.log('Upload failed', err);
      } else {
        console.log('Uploaded successfully');
      }
  });
}

/* Select a file to get the temporary path (with an image as an example here). For other types of files, see the official APIs of WeChat Mini Program. */
wx.chooseImage({
    count: 1, // Default value: `9`
    sizeType: ['original'], // You can specify whether to use the original or compressed image. The original is used by default.
    sourceType: ['album', 'camera'], // You can specify whether the source is an album or camera. Both are included by default.
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var fileName = filePath.substr(filePath.lastIndexOf('/') + 1);
        handleFileInUploading(fileName, filePath);
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

>! This API is used to read object content. To download a file through a browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, see [Generating Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31711).
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
