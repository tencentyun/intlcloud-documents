## Download and Installation

### Relevant Resources

- The COS XML SDK for JavaScript source code can be downloaded [here](https://github.com/tencentyun/cos-js-sdk-v5).
- The sample demo can be download [here](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).

### Preparing the Environment

1. The SDK for JavaScript requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file uploading and file MD5 checksum calculation.
2. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM Console](https://console.cloud.tencent.com/capi) and get your project's SecretId and SecretKey.
4. Configure a CORS rule. AllowHeader should be configured as `*`. ExposeHeaders requires ETag, Content-Length, and other header fields that JS needs to read as shown below. For more information, see [Setting Up Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
![CORS example](https://main.qcloudimg.com/raw/bdb4f616f2afe4ca18ba663446873fd4.png)

> For more information on the meanings of parameters such as SecretId, SecretKey, and Bucket contained herein and how to get them, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).

### Installing the SDK
You can install the SDK in the following ways:

#### Importing via script

```html
<script src="./cos-auth.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name COS, and its constructor can create an SDK instance.

#### Importing via webpack

Install the SDK dependencies by running `npm i cos-js-sdk-v5 --save`, which supports webpack packaging scenarios. You can use import NPM as a module with the following code:
```js
var COS = require('cos-js-sdk-v5');
```

## Getting Started

### Getting a Temporary Key

If the key is placed on the frontend, the SecretId and SecretKey will be exposed; therefore, we put the permanent key on the backend, and the frontend gets a temporary key from the backend through AJAX. In actual deployment, please add an additional authentication step of your website on the backend. For more information, see [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048).


### Initialization

1. Create a web.html file, enter the following code, and modify the bucket name and region in web.html.
2. Deploy the temporary key service on the backend and modify the key service address in getAuthorization.
3. Place the web.html file on the web server, visit the page in a browser, and test file uploading. The sample code for web.html is as follows:

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

#### Use Cases

Create a COS SDK instance in the following methods:
- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server examples for JS and PHP: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server examples for other programming languages, see the [COS SDK for STS](https://github.com/tencentyun/qcloud-cos-sts-sdk)
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
- Method 2 (recommended): The permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can finely manage the permissions through Scope.
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // Server example: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
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
                    XCosSecurityToken: credentials.sessionToken, // The provided sessionToken needs to be passed to 
                    ExpiredTime: data.expiredTime,
                    ScopeLimit: true, // Refined permission control needs to be set to true, limiting that the key can be reused only for the same request
                });
            }
        });
    }
});
```
- Method 3 (not recommended): The frontend needs to get a signature through getAuthorization before each request, and the backend uses a fixed or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control the permission of multipart upload and thus is not recommended.
```js
var cos = new COS({
    // Required parameters
    getAuthorization: function (options, callback) {
        // The server obtains a signature. For more information, see the COS SDK for the corresponding programming language: https://cloud.tencent.com/document/product/436/6474
        // Note: There may be a security risk. The backend needs to strictly control the permissions through method and pathname, such as prohibiting put /
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
    FileParallelLimit: 3,    // Control the number of concurrent file uploads
    ChunkParallelLimit: 3,   // Control the number of concurrent part uploads for a single file
    ProgressInterval: 1000,  // Control the interval of upload onProgress callbacks
});
```
- Method 4 (not recommended): The frontend uses a fixed key to calculate a signature. This method is suitable for frontend debugging. If you use this method, be sure to avoid key disclosure.
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
| SecretKey | User SecretKey, which is recommended to be used only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance; default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file; default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries upon multipart upload failure; default value: 3 (a request will be made 4 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes; default value: 1,048,576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using uploadFiles, if the file size is over the value of this parameter, multipart upload (sliceUploadFile) will be used; otherwise, simple upload (putObject) will be used | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same uploaded file; default value: 3 | Number | No |
| CopyChunkSize | Number of retries upon multipart upload failure; default value: 3 (a request will be made 4 times in total, including the initial one) | Number | No |
| CopySliceSize | Part size in the multipart upload in bytes; default value: 1,048,576 (1 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method onProgress in milliseconds; default value: 1,000 | Number | No |
| Protocol | The protocol used when the request is made; value range: `https:`, `http:`. By default, `http:` will be used when the current page is determined to be in `http:`; otherwise, `https:` will be used | String | No |
| ServiceDomain | The request domain name when the getService method is called, such as `cos.ap-beijing.myqcloud.com` | String | No |
| Domain | The request domain name of the Bucket call, where a template can be used, such as `"{Bucket}.cos.{Region}.myqcloud.com" `| String | No |
| UploadQueueSize | The maximum size of the upload queue. Excessive tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10,000 | Number | No |
| ForcePathStyle | Forces the use of a suffix to send requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies the Content-MD5 of the uploaded file, which is false by default. If enabled, the MD5 value will be calculated for the file content when the file is uploaded, which may be time-consuming for large files | Boolean | No |
| GetAuthorization | The callback method for getting the signature. If there is no SecretId or SecretKey, this parameter is mandatory | Function | No |

#### getAuthorization Callback Function Descriptions (Using Method 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Parameter object necessary for getting the temporary key | Function |
| - Bucket  | Bucket name in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| - Region | Bucket region. For the enumerated values, see [Bucket Region Information](https://intl.cloud.tencent.com/document/product/436/6224) | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | tmpSecretId of the obtained temporary key | String | Yes |
| TmpSecretKey | tmpSecretKey of the obtained temporary key | String | No |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |
| ExpiredTime | expiredTime of the obtained temporary key, i.e., the timeout period | String | No |

#### getAuthorization Callback Function Descriptions (Using Method 2)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization function callback parameter descriptions

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | -------- | ---- |
| options | Parameter object necessary for getting the signature | Object | No |
| - Method | Method of the current request | Object | No |
| - Pathname | Request path used for signature calculation | String | No |
| - Key | An object key (object name) is a unique ID of an object in the bucket. For more information, see [Object Key Description](https://intl.cloud.tencent.com/document/product/436/13324) | String | No |
| - Query | Query parameter object of the current request in the format of {key: 'val'} | Object | No |
| - Headers | Header parameter object of the current request in the format of {key: 'val'} | Object | No |
| callback | Callback after the temporary key is obtained | Function | No |

After the getAuthorization calculation is completed, the callback returns a signature string or an object:
If a signature string is returned, the string type is the credential field "Authorization" to be used by the authentication header of the request.
If an object is returned, the attributes of the object are as shown below:

| Attribute Name | Parameter Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization | The temporary key obtained | String | Yes |
| XCosSecurityToken | sessionToken of the obtained temporary key, which corresponds to the x-cos-security-token field in the header | String | No |

#### Getting an Authentication Credential

There are three ways to obtain an authentication credential for the instance:

1. During instantiation, pass in the SecretId and SecretKey, and each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback, and each time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getAuthorization callback. When this callback is called, a temporary key will be returned, and after the key expires, the callback will be called again.

Below are some examples of commonly used APIs. For more detailed initialization methods, see the examples in the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Uploading an Object

The simple upload API is suitable for uploading small files. For large files, use the multipart upload API. For more information, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31538).
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

### Querying Object List

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

>  This API is used to read the object content. If you need to launch a browser to download the file, you can get the URL through cos.getObjectUrl and then start a download in the browser. For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31540).

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
