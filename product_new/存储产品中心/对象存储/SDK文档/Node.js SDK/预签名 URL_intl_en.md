## Overview

The SDK for Node.js provides APIs for getting object URLs and pre-signed request URLs. For details, see the descriptions and samples below.

## Signature Calculation

In all COS XML API requests, the authentication credential "Authorization" is required for all the operations on private resources for COS to determine whether a request is valid.

There are two ways to use the authentication credential:

1. Put it in the header parameter; field name: authorization.
2. Put it in the URL parameter; field name: sign.

The COS.getAuthorization method is used to calculate the authentication credential (Authorization), which is the signing information used to verify the request validity.

>  It is recommended to only use this method for frontend debugging and not in real projects as it involves key disclosure risks.

#### Use Cases

Obtain the authentication credential for file download:

```js
var Authorization = COS.getAuthorization({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
    Method: 'get',
    Key: 'a.jpg',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId | User's SecretId | String | Yes |
| SecretKey | User's SecretKey | String | Yes |
| Method | HTTP operation method such as `GET`, `POST`, `DELETE`, and `HEAD` | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. **If the request operation is to be performed on a file, this parameter is required and should be a filename.** If the operation is on a bucket, this parameter should be left empty | String | No |
| Query | Query parameter object of the request | Object | No |
| Headers | Header parameter object of the request | Object | No |
| Expires | Validity period of the signature; unit: second. Default value: 900 | Number | No |

#### Returned Value Description

The returned value is the calculated authentication credential string "authorization".

## Getting a Pre-signed Request URL

### Samples for Download Requests

Sample 1. Get an object URL without signature

```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: false
});
```

Sample 2. Get a signed object URL

```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg'
});
```

Sample 3. If the signing process is asynchronous, you need to get the signed URL through callback

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 4. Specify the validity period of the link

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: true,
    Expires: 3600, // Unit: second
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 5. Get the file URL and download the file

```js
var request = require('request');
var fs = require('fs');
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    console.log(data.Url);
    var req = request(data.Url, function (err, response, body) {
        console.log(err || body);
    });
    var writeStream = fs.createWriteStream(__dirname + '/1.jpg');
    req.pipe(writeStream);
});
```

### Samples for Upload Requests

Sample 1. Get a pre-signed URL for `Put Object` upload

```js
var request = require('request');
var fs = require('fs');
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    console.log(data.Url);
    var readStream = fs.createReadStream(__dirname + '/1.jpg');
    var req = request({
        method: 'PUT',
        url: data.Url,
    }, function (err, response, body) {
        console.log(err || body);
    });
    readStream.pipe(req);
});
```

### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | Object key (object name), a unique ID of an object in a bucket. **If the request operation is to be performed on a file, this parameter is required and should be a filename.** If the operation is on a bucket, this parameter should be left empty | String | Yes |
| Sign | Whether to return a signed URL | Boolean | No |
| Method | HTTP operation method such as `GET`, `POST`, `DELETE`, and `HEAD`. Default value: `GET` | String | No |
| Query | Query parameter object used in the signature calculation | Object | No |
| Headers | Header parameter object used in the signature calculation | Object | No |
| Expires | Validity period of the signature; unit: second. Default value: 900 | Number | No |

### Returned Value Description

The returned value is a string. There are two possible scenarios:

1. If the signature can be calculated synchronously (for example, the SecretId and SecretKey have been passed in during instantiation), the signed URL will be returned by default.
2. Otherwise; a URL without a signature will be returned.

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - Url | Calculated URL | String |
