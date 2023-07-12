## Download and Installation

#### Relevant resources

- Source code of COS XML JS SDK download: [XML JavaScript SDK](https://github.com/tencentyun/cos-js-sdk-v5).
- SDK download: [XML JavaScript SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-js-sdk-v5/latest/cos-js-sdk-v5.zip).
- Demo download: [JS Sample](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).
- For the complete sample code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/JavaScript).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [JavaScript SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40775).


>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>

#### Environment requirements

1. The SDK for JavaScript requires the browser to support basic HTML5 features (IE 10 and higher) for AJAX file uploading and MD5 checksum calculation.
2. Log in to the [COS console](https://console.cloud.tencent.com/cos5), [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309), and get the bucket name and [region name](https://intl.cloud.tencent.com/document/product/436/6224).
3. Log in to the [CAM console](https://console.cloud.tencent.com/capi) and get the SecretId and SecretKey of your project.
4. Configure CORS rule. Put in `*` for `AllowHeader`. For `ExposeHeaders`, put in `ETag`, `Content-Length`, and the other header fields that JS needs to read as shown below. For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)

>? 
> - For the definition of parameters such as `SecretId`, `SecretKey`, and `Bucket`, see COS’s [Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
> - If you are using cross platform framework such as uni-app, and encounter problems when packaging the app (such as iOS or Android app), use the iOS SDK or Android SDK.
> 

#### Installing SDK

You can install the SDK in the following ways:

#### Importing via script
>? We recommend you download the SDK to local and then import it. You can download the latest SDK file "cos-js-sdk-v5.min.js" at [URL 1](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/dist/cos-js-sdk-v5.min.js) or [URL 2](https://cdn.jsdelivr.net/npm/cos-js-sdk-v5/dist/cos-js-sdk-v5.min.js).
>
```html
<!--src is a local path. Set it based on the directory structure of your project.-->
<script src="../dist/cos-js-sdk-v5.min.js"></script>
```

When the script tag references the SDK, the SDK occupies the global variable name COS, and its constructor can create an SDK instance.

#### Importing via webpack

Install the SDK dependencies by running `npm i cos-js-sdk-v5 --save`, which supports webpack packaging scenarios. You can use npm import as a module with the following code:

```js
var COS = require('cos-js-sdk-v5');

// or

import COS from 'cos-js-sdk-v5';
```

## Getting Started

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


### Getting a temporary key

As placing a permanent key on the frontend may cause security risks, we recommend you use temporary keys during formal deployment. The implementation process is as follows: the frontend first requests the server, and then the server uses the permanent key to call the STS service to apply for a temporary key (for more information, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048)) and returns it to the frontend.

>!If the site has a login state, login state verification should be added to the temporary key getting API.

### Initialization

1. Create a web.html file, enter the following code, and modify the bucket name and region in web.html.
2. Deploy the temporary key service on the backend and modify the key service address in getAuthorization.
3. Place the `web.html` file on the web server, visit the page in a browser, and test file uploading. The sample code for `web.html` is as follows:

```html
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>

// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
var Bucket = 'examplebucket-1250000000';  /* Bucket. Required */

// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. 
// The region details can be viewed at https://intl.cloud.tencent.com/document/product/436/6224.
var Region = 'COS_REGION';      /* Bucket region. Required */

// Initialize an instance.
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // It will not be called during initialization and will be entered only when a COS method such as `cos.putObject` is called.
        // Get a temporary key asynchronously.
        // Server-side JS and PHP sample: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048

        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL.
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
              // We recommend that you use the server time as the signature start time to avoid signature errors caused by time deviations.
              StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
              ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000000
          });
        };
        xhr.send();
    }
});

// The COS instance can then be used to call a COS request.

</script>
```

### Configuration item

#### Sample code

Create a COS SDK instance in one of the following ways:

- Method 1 (recommended): The backend gets a temporary key and sends it to the frontend for signature calculation.

[//]: # ".cssg-snippet-global-init-sts"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Get a temporary key asynchronously.
        // Server-side JS and PHP sample: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // For server-side examples for other programming languages, see the COS SDK for STS: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // For the STS documentation, visit https://intl.cloud.tencent.com/document/product/436/14048

        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL.
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
              // We recommend that you use the server time as the signature start time to avoid signature errors caused by time deviations.
              StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
              ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000000
          });
        };
        xhr.send();
    }
});
```

- Method 2 (recommended). Permissions are controlled in a more refined manner. The backend gets a temporary key and sends it to the frontend. The frontend reuses the key only for the same request, and the backend can granularly manage permissions through Scope.

[//]: # ".cssg-snippet-global-init-sts-scope"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Server example: https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/scope.md
        // Get a temporary key asynchronously.
        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL.
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
                // We recommend that you use the server time as the signature start time to avoid signature errors caused by time deviations.
                StartTime: data.startTime, // Timestamp in seconds, such as 1580000000
                ExpiredTime: data.expiredTime, // Timestamp in seconds, such as 1580000000
                ScopeLimit: true, // Refined permission control needs to be set to true, limiting the key to be reused only for the same request
            });
        };
        xhr.send(JSON.stringify(options.Scope));
    }
});
```

