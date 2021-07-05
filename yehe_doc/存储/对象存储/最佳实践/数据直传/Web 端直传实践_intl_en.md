## Overview
This document describes how to use simple code to upload files to a COS bucket directly from the web without using an SDK.

>! This document is based on the XML [APIs](https://intl.cloud.tencent.com/document/product/436/7751).

<span id="1"></span>
## Prerequisites

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and create a bucket to obtain the `Bucket` (bucket name) and `Region` (region name). For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Go to the bucket detail page, choose the **Security Management** tab, and select **CORS (Cross-Origin Resource Sharing)** from the drop-down list. Then, click **Add a Rule**. A configuration example is shown in the following figure. For more information, please see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
![](https://main.qcloudimg.com/raw/eb73177a2302ad976be301254bcd9630.png)
3. Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) and obtain the `SecretId` and `SecretKey` of your project.



## Directions


>!In official deployment, add a layer of permission check of your website.

### Getting temporary key and calculating signature
For security reasons, the signature uses a temporary key. For building a temporary key service on the server, please see [PHP Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) and [Nodejs Sample](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js).
To use other languages or implement it on your own, please take the following steps:
1. Obtain a temporary key from the server. The server first uses the `SecretId` and `SecretKey` of a fixed key to obtain the `tmpSecretId`, `tmpSecretKey`, and `sessionToken` of the temporary key from the STS service. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) or [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk).
2. The frontend calculates the signature based on the `tmpSecretId`, `tmpSecretKey`, `method`, and `pathname`. You can use [cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js) to calculate the signature as described in this document. If required by the actual business, the signature can also be calculated at the backend.
3. If you use the `PutObject` API for the upload, you can specify the calculated signature and `sessionToken` in the `authorization` and `x-cos-security-token` fields, respectively, in the request header.
If you use the `PostObject` API for the upload, you can specify the calculated signature and `sessionToken` in the `Signature` and `x-cos-security-token` fields, respectively, in the request form.


### Frontend upload
#### Solution A: Upload with AJAX
To upload with AJAX, your browser needs to support the basic features of HTML5. You can implement this solution by referring to [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) and taking the steps below:
1. Obtain the bucket information by taking the steps in [Prerequisites](#1).
2. Create a `test.html` file. Then, modify the values `Bucket` and `Region` in the following code and copy the code to the `test.html` file.
3. Deploy the signature service at the backend and modify the signature service address in `test.html`.
(4) Place `test.html` on the Web server. Then, browser the page to test the file upload feature.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax Put Upload</title>
    <style>
        h1, h2 {
            font-weight: normal;
        }

        #msg {
            margin-top: 10px;
        }
    </style>
</head>
<body>

<h1>Ajax Put Upload</h1>

<input id="fileSelector" type="file">
<input id="submitBtn" type="submit">

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {
        // Parameters used for the request
        var Bucket = 'examplebucket-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';  // The prefix is used to concatenate the request URL. Use the default bucket endpoint.

        // URL-encode more characters.
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // Calculate the signature.
        var getAuthorization = function (options, callback) {
            // var url = 'http://127.0.0.1:3000/sts-auth' +
            var url = '../server/sts.php';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', url, true);
            xhr.onload = function (e) {
                var credentials;
                try {
                    credentials = (new Function('return ' + xhr.responseText))().credentials;
                } catch (e) {}
                if (credentials) {
                    callback(null, {
                        SecurityToken: credentials.sessionToken,
                        Authorization: CosAuth({
                            SecretId: credentials.tmpSecretId,
                            SecretKey: credentials.tmpSecretKey,
                            Method: options.Method,
                            Pathname: options.Pathname,
                        })
                    });
                } else {
                    console.error(xhr.responseText);
                    callback('Signature obtaining error');
                }
            };
            xhr.onerror = function (e) {
                callback('Signature obtaining error');
            };
            xhr.send();
        };

        // Upload a file.
        var uploadFile = function (file, callback) {
            var Key = 'dir/' + file.name; // File directory and filename
            getAuthorization({Method: 'PUT', Pathname: '/' + Key}, function (err, info) {

                if (err) {
                    alert(err);
                    return;
                }

                var auth = info.Authorization;
                var SecurityToken = info.SecurityToken;
                var url = prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/');
                var xhr = new XMLHttpRequest();
                xhr.open('PUT', url, true);
                xhr.setRequestHeader('Authorization', auth);
                SecurityToken && xhr.setRequestHeader('x-cos-security-token', SecurityToken);
                xhr.upload.onprogress = function (e) {
                    console.log('Upload progress ' + (Math.round(e.loaded / e.total * 10000) / 100) + '%');
                };
                xhr.onload = function () {
                    if (/^2\d\d$/.test('' + xhr.status)) {
                        var ETag = xhr.getResponseHeader('etag');
                        callback(null, {url: url, ETag: ETag});
                    } else {
                        callback('File' + Key + ' Upload failed. Status code: ' + xhr.status);
                    }
                };
                xhr.onerror = function () {
                    callback('File ' + Key + ' Upload failed. Check whether the CORS rule has been set');
                };
                xhr.send(file);
            });
        };

        // Listen on form submission.
        document.getElementById('submitBtn').onclick = function (e) {
            var file = document.getElementById('fileSelector').files[0];
            if (!file) {
                document.getElementById('msg').innerText = 'File to upload not selected';
                return;
            }
            file && uploadFile(file, function (err, data) {
                console.log(err || data);
                document.getElementById('msg').innerText = err ? err : ('Upload successful, ETag=' + data.ETag);
            });
        };
    })();
