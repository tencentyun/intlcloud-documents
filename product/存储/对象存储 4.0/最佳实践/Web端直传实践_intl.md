## Introduction
This document describes how to directly upload files to a COS bucket from the web with simple codes and without using SDK.
>! This document is based on XML APIs.

## Procedure
<span id="Preparations"></span>
### 1.Preparations
(1) Go to the [COS Console](https://console.cloud.tencent.com/cos4) to create a bucket and obtain Bucket (bucket name) and Region (region name).
(2) Go to the [Key Management Console](https://console.cloud.tencent.com/cam/capi) to obtain your project's SecretId and SecretKey.
(3) In the COS Console, go to the created bucket and click **Basic Configuration** to configure the CORS rules, as shown below:
![cors](//mc.qcloudimg.com/static/img/2e7791e9274ce3ebf8b25bbeafcd7b45/image.png)

### 2. Set up temporary key service
For security purposes, we recommend you to use temporary keys to calculate a signature. To create and use temporary keys, you need to set up the temporary key service on your server. For more information, see [PHP Example](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) and [Nodejs Example](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js).
For other languages, see [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk) or [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048).

>! For higher security, when deploying the temporary key service, add an additional layer of website authentication on the server side.


### 3. Compute signatures
For security purposes, we recommend you to use temporary keys to calculate a signature. To create and use temporary keys, you need to set up the temporary key service on your server. For more information, see [PHP Example](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) and [Nodejs Example](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js).
If you want to use other languages or use APIs directly, follow the procedures below:
(1) When signatures are needed by the frontend, obtain the temporary keys from the server and input required parameters "method" and "pathname";
(2) The server first obtains the temporary keys tmpSecretId, tmpSecretKey, and sessionToken from the STS service using the fixed keys SecretId and SecretKey. For more information, see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048) or [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk);
(3) The signatures are computed at the frontend with tmpSecretId, tmpSecretKey, and parameters "method" and "pathname". The following example already includes the steps on how to compute the signatures at frontend. The signatures can also be computed at backend if necessary.
(4) The server returns the computed signatures "authorization" and "sessionToken" to the frontend, which puts the two values in the fields "Authorization" and "x-cos-security-token" in the header to send an upload request to COS API.

>! For higher security, when deploying the temporary key service, add an additional layer of website authentication on the server side.

### 4. Upload at frontend
#### Solution A: Upload with AJAX
Your browser needs to support basic HTML5 features before you can perform an upload operation with AJAX. Implement this solution by referring to [PUT Object](https://cloud.tencent.com/document/product/436/7749) and following the steps below:
(1) Complete the relevant configurations of bucket as described in [Step 1. Preparations](#前期准备).
(2) Create a `test.html` file, modify Bucket and Region in the code below, and then copy to the `test.html` file.
(3) Deploy the signature service at backend and modify the signature service address in `test.html`.
(4) Place `test.html` on the Web server, then access the page via your browser to test the file upload.

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
        // Request required parameters
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';

        // URL encoding is required for characters
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // Compute the signatures
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
                        XCosSecurityToken: credentials.sessionToken,
                        Authorization: CosAuth({
                            SecretId: credentials.tmpSecretId,
                            SecretKey: credentials.tmpSecretKey,
                            Method: options.Method,
                            Pathname: options.Pathname,
                        })
                    });
                } else {
                    console.error(xhr.responseText);
                    callback('Error while obtaining the signatures');
                }
            };
            xhr.onerror = function (e) {
                 callback('Error while obtaining the signatures');
            };
            xhr.send();
        };

        // Upload files
        var uploadFile = function (file, callback) {
            var Key = 'dir/' + file.name; // Specify the directory and file names for upload.
            getAuthorization({Method: 'PUT', Pathname: '/' + Key}, function (err, info) {

                if (err) {
                    alert(err);
                    return;
                }

                var auth = info.Authorization;
                var XCosSecurityToken = info.XCosSecurityToken;
                var url = prefix + camSafeUrlEncode(Key).replace(/%2F/, '/');
                var xhr = new XMLHttpRequest();
                xhr.open('PUT', url, true);
                xhr.setRequestHeader('Authorization', auth);
                XCosSecurityToken && xhr.setRequestHeader('x-cos-security-token', XCosSecurityToken);
                xhr.upload.onprogress = function (e) {
                    console.log('Upload progress ' + (Math.round(e.loaded / e.total * 10000) / 100) + '%');
                };
                xhr.onload = function () {
                    if (xhr.status === 200 || xhr.status === 206) {
                        var ETag = xhr.getResponseHeader('etag');
                        callback(null, {url: url, ETag: ETag});
                    } else {
                        callback('File' + Key + ' Upload failed. Status code: ' + xhr.status);
                    }
                };
                xhr.onerror = function () {
                    callback('File ' + Key + ' Upload failed. Check whether CORS cross-origin rule has been set.');
                };
                xhr.send(file);
            });
        };

        // Listen on form submission
        document.getElementById('submitBtn').onclick = function (e) {
            var file = document.getElementById('fileSelector').files[0];
            if (!file) {
                document.getElementById('msg').innerText = 'No file selected for upload';
                return;
            }
            file && uploadFile(file, function (err, data) {
                console.log(err || data);
                document.getElementById('msg').innerText = err ? err : ('Upload successful. ETag=' + data.ETag);
            });
        };
    })();
