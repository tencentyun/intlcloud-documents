## Overview

This document provides code samples to obtain an object URL.

## Obtaining Object URL

#### API description

This API is used to query the URL to access an object. This API does not verify whether the object exists or not.

#### Example

[//]: # (.cssg-snippet-get-presign-download-url)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',
    Sign: false,    /* Obtain an unsigned object URL. */
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Sign | Whether to return a signed URL. Default value: `true` | Boolean | No |
| Protocol    | It can be `http:` (default) or `https:` | String | No |
| Domain    | Bucket access domain. Default value: `{BucketName-APPID}.cos.{Region}.myqcloud.com` | String | No |
| Method | HTTP request method such as `GET`, `POST`, `DELETE`, or `HEAD`. Default value: `GET` | String | No |
| Query | Query parameter object for signature calculation in the format of {key: 'val'} | Object | No |
| Headers | Header parameter object for signature calculation | Object | No |
| Expires | Signature expiration time in seconds. Default value: `900` | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------ | ------------------------------------------------------------ | ------ |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - Url | Calculated URL | String |
