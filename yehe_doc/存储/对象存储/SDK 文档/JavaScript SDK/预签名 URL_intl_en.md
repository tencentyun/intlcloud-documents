## Overview

The JavaScript SDK provides the API for getting an object URL and the presigned URL for a request. 

## Signature Calculation

In all COS XML API requests, the authentication credential `Authorization` is required for all operations on private resources for COS to determine whether a request is valid.

There are two ways to use the authentication credential:

1. Put it in the header parameter; field name: authorization.
2. Put it in the URL parameter; field name: sign.

The COS.getAuthorization method is used to calculate the authentication credential (Authorization), which is the signing information used to verify the request validity.

> ! It is recommended to only use this method for frontend debugging and not in real projects as it involves key disclosure risks.

#### Use case 

Obtain the authentication credential for object download:

[//]: # (.cssg-snippet-get-authorization)
```js
// You can obtain/manage SECRETID and SECRETKEY at https://console.cloud.tencent.com/cam/capi
var Authorization = COS.getAuthorization({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
    Method: 'get',
    Key: 'exampleobject',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId | User SecretId | String | No |
| SecretKey | User's SecretKey | String | Yes |
| Method | HTTP request method such as `GET`, `POST`, `DELETE`, and `HEAD` | String | Yes |
| Key | Object key (object name) is the unique ID of an object in a bucket. **If the request operation is to be performed on a file, this parameter is required and should be a filename.** If the operation is on a bucket, this parameter should be left empty | String | No |
| Query | Query parameter object of the request | Object | No |
| Headers | Header parameter object of the request | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Returned value description

The returned value is the calculated authentication credential string `authorization`.

## Obtaining pre-signed URL used for requests

### Samples for download requests

Sample 1. Get an unsigned object URL

[//]: # (.cssg-snippet-get-presign-download-url)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
    Sign: false
});
```

Sample 2. Get a signed object URL

[//]: # (.cssg-snippet-get-presign-download-url-signed)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject'
});
```

Sample 3. Get a signed URL through `callback`

> ? If the signing process is asynchronous, you need to get the signed URL through a callback.

[//]: # (.cssg-snippet-get-presign-download-url-callback)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 4. Specify the validity period of the link

[//]: # (.cssg-snippet-get-presign-download-url-expiration)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
    Sign: true,
    Expires: 3600, // Unit: second
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 5. Get an object URL and download the object

[//]: # (.cssg-snippet-get-presign-download-url-then-fetch)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // Adds the parameter for a forced download
    window.open(downloadUrl); // This opens the url in a new window. If you need to open the url in the current window, you can use the hidden iframe for download, or use the <a> tag download attribute.
});
```

### Samples for upload requests

Sample 1. Get a pre-signed URL for `Put Object` upload

[//]: # (.cssg-snippet-get-presign-upload-url)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Method: 'PUT',
    Key: 'exampleobject',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    console.log(data.Url);
    
    // After the URL is obtained, the object can be uploaded in the frontend using AJAX.
    var xhr = new XMLHttpRequest();
    xhr.open('PUT', data.Url, true);
    xhr.onload = function (e) {
        console.log('Uploaded successfully', xhr.status, xhr.statusText);
    };
    xhr.onerror = function (e) {
        console.log('Upload failed', xhr.status, xhr.statusText);
    };
    xhr.send(file); // “file” is the object to upload.
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format: `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique ID of an object in a bucket. **If the request operation is to be performed on a file, this parameter is required and should be a filename.** If the operation is on a bucket, this parameter should be left empty | String | Yes |
| Sign | Whether to return a signed URL. Default value: `true` | Boolean | No |
| Method | HTTP request method such as `GET`, `POST`, `DELETE`, and `HEAD`. Default value: `GET` | String | No |
| Query | Query parameter object used in the signature calculation | Object | No |
| Headers | Header parameter object used in the signature calculation | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Returned value description

The returned value is a string. There are two possible scenarios:

1. If the signature can be calculated synchronously (for example, the SecretId and SecretKey have been passed in during instantiation), the signed URL will be returned by default.
2. Otherwise, an unsigned URL will be returned.

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - Url | Calculated URL | String |