</script>

</body>
</html>
```

The result is as follows:
![Upload with Ajax](https://main.qcloudimg.com/raw/970bc04c0a1e0b3c5be077f360000424.png)

#### Solution B: Upload with a form
HTML form supports uploading with a lower browser version (e.g., IE8). The current solution uses the [Post Object](https://intl.cloud.tencent.com/document/product/436/14690) API. The directions are described as follows:
1. Obtain the bucket information by taking the steps in [Prerequisites](#1).
2. Create a `test.html` file. Then, modify the values `Bucket` and `Region` in the following code and copy the code to the `test.html` file.
3. Deploy the signature service at the backend and modify the signature service address in `test.html`.
4. In the directory where `test.html` is stored, create an empty `empty.html` file to be redirected back when the upload is successful.
5. Place `test.html` and `empty.html` on the Web server. Then, browse the page to test the file upload feature.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Simple Upload with a Form</title>
    <style>h1, h2 {font-weight: normal;}#msg {margin-top:10px;}</style>
</head>
<body>

<h1>Simple Upload with a Form (IE8-Compatible)</h1>
<div>The browser should at least be IE6 and onprogress is not supported.</div>

<form id="form" target="submitTarget" action="" method="post" enctype="multipart/form-data" accept="*/*">
    <input id="name" name="name" type="hidden" value="">
    <input name="success_action_status" type="hidden" value="200">
    <input id="success_action_redirect" name="success_action_redirect" type="hidden" value="">
    <input id="key" name="key" type="hidden" value="">
    <input id="Signature" name="Signature" type="hidden" value="">
    <input name="Content-Type" type="hidden" value="">
    <input id="x-cos-security-token" name="x-cos-security-token" type="hidden" value="">

    <!-- Put the file field at the end of the form (in case the file content is too long) to avoid affecting the signature field and authentication. -->
    <input id="fileSelector" name="file" type="file">
    <input id="submitBtn" type="button" value="Submit">
</form>
<iframe id="submitTarget" name="submitTarget" style="display:none;" frameborder="0"></iframe>

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {

        // Parameters used for the request
        var Bucket = 'examplebucket-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';  // The prefix is used to concatenate the request URL. Use the default bucket endpoint.
        var form = document.getElementById('form');
        form.action = prefix;

        // URL-encode more characters.
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // Calculate the signature.
        var getAuthorization = function (options, callback) {
            // var url = 'http://127.0.0.1:3000/sts' +
            var url = '../server/sts.php';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', url, true);
            xhr.onreadystatechange = function (e) {
                if (xhr.readyState === 4) {
                    if (/^2\d\d$/.test('' + xhr.status)) {
                        var credentials;
                        try {
                            credentials = (new Function('return ' + xhr.responseText))().credentials;
                        } catch (e) {}
                        if (credentials) {
                            callback(null, {
                                SecurityToken: credentials.sessionToken,
                                Authorization: CosAuth({
                                    SecretId: credentials.tmpSecretId,
                                    SecretKey: credentials.tmpSecretKey,
                                    Method: options.Method,
                                    Pathname: options.Pathname,
                                })
                            });
                        } else {
                            console.error(xhr.responseText);
                            callback('Signature obtaining error');
                        }
                    } else {
                        callback('Signature obtaining error');
                    }
                }
            };
            xhr.send();
        };

        // Listen on whether the upload is completed.
        var Key;
        var submitTarget = document.getElementById('submitTarget');
        var showMessage = function (err, data) {
            console.log(err || data);
            document.getElementById('msg').innerText = err ? err : ('Upload successful, ETag=' + data.ETag);
        };
        submitTarget.onload = function () {
            var search;
            try {
                search = submitTarget.contentWindow.location.search.substr(1);
            } catch (e) {
                showMessage('File ' + Key + ' Upload failed');
            }
            if (search) {
                var items = search.split('&');
                var i, arr, data = {};
                for (i = 0; i < items.length; i++) {
                    arr = items[i].split('=');
                    data[arr[0]] = decodeURIComponent(arr[1] || '');
                }
                showMessage(null, {url: prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/'), ETag: data.etag});
            } else {
            }
        };

        // Initiate an upload.
        document.getElementById('submitBtn').onclick = function (e) {
            var filePath = document.getElementById('fileSelector').value;
            if (!filePath) {
                document.getElementById('msg').innerText = 'File to upload not selected';
                return;
            }
            Key = 'dir/' + filePath.match(/[\\\/]?([^\\\/]+)$/)[1]; // File directory and filename
            getAuthorization({Method: 'POST', Pathname: '/'}, function (err, AuthData) {
                // Place an empty "empty.html" file in the current directory to be redirected back when the upload is completed with the API.
                document.getElementById('success_action_redirect').value = location.href.substr(0, location.href.lastIndexOf('/') + 1) + 'empty.html';
                document.getElementById('key').value = Key;
                document.getElementById('Signature').value = AuthData.Authorization;
                document.getElementById('x-cos-security-token').value = AuthData.SecurityToken || '';
                form.submit();
            });
        };
    })();
</script>
</body>
</html>
```

The result is shown as follows:
![Upload with a form](https://main.qcloudimg.com/raw/90a3460c58ed7e056f08624ce329c1a4.png)

## Reference
If you need to call more APIs, please see the following JavaScript SDK document:
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/11459)
