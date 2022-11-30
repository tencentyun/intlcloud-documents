## Overview
This document describes how to use simple code to upload files to a COS bucket directly through a WeChat Mini Program without using an SDK.

>! The content of this document is based on the XML edition of APIs.
>


<span id="preparations"></span>
## Prerequisites
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and create a bucket with `BucketName` (bucket name) and `Region` (region name) specified. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) and obtain your project's SecretId and SecretKey on the API key management page.

## Directions

#### 1. Configuring the WeChat Mini Program Allowlist
To request COS in your WeChat Mini Program, you need to log in to the WeChat Official Accounts Platform and configure the domain name allowlist in **Development** > **Development Settings**. The SDK uses two APIs: wx.uploadFile and wx.request.
- For the cos.postObject method, requests are sent using wx.uploadFile.
- For other methods, requests are sent using wx.request.

For both methods, you need to configure COS domain names in corresponding allowlists. There are two forms of allowed domain names.

- If only one bucket is used, you can configure the bucket domain name as the allowed domain name, such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
- If multiple buckets are used, you can choose to use suffixed COS requests by placing the buckets in the pathname. In this case, you need to configure the region domain name as the allowed domain name, such as `cos.ap-guangzhou.myqcloud.com`. For details, see the comments in the following code.

#### 2. Getting Temporary Key and Calculating Signature

