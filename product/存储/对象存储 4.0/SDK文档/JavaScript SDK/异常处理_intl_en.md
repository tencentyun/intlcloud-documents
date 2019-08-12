## Overview

If an SDK API call to request the COS service fails, an error message will be returned in the callback.

## Error Example

```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function(err, data) {
    if (err) {
        console.log(err.error);
    }
});
```

## Client Exceptions

| Parameter Name | Description | Type |
| ------- | ------------------------------------------------------------ | ------------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - error | Request error message | Object/String |

## Server Exceptions

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ------------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - error | Request error message | Object/String |
| - - Code | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| - - Message | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| - - RequestId | A unique ID in the server request log that can be submitted in a [ticket](https://console.cloud.tencent.com/workorder/category) for troubleshooting | String |
