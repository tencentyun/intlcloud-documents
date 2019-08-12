## Overview

The SDK for JavaScript provides APIs to get object URLs and pre-signed request URLs.

## Signature Calculation

In all COS XML API requests, private resource operations require the authentication credential "authorization" which is used to determine whether the current request is legal.

There are two ways to use the authorization:

1. Put it in the header parameter (field name: authorization).
2. Put i in the URL parameter (field name: sign).

The COS.getAuthorization method is used to calculate the authorization, i.e., signature information used to verify the request validity.

> This method is recommended only for frontend debugging. It is not recommended to use it in real projects as there may be a risk of key disclosure.

#### Use Cases

Obtain the authorization for file download:

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
| Method | HTTP operation method such as GET, POST, DELETE, and HEAD | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. **If the request operation is for a file, this parameter is a filename and required.** If the operation is for a bucket, this parameter is blank | String | No |
| Query | Query parameter object of the request | Object | No |
| Headers | Header parameter object of the request | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Return Value Description

The return value is the calculated authentication credential string "authorization".

## Getting a Pre-signed Request URL

#### Sample Request for Download

Example 1. Get an object URL without signature

```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: false
});
```

Example 2. Get a signed object URL

```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg'
});
```

Example 3. If the signing process is async, you need to get the signed URL through callback

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

Example 4. Specify validity period of the link

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: true,
    Expires: 3600, // In seconds
}, function (err, data) {
    console.log(err || data.Url);
});
```

Example 5. Get the file URL and download the file

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (!err) return console.log(err);
    var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // Supplement the parameter for forced download
    window.open(downloadUrl); // This indicates to open the URL in a new window. If you want to open it in the current window, use the hidden iframe to download or use the "a" tag download attribute to assist in downloading
});
```

#### Sample Request for Upload

Example 1. Get a pre-signed Put Object upload URL

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (!err) return console.log(err);
    console.log(data.Url);
    var xhr = new XMLHttpRequest();
    xhr.open('PUT', data.Url, true);
    xhr.onload = function (e) {
        console.log(xhr.responseText);
    };
    xhr.onerror = function (e) {
        console.log('error getting the signature');
    };
    xhr.send();
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Key | An object key (object name) is a unique ID of an object in the bucket. <br>**If the request operation is for a file, this parameter is a filename and required.** <br>If the operation is for a bucket, this parameter is blank | String | Yes |
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
