## Download and Installation

#### Relevant resources

- Download COS XML SDK source code for Weixin Mini Programs source code here [XML SDK for Weixin Mini Program](https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the XML mini program SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-wx-sdk-v5/latest/cos-wx-sdk-v5.zip).
- Download the demo here [XML SDK for Weixin Mini Program Demo](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- For the complete sample code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/MiniProgram).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [Mini Program SDK FAQs](https://intl.cloud.tencent.com/document/product/436/38958).

>? If you encounter errors such as non-existent functions or methods when using the SDK, you can update the SDK to the latest version and try again.
>

#### Environmental dependencies

1. This SDK is only applicable to Weixin Mini Programs.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [region information](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get your project's `SecretId` and `SecretKey`.

>? 
> - For the definition of parameters such as `SecretId`, `SecretKey`, and `Bucket`, see COS’s [Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
> - If you are using cross platform framework such as uni-app, and encounter problems when packaging the app (such as iOS or Android app), use the iOS SDK or Android SDK.
> - SDKs on versions earlier than v1.2.0 support the `XCosSecurityToken` field only. For later SDKs, use `SecurityToken` instead.
> 


#### Installing SDK

There are two ways to install the SDK for Weixin Mini Programs: manual installation and installation through npm as detailed below.

#### Installing manually

Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) file in the source code directory to any path in the root directory of your Weixin Mini Program code and reference it using a relative path:

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

#### Installing through npm

If the code of your Weixin Mini Program is packaged using webpack, install the dependencies via npm:

```plaintext
npm install cos-wx-sdk-v5
```

Here, the program code is referenced by using `var COS = require('cos-wx-sdk-v5');`. For more information, see [Support for npm](https://developers.weixin.qq.com/miniprogram/dev/devtools/npm.html).

## Getting Started

### Configuring domain name allowlist for Weixin Mini Programs

To request COS in your Weixin Mini Program, you need to log in to the [Weixin Official Accounts Platform](https://mp.weixin.qq.com) and configure the domain name allowlist in **Development** > **Development Settings** > **Server Domain Name**. The SDK uses the following two APIs:

1. For cos.postObject, use the wx.uploadFile API.
2. For other methods, use the wx.request API.

For both methods, you need to configure the COS domain name. There are two forms of domain name allowlists.

1. For standard requests, you can configure the bucket domain name as the allowed domain name, for example:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`
2. If multiple buckets are used in your Weixin Mini Program, you can choose to use suffixed COS requests by passing in `ForcePathStyle: true` when instantiating the SDK. In this case, you need to configure the region domain name as the allowed domain name, such as `cos.ap-guangzhou.myqcloud.com`.

### Initialization

>!
>- We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.



```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

```js
var cos = new COS({
    // ForcePathStyle: true, // If multiple buckets are used, you can use suffixed requests to reduce the number of allowed domain names to be configured; the region domain name will be used for requests.
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
                    // For SDKs on versions earlier than v1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    SecurityToken: credentials.sessionToken,
                    // We recommend that you use the server time as the signature start time to avoid signature errors caused by time deviations.
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

### Configuration item

#### Sample code

Create a COS SDK instance in the following methods:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

```js
var cos = new COS({
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
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
                    // For SDKs on versions earlier than v1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    SecurityToken: credentials.sessionToken,
                    // We recommend that you use the server time as the signature start time to avoid signature errors caused by time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
                });
            }
        });
    }
});
```
>? For more information about how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

- Method 2 (recommended): Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through Scope.

```js
var cos = new COS({
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
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
                    // For SDKs on versions earlier than v1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    SecurityToken: credentials.sessionToken,
                    // We recommend that you use the server time as the signature start time to avoid signature errors caused by time deviations.
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting the key to be reused only for the same request
                });
            }
        });
    }
});
```

>? For more information about how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

- Method 3 (not recommended). The frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a fixed or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control permissions for multipart upload and thus is not recommended.

```js
var cos = new COS({
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
    // Required parameter
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: there may be a security risk associated with this method. The backend needs to strictly control permissions through method and pathname, such as prohibiting put /
        wx.request({
            url: 'https://example.com/server/auth.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                if (!data || !data.authorization) return console.error('authorization invalid');
                callback({
                    Authorization: data.authorization,
                    // For SDKs on versions earlier than v1.2.0, use `XCosSecurityToken` instead of `SecurityToken`.
                    // SecurityToken: data.sessionToken, // If a temporary key is used, sessionToken needs to be passed to SecurityToken.
                });
            }
        });
    },
});
```

- Method 4 (not recommended): The frontend uses a permanent key to calculate the signature. This method can be used for frontend debugging. If you use this method, be sure to avoid key disclosure.

```js
// Log in to https://console.cloud.tencent.com/cam/capi to check and manage the SecretId and SecretKey of your project.
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
    SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload. The SDK version must be v1.3.0 or later.
});
```

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User's `SecretKey`, which we recommend to be used only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure. Default value: 2 (a request will be made 3 times in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is greater than the value of this parameter, multipart upload (sliceUploadFile) is used; otherwise, simple upload (putObject) is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: `10485760` (10 MB) | Number | No |
| CopySliceSize | When a file is copied using sliceCopyFile, if the file size is greater than the value of this parameter, multipart copy (sliceCopyFile) is used; otherwise, simple copy (putObjectCopy) is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| ServiceDomain | The request domain name when `getService` is called, such as `service.cos.myqcloud.com` | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template, such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5  | Forces the verification of Content-MD5 for file uploads, which calculates the MD5 checksum of the file request body and places it in the Content-MD5 field of the header. Default value: false | Boolean | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required. <br> **Note: This callback method is passed in during instance initialization, and is only executed to obtain the signature when the instance calls APIs.** | Function | No |
| UseAccelerate          | Whether to enable a global acceleration endpoint. Default value: `false`. If you set the value to `true`, you need to enable global acceleration for the bucket. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406). | Boolean | No   |
| SimpleUploadMethod     | The name of the method for simply uploading small files during advanced upload and batch upload. Valid values: `postObject`, `putObject`. Default value: `postObject`. This parameter is supported starting from v1.3.0. | String | No |

#### getAuthorization Callback function description (Format 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

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
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. Use `XCosSecurityToken` instead of `SecurityToken` for SDKs on versions earlier than v1.2.0. | String | Yes |
| StartTime | The timestamp in seconds of when you obtained the key, such as `1580000000`. Passing in this parameter as the signature start time can avoid signature expiration issues due to time deviation on the frontend. | String | No   |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | Yes |

#### getAuthorization Callback function description (Format 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object for getting the signature | Object |
| - Method | Method of the current request | Object | 
| - Pathname | Request path used for signature calculation | String |
| - Key | An object key (object name), the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). <br> **Note: This parameter is empty if the API that uses the instance is not an object-operation API.** | String |
| - Query | Query parameter in the current request. Format: {key: 'val'} | Object |
| - Headers | Headers in the current request. Format: {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function | 

Once the getAuthorization callback function is finished, it returns one of the following:
An Authorization string.
An object whose attributes are listed as follows:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. Use `XCosSecurityToken` instead of `SecurityToken` for SDKs on versions earlier than v1.2.0. | String | No |

#### Getting an authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function. Each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getSTS` callback. Each time a temporary key is required, it will be returned to the instance for signature calculation within the instance during each request.

