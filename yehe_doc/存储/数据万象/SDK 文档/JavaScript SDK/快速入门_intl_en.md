## Download and Installation

#### Related resources

- Download the COS XML JavaScript SDK source code from [GitHub](https://github.com/tencentyun/cos-js-sdk-v5).
- Download the XML JavaScript SDK from [GitHub](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-js-sdk-v5/latest/cos-js-sdk-v5.zip).
- Download the XML JavaScript SDK demo from [GitHub](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).
- For all the code samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/JavaScript).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/40775).


>? If you encounter errors such as non-existent functions or methods when using the XML SDK, update the SDK to the latest version and try again.
>

#### Environment requirements

1. The JavaScript SDK requires the browser to support basic HTML5 features (IE 10 or later) for AJAX file uploading and MD5 checksum calculation.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get the `SecretId` and `SecretKey` of your project.
4. Configure a CORS rule. Set `*` for `AllowHeader`. For `ExposeHeaders`, set `ETag`, `Content-Length`, and other header fields that JavaScript needs to read as shown below. For more information, see [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318).


>? 
> - For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, see [Introduction](https://intl.cloud.tencent.com/document/product/436/7751).
> - If you use cross-platform frameworks such as uni-app and encounter problems when packaging the iOS or Android app, use the iOS SDK or Android SDK instead.
> 

#### Installing SDK

You can install the SDK in the following ways:

#### Importing via script
>? Click [here](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/dist/cos-js-sdk-v5.min.js) to download the latest `cos-js-sdk-v5.min.js`.
```html
<script src="https://cdn.jsdelivr.net/npm/cos-js-sdk-v5/dist/cos-js-sdk-v5.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name `COS`, and its constructor can create an SDK instance.

#### Importing via webpack

Install the SDK dependencies by running `npm i cos-js-sdk-v5 --save`, which supports webpack packaging scenarios. You can use npm import as a module with the following code:

```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

### Getting temporary key

As placing a permanent key on the frontend may cause security risks, we recommend you use temporary keys during formal deployment. The implementation process is as follows: the frontend first requests the server, and then the server uses the permanent key to call the STS service to apply for a temporary key as described in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) and returns it to the frontend.

>!If the site has a login state, login state verification should be added to the temporary key getting API.

### Initialization

1. Create a `web.html` file, enter the following code, and modify the bucket name and region in `web.html`.
2. Deploy the temporary key service on the backend and modify the key service address in `getAuthorization`.
3. Place the `web.html` file on the web server, visit the page in a browser, and test file uploading. The sample code for `web.html` is as follows:

```html
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>

// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
var Bucket = 'examplebucket-1250000000';  /* Bucket (required) */

// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. 
// For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
var Region = 'COS_REGION';     /* Bucket region (required) */

// Initialize an instance
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously.
        // For server-side samples for JavaScript and PHP, visit https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/.
        // For server-side samples for other programming languages, see the COS STS SDK at https://github.com/tencentyun/qcloud-cos-sts-sdk.
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048.

        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
                var credentials = data.credentials;
            } catch (e) {
            }
            if (!data || !credentials) {
              return console.error('credentials invalid:\n' + JSON.stringify(data, null, 2))
            };
            callback({
              TmpSecretId: credentials.tmpSecretId,
              TmpSecretKey: credentials.tmpSecretKey,
              SecurityToken: credentials.sessionToken,
              // We recommend you use the server time as the signature start time, so as to avoid signature errors due to time deviations.
              StartTime: data.startTime, // Timestamp in seconds, such as 1580000000.
              ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000000.
          });
        };
        xhr.send();
    }
});

// The COS instance can then be used to call a COS request.

</script>
```

### Configuration items

#### Samples

Create a COS SDK instance in the following ways:

- Option 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

[//]: # ".cssg-snippet-global-init-sts"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously.
        // For server-side samples for JavaScript and PHP, visit https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/.
        // For server-side samples for other programming languages, see the COS STS SDK at https://github.com/tencentyun/qcloud-cos-sts-sdk.
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048.

        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
                var credentials = data.credentials;
            } catch (e) {
            }
            if (!data || !credentials) {
              return console.error('credentials invalid:\n' + JSON.stringify(data, null, 2))
            };
            callback({
              TmpSecretId: credentials.tmpSecretId,
              TmpSecretKey: credentials.tmpSecretKey,
              SecurityToken: credentials.sessionToken,
              // We recommend you use the server time as the signature start time, so as to avoid signature errors due to time deviations.
              StartTime: data.startTime, // Timestamp in seconds, such as 1580000000.
              ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000000.
          });
        };
        xhr.send();
    }
});
```

- Option 2 (recommended): Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through `Scope`.

[//]: # ".cssg-snippet-global-init-sts-scope"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Server-side sample: https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/scope.md
        // Get a temporary key asynchronously.
        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL
        var xhr = new XMLHttpRequest();
        xhr.open('POST', url, true);
        xhr.setRequestHeader('Content-Type', 'application/json');
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
                var credentials = data.credentials;
            } catch (e) {
            }
            if (!data || !credentials) {
                return console.error('credentials invalid:\n' + JSON.stringify(data, null, 2))
            };
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                SecurityToken: credentials.sessionToken,
                // We recommend you use the server time as the signature start time, so as to avoid signature errors due to time deviations.
                StartTime: data.startTime, // Timestamp in seconds, such as 1580000000.
                ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000000.
                ScopeLimit: true, // For refined permission control, you need to set this parameter to `true`, so that the key can be reused only for the same request.
            });
        };
        xhr.send(JSON.stringify(options.Scope));
    }
});
```

