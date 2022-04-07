## Introduction

This document describes how to use simple code to upload files directly to a COS bucket through a WeChat Mini Program without relying on the SDK.

>!  The content of this document is based on the XML edition of APIs.

<span id="preparations"></span>

## Prophase condition

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), create a bucket, and get the bucket name and [Region name](https://intl.cloud.tencent.com/document/product/436/6224). 
2. Log in to the CAM Console and obtain your project's SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) Page.

## Steps

### 1. Configuring the WeChat Mini Program Allowlist

Mini Program requests that COS needs to log in to WeChat's public platform and configure the domain name allowlist in "Development"-> "Development Settings". The SDK uses two APIs: wx.uploadFile and wx.request.

- For the cos.postObject method, requests are sent using wx.uploadFile.
- For other methods, requests are sent using wx.request.

You need to configure COS domain names in corresponding allowlists. There are two forms of allowed domain names.

- If only one bucket is used, you can configure the bucket domain name as the allowlist domain name, such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
- If multiple buckets are used, you can choose to use suffixed COS requests by placing the buckets in the pathname. In this case, you need to configure the region domain name as the allowlist, such as `cos.ap-guangzhou.myqcloud.com`.

### 2. Getting Temporary Key and Calculating Signature

For security reasons, the signature uses a temporary key. For building a temporary key service on the server, see [PHP Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) And [Nodejs Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js). 
 If you use other languages or want to implement it on your own, follow the steps below: 
 (1) Obtain a temporary key from the server. The server first obtains the tmpSecretId, tmpSecretKey, and sessionToken of the temporary key from the STS service using the SecretId and SecretKey of the fixed key. For more information, see [Temporary Key Generation and Usage Guidelines](https://intl.cloud.tencent.com/document/product/436/14048) Or [Cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk) .

>! As only the PostObject API can be used for uploads through an online program, allowing ""name/cos:PostObject"" should be added to the policy action of the STS.

 (2) The frontend calculates the signature based on the tmpSecretId, tmpSecretKey, method, and pathname. For more information about signature calculation, see [Cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js). If required by the actual business, the signature can be calculated in the backend too. 
 (3) put the calculated signature and sessionToken, in the Signature and x-cos-security-token fields of formData when Mini Program sends the request, and send the upload request to COS API.

>!  In official deployment, add a layer of permission check of your website.


#### 3. Suffix request

The general request format of COS API is similar. `POST http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/` The requested domain name is Bucket domain name. In this way, if you use more than one Bucket in Mini Program, you need to configure the Bucket domain name as an allowlist domain name. The solution is as follows:

COS provides a suffix request format `POST http://cos.ap-beijing.myqcloud.com/examplebucket-1250000000/` The requested domain name is the regional domain name, and the name of Bucket is placed in the requested path. If you use multiple Bucket in the same region in Mini Program, you only need to configure one domain name. `cos.ap-beijing.myqcloud.com` As an allowed domain name.

The suffix request format should be noted that the path used when signing should be prefixed with the name of Bucket, for example `/examplebucket-1250000000/`.


#### 4. Sample Code for Direct Upload

For uploads through the WeChat Mini Program, the wx.uploadFile API is used. As it only supports the POST method, the current scheme uses the [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) API. Below are the steps:

```js
var CosAuth = require('./cos-auth'); // Here, reference the cos-auth.js, which is downloaded at https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js 

var Bucket = 'examplebucket-1250000000';
var Region = 'ap-shanghai';
var ForcePathStyle = false; // Whether to use a suffix, which involves signature calculation and domain name allowlist configuration

var uploadFile = function () {

    // Parameters used for the request
    var prefix = 'https://' + Bucket + '.cos.' + Region + '.myqcloud.com/';
    if (ForcePathStyle) {
		
        / / the domain name of the suffix request is signed using a regional domain name instead of a Bucket domain name. For more information, please see ""3."" Suffix request ""
        var prefix = 'https://' + Bucket + '.cos.' + Region + '.myqcloud.com/'; 
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
            callback(data.credentials);
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

    // Uploading the file
    var uploadFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // The name of the file to be uploaded is specified here
        var signPathname = '/'; // For the PostObject API, the Key is placed in the Body for transmission, so the request path and signature path are /
        if (ForcePathStyle) {
	        / / the path used in the signature of the suffix request should include the name of Bucket. For more information, please see ""3."" Suffix request ""
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

    // Select the file
    wx.chooseImage({
        count: 1, // Default value: 9
        sizeType: ['original'], // You can specify whether the image is original or compressed. Original by default
        sourceType: ['album', 'camera'], // You can specify whether the source is album or camera. Both can be the source by default
        success: function (res) {
            uploadFile(res.tempFiles[0].path);
        }
    })
};
```

## Related Documents

If you need to use Mini Program SDK, please see Mini Program SDK [Getting Started](https://intl.cloud.tencent.com/document/product/436/30609)  documentation.
