## Overview

The SDK for WeChat Mini Program provides samples for calculating signatures and getting object URLs and pre-signed request URLs.

## Signature Calculation

In all COS XML API requests, private resource operations require the authentication credential "authorization" which is used to determine whether the current request is legal.

There are two ways to use the authorization:

1. Put it in the header parameter (field name: authorization).
2. Put i in the URL parameter (field name: sign).

The COS.getAuthorization method is used to calculate the authorization, i.e., signing information used to verify the request validity.

>  This method is recommended only for frontend debugging. It is not recommended to use it in real projects as there may be a risk of key disclosure.

#### Use Cases

Obtain the authorization for object download:

```js
var Authorization = COS.getAuthorization({
    SecretId: 'COS_SECRETID',
    SecretKey: 'COS_SECRETKEY',
    Method: 'get',
    Key: 'picture.jpg',
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
| Method | HTTP operation method such as GET, POST, DELETE, and HEAD | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. <br><li>**If the request operation is for a file, this parameter is a filename and required.** <br><li>If the operation is for a bucket, this parameter is blank | String | No |
| Query | Query parameter object of the request | Object | No |
| Headers | Header parameter object of the request | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Return Value Description

The return value is the calculated authentication credential string "authorization".

## Getting a Pre-signed Request URL

#### Upload Request Description

Uploading files in a WeChat Mini Program can only be done via the POST Object API. Getting a pre-signed URL is not applicable to this API. If you need to upload files by yourself, do as described in [WeChat Mini Program Upload Practices](https://intl.cloud.tencent.com/document/product/436/30934).

#### Sample Request for Download

Sample 1. Get an object URL without signature

```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: false
});
```

Sample 2. Get a signed object URL

```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg'
});
```

Sample 3. Get the signed URL through callback

> ? If the signing process is async, you need to get the signed URL through callback

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 4. Specify validity period of the link

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: true,
    Expires: 3600, // In seconds
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 5. Get the object URL and download the object

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: true
}, function (err, data) {
    if (!err) return console.log(err);
    wx.downloadFile({
        url: data.Url, // A domain name with a URL needs to be used as the download whitelist
        success (res) {
            console.log(res.statusCode, res.tempFilePath);
        },
        fail: function (err) {
            console.log(err);
        },
    });
});
```



#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. <br><li>**If the request operation is for a file, this parameter is a filename and required.** <br><li>If the operation is for a bucket, this parameter is blank | String | Yes |
| Sign | Whether to return a signed URL | Boolean | No |
| Method | HTTP operation method such as GET, POST, DELETE, and HEAD. Default value: GET | String | No |
| Query | Query parameter object participating in signature calculation | Object | No |
| Headers | Header parameter object participating in signature calculation | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Return Value Description

The return value is a string in the following two cases:

1. If the signature can be calculated synchronously (for example, passing in the SecretId and SecretKey through instantiation), the signed URL will be returned by default.
2. Otherwise; a URL with no signature will be returned.

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - Url | Calculated URL | String |

