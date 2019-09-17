## Download and Installation

### Relevant Resources

- COS XML JS SDK source code: [Download here](https://github.com/tencentyun/cos-js-sdk-v5).
- Demo: [Download here](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).

### Preparing the Environment

1. JavaScript SDK requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file upload and MD5 checksum calculation.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), [create a bucket](https://cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get the SecretId and SecretKey of your project.
4. Configure CORS rule. Put in `*` for AllowHeader. For ExposeHeaders, put in ETag, Content-Length, and other header fields JS needs to read as shown below. For more information, see [Setting Cross-Origin Resource Sharing](https://cloud.tencent.com/document/product/436/13318).
![CORS example](https://main.qcloudimg.com/raw/bdb4f616f2afe4ca18ba663446873fd4.png)

>For the definitions of SecretId, SecretKey, Bucket and other terms, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).

### Installing the SDK
You can install the SDK in the following ways:

#### Importing via script

```html
<script src="./cos-auth.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name COS, and its constructor can create an SDK instance.

#### Importing via webpack

Installing the SDK dependencies by running `npm i cos-js-sdk-v5 --save` supports webpack packaging scenarios. You can use NPM import as a module with the following code:
```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

### Getting a Temporary Key

If the key is placed on the frontend, the SecretId and SecretKey will be exposed; therefore, we put the permanent key on the backend, and the frontend gets a temporary key from the backend through AJAX. In actual deployment, please add an additional authentication step of your website on the backend. For more information, see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048).


### Initialization

1. Create a web.html file, enter the following code, and modify the bucket name and region in web.html.
2. Deploy the temporary key service on the backend and modify the key service address in getAuthorization.
3. Place the web.html file on the web server, visit the page in a browser, and test file upload. The sample code for web.html is as follows:

```
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'examplebucket-1250000000';
var Region = 'ap-beijing';

// Initialize an instance
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
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side JS and PHP sample: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For examples of other server-side programming languages, see COS STS SDK: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://cloud.tencent.com/document/product/436/14048
        $.get('http://example.com/server/sts.php', {
            // The required parameters can be obtained from options
        }, function (data) {
            callback({
                TmpSecretId: data.TmpSecretId,
                TmpSecretKey: data.TmpSecretKey,
                XCosSecurityToken: data.XCosSecurityToken,
                ExpiredTime: data.ExpiredTime, // The SDK will not call getAuthorization again before the ExpiredTime time
            });
        });
    }
});
```
- Method 2 (recommended): The permissions are controlled in a fine-grained manner. The backend gets a temporary key and sends it to the frontend. The frontend only reuses the key for the same request, and the backend can manage the permissions in a fine-grained manner through Scope.
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server-side sample: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
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
                    XCosSecurityToken: credentials.sessionToken, // sessionToken needs to be passed to XCosSecurityToken 
                    ExpiredTime: data.expiredTime,
                    ScopeLimit: true, // You need to set the fine-grained permission control to true to make sure that the key will only be reused for the same request
                });
            }
        });
    }
});
```
- Method 3 (not recommended): The frontend needs to get a signature through getAuthorization before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This method will make it difficult for you to control the permission of multipart upload and thus is not recommended.
```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: There is a security risk. The backend needs to strictly control the permissions through method and pathname, such as prohibiting put /
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
- Method 4 (not recommended): The frontend uses a fixed key to calculate the signature. This method can be used for frontend debugging, but be sure to avoid key disclosure.
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
| FileParallelLimit | Number of concurrent file uploads in the same instance; default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for a single file; default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure; default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No|
| ChunkSize | The size of each part in bytes for multipart upload; default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is over the value of this parameter, multipart upload (sliceUploadFile) will be used; otherwise, simple upload (putObject) will be used | Number | No |
| CopyChunkParallelLimit | Number of concurrent part copy uploads for multipart replication; default value: 20 | Number | No |
| CopyChunkSize | The size of each part in bytes for multipart replication (sliceCopyFile); default value: 10,485,760 (10 MB) | Number | No |
| CopySliceSize | For file replication, if the file size is over the value of this parameter, multipart replication (sliceCopyFile) will be used; otherwise, simple replication (putObjectCopy) will be used | Number | No |
| ProgressInterval | Callback frequency in milliseconds for the upload progress callback method onProgress; default value: 1,000 | Number | No |
| Protocol | The protocol used to make a request; valid values: `https:`, `http:`. By default, `http:` will be used when the current page is using `http:`; otherwise, `https:` will be used | String | No |
| ServiceDomain | The request domain name when the getService method is called, such as `cos.ap-beijing.myqcloud.com` | String | No |
| Domain | The request domain name of the Bucket call. You can use a template, such as `"{Bucket}.cos.{Region}.myqcloud.com" `| String | No |
| UploadQueueSize | The maximum size of the upload queue. Tasks out of the maximum length will be cleared if their status is not waiting, checking, or uploading. Default value: 10,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies Content-MD5 when uploading files, which is false by default. If it is enabled, the MD5 value of the uploading files will be calculated, which may be time-consuming for large files | Boolean | No |
| GetAuthorization | The callback method for getting the signature. If there is no SecretId or SecretKey, this parameter is required | Function | No |

