## Download and Installation

#### Relevant Resources

- Source code of COS XML JS SDK: [XML JS SDK](https://github.com/tencentyun/cos-js-sdk-v5).
- Demo: [JS Sample](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).

### Environment Requirements

1. JavaScript SDK requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file upload and MD5 checksum calculation.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get the SecretId and SecretKey of your project.
4. Configure the CORS rule. Put in `*` for AllowHeader. For ExposeHeaders, put in ETag, Content-Length, and other JS-required header fields. For more information, see [Setting Cross-Origin Access](https://cloud.tencent.com/document/product/436/13318).
   ![CORS example](https://main.qcloudimg.com/raw/925cef63c1a4a5e849f464984e0446e7.png)

> For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).

#### Installing the SDK

You can install the SDK in the following ways:

#### Importing via script

```html
<script src="./cos-js-sdk-v5.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name COS, and its constructor can create an SDK instance.

#### Importing via webpack

Installing the SDK dependencies by running `npm i cos-js-sdk-v5 --save` supports webpack packaging scenarios. You can use NPM import as a module with the following code:

```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

### Getting a Temporary Key

Using a fixed key on the frontend exposes your SecretId and SecretKey. Therefore, we store the permanent key on the backend, and the frontend uses a temporary key generated from the backend through AJAX. In actual deployment, please add an additional authentication step on the backend. For more information, see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048).

### Initialization

1. Create a web.html file, enter the following code, and modify the bucket name and region in web.html.
2. Deploy the temporary key service on the backend and modify the key service address in getAuthorization.
3. Place the web.html file on the web server, visit the page in a browser, and test file upload. The sample code for web.html is as follows:

```html
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'examplebucket-1250000000';
var Region = 'COS_REGION';      /* Bucket region. Required */

// Initialize the instance.
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously
        $.get('http://example.com/server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            var credentials = data.credentials;
            callback({
                 TmpSecretId: credentials.tmpSecretId,
                 TmpSecretKey: credentials.tmpSecretKey,
                 XCosSecurityToken: credentials.sessionToken,
                 // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                 StartTime: data.startTime, // Displayed in seconds
                 ExpiredTime: data.expiredTime
            });
        });
    }
});

// The COS instance can then be used to call a COS request
// TODO

</script>
```

### Configuration Items

#### Usage Examples

Create a COS SDK instance in one of the following ways:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

[//]: # (.cssg-snippet-global-init-sts)
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side JS and PHP sample: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048
        $.get('http://example.com/server/sts.php', {
            // The required parameters can be obtained from options
        }, function (data) {
            callback({
                TmpSecretId: data.TmpSecretId,
                TmpSecretKey: data.TmpSecretKey,
                XCosSecurityToken: data.XCosSecurityToken,
                // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                StartTime: data.startTime, // Displayed in seconds
                ExpiredTime: data.ExpiredTime, // The SDK will not call getAuthorization again before the ExpiredTime time
            });
        });
    }
});
```

- Method 2 (recommended): The permissions are controlled in a fine-grained manner. The backend gets a temporary key and sends it to the frontend. The frontend only reuses the key for the same request, and the backend can manage the permissions in a fine-grained manner through Scope.

[//]: # (.cssg-snippet-global-init-sts-scope)
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side sample: https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/scope.md
        $.ajax({
            method: 'POST',
            url: ' http://example.com/server/sts-scope.php',
            data: JSON.stringify(options.Scope),
            beforeSend: function () {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                    StartTime: data.startTime, // Displayed in seconds
                    ExpiredTime: data.expiredTime,
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting that the key can be reused only for the same request
                });
            }
        });
    }
});
```

- Method 3 (not recommended): The frontend needs to get a signature through getAuthorization before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This method will make it difficult for you to control the permission of multipart upload and thus is not recommended.