- Method 3 (not recommended): The frontend needs to get a signature through `getAuthorization` before each request, and the backend uses a permanent or temporary key to calculate the signature and returns it to the frontend. This method makes it difficult to control permissions for multipart upload and thus is not recommended.

[//]: # ".cssg-snippet-global-init-signature"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // The `getAuthorization` parameter is required.
    getAuthorization: function (options, callback) {
        // Obtain the signature asynchronously.

        var url = 'http://example.com/server/sts.php'; // Replace the URL with your own real server URL.
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
                // SecurityToken: data.sessionToken, // If a temporary key is used, sessionToken needs to be passed to SecurityToken.
            });
        };
        xhr.send(JSON.stringify(data));
    },
});
```

- Method 4 (not recommended): The frontend uses a permanent key to calculate the signature. This method can be used for frontend debugging. If you use this method, be sure to avoid key disclosure.

[//]: # ".cssg-snippet-global-init"
```js
var COS = require('cos-js-sdk-v5');

// Log in to https://console.cloud.tencent.com/cam/capi to check and manage the SecretId and SecretKey of your project.
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
});
```

#### Constructor parameters

| Parameter | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User's `SecretKey`, which we recommend to be used only for frontend debugging and should not be disclosed | String | No |
| FileParallelLimit | Number of concurrent file uploads in the same instance. Default value: 3 | Number | No |
| ChunkParallelLimit | Number of concurrent part uploads for the same uploaded file. Default value: 3 | Number | No |
| ChunkRetryTimes | Number of retries for multipart upload failure. Default value: 2 (a request will be made 3 time in total, including the initial one) | Number | No|
| ChunkSize | Part size in the multipart upload in bytes. Default value: 1048576 (1 MB) | Number | No |
| SliceSize | When files are uploaded in batches using `uploadFiles`, if the file size is greater than the value of this parameter (measured in bytes), multipart upload is used; otherwise, simple upload is used. Default value: 1048576 (1 MB) | Number | No |
| CopyChunkParallelLimit | Number of concurrent part uploads for the same multipart copy operation. Default value: 20 | Number | No |
| CopyChunkSize | Number of bytes in each part during a multipart copy operation with `sliceCopyFile`. Default value: 10485760 (10 MB) | Number | No |
| CopySliceSize | When a file is copied by using `sliceCopyFile`, if the file size is greater than the value of this parameter, multipart copy is used; otherwise, simple copy is used. Default value: 10485760 (10 MB) | Number | No |
| ProgressInterval | Callback frequency of the upload progress callback method `onProgress` in milliseconds. Default value: 1000 | Number | No |
| Protocol | The protocol used when the request is made. Valid values: `https:`, `http:`. By default, `http:` is used when the current page is determined to be in `http:` format; otherwise, `https:` is used | String | No |
| Domain | The custom request domain name used to call a bucket or object API. You can use a template, such as `"{Bucket}.cos.{Region}.myqcloud.com"` which will use the bucket and region passed in the replacement parameters when an API is called. | String | No |
| UploadQueueSize | The maximum size of the upload queue. Excess tasks will be cleared if their status is not waiting, checking, or uploading. Default value: 10000 | Number | No |
| ForcePathStyle | Forces the use of a suffix when sending requests. The suffixed bucket will be placed in the pathname after the domain name, and the bucket will be added to the signature pathname for calculation. Default value: false | Boolean | No |
| UploadCheckContentMd5 | Verifies Content-MD5 when uploading files, which is false by default. If it is enabled, the MD5 value of the uploading files will be calculated, which may be time-consuming for large files | Boolean | No |
| getAuthorization | Callback method for getting the signature. If there is no `SecretId` or `SecretKey`, this parameter is required. <br> **Note: This callback method is passed in during instance initialization, and is only executed to obtain the signature when the instance calls APIs.** | Function | No |
| Timeout | Timeout period in milliseconds. Default value: 0, indicating no timeout period. | Number | No |
| UseAccelerate          | Whether to enable a global acceleration endpoint. Default value: `false`. If you set the value to `true`, you need to enable global acceleration for the bucket. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406). | Boolean | No   |

#### getAuthorization Callback function description (Format 1)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization callback parameter descriptions:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | -------- |
| options | Required for getting the signature | Object |
| - Bucket  | Bucket name in the format `BucketName-APPID`. The bucket name entered here must be in this format | String |
| Region | Bucket region. For the enumerated values, see [bucket regions](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| callback | Callback method after the temporary key is obtained | Function |

After the temporary key is obtained, the callback returns an object. The attributes of the returned object are as listed below:

| Attribute | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId | `tmpSecretId` of the obtained temporary key | String | Yes |
| TmpSecretKey | `tmpSecretKey` of the obtained temporary key | String | Yes |
| SecurityToken | sessionToken of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | Yes |
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
| - Method | Method of the current request | String |
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
| SecurityToken | `sessionToken` of the obtained temporary key, which corresponds to the `x-cos-security-token` field in the header | String | No |

#### Getting an authentication credential

There are three ways to get the authentication credentials for your instance by passing in different parameters during instantiation:

1. During instantiation, pass in your `SecretId` and `SecretKey`. Each time a signature is required, it will be internally calculated by the instance.
2. During instantiation, pass in the getAuthorization callback. Every time a signature is required, it will be calculated and returned to the instance through this callback.
3. During instantiation, pass in the getAuthorization callback. When the callback is called, a temporary key will be returned. After the key expires, the callback will be called again.

### Enabling DataInsight

We have introduced the [Tencent Beacon](https://beacon.tencent.com/) into the SDK to track down and optimize the SDK quality for a better user experience.
>? DataInsight only monitors the COS request performance and doesn't report any business data.
>

To enable this feature, make sure that the SDK version is 1.4.0 or later and specify `EnableTracker` as `true` during initialization.

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
The sync method is based on JavaScript's async and await (keep browser compatibility in mind when using it). The code of the callback method above is equivalent to the following code:

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
  console.log('Uploaded successfully', fuploadResult.data);
}
```

