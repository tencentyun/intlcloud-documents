## Overview
This document describes how to use simple code to upload files directly to a COS bucket through a WeChat Mini Program without relying on the SDK.

> The content of this document is based on the XML edition of APIs.


## Steps

<span id="preparations"></span>
### 1. Preparations
(1) Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and set the BucketName and Region.
(2) Log in to the CAM Console and obtain your project's SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.


### 2. Configuring the WeChat Mini Program Whitelist
To request COS in the WeChat Mini Program, you need to log in to the WeChat Official Accounts Platform and configure the domain name whitelist in "Development" > "Development Settings". The SDK uses two APIs: wx.uploadFile and wx.request.
- For the cos.postObject method, requests are sent using wx.uploadFile.
- For other methods, requests are sent using wx.request.

For both of them, you need to configure the COS domain name in the corresponding whitelist. There are two formats of domain names configured in the whitelist:

- If only one bucket is used, you can configure the bucket domain name as the whitelist domain name, such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
- If multiple buckets are used, you can choose to use suffixed COS requests by placing the buckets in the pathname. In this case, you need to configure the region domain name as the whitelist, such as `cos.ap-guangzhou.myqcloud.com`. See the annotations in the code below for details.

### 3. Getting Temporary Key and Calculating Signature
For security reasons, the signature uses a temporary key. For building a temporary key service on the server, see [PHP Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) and [Nodejs Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js).
If you use other languages or want to implement it on your own, follow the steps below:
(1) Obtain a temporary key from the server. The server first obtains the tmpSecretId, tmpSecretKey, and sessionToken of the temporary key from the STS service using the SecretId and SecretKey of the fixed key. For more information, see [Temporary Key Generation and Usage Guidelines](https://intl.cloud.tencent.com/document/product/436/14048) or [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk).
>As only the PostObject API can be used for uploads through an online program, allowing "name/cos:PostObject" should be added to the policy action of the STS.

(2) The frontend calculates the signature based on the tmpSecretId, tmpSecretKey, method, and pathname. For more information about signature calculation, see [cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js). If required by the actual business, the signature can be calculated in the backend too.
(3) The frontend authorizes the signature calculated with sessionToken and puts the two values returned by the server into the x-cos-security-token and authorization fields of the header to send an upload request to the COS API.

>In official deployment, add a layer of permission check of your website.

### 4. Sample Code for Direct Upload

For uploads through the WeChat Mini Program, the wx.uploadFile API is used. As it only supports the POST method, the current scheme uses the [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) API. Below are the steps:

```js
var CosAuth = require('./cos-auth'); //  COS signature method https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js

var Bucket = 'examplebucket-1250000000';
var Region = 'ap-shanghai';
var ForcePathStyle = false; // Whether to use a suffix, which involves signature calculation and domain name whitelist configuration

var uploadFile = function () {

    // Parameters used for the request
    var prefix = 'https://' + Bucket + '.cos.' + Region + '.myqcloud.com/';
    if (ForcePathStyle) {
        prefix = 'https://cos.' + Region + '.myqcloud.com/' + Bucket + '/'; // This is the suffix, and the signature should also specify Pathname: '/' + Bucket + '/'
    }

    // URL-encoding format for encoding more characters
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
            callback();
            return;
        }
        wx.request({
            method: 'GET',
            url: 'https://example.com/sts.php', // Server-side signature. For more information, see the instructions for getting the temporary key above
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

    // Calculate the signature
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

    // Upload the file
    var uploadFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // The name of the file to be uploaded is specified here
        var signPathname = '/'; // For the PostObject API, the Key is placed in the Body for transmission, so the request path and signature path are /
        if (ForcePathStyle) {
            signPathname = '/' + Bucket + '/'; // If a suffixed request is used, the domain name is a region domain name, and the bucket is placed in the path
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
                    if (res.statusCode === 200) {
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

    // Select the file
    wx.chooseImage({
        count: 1, // 9 by default
        sizeType: ['original'], // You can specify whether the image is original or compressed. Original by default
        sourceType: ['album', 'camera'], // You can specify whether the source is album or camera. Both by default
        success: function (res) {
            uploadFile(res.tempFiles[0].path);
        }
    })
};
```

## Related Documents

To use the WeChat Mini Program SDK, see [COS SDK Documentation for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/30609).