[//]: # (.cssg-snippet-global-init-signature)
```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: This method involves security risks. The backend needs to strictly control the permissions through method and pathname, such as prohibiting `PUT` /
        $.get('http://example.com/server/auth.php', {
            method: options.Method,
            pathname: '/' + options.Key,
        }, function (data) {
            callback({
                Authorization: data.authorization,
                // XCosSecurityToken: data.sessionToken, // If a temporary key is used, sessionToken needs to be passed to XCosSecurityToken
            });
        });
    },
    // Optional parameters
    FileParallelLimit: 3,    // Limit the number of concurrent file uploads
    ChunkParallelLimit: 3,   // Limit the number of concurrent part uploads when using multipart upload for a single file
    ProgressInterval: 1000,  // Limit the interval of upload onProgress callbacks
});
```

- Method 4 (not recommended): The frontend uses a fixed key to calculate the signature. This method can be used for frontend debugging. If you use this method, be sure to avoid key disclosure.

[//]: # (.cssg-snippet-global-init)
```js
var cos = new COS({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
});
```

#### Parameters of the constructor

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User SecretKey, which is recommended to be used only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure. Default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload; unit: byte. Default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When using uploadFiles for batch upload, if the file size is greater than this value, multipart upload will be used, otherwise simple upload will be called, unit is byte, the default value is 1048576 (1MB) | Number | No |
| CopyChunkParallelLimit | When performing the multipart copy operation, number of concurrent multipart copy uploads. The default value is 20 | Number | No |
| CopyChunkSize | When using sliceCopyFile to copy files in multipart, the byte size of each part, the default value is 10485760 (10MB) | Number | No |
| CopySliceSize | When copying a file using sliceCopyFile, if the file size is greater than this value, multipart copy will be used; otherwise simple copy will be called. The default value is 10485760(10MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress`; unit: millisecond. Default value: 1,000 | Number | No |
| Protocol | The protocol used to make a request; valid values: `https:`, `http:`. By default, `http:` will be used when the current page is using `http:`; otherwise, `https:` will be used | String | No |
| Domain | Custom request domain names when calling buckets and objects APIs. You can use templates, <br>such as`" {Bucket} .cos. {Region}.myqcloud.com"`, that is, when calling the API, the bucket and region passed in the parameters will be used | String | No |
| UploadQueueSize | The maximum size of the upload queue. Tasks out of the maximum length will be cleared if their status is not waiting, checking, or uploading. Default value: 10,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix to send requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies Content-MD5 when uploading files, which is false by default. If it is enabled, the MD5 value of the uploading files will be calculated, which may be time-consuming for large files | Boolean | No |
| GetAuthorization | The callback method used to get the signature. If there is no SecretId or SecretKey, this parameter is required | Function | No |
| Timeout | Timeout, unit in milliseconds. Default value is 0, that is, no timeout is set | Number | No |

#### getAuthorization Callback Function Descriptions (Using Method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the temporary key | Function |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| callback | Callback method after the temporary key is obtained | Function |

Callback passes back an object after the temporary key is acquired. Here is a list of the attributes of this object:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | tmpSecretId of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
| ExpiredTime | expiredTime of the obtained temporary key, i.e., the timeout period | String | Yes |

#### getAuthorization Callback Function (Using Method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions:

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object |
| - Method | Method of the current request | Object | 
| - Pathname | Request path used for signature calculation | String | 
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | 
| - Query | Query parameter object of the current request in the format of {key: 'val'} | Object | 
| - Headers | Header parameter object of the current request in the format of {key: 'val'} | Object | 
| callback | Callback after the temporary key is obtained | Function | 

After the calculation of getAuthorization is completed, callback parameter supports two formats:
Format 1: Returns the authentication string Authorization.
Format 2: Returns an object. The object attribute list is as follows:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | Calculated signature string                                         | String | Yes   |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |

#### Acquiring authentication credentials

You can obtain the authentication credentials for your instance in three ways by passing in different parameters during instantiation:

1. During instantiation, pass in the SecretId and SecretKey, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback. Every time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getAuthorization callback. When the callback is called, a temporary key will be returned. After the key expires, the callback will be called again.

Below are some examples of common APIs. For more detailed initialization methods, please see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading an object

This API is suitable for uploading small files. For large files, please use the multipart upload API. For more information, see [Actions on Objects](https://intl.cloud.tencent.com/document/product/436/30596).

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload file object
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### Querying Object List

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/',           /* Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Download an Object

> This API is used to read the object content. If you need to launch a browser to download the file, you can get the URL through cos.getObjectUrl and then start a download in the browser. For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/30598).

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

### Delete an object

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```