### Enabling DataInsight

We have introduced the [Tencent Beacon](https://beacon.tencent.com/) into the SDK to track down and optimize the SDK quality for a better user experience.
>? DataInsight only monitors the COS request performance and doesn't report any business data.
>

To enable this feature, make sure that the SDK version is 1.4.0 or later and specify `EnableTracker` as `true` during initialization.
Then, add the following to the valid request domain name allowlist of the mini program: `https://h.trace.qq.com;https://oth.str.beacon.qq.com;https://otheve.beacon.qq.com;`.

```js
new COS({
  EnableTracker: true,
})
```

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

>! If you need to create a bucket via the Weixin Mini Program, but the bucket name is unknown, you cannot configure the bucket name as an allowed domain name. Instead, you can use suffixed calls. For more information, see [FAQs](https://intl.cloud.tencent.com/document/product/436/10687).
>

### Querying the bucket list

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### Uploading an object

We strongly recommend you use the advanced upload API `uploadFile`, which automatically uses simple upload for small files and multipart upload for large files for a better performance. For more information, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/43881).
If you use the temporary key method, you need to grant the permissions of both simple upload and multipart upload as instructed in [Working with COS API Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580).
For SDK FAQs, see [FAQs](https://intl.cloud.tencent.com/document/product/436/40775).

```js
/* Initialize COS */
var cos = new COS({
  // getAuthorization: funciton() {}, // See above for initialization.
  SimpleUploadMethod: 'putObject', // We strongly recommend you use `putObject` when simply uploading small files during advanced upload and batch upload.
});

function handleFileInUploading(fileName, filePath) {
  cos.uploadFile({
      Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
      Region: 'COS_REGION',     /* Bucket region. Required */
      Key: fileName,              /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
      FilePath: filePath, /* Path of the file to be uploaded (required) */
      SliceSize: 1024 * 1024 * 5,     /* Threshold (5 MB in this example) to trigger multipart upload. If the file size is less than 5 MB, simple upload is used. This parameter is optional. You can adjust it as needed. */
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

/* Select a file to get the temporary path (with an image as an example here). For other types of files, see the official APIs of Weixin Mini Program. */
wx.chooseImage({
    count: 1, // Default value: 9
    sizeType: ['original'], // You can specify whether to use the original or compressed image. The original is used by default value.
    sourceType: ['album', 'camera'], // You can specify whether the source is an album or camera. Both are included by default. 
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var fileName = filePath.substr(filePath.lastIndexOf('/') + 1);
        handleFileInUploading(fileName, filePath);
    }
});
```

### Querying objects

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

>! This API is used to read object content. To download a file using your browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, see [Pre-signed URLs](https://intl.cloud.tencent.com/document/product/436/31711).
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