>! `cos.getObjectUrl` currently only supports the callback method.
>

### Tips

In most cases, you only need to create a COS SDK instance, and use it directly where SDK methods need to be called.

```js
/* Sample Vue project */

/* Create `cos.js` and export the COS instance */
import COS from 'cos-js-sdk-v5'; // SDK installed using npm
const cos = new COS({
  ....
});
export default cos;

/* `page.vue` in a single page */
<template>
  <input id="fileSelector" type="file" @change="upload" />
</template>
<script>
  /* Import the path of the `cos.js` newly created above */
  import cos from 'cos';
  export default {
    data() {},
    methods: {
      upload(e) {
        const file = e.target.files && e.target.files[0];
        /* Call the method of COS SDK directly */
        cos.uploadFile({
          Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
          Region: 'COS_REGION',     /* Bucket region. Required */
          Key: '1.jpg',  /* Object key stored in the bucket (for example, `1.jpg` and `a/b/test.txt`). Required. */
          Body: file, // Upload the file object
          SliceSize: 1024 * 1024 * 5,     /* Threshold (5 MB in this example) to trigger multipart upload. If the file size is less than 5 MB, simple upload is used. This parameter is optional. You can adjust it as needed. */
        });
      }
    },
  }
</script>
```

Below are some common APIs. For more detailed initialization methods, see the [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js).

### Querying objects

[//]: #	".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Prefix: 'a/',           /* All files in directory `a`. Optional */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### Uploading an object

We strongly recommend you use the advanced upload API `uploadFile`, which automatically uses simple upload for small files and multipart upload for large files for a better performance. For more information, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/43861).
If you use the temporary key method, you need to grant the permissions of both simple upload and multipart upload as instructed in [Working with COS API Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580).
For SDK FAQs, see [FAQs](https://intl.cloud.tencent.com/document/product/436/40775).

[//]: # ".cssg-snippet-upload-file"
```html
<!-- DOM element in the HTLM file -->

<!-- Choose an image to upload -->
<input id="fileSelector" type="file" />
<!-- Click the button to upload the image -->
<input id="submitBtn" type="submit" />
```

```js
function handleFileInUploading(file) {
  cos.uploadFile({
      Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
      Region: 'COS_REGION',     /* Bucket region. Required */
      Key: '1.jpg',              /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
      Body: file, // Upload the file object
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

/* Select a file */
document.getElementById('submitBtn').onclick = function (e) {
  var file = document.getElementById('fileSelector').files[0];
  if (!file) {
    document.getElementById('msg').innerText = 'File to upload not selected';
    return;
  }
  handleFileInUploading(file);
};

```

### Downloading an object

> Object download is implemented by generating a pre-signed URL and triggering download in the browser.

[//]: # ".cssg-snippet-get-object"
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: '1.jpg',  /* Object key stored in the bucket (for example, `1.jpg` and `a/b/test.txt`). Required. */
}, function(err, data) {
    if (err) return console.log(err);
     /* Implement forced download by specifying `response-content-disposition=attachment` */
    var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment';
    /* The filename can be concatenated to rename the object during download */
    /* downloadUrl += ';filename=myname'; */
    // (The window.open() mode is recommended.) This opens the URL in a new window. If you need to open the URL in the current window, you can use the hidden iframe for download, or use the <a> tag download attribute.
    window.open(downloadUrl);
});
```

### Deleting an object

[//]: #	".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: '1.jpg',  /* Object key stored in the bucket (for example, `1.jpg` and `a/b/test.txt`). Required. */
}, function(err, data) {
    console.log(err || data);
});
```
