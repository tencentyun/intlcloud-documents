## Overview

The JavaScript SDK provides the API for getting an object URL and the presigned URL for a request. 

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 



## Signature Calculation

In all COS XML API requests, the authentication credential `Authorization` is required for all operations on private resources for COS to determine whether a request is valid.

There are two ways to use the authentication credential:

1. Put it in the header parameter; field name: authorization.
2. Put it in the URL parameter; field name: sign.

The `COS.getAuthorization` method is used to calculate the authentication credential (Authorization), which is the signing information used to verify the validity of the request.

>! It is recommended that this method is only used for frontend debugging but not in actual projects, as it may disclose keys.
>

#### Example

Obtain the authentication credential for object download:

[//]: # (.cssg-snippet-get-authorization)
```js
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to check and manage the `SecretId` and `SecretKey` of your project.
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

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId | User SecretId | String | Yes |
| SecretKey | User's `SecretKey` | String | Yes |
| Method | HTTP request method such as `GET`, `POST`, `DELETE`, or `HEAD` | String | Yes |
| Key | Object key (object name) is the unique ID of an object in a bucket. **If the request operation is to be performed on a file, this parameter is required and should be a filename.** If the operation is on a bucket, this parameter should be left empty | String | No |
| Query | `query` parameter object of the request | Object | No |
| Headers | `header` parameter object of the request | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Returned value description

The returned value is the calculated authentication credential string `authorization`.

## Getting a Pre-signed Request URL

### Download request samples

Sample 1. Get an object URL without a signature

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

Sample 4. Specify the validity period of a link

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

Sample 5. Get the object URL and download the object

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

### Upload request samples 

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
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name) is the unique ID of an object in a bucket. **If the request operation is to be performed on a file, this parameter is required and should be a filename.** If the operation is on a bucket, this parameter should be left empty | String | Yes |
| Sign | Whether to return a signed URL. Default value: `true` | Boolean | No |
| Protocol    | It can be `http:` (default) or `https:` | String | No |
| Domain    | Bucket access domain. Default value: `{BucketName-APPID}.cos.{Region}.myqcloud.com` | String | No |
| Method | HTTP request method such as `GET`, `POST`, `DELETE`, or `HEAD`. Default value: `GET` | String | No |
| Query | Query parameter object for signature calculation in the format of {key: 'val'} | Object | No |
| Headers | Header parameter object for signature calculation | Object | No |
| Expires | Signature expiration time in seconds. Default value: `900` | Number | No |

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
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - Url | Calculated URL | String |