For security reasons, the signature uses a temporary key. For details on how to build a temporary key service on the server, see [PHP Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) and [Nodejs Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js).
If you use other languages or want to implement it on your own, follow the steps below:
(1) Obtain a temporary key from the server. The server first obtains the tmpSecretId, tmpSecretKey, and sessionToken of the temporary key from the STS service using the SecretId and SecretKey of the fixed key. For more information, see [Temporary Key Generation and Usage Guidelines](https://intl.cloud.tencent.com/document/product/436/14048) or [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk).
>!Based on whether the PUT or POST request is used, an action that "name/cos:PutObject" or "name/cos:PostObject" is allowed needs to be added to the policy action of the STS.

(2) The frontend calculates the signature based on the tmpSecretId, tmpSecretKey, method, and pathname. For more information about signature calculation, see [cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js). If required by the actual business, the signature can also be calculated in the backend.
(3) Based on the used request, process the calculated signature and sessionToken as follows:
  - For the POST request, put them in the `Signature` and `x-cos-security-token` fields of `formData` and send the upload request to COS API.
  - For the PUT request, put them in the `Signature` and `x-cos-security-token` fields of `headers` and send the upload request to COS API.

>!In official deployment, add a layer of permission check of your website.
>

#### 3. Suffix Request

The general request format of COS API is similar to `POST http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/`. The requested domain name is a bucket domain name. In this way, if you use more than one bucket in the WeChat Mini Program, you need to configure the bucket domain name as an allowed domain name. The solution is as follows:

COS provides a suffix request format `POST http://cos.ap-beijing.myqcloud.com/examplebucket-1250000000/`. The requested domain name is a region domain name, and the bucket name is placed in the requested path. If you use multiple buckets in the same region in the WeChat Mini Program, you need to configure only one domain name `cos.ap-beijing.myqcloud.com` as an allowed domain name.

Note that, for the suffix request format, the path used during signing must be prefixed with the bucket name, for example, `/examplebucket-1250000000/`.

#### 4. Sample Code for Direct Upload

The following code lists examples of both [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) API (recommended) and [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) API. The operation guide is as follows:

```js
var CosAuth = require('./cos-auth'); // cos-auth.js is referenced, and the download address is https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js. 

var Bucket = 'examplebucket-1250000000';
var Region = 'ap-shanghai';
var ForcePathStyle = false; // Whether to use a suffix, which involves signature calculation and domain name allowlist configuration. For details about suffix requests, see the description above.

var uploadFile = function () {

    // Parameters used for the request
    var prefix = 'https://' + Bucket + '.cos.' + Region + '.myqcloud.com/';
    if (ForcePathStyle) {
		// The domain name used by the suffix request during signing is the region domain name, not the bucket domain name. For more information, see "3. Suffix Request" described above.
        prefix = 'https://cos.' + Region + '.myqcloud.com/' + Bucket + '/'; 
    }

    // URL-encode more characters.
    var camSafeUrlEncode = function (str) {
        return encodeURIComponent(str)
            .replace(/!/g, '%21')
            .replace(/'/g, '%27')
            .replace(/\(/g, '%28')
            .replace(/\)/g, '%29')
            .replace(/\*/g, '%2A');
    };

    // Get the temporary key
    var stsCache;
    var getCredentials = function (callback) {
        if (stsCache && Date.now() / 1000 + 30 < stsCache.expiredTime) {
            callback(data.credentials);
            return;
        }
        wx.request({
            method: 'GET',
            url: 'https://example.com/sts.php', // Server-side signature. For more information, see the instructions for getting the temporary key above.
            dataType: 'json',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                if (credentials) {
                    stsCache = data
                } else {
                    wx.showModal({title: 'failed to get the temporary key', content: JSON.stringify(data), showCancel: false});
                }
                callback(stsCache && stsCache.credentials);
            },
            error: function (err) {
                wx.showModal({title: 'failed to get the temporary key', content: JSON.stringify(err), showCancel: false});
            }
        });
    };

    // Calculate the signature.
    var getAuthorization = function (options, callback) {
        getCredentials(function (credentials) {
            callback({
                XCosSecurityToken: credentials.sessionToken,
                Authorization: CosAuth({
                    SecretId: credentials.tmpSecretId,
                    SecretKey: credentials.tmpSecretKey,
                    Method: options.Method,
                    Pathname: options.Pathname,
                })
            });
        });
    };

    // Upload the file through POST.
    var postFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // The name of the file to be uploaded is specified here.
        var signPathname = '/'; // For the PostObject API, the Key is placed in the Body for transmission, so the request path and signature path are /.
        if (ForcePathStyle) {
			  // The path used by the suffix request during signing must contain the bucket name. For more information, see "3. Suffix Request" described above.
            signPathname = '/' + Bucket + '/';  
        }
        getAuthorization({Method: 'POST', Pathname: signPathname}, function (AuthData) {
            var requestTask = wx.uploadFile({
                url: prefix,
                name: 'file',
                filePath: filePath,
                formData: {
                    'key': Key,
                    'success_action_status': 200,
                    'Signature': AuthData.Authorization,
                    'x-cos-security-token': AuthData.XCosSecurityToken,
                    'Content-Type': '',
                },
                success: function (res) {
                    var url = prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/');
                    console.log(res.statusCode);
                    console.log(url);
                    if (/^2\d\d$/.test('' + res.statusCode)) {
                        wx.showModal({title: 'upload succeeded', content: url, showCancel: false});
                    } else {
                        wx.showModal({title: 'upload failed', content: JSON.stringify(res), showCancel: false});
                    }
                },
                fail: function (res) {
                    wx.showModal({title: 'upload failed', content: JSON.stringify(res), showCancel: false});
                }
            });
            requestTask.onProgressUpdate(function (res) {
                console.log('progress:', res);
            });
        });
    };

    // Upload the file through PUT.
    var putFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // The name of the file to be uploaded is specified here.
        var signPathname = '/'; // For the PostObject API, the Key is placed in the Body for transmission, so the request path and signature path are /.
        if (ForcePathStyle) {
			  // The path used by the suffix request during signing must contain the bucket name. For more information, see "3. Suffix Request" described above.
            signPathname = '/' + Bucket + '/' + Key;  
        }
        getAuthorization({Method: 'PUT', Pathname: signPathname}, function (AuthData) {
          // The PUT request needs to read the file content from the temporary path of the file.
          var wxfs = wx.getFileSystemManager();
          wxfs.readFile({
            filePath: filePath,
            success: function (fileRes) {
              var requestTask = wx.request({
                url: prefix + signPathname.substr(signPathname.lastIndexOf('/') + 1),
                method: 'PUT',
                header: {
                  'Authorization': AuthData.Authorization,
                  'x-cos-security-token': AuthData.XCosSecurityToken,
                },
                data: fileRes.data,
                success: function success(res) {
                  var url = prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/');
                  if (res.statusCode === 200) {
                      wx.showModal({title: 'upload succeeded', content: url, showCancel: false});
                  } else {
                      wx.showModal({title: 'upload failed', content: JSON.stringify(res), showCancel: false});
                  }
                  console.log(res.statusCode);
                  console.log(url);
                },
                fail: function fail(res) {
                  wx.showModal({title: 'upload failed', content: JSON.stringify(res), showCancel: false});
                },
              });
              requestTask.onProgressUpdate(function (res) {
                  console.log('in progress:', res);
              });
            },
          });
        });
    };

    // Select the file
    wx.chooseImage({
        count: 1, // Default value: 9
        sizeType: ['original'], // You can specify whether the image is original or compressed. Original by default
        sourceType: ['album', 'camera'], // You can specify whether the source is an album or camera. Both are included by default. 
        success: function (res) {
            putFile(res.tempFiles[0].path); // PUT for the upload request, which is recommended.
            // postFile(res.tempFiles[0].path); // POST for the upload request.
        }
    })
};
```

## References

If you need to use a Mini Program SDK, see [Getting Started with Mini Program SDK](https://intl.cloud.tencent.com/document/product/436/30609).

