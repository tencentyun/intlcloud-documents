## Introduction

This document describes how to directly transfer files to a Cloud Object Storage (COS) bucket in a Mini Program with simple code without relying on the SDK.

> ! The content of this document is based on the XML version of the API.

<span id="preparation"></span>

## Preconditions

1. Log in to the [COS console](https://console.tencentcloud.com/cos5) and create a bucket with `BucketName` (bucket name) and `Region` (region name) specified. For more information, see [Creating Buckets](https://www.tencentcloud.com/document/product/436/13309).
2. Log in to the [CAM console](https://console.tencentcloud.com/cam/capi) and obtain your project's SecretId and SecretKey on the API key management page.
3. Configure the applet domain name whitelist

To request COS in the Mini Program, you need to log in to the WeChat public platform, and configure the domain name whitelist in "Development" -> "Development Settings". The SDK uses two interfaces: wx.uploadFile and wx.request.

- cos.postObject uses wx.uploadFile to send the request.
- Other methods use wx.request to send requests.

Both need to configure the COS domain name in the corresponding white list. There are two formats of domain names configured in the whitelist:

- If only one bucket is used, you can configure the Bucket domain name as a whitelist domain name, for example `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
- If multiple storage buckets are used, you can choose the suffix method to request COS, and place the bucket in the pathname to request. This method needs to configure the regional domain name as a whitelist, such as `cos.ap-guangzhou.myqcloud.com`. For details, please refer to the comments in the code below.

## plan description

### Implementation process

1. Select a file on the front end, and the front end will send the suffix to the server.
2. The server generates a random COS file path with time according to the suffix, calculates the corresponding signature, and returns the URL and signature information to the front end.
3. The front end uses a PUT or POST request to directly upload the file to COS.

### Solution Advantages

- Permissions security: Using server-side signatures can effectively limit the scope of security permissions, which can only be used to upload a specified file path.
- Path security: The random COS file path is determined by the server, which can effectively avoid the problem of existing files being overwritten and security risks.

### Suffix request

The general request format of COS API is similar to `POST http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/`, and the requested domain name is the bucket domain name. In this way, if multiple storage buckets are used in the applet, you need to configure the bucket domain name as a whitelist domain name. The solution is as follows:

COS provides a postfix request format `POST http://cos.ap-beijing.myqcloud.com/examplebucket-1250000000/`, the requested domain name is the regional domain name, and the bucket name is placed in the requested path. To use multiple storage buckets in the same region in the applet, you only need to configure a domain name `cos.ap-beijing.myqcloud.com` as the whitelist domain name.

Note that the suffix request format needs to be noted that the path used when signing should be prefixed with the bucket name, for example `/examplebucket-1250000000/`.

## Practical steps

### Configure the server to implement signature

> ! Please add a layer of authority check on your website itself when the server is officially deployed.

How to calculate the signature can refer to the document [Request Signature](https://cloud.tencent.com/document/product/436/7778).
Please refer to [Nodejs Example](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js) for the server-side calculation signature code using Nodejs.

### Small program upload example

The following code is an example of [PUT Object ](https://cloud.tencent.com/document/product/436/7749) interface (recommended) and [POST Object ](https://cloud.tencent.com/document /product/436/14690) interface, the operation guide is as follows:

#### Upload using POST

```js
var uploadFile = function () {
   // url encode format for encoding more characters
   var camSafeUrlEncode = function (str) {
     return encodeURIComponent(str)
       .replace(/!/g, '%21')
       .replace(/'/g, '%27')
       .replace(/\(/g, '%28')
       .replace(/\)/g, '%29')
       .replace(/\*/g, '%2A');
   };

   // get the signature
   var getAuthorization = function (options, callback) {
     wx.request({
       method: 'GET',
       // Replace it with your own server address to get the post upload signature
       url: 'http://127.0.0.1:3000/post-policy?ext=' + options.ext,
       dataType: 'json',
       success: function (result) {
         var data = result. data;
         if (data) {
           callback(data);
         } else {
           wx. showModal({
             title: 'Failed to obtain temporary key',
             content: JSON. stringify(data),
             showCancel: false,
           });
         }
       },
       error: function (err) {
         wx. showModal({
           title: 'Failed to obtain temporary key',
           content: JSON. stringify(err),
           showCancel: false,
         });
       },
     });
   };

   var postFile = function ({ prefix, filePath, key, formData }) {
     var requestTask = wx.uploadFile({
       url: prefix,
       name: 'file',
       filePath: filePath,
       formData: formData,
       success: function (res) {
         var url = prefix + '/' + camSafeUrlEncode(key).replace(/%2F/g, '/');
         if (res. statusCode === 200) {
           wx.showModal({ title: 'Uploaded successfully', content: url, showCancel: false });
         } else {
           wx. showModal({
             title: 'Upload failed',
             content: JSON. stringify(res),
             showCancel: false,
           });
         }
         console.log(res.header['x-cos-request-id']);
         console.log(res.statusCode);
         console.log(url);
       },
       fail: function (res) {
         wx. showModal({
           title: 'Upload failed',
           content: JSON. stringify(res),
           showCancel: false,
         });
       },
     });
     requestTask.onProgressUpdate(function (res) {
       console.log('Progress:', res);
     });
   };

   // upload files
   var uploadFile = function (filePath) {
     var extIndex = filePath. lastIndexOf('.');
     var fileExt = extIndex >= -1 ? filePath. substr(extIndex + 1) : '';
     getAuthorization({ ext: fileExt }, function (AuthData) {
       // Parameters used in the request
       var prefix = 'https://' + AuthData.cosHost;
       var key = AuthData.cosKey; // It is safer to let the server decide the file name
       var formData = {
         key: key,
         success_action_status: 200,
         'Content-Type': '',
         'q-sign-algorithm': AuthData.qSignAlgorithm,
         'q-ak': AuthData.qAk,
         'q-key-time': AuthData.qKeyTime,
         'q-signature': AuthData.qSignature,
         policy: AuthData. policy,
       };
       if (AuthData. securityToken)
         formData['x-cos-security-token'] = AuthData.securityToken;
       postFile({ prefix, filePath, key, formData });
     });
   };

   // Select a document
   wx.chooseMedia({
     count: 1, // default 9
     sizeType: ['original'], // You can specify whether it is the original image or the compressed image, here the original image is used by default
     sourceType: ['album', 'camera'], // You can specify whether the source is an album or a camera, and the default is both
     success: function (res) {
       uploadFile(res. tempFiles[0]. tempFilePath);
     },
   });
};
```

#### Upload using PUT

```js
var uploadFile = function () {
   // url encode format for encoding more characters
   var camSafeUrlEncode = function (str) {
     return encodeURIComponent(str)
       .replace(/!/g, '%21')
       .replace(/'/g, '%27')
       .replace(/\(/g, '%28')
       .replace(/\)/g, '%29')
       .replace(/\*/g, '%2A');
   };

   // get the signature
   var getAuthorization = function (options, callback) {
     wx.request({
       method: 'GET',
       // Replace it with your own server address to get the put upload signature
       url: 'http://127.0.0.1:3000/put-sign?ext=' + options.ext,
       dataType: 'json',
       success: function (result) {
         var data = result. data;
         if (data) {
           callback(data);
         } else {
           wx. showModal({
             title: 'Failed to obtain temporary key',
             content: JSON. stringify(data),
             showCancel: false,
           });
         }
       },
       error: function (err) {
         wx. showModal({
           title: 'Failed to obtain temporary key',
           content: JSON. stringify(err),
           showCancel: false,
         });
       },
     });
   };

   var putFile = function ({ prefix, filePath, key, AuthData }) {
     // put upload needs to read the real content of the file to upload
     const wxfs = wx.getFileSystemManager();
     wxfs. readFile({
       filePath: filePath,
       success: function (fileRes) {
         var requestTask = wx. request({
           url: prefix + '/' + key,
           method: 'PUT',
           header: {
             Authorization: AuthData.authorization,
             'x-cos-security-token': AuthData.securityToken,
           },
           data: fileRes.data,
           success: function success(res) {
             var url = prefix + '/' + camSafeUrlEncode(key).replace(/%2F/g, '/');
             if (res. statusCode === 200) {
               wx. showModal({
                 title: 'Uploaded successfully',
                 content: url,
                 showCancel: false,
               });
             } else {
               wx. showModal({
                 title: 'Upload failed',
                 content: JSON. stringify(res),
                 showCancel: false,
               });
             }
             console.log(res.statusCode);
             console.log(url);
           },
           fail: function fail(res) {
             wx. showModal({
               title: 'Upload failed',
               content: JSON. stringify(res),
               showCancel: false,
             });
           },
         });
         requestTask.onProgressUpdate(function (res) {
           console.log('Progress:', res);
         });
       },
     });
   };

   // upload files
   var uploadFile = function (filePath) {
     var extIndex = filePath. lastIndexOf('.');
     var fileExt = extIndex >= -1 ? filePath. substr(extIndex + 1) : '';
     getAuthorization({ ext: fileExt }, function (AuthData) {
       const prefix = 'https://' + AuthData.cosHost;
       const key = AuthData. cosKey;
       putFile({ prefix, filePath, key, AuthData });
     });
   };

   // Select a document
   wx.chooseMedia({
     count: 1, // default 9
     sizeType: ['original'], // You can specify whether it is the original image or the compressed image, here the original image is used by default
     sourceType: ['album', 'camera'], // You can specify whether the source is an album or a camera, and the default is both
     success: function (res) {
       uploadFile(res. tempFiles[0]. tempFilePath);
     },
   });
};
```

## Related documents

To use the Mini Program SDK, please refer to the Mini Program SDK [Quick Start](https://cloud.tencent.com/document/product/436/31953) document.
