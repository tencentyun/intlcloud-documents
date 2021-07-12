## Overview

This document provides code samples related to obtaining an object URL.

## Obtaining Object URL

#### Feature description 

This API is used to query the URL to access an object. This API does not verify whether the object exists or not.

#### Use case 

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
| Bucket  | Bucket name in the format: `BucketName-APPID`. | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Sign | Whether to return a signed URL. Default value: `true` | Boolean | No |
| Protocol    | It can be `http:` (default) or `https:` | String | No |
| Domain    | Bucket access domain. Default value: `{BucketName-APPID}.cos.{Region}.myqcloud.com` | String | No |
| Method | HTTP request method such as `GET`, `POST`, `DELETE`, or `HEAD`. Default value: `GET` | String | No |
| Query | Query parameter object used in the signature calculation | Object | No |
| Headers | Header parameter object used in the signature calculation | Object | No |
| Expires | Signature expiration time in seconds. Default value: 900 seconds | Number | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - Url | Calculated URL | String |