- Option 3 (not recommended): The frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This option makes it difficult to control permissions for multipart upload and thus is not recommended.

[//]: # ".cssg-snippet-global-init-signature"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Get a signature asynchronously

        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL
        var method = (options.Method || 'get').toLowerCase();
        var query = options.Query || {};
        var headers = options.Headers || {};
        var pathname = options.Pathname || '/';
        var xhr = new XMLHttpRequest();
        var data = {
            method: method,
            pathname: pathname,
            query: query,
            headers: headers,
        };
        xhr.open('POST', url, true);
        xhr.setRequestHeader('content-type', 'application/json');
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
            } catch (e) {
            }
            if (!data || !data.authorization) return console.error('authorization invalid');
            callback({
                Authorization: data.authorization,
                // SecurityToken: data.sessionToken, // If a temporary key is used, `sessionToken` needs to be passed to `SecurityToken`.
            });
        };
        xhr.send(JSON.stringify(data));
    },
});
```

- Option 4 (not recommended): The frontend uses a permanent key to calculate the signature. This option can be used for frontend debugging. If you use this option, be sure to avoid key disclosure.

[//]: # ".cssg-snippet-global-init"
```js
var COS = require('cos-js-sdk-v5');

// Log in at https://console.cloud.tencent.com/cam/capi to view and manage the `SECRETID` and `SECRETKEY`.
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
});
```

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | Your `SecretId`. | String | No |
| SecretKey | Your `SecretKey`. We recommend you only use it for frontend debugging and avoid disclosing it. | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3. | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3. | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload/copy failure. Default value: `2` (a request will be made three times in total, including the initial one). | Number | No |
| ChunkSize | Part size in the multipart upload in bytes. Default value: `1048576` (1 MB). | Number | No |
| SliceSize | When files are uploaded in batches through `uploadFiles`, if the file size in bytes is greater than the value of this parameter, multipart upload will be used; otherwise, simple upload will be used. Default value: `1048576` (1 MB). | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: `20`. | Number | No |
| CopyChunkSize  | Number of bytes in each part during a multipart copy operation through `sliceCopyFile`. Default value: `10485760` (10 MB). | Number | No |
| CopySliceSize | When a file is copied through `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy will be used; otherwise, simple copy will be used. Default value: `10485760` (10 MB). | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: `1000`. | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` will be used when the current page is determined to be in `http:`; otherwise, `https:` will be used. | String | No |
| Domain | The custom request domain name used to call an API to manipulate a bucket or object. A template can be used, such as `"{Bucket}.cos.{Region}.myqcloud.com"`, which will use the bucket and region passed in the parameters for replacement when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess jobs will be cleared if their status is not `waiting`, `checking`, or `uploading`. Default value: `10000`. | Number | No |
| ForcePathStyle | Whether to forcibly use a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: `false`. | Boolean | No |
| UploadCheckContentMd5  | Whether to verify `Content-MD5` during file upload, which is `false` by default. If it is enabled, the MD5 checksum of the uploaded file will be calculated, which may be time-consuming for large files. | Boolean | No |
| getAuthorization | The callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter will be required. <br>**Note: This callback method is passed in during instance initialization and is only executed to obtain the signature when the instance calls APIs.** | Function | No |
| Timeout | Timeout period in milliseconds. Default value: `0`, indicating no timeout period. | Number | No |
| UseAccelerate          | Whether to enable a global acceleration endpoint. Default value: `false`. If you set the value to `true`, you need to enable global acceleration for the bucket. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406). | Boolean | No   |

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
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. | String | Yes |
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
| - Method | The method of the current request | String   |
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
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header. | String | No |

#### Getting authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the `getAuthorization` callback function. Each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the `getAuthorization` callback. When the callback is called, a temporary key will be returned. After the key expires, the callback will be called again.

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

Below are some common API samples. For more detailed initialization methods, see the demo at [GitHub](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading object

The simple upload API is suitable for uploading small files. For large files, use the multipart upload API. For more information, see [Object Operations](https://www.tencentcloud.com/document/product/436/43552).

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Key: 'exampleobject',              /* Object key (required) */
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the file object
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
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Prefix: 'a/',           /* Prefix (optional) */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading object

> !This API is used to read object content. To download a file through a browser, you should first get a download URL through the `cos.getObjectUrl` method. For more information, see [Generating Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31540).

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Key: 'exampleobject',              /* Object key (required) */
}, function(err, data) {
    console.log(err || data.Body);
});
```

### Deleting object

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Bucket (required) */
    Region: 'COS_REGION',     /* Bucket region (required) */
    Key: 'exampleobject'        /* Object key (required) */
}, function(err, data) {
    console.log(err || data);
});
```
