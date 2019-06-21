## Download and Installation

### Related resources

Download Mini Program SDK resources from [GitHub download](https://github.com/tencentyun/cos-wx-sdk-v5).

### Environment dependencies

Applicable to WeChat Mini Program environment.

### Install SDK
You can install the Mini Program SDK manually or using npm. The installation methods are as follows.

- Manual installation
Copy the [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js) from the source code to the code directory of your mini program. The code can be referenced by the relative path:
```shell
var COS = require('./cos-wx-sdk-v5.js')
```
- Installation via npm
If the mini program code is packaged with webpack, you can install the dependency via npm:
```shell
npm install cos-wx-sdk-v5
```
The mini program code is referenced by `var COS = require('cos-wx-sdk-v5');`.

### Preparations

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4) to create a bucket and obtain Bucket (bucket name) and Region (region name).
2. Obtain the SecretId and SecretKey for your project in [Key Management](https://console.cloud.tencent.com/capi) on the console.

#### Compute a signature

If the signature computing is implemented at the frontend, SecretId and SecretKey can be exposed. For this reason, the signature computing is performed at the backend. The frontend obtains the temporary key via ajax from the backend. Add a permission verification of your website at the backend during the deployment.

Click here to see the [examples of signatures](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/) in PHP and Node.js. For other languages, see [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048).

## Getting Started

### Initialization

```js
var cos = new COS({
    // ForcePathStyle: true. // If a lot of buckets are used, you can access the domain names by using suffix match so as to reduce the number of domain names configured in the whitelist. The domain name of the region where the bucket resides will be used when sending requests.
    getAuthorization: function (options, callback) {
        // Obtain the signature asynchronously
        wx.request({
            url: 'https://example.com/sts.php',
            data: {
                Method: options.Method,
                Key: options.Key
            },
            dataType: 'text',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime, // The SDK will not call getAuthorization again before the ExpiredTime.
                });
            }
        });
    }
});
```

For more information about the initialization method, see the [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-sdk.js).

### Create a bucket

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
}, function (err, data) {
    console.log(err || data);
});
```

>If you need to create a bucket in the mini program, but the bucket name is unknown, you cannot add the bucket name to the domain name whitelist. See [FAQs](https://intl.cloud.tencent.com/document/product/436/10687)。 for relevant solutions.

### Query the bucket list

```js
cos.getService(function (err, data) {
    console.log(err || data);
});
```

### Upload an object

The upload API wx.uploadFile in Mini Program only supports POST requests, while the postObject API is needed for uploading files in SDK. If only the API for uploading files is needed in the mini program, it is recommended not to reference SDK. See the simple example [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js).

```js
// First select a file to obtain a temporary path
wx.chooseImage({
    count: 1, // The default value is 9
    sizeType: ['original'], // You can specify whether to use the original image or the compressed image. The original image is used by default.
    sourceType: ['album', 'camera'], // You can specify whether the source is the album or the camera, and both are used by default.
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var filename = filePath.substr(filePath.lastIndexOf('/') + 1);
        cos.postObject({
            Bucket: 'examplebucket-1250000000',
            Region: 'ap-beijing',
            Key: filename,
            FilePath: filePath,
            onProgress: function (info) {
                console.log(JSON.stringify(info));
            }
        }, function (err, data) {
            console.log(err || data);
        });
    }
});
```

### Query the object list

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/',
}, function (err, data) {
    console.log(err || data);
});
```

### Obtain object Url

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.png',
}, function (err, data) {
    console.log(err || data.Url);
});
```

### Upload text content to the object

Uploading text content can be completed via the putObject API. The wx.request API is actually called in this case.

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.txt',
    Body: 'hello',
    onProgress: function (info) {
        console.log(JSON.stringify(info));
    }
}, function (err, data) {
    console.log(err || data);
});
```

### Read the text content of the object

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### Delete an object

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.png',
}, function (err, data) {
    console.log(err || data.Body);
});
```

## FAQs
If you have any questions while using the Mini Program SDK, see the mini program section in [FAQs](https://intl.cloud.tencent.com/document/product/436/10687).


## Related Documents

The documents are being optimized. The mini program does not support multipart-related APIs. If you need to use upload and download features, view the [source code](https://github.com/tencentyun/cos-wx-sdk-v5) and [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js). For other API documentations, see the [API documentation](https://intl.cloud.tencent.com/document/product/436/12260) of JavaScript SDK.

