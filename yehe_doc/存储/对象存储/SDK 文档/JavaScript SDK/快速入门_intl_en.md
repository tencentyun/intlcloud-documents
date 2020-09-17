## Download and Installation

#### Related resources

- Source code of COS XML JS SDK download: [XML JavaScript SDK](https://github.com/tencentyun/cos-js-sdk-v5).
- Fast SDK download: [XML JavaScript SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-js-sdk-v5/latest/cos-js-sdk-v5.zip).
- Demo: [JS Sample](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).
- Find all code samples for this SDK [here](https://github.com/tencentyun/cos-snippets/tree/master/JavaScript).

#### Environment requirements

1. The SDK for JavaScript requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file uploading and MD5 checksum calculation.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get the SecretId and SecretKey of your project.
4. Configure the CORS rule. Put in `*` for AllowHeader. For ExposeHeaders, put in ETag, Content-Length, and other JS-required header fields. For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
   ![CORS example](https://main.qcloudimg.com/raw/925cef63c1a4a5e849f464984e0446e7.png)

>For the definitions of parameters such as `SecretId`, `SecretKey`, and `Bucket`, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

#### Installing SDK

You can install the SDK in the following ways:

#### Importing via script

```html
<script src="./cos-js-sdk-v5.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name COS, and its constructor can create an SDK instance.

#### Importing via webpack

Install the SDK dependencies by running `npm i cos-js-sdk-v5 --save`, which supports webpack packaging scenarios. You can use npm import as a module with the following code:

```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

## Getting a Temporary Key

As exposing your permanent key to the front end poses security risks, we recommend using temporary keys instead in the real environment. To do so, the front end first requests a temporary key from the server. The server then obtains the temporary key by calling the STS service using the permanent key (For more information, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048), and returns it to the front end for use.

>!If your site has a login status, you should add login status verification to your API for generating temporary keys. 

### Initialization

1. Create a web.html file, enter the following code, and modify the bucket name and region in web.html.
2. Deploy the temporary key service on the backend and modify the key service address in getAuthorization.
3. Place the `web.html` file on the web server, please visit the page in a browser, and test file uploading. The sample code for `web.html` is as follows:

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

// Next you can use a COS instance to call a COS request
// TODO

</script>
```

### Configuration

#### Samples

Create a COS SDK instance in one of the following ways:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

[//]: # ".cssg-snippet-global-init-sts"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side JS and PHP sample: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048
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
            beforeSend: function (xhr) {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    // We recommend using the time the server receives the credentials as the StartTime, so as to avoid signature error due to time deviations. 
                    StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                    ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000900
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting that the key can be reused only for the same request
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
    FileParallelLimit: 3,    // Limit the number of concurrent file uploads
    ChunkParallelLimit: 3,   // Limit the number of concurrent part uploads when using multipart upload for a single file
    ProgressInterval: 1000,  // Limit the interval of upload onProgress callbacks
});
```

- Method 4 (not recommended): The frontend uses a fixed key to calculate the signature. This method can be used for frontend debugging, but be sure to avoid key disclosure.

[//]: # ".cssg-snippet-global-init"
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
| CopySliceSize | When a file is copied by using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency in milliseconds for the upload progress callback method onProgress; default value: 1,000 | Number | No |
| Protocol | The protocol used to make a request; valid values: `https:`, `http:`. By default, `http:` will be used when the current page is using `http:`; otherwise, `https:` will be used | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template, such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Tasks out of the maximum length will be cleared if their status is not waiting, checking, or uploading. Default value: 10,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix to send requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies Content-MD5 when uploading files, which is false by default. If it is enabled, the MD5 value of the uploading files will be calculated, which may be time-consuming for large files | Boolean | No |
| GetAuthorization | The callback method for getting the signature. If there is no SecretId or SecretKey, this parameter is required | Function | No |
| Timeout | Timeout, unit in milliseconds. Default value is 0, that is, no timeout is set | Number | No |

#### getAuthorization Callback Function Descriptions (Using Method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object | No |
| - Bucket  | Bucket name in the format `BucketName-APPID`. The bucket name entered here must be in this format | String |
| Region | Bucket region. For the enumerated values, see [bucket regions](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| callback | Callback method after the temporary key is obtained | Function |

Callback passes back an object after the temporary key is acquired. Here is a list of the attributes of this object:

| Attribute Name| Description | Type  |Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
| StartTime | Key acquisition start time measured in seconds, i.e., the timestamp of the key acquisition time, such as 1580000000. This parameter is used as the signature start time. Passing in this parameter can avoid signature expiration issues due to time deviation on the frontend |
| ExpiredTime | `expiredTime` of the obtained temporary key measured in seconds, i.e., the timeout timestamp, such as 1580000900 | String | Yes |

#### getAuthorization Callback Function (Using Method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions:

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the signature | Object | No |
| - Method | Current request method | String |
| - Pathname | Request path used for signature calculation | String |
| - Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| - Query | Query parameter object of the current request in the format of {key: 'val'} | Object |
| - Headers | Header parameter object of the current request in the format of {key: 'val'} | Object |
| callback | Callback after the temporary key is obtained | Function |

After the calculation of getAuthorization is completed, callback parameter supports two formats:
Format 1: Returns the authentication string Authorization.
Format 2: Returns an object. The object attribute list is as follows:

| Attribute Name| Description | Type  |Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | Calculated signature string | String | Yes |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |

#### Acquiring authentication credentials

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in the SecretId and SecretKey. Every time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback. Every time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getAuthorization callback. When the callback is called, a temporary key will be returned. After the key expires, the callback will be called again.

Below are some examples of common APIs. For more detailed initialization methods, please see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading an object

This API is suitable for uploading small files. For large files, please use the multipart upload API. For more information, see [Actions on Objects](https://intl.cloud.tencent.com/document/product/436/31538).

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
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

### Querying object list

[//]: # ".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/', /*Optional*/
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an object

> This API is used to read the object content. If you need to launch a browser to download the file, you can get the URL through cos.getObjectUrl and then start a download in the browser. For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31540).

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /*Required*/
}, function(err, data) {
    console.log(err || data.Body);
});
```

### Deleting an object

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject' /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```
