## Overview

This document provides an overview of APIs and SDK code samples related to CORS preflight requests.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a preflight request for cross-origin access | Sends a preflight request to check whether a real cross-origin access request can be sent |

#### Description

This API (`OPTIONS Object`) is used to send a preflight request to check the CORS configuration of an object. Before making an actual CORS request, you can send an OPTIONS request that includes the source origin, HTTP method, and headers to COS to determine whether an actual CORS request can be sent. If there is no CORS configuration, "403 Forbidden" will be returned. **You can enable CORS for a bucket using the `PUT Bucket cors` API.**

#### Sample code

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Origin: 'https://www.qq.com', /*Required*/
    AccessControlRequestMethod: 'PUT', /*Required*/
    AccessControlRequestHeaders: 'origin,accept,content-type' /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Origin | Origin domain name of the simulated CORS request | String | Yes |
| AccessControlRequestMethod | HTTP method of the simulated CORS request | String | Yes |
| AccessControlRequestHeaders | Headers of the simulated CORS request | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - headers | Headers | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - AccessControlAllowOrigin | Source origins (separated by commas) of the simulated CORS request. If the origins are not allowed, this header will not be returned. Example: `*` | String |
| - AccessControlAllowMethods | HTTP methods of the simulated cross-origin access request separated by commas, such as `PUT`, `GET`, `POST`, `DELETE`, and `HEAD`. This header will not be returned if the request method is not allowed | String |
| - AccessControlAllowHeaders | Headers (separated by commas) of the simulated CORS request (for example, `accept,content-type,origin,authorization`). If none of the stimulated request headers is allowed, this header will not be returned. | String |
| - AccessControlExposeHeaders | Response headers supported by CORS, such as `ETag`. The headers are separated by commas | String |
| - AccessControlMaxAge | Validity period of the result of the `OPTIONS` request, for example, `3600` | String  |
| - OptionsForbidden | Whether the `OPTIONS` request is forbidden. If the returned HTTP status code is 403, this value is `true`. | Boolean |