</script>

</body>
</html>
```

The result is as shown below:
![Ajax 上传](https://main.qcloudimg.com/raw/4bfc2883d71deddccc76b250ebb6a051.png)

#### Solution B: Upload with Form
Lower version of browser (e.g. IE8) supports uploading files with Form. Implement this solution by referring to [XML APIs: PostObject API](/doc/product/436/7751) and following the steps below:
(1) Complete the relevant configurations of bucket as described in [Step 1. Preparations](#前期准备).
(2) Create a `test.html` file, modify Bucket and Region in the code below, and then copy to the `test.html` file.
(3) Deploy the signature service at backend and modify the signature service address in `test.html`.
(4) In the directory where `test.html` resides, create an empty `empty.html` to be redirected back when upload is successful.
(5) Place `test.html` and `empty.html` on the Web server, then access the page via your browser to test the file upload.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Form-data upload</title>
    <style>h1, h2 {font-weight: normal;}#msg {margin-top:10px;}</style>
</head>
<body>

<h1>Form-data upload (IE8-compatible)</h1>
<div>The minimum version supporting upload is IE6 (onprogress is not supported).</div>

<form id="form" target="submitTarget" action="" method="post" enctype="multipart/form-data" accept="*/*">
    <input id="name" name="name" type="hidden" value="">
    <input name="success_action_status" type="hidden" value="200">
    <input id="success_action_redirect" name="success_action_redirect" type="hidden" value="">
    <input id="key" name="key" type="hidden" value="">
    <input id="Signature" name="Signature" type="hidden" value="">
    <input name="Content-Type" type="hidden" value="">
    <input id="x-cos-security-token" name="x-cos-security-token" type="hidden" value="">
    <input id="fileSelector" name="file" type="file">
    <input id="submitBtn" type="button" value="Submit">
</form>
<iframe id="submitTarget" name="submitTarget" style="display:none;" frameborder="0"></iframe>

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {

        // Request required parameters
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';
        var form = document.getElementById('form');
        form.action = prefix;

        // URL encoding is required for characters
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // Compute the signatures
        var getAuthorization = function (options, callback) {
            // var url = 'http://127.0.0.1:3000/sts' +
            var url = '../server/sts.php';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', url, true);
            xhr.onreadystatechange = function (e) {
                if (xhr.readyState === 4) {
                    if (xhr.status === 200) {
                        var credentials;
                        try {
                            credentials = (new Function('return ' + xhr.responseText))().credentials;
                        } catch (e) {}
                        if (credentials) {
                            callback(null, {
                                XCosSecurityToken: credentials.sessionToken,
                                Authorization: CosAuth({
                                    SecretId: credentials.tmpSecretId,
                                    SecretKey: credentials.tmpSecretKey,
                                    Method: options.Method,
                                    Pathname: options.Pathname,
                                })
                            });
                        } else {
                            console.error(xhr.responseText);
                            callback('Error while obtaining the signatures');
                        }
                    } else {
                        callback('Error while obtaining the signatures');
                    }
                }
            };
            xhr.send();
        };

        // Listen on whether upload is completed.
        var Key;
        var submitTarget = document.getElementById('submitTarget');
        var showMessage = function (err, data) {
            console.log(err || data);
            document.getElementById('msg').innerText = err ? err : ('Upload successful. ETag=' + data.ETag);
        };
        submitTarget.onload = function () {
            var search;
            try {
                search = submitTarget.contentWindow.location.search.substr(1);
            } catch (e) {
                showMessage('File ' + Key + '  upload failed.');
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

        // Initiate an upload
        document.getElementById('submitBtn').onclick = function (e) {
            var filePath = document.getElementById('fileSelector').value;
            if (!filePath) {
                document.getElementById('msg').innerText = 'No file selected for upload';
                return;
            }
            Key = 'dir/' + filePath.match(/[\\\/]?([^\\\/]+)$/)[1]; // Specify the directory and file names for upload.
            getAuthorization({Method: 'POST', Pathname: '/'}, function (err, AuthData) {
                // Place an empty "empty.html" in the current directory to be redirected back when the upload is completed with the API.
                document.getElementById('success_action_redirect').value = location.href.substr(0, location.href.lastIndexOf('/') + 1) + 'empty.html';
                document.getElementById('key').value = Key;
                document.getElementById('Signature').value = AuthData.Authorization;
                document.getElementById('x-cos-security-token').value = AuthData.XCosSecurityToken || '';
                form.submit();
            });
        };
    })();
</script>

</body>
</html>
```
The result is as shown below:
![Form 表单上传](https://main.qcloudimg.com/raw/ef666461bc5f88715f28934393ebe4f4.png)
## Related Documents
If you need to call more APIs, see the following JavaScript SDK documents:
- [JavaScript SDK](https://cloud.tencent.com/document/product/436/11459)
- [JavaScript SDK (earlier versions of APIs)](https://cloud.tencent.com/document/product/436/8095)