#### getAuthorization Callback Function (Using Method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization Callback Parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting temporary keys | Function |
| - Bucket  | Bucket name in the format of BucketName-APPID | String |
| - Region | The region where the bucket resides. For the enumerators, see [Bucket Region Information](https://cloud.tencent.com/document/product/436/6224) | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | tmpSecretId of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | The sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |
| ExpiredTime | expiredTime of the obtained temporary key, i.e., the timeout period | String | No |

#### getAuthorization Callback Function (Using Method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization Callback Parameters

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | -------- | ---- |
| options | Parameter object necessary for getting the signature | Object | No |
| - Method | Method of the current request | Object | No |
| - Pathname | Request path used for signature calculation | String | No |
| - Key | An object key (object name) is a unique ID for an object in a bucket. For more information, see [Object Key Description](https://cloud.tencent.com/document/product/436/13324) | String | No |
| - Query | Query parameter object of the current request in the format of {key: 'val'} | Object | No |
| - Headers | Header parameter object of the current request in the format of {key: 'val'} | Object | No |
| callback | Callback after the temporary key is obtained | Function | No |

After the getAuthorization calculation is completed, the callback returns a signature string or an object:
If a signature string is returned, the string is the credential field "Authorization" in the authentication header to be used by the request.
If an object is returned, the attributes of the object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | The authorization calculated with a permanent or temporary key | String | Yes |
| XCosSecurityToken | The sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |

#### Getting an Authentication Credential

There are three ways to obtain an authentication credential for the instance:

1. During instantiation, pass in the SecretId and SecretKey. Every time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback. Every time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getAuthorization callback. When the callback is called, a temporary key will be returned. After the key expires, the callback will be called again.

Below are some examples of common APIs. For more detailed initialization methods, see the examples in the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading an Object

The simple upload API can be used to upload small files. For large files, use the multipart upload API. For more information, see [Object Operations](https://cloud.tencent.com/document/product/436/35649).
```js
document.getElementById('file-selector').onchange = function () {
    var file = this.files[0];
    if (!file) return;
    cos.putObject({
        Bucket: 'examplebucket-1250000000',
        Region: 'ap-beijing',
        Key: 'destination path/' + file.name,
    }, function (err, data) {
        console.log(err || data);
    });
});
```

### Querying the Object List

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/', // Pass in the prefix of files to be listed here
}, function (err, data) {
    console.log(err || data.Contents);
});
```

### Downloading an Object

> ! This API is used to read the object content. If you need to launch a browser to download the file, you can get the URL through cos.getObjectUrl and then start a download in the browser. For more information, see [Pre-signed URL](https://cloud.tencent.com/document/product/436/35651).

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
